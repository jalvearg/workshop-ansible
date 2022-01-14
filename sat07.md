<h1>Registrando Hosts de contenido</h1>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat100.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento el procedimiento de registro de host de contenido en Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Identificación y planificación de los recursos host de contenido en Red Hat Satellite (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Registrar un host de contenido de forma manual GUI. (Demostrativo)
<br>- Crear una llave de activación por la GUI . (Demostrativo)
<br>- Registrar un host de contenido por una llave de activación. (Demostrativo)
<br>- Crear una llave de activación por la CLI . (Demostrativo)
<br>- Laboratorio: Registrando host de contenido
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Registrar un host de contenido de forma manual GUI. (Demostrativo)
La siguiente demostración tiene como finalidad aprender a registrar un host de contenido de forma manual por la herramienta gráfica.

**Hosts > Content Host**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat700.png?raw=true"width="800" height="400"></p>

En la pagina de Host de contenido darle click al boton **Registrar host de contenido**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat701.png?raw=true"width="800" height="400"></p>

Los datos que se muestran en las imágenes son los primeros pasos que se tendrán que realizar de manera secuencial en los clientes asignados para poder registrarlos

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat702.png?raw=true"width="800" height="400"></p>

Los siguientes pasos se realizaran posterior al registro de suscripción y al registro del canal respectivo

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat703.png?raw=true"width="800" height="400"></p>

Seguir la secuencia de pasos como se indica a continuación:

```
[root@client01 ~]#  curl --insecure --output katello-ca-consumer-latest.noarch.rpm https://satellite.opennova.pe/pub/katello-ca-consumer-latest.noarch.rpm
```
```
[root@client01 ~]# yum localinstall katello-ca-consumer-latest.noarch.rpm -y
```
```
[root@client01 ~]# subscription-manager register --org="Default_Organization" --environment="Library"
Registering to: satellite.opennova.pe:443/rhsm
Username: admin
Password:
The system has been registered with ID: f3e3aea1-abce-4647-8a02-5533c5062ff5
The registered system name is: client01.opennova.pe
```

Una vez registrado el host de contenido este estará en estado **Unentitled** darle click al enlace del host

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat704.png?raw=true"width="800" height="400"></p>

Se debe modificar el tab de Suscripciones como se muestra en la siguiente imagen para agregarle una suscripción valida.

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat705.png?raw=true"width="800" height="400"></p>

Una vez modificado correctamente se deberá visualizar con el estado de **Fully Entitled**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat705_00.png?raw=true"width="800" height="400"></p>

En el tab de Información modificar el contenido como se muestra en la siguiente imagen

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat706.png?raw=true"width="800" height="400"></p>

Luego de esto se podrá visualizar que esta operativo en la columna de Estatus de suscripción

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat707.png?raw=true"width="800" height="400"></p>

Para validar deberemos ejecutar los siguientes comandos en el sistema operativo

```
[root@client01 ~]# subscription-manager list
+-------------------------------------------+
    Installed Product Status
+-------------------------------------------+
Product Name:   Red Hat Enterprise Linux for x86_64
Product ID:     479
Version:        8.2
Arch:           x86_64
Status:         Subscribed
Status Details:
Starts:         04/15/2020
Ends:           04/14/2021
```

Validar los repositorios asociados
```
[root@client01 ~]# subscription-manager repos --list
+----------------------------------------------------------+
    Available Repositories in /etc/yum.repos.d/redhat.repo
+----------------------------------------------------------+
Repo ID:   rhel-8-for-x86_64-appstream-rpms
Repo Name: Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)
Repo URL:  https://satellite.opennova.pe/pulp/repos/Default_Organization/Library/content/dist/rhel8/8.2/x86_64/appstream/os
Enabled:   1

Repo ID:   satellite-tools-6.7-for-rhel-8-x86_64-rpms
Repo Name: Red Hat Satellite Tools 6.7 for RHEL 8 x86_64 (RPMs)
Repo URL:  https://satellite.opennova.pe/pulp/repos/Default_Organization/Library/content/dist/layered/rhel8/x86_64/sat-tools/6.7/os
Enabled:   0

Repo ID:   rhel-8-for-x86_64-baseos-rpms
Repo Name: Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)
Repo URL:  https://satellite.opennova.pe/pulp/repos/Default_Organization/Library/content/dist/rhel8/8.2/x86_64/baseos/os
Enabled:   1
```

Ahora debemos habilitar el repositorio el repositorio satellite-tools-6.7-for-rhel-8-x86_64-rpms

```
[root@client01 ~]# subscription-manager repos --enable=satellite-tools-6.7-for-rhel-8-x86_64-rpms
[root@client01 ~]# yum repolist
Updating Subscription Management repositories.
repo id                                                      repo name
rhel-8-for-x86_64-appstream-rpms                             Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)
rhel-8-for-x86_64-baseos-rpms                                Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)
satellite-tools-6.7-for-rhel-8-x86_64-rpms                   Red Hat Satellite Tools 6.7 for RHEL 8 x86_64 (RPMs)
```

Procedemos a instalar las clientes y herramientas de katello 
```
[root@client01 ~]# yum -y install katello-host-tools
[root@client01 ~]# yum -y install katello-host-tools-tracer
[root@client01 ~]# yum -y install katello-agent
```
Instalar paquetes básicos de administración para validar el funcionamiento de los repositorios de sistema operativo

```
yum install -y net-tools bind-utils sos git vim bash-completion
```
Finalmente en la vista de host de contenido podrán verificar que ahora pueden ver tanto: erratas, bugfix y mejoras, así como la cantidad de paquetes disponibles involucrados.

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat708.png?raw=true"width="800" height="400"></p>

Para instalar un paquete de software ir al objeto de cliente registrado y darle a tab de Paquetes como se muestra a continuación.

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat708_1.jpg?raw=true"></p>

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat708_2.jpg?raw=true"></p>

Para instalar una errata de software ir al objeto de cliente registrado y darle a tab de Erratas como se muestra a continuación.

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat708_3.jpg?raw=true"></p>

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat708_4.jpg?raw=true"></p>

Para borrar el registro ejecutar la opción Delete Hosts como se muestra en la imagen

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat709.png?raw=true"width="800" height="400"></p>

A nivel de sistema operativo se debe ejecutar los siguientes comandos:
```
[root@client01 ~]# subscription-manager unregister
[root@client01 ~]# subscription-manager clean
[root@client01 ~]# yum clean all
```


# Crear una llave de activación por la GUI . (Demostrativo)
**Content > Activation Keys**
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat710.png?raw=true"width="800" height="400"></p>

En la pagina de Llaves de activacion hace click en el boton **Create Activation Key**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat711.png?raw=true"width="800" height="400"></p>

En la pagina **Nueva llave de activación** ingresar la información como se muestra en la imagen
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat712.png?raw=true"width="800" height="400"></p>

En el tab de **Información** indicar la **versión** como se muestra en la imagen
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat713.png?raw=true"width="800" height="400"></p>

En el tab de **Suscripciones** agregar la **suscripción** respectiva como se muestra en la imagen
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat714.png?raw=true"width="800" height="400"></p>

En el tab de **Repository Sets** marcar los **3 repositorios** indicados y darle a **Override to Enabled**
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat715.png?raw=true"width="800" height="400"></p>

Verificar que la llave de activación se haya creado correctamente

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat716.png?raw=true"width="800" height="400"></p>

# Registrar un host de contenido por una llave de activación. (Demostrativo)
En el sistema operativo ejecutar lo siguiente:

```
[root@client01 ~]# curl --insecure --output katello-ca-consumer-latest.noarch.rpm https://satellite.opennova.pe/pub/katello-ca-consumer-latest.noarch.rpm
[root@client01 ~]# yum localinstall katello-ca-consumer-latest.noarch.rpm -y
[root@client01 ~]# subscription-manager register --org="Default_Organization" --activationkey="rhel8"
```

Validar que se pueda tener los repositorios
```
[root@client01 ~]# yum repolist
Updating Subscription Management repositories.
repo id                                                      repo name
rhel-8-for-x86_64-appstream-rpms                             Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)
rhel-8-for-x86_64-baseos-rpms                                Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)
satellite-tools-6.7-for-rhel-8-x86_64-rpms                   Red Hat Satellite Tools 6.7 for RHEL 8 x86_64 (RPMs)
[root@client01 ~]# yum list all
```
Finalmente verificar en la pagina de Host de contenido que se pueda visualizar el sistema suscrito y con información disponible

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat717.png?raw=true"width="800" height="400"></p>

# Crear una llave de activación por la CLI . (Demostrativo)

Crear la **llave de activación rhel82** como se muestra a continuación:

```
[nova@satellite ~]$ hammer activation-key create --name rhel84 --description 'Llaves de activacion para clientes Red Hat Enterprise Linux 8.4' --organization 'OpenNova' --lifecycle-environment 'Library' --content-view 'Default Organization View' --unlimited-hosts --release-version '8'
Activation key created.
```

Listar la llave de activación
```
[nova@satellite ~]$ hammer activation-key list --organization 'OpenNova'
---|--------|----------------|-----------------------|--------------------------
ID | NAME   | HOST LIMIT     | LIFECYCLE ENVIRONMENT | CONTENT VIEW
---|--------|----------------|-----------------------|--------------------------
1  | rhel8  | 1 of Unlimited | Library               | Default Organization View
4  | rhel84 | 0 of Unlimited | Library               | Default Organization View
---|--------|----------------|-----------------------|--------------------------
```

Verificar el id de la suscripción de Red Hat Enterprise Linux

```
[nova@satellite ~]$ hammer subscription list
```

Agregar la suscripción a la llave de activación
```
[nova@satellite ~]$ hammer activation-key add-subscription --subscription-id 4 --organization 'OpenNova' --name rhel84
```

Habilitar el repositorio de herramientas satellite a la llave de activación
```
[nova@satellite ~]$ hammer activation-key content-override --content-label satellite-tools-6.9-for-rhel-8-x86_64-rpms --value 1 --organization 'OpenNova' --name rhel84
```

Reutilizar el cliente asignado, **des-registrar y registrar** con la nueva llave de activación **rhel82**
```
[root@client01 ~]# subscription-manager unregister
[root@client01 ~]# subscription-manager clean
[root@client01 ~]# yum clean all
[root@client01 ~]# subscription-manager register --org="OpenNova" --activationkey="rhel84"
[root@client01 ~]# yum repolist
[root@client01 ~]# yum list all
```

Borrar llave de activacion
```
[nova@satellite ~]$ hammer activation-key delete --organization 'OpenNova' --name rhel84
Activation key deleted.
```

Verificar que la llave se haya borrado
```
[nova@satellite ~]$ hammer activation-key list --organization 'OpenNova'
---|-------|----------------|-----------------------|--------------------------
ID | NAME  | HOST LIMIT     | LIFECYCLE ENVIRONMENT | CONTENT VIEW
---|-------|----------------|-----------------------|--------------------------
1  | rhel8 | 1 of Unlimited | Library               | Default Organization View
---|-------|----------------|-----------------------|--------------------------
```

# Laboratorio de la Unidad: 
<br>**1. Registrar el cliente asignado mediante procedimiento manual indicado en la demostración**
<br> Instalar el paquete zsh por la herramienta grafica dentro del tab de Packages.
<br> Instalar el Red Hat Security Advisore: RHSA-2021:3548 por la herramienta grafica dentro del tab Errata.
<br> Una vez registrado y validado, proceder a des-registrarlo para registrarlo por una llave de activación.
<br>
<br>**2. Registrar el cliente asignado mediante procedimiento de llave de activación se deberá crear la llave de activación AK_RHEL8_USER_X como se muestra en la demostración, donde X es el numero de su usuario del 1 al 6**
<br> Una vez creada la llave proceder a registrar el cliente asignado utilizando la llave de activación AK_RHEL8_USER_X donde X es el numero de cliente del 1 al 6

