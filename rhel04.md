# 3. Instalación de paquetes de software
![](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel006.png)

**Meta:**
  * Descargar, instalar, actualizar y administrar paqueteria de software Red Hat.

**Objetivos:** 
  * Entender el proceso de registro de suscripción utilizando Red Hat Subscription Management (RHSM).
  * Aprender a utilizar el utilitario yum para la gestión de paqueteria de software.
  * Habilitar y des-habilitar repositorios locales de software.

**Secciones:**
  * Registrando sistemas vía Red Hat Subscription Manager (Teórico - Demostrativo)
  * Utilizando el gestor de paqueteria yum (Teórico - Demostrativo)
  * Configurando repositorios locales con yum (Demostrativo)

**Laboratorio:**
  * Configurando repositorio local e instalando software.

# Registrando sistemas vía Red Hat Subscription Management (Teórico - Demostrativo)

**Objetivos**:
  Después de completar esta sección el estudiante estará preparado para:
* Realizar el registro de suscripciones en el portal de Red Hat.

# Red Hat Subscription Management y Red Hat Subscription Manager (Teórico - Demostración)
![RHSM01](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel007.png)
Red Hat Subscription Management le permite a los usuarios realizar un seguimiento de la calidad y consumo de sus suscripciones.

![RHSM02](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel008.png)
Red Hat Subscription-Manager el registro y uso de una suscripción es un proceso que consta de dos partes. Primero, registre el sistema, luego aplique la suscripción.

**1. Registro de suscripción**
```
[root@nova ~]# subscription-manager register
Registering to: subscription.rhsm.redhat.com:443/subscription
Username: <username>
Password: ********
```
**2. Adjuntar la suscripción**
<br>Listar suscripciones disponibles, si se tienen mas de un tipo de suscripciones se puede utilizar el dato del Pool ID, para asociar una suscripciones en particular.
```
[root@nova ~]# subscription-manager list --available
+-------------------------------------------+
    Available Subscriptions
+-------------------------------------------+
...
Subscription Name:   Red Hat Cloud Infrastructure, Premium (4 Sockets)
...
Pool ID: 123asdzxc123asdzxc123asdzxccvbnh
```
**Ajuntar suscripción automática**
```
[root@nova ~]# subscription-manager attach --auto
```
**Ajuntar suscripción indicando el Pool ID especifico**
```
[root@nova ~]# subscription-manager attach --pool=<POOL_ID>
```
**Verificar los repositorios habilitados por defecto**
```
[root@nova ~]# subscription-manager repos --list | grep -B 2 Enabled.*1
Repo Name: Red Hat Enterprise Linux 7 Server (RPMs)
Repo URL:  https://cdn.redhat.com/content/dist/rhel/server/7/$releasever/$basearch/os
Enabled:   1
```
**Validar el registro automático vía yum**
```
[root@nova ~]# yum clean all
[root@nova ~]# yum repolist
[root@satellite ~]# yum repolist
repo id                                          repo name                                                                            status
rhel-7-server-rpms/7Server/x86_64                Red Hat Enterprise Linux 7 Server (RPMs)                                             172+29,253
```

**Quitar registros de un sistema**
```
[root@nova ~]# subscription-manager remove --all
[root@nova ~]# subscription-manager unregister
[root@nova ~]# subscription-manager clean
[root@nova ~]# yum clean all
```
# Utilizando el gestor de paqueteria yum (Teórico - Demostración)

**Objetivos**:
  Después de completar esta sección el estudiante estará preparado para:
* Administrar la paqueteria de software mediante el uso de yum.

# Administrando paqueteria de software con yum (Teórico - Demostración)
![Linux FS](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel009.png)
<br>
**El siguiente cuadro referencial indica en resumen la función de cada directorio del sistema de archivos linux**

| Directorio | Descripción |
| --- | --- |
| yum list '\<packagename\>'| Muestra los paquetes instalados y disponibles.|
| yum search '\<packagename>\'|Enumera los paquetes por palabras clave que se encuentran solo en los campos de nombre y resume.|
| yum info '\<packagename>\'| Muestra información detallada sobre le paquete en consulta.|
| yum provides '\<pathname>\' | Muestra paquetes que coinciden con el nombre de ruta especificada. |
| yum install '\<packagename>\'| Instala el paquete y sus dependencias de software. |
| yum update '\<packagename>\' | Actualiza el paquete de software y sus dependencias relacionadas.|
| yum remove '\<packagename>\' | Remueve el paquete de software instalado.|
| yum history | Muestra el listado de paquetes instalados y removidos.|
| yum history undo '\<num>\' | Retorna al estando anterior antes de instalar o remover un paquete, esta opción borra incluso las dependencias.|
| yum group list |Lista grupo de paquetes. Si se le agrega la palabra 'hidden' mostrara la lista completa incluida ocultos.|
| yum group info '\<groupname>\'| Muestra la información del grupo de paquetes a instalar.|
| yum group install '\<groupname>\'| Instala el grupo de paquetes indicado.|

# Configurando repositorios locales con yum (Demostrativo)
**Objetivos**:
  Después de completar esta sección el estudiante estará preparado para:
* Gestionar repositorios locales

# Creando repositorios locales mediante la ISO (Demostrativo)
A continuación se indicaran los pasos necesario para la creación de repositorios locales mediante el uso de la ISO
<br>
**1. Descargar la iso de la versión de sistema operativo a utilizar**
<br> Descargar la iso necesario de la pagina de Red Hat [Descargar ISO](https://access.redhat.com/downloads/). Deberán autenticarse utilizando sus credenciales Red Hat.

**2. Crear una carpeta en el sistema y montar la iso**
```
[root@nova ~]# mkdir /mnt/rhel84 ; mount -o loop /root/rhel84.iso /mnt/rhel84
```
**3. Configuración del repositorio local**
```
[root@nova ~]# cat /etc/yum.repos.d/rhel84.repo
[rhel84-BaseOS]
name=RHEL84 BaseOS Local Repository
baseurl=file:///mnt/rhel84/BaseOS
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
[rhel84-AppStream]
name=RHEL84 AppStream Local Repository
baseurl=file:///mnt/rhel84/AppStream
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```
**Verificar que el repositorio cargue sin problema**
```
[root@nova ~]# yum repolist
Updating Subscription Management repositories.
Unable to read consumer identity
This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.
repo id                                                               repo name
rhel84-AppStream                                                      RHEL84 AppStream Local Repository
rhel84-BaseOS                                                         RHEL84 BaseOS Local Repository
[root@nova ~]# yum list all
```
**Instalar software para validar que el repositorio es funcional**
```
[root@nova ~]# yum install -y vim git net-tools
```

# Creando repositorios locales mediante enlaces locales (Demostrativo)
A continuación se indicaran los pasos necesario para la creación de repositorios locales mediante el uso enlaces (ftp - http) locales.
<br>
**1. Configuración del repositorio local**
```
[root@nova ~]# cat /etc/yum.repos.d/rhel84.repo
[rhel84-BaseOS]
name=RHEL84 BaseOS Local Repository
baseurl=ftp://classroom.opennova.pe/rhel8/BaseOS
enabled=1
gpgecheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
[rhel84-AppStream]
name=RHEL84 AppStream Local Repository
baseurl=ftp://classroom.opennova.pe/rhel8/AppStream
enabled=1
gpgecheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```
**Verificar que el repositorio cargue sin problema**
```
[root@nova ~]# yum repolist
Updating Subscription Management repositories.
Unable to read consumer identity
This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.
repo id                                                               repo name
rhel84-AppStream                                                      RHEL84 AppStream Local Repository
rhel84-BaseOS                                                         RHEL84 BaseOS Local Repository
[root@nova ~]# yum list all
```
**Instalar software para validar que el repositorio es funcional**
```
[root@nova ~]# yum install -y vim git net-tools
```


# Laboratorio: Configurando repositorio local e instalando software
En el siguiente laboratorio tendrá que realizar las siguientes operaciones:
1. Configurar un repositorio local con la iso y/o url proporcionada. El nombre del repositorio deberá ser rhel84.repo y deberá contener las directivas de configuración para los repositorios BaseOS y AppStream.
2. Instalar el paquete bash-completion, sos.
3. Instalar el grupo de paquetes Networking Tools.
4. Instalar el servicio vsftpd.
5. Instalar el servicio httpd
6. Desinstalar el servicio httpd y sus dependencias


Solución:

1. Configurar un repositorio local con la iso y/o url proporcionada. El nombre del repositorio deberá ser rhel84.repo y deberá contener las directivas de configuración para los repositorios BaseOS y AppStream.
```
[root@nova ~]# cat /etc/yum.repos.d/rhel84.repo
[rhel84-BaseOS]
name=RHEL84 BaseOS Local Repository
baseurl=ftp://classroom.opennova.pe/rhel8/BaseOS
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
[rhel84-AppStream]
name=RHEL84 AppStream Local Repository
baseurl=ftp://classroom.opennova.pe/rhel8/AppStream
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```

2. Instalar los paquetes de bash-completion, sos.
```
[root@nova ~]# yum install -y bash-completion sos
```
3. Instalar el grupo de paquetes Networking Tools.
```
[root@nova ~]# yum groupinstall 'Networking Tools'
```
4. Instalar el servicio vsftpd.
```
[root@nova ~]# yum install -y vsftpd 
```
5. Instalar el servicio httpd
```
[root@nova ~]# yum install -y httpd
```
6. Desinstalar el servicio httpd y sus dependencias
<br> En este punto con el comando yum history validar que ID contiene la instalación previa de httpd para poder deshacer el cambio.
```
[root@nova ~]# yum history
Updating Subscription Management repositories.
Unable to read consumer identity
This system is not registered to Red Hat Subscription Management. You can use subscription-manager to register.
ID     | Command line             | Date and time    | Action(s)      | Altered
-------------------------------------------------------------------------------
     4 | install httpd            | 2020-08-24 00:33 | Install        |   10
     3 | group install Networking | 2020-08-24 00:29 | Install        |   13
     2 | install -y vim git net-t | 2020-08-24 00:21 | Install        |   53
     1 |                          | 2020-08-23 23:43 | Install        |  422 EE
[root@nova ~]# yum history undo 4

```
