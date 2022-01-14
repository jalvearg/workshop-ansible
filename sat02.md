<h1>Entendimiento y visualización del proceso de instalación</h1>
<p>
<strong>Meta:</strong>
<br>- Entender el proceso de instalación de la solución Red Hat Satellite así como el diseño sugerido para una correcta implementación.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Instalación de Red Hat Satellite (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>-  .(Teórico - Practico)
<br>- Validación de pre-requisitos para la instalación de Red Hat Satellite.(Teórico)
<br>- Instalación de Red Hat Satellite. (Demostración)
</p>
<p>
<strong>Laboratorios:</strong>
<br>- Instalación de Red Hat Satellite
</p>

# Validación de pre-requisitos para la instalación de Red Hat Satellite

Los siguientes requisitos se aplican al sistema operativo base:
* arquitectura x86_64
* La última versión de Red Hat Enterprise Linux 7 Server
* CPU de 4 núcleos a 2,0 GHz como mínimo
* Se requiere un mínimo de 20 GB de RAM para que el servidor satélite funcione. Además, también se recomienda un mínimo de 4 GB de RAM para SWAP. Es posible que el satélite que se ejecuta con menos RAM que el valor mínimo no funcione correctamente
* Un nombre de host único, que puede contener letras minúsculas, números, puntos (.) Y guiones (-)
* Una suscripción actual a Red Hat Satellite
* Acceso de usuario administrativo (root)
* Una máscara de sistema de 0022 (umask 0022)
* Resolución DNS completa registro A y PTR usando un nombre de dominio completamente calificado

NOTA: El servidor en el cual se instalara satellite deberá ser dedicado para este servicio.

**Requerimientos de almacenamiento**

| Directorio | Tamaño en instalacion | Tamaño en ejecucion|
| --- | --- | --- |
| /var/cache/pulp/ | 1 MB | 20 GB |
| /var/lib/pulp/ | 1 MB | 300 GB |
|/var/lib/mongodb/ | 3.5 GB | 50 GB|
|/var/lib/qpidd/ | 25 MB | Not Applicable|
|/var/log/ |10 MB | 10 GB |
|/var/opt/rh/rh-postgresql12 | 100 MB | 10 GB |
|/var/spool/squid/ | 0 MB | 10 GB |
| /usr | 3 GB | Not Applicable |
| /opt | 3 GB | Not Applicable |
| /opt/puppetlabs | 500 MB | Not Applicable |

**Directrices para sistema de archivos**
* Utilice el sistema de archivos XFS para Red Hat Satellite 6 porque no tiene las limitaciones de inodo que tiene ext4. Debido a que Satellite Server usa muchos enlaces simbólicos, es probable que su sistema se quede sin inodos si usa ext4 con su configuracion por defecto.
* No use NFS con MongoDB porque MongoDB no usa I/O convencional para acceder a archivos de datos y ocurren problemas de rendimiento cuando tanto los archivos de datos como los archivos de diario están alojados en NFS. Si es necesario para usar NFS, monte el volumen con las siguientes opciones en el archivo /etc/fstab: bg, nolock y noatime.
* No utilice NFS para el almacenamiento de datos de Pulp. El uso de NFS para Pulp tiene un impacto negativo en el rendimiento de la sincronización de contenido.
* Do not use the GFS2 file system as the input-output latency is too high.

**Almacenamiento de archivos de log**
* Los archivos de log son escritos en `/var/log/messages/`, `/var/log/httpd/`, and `/var/lib/foreman-proxy/openscap/content/`

NOTA: La cantidad exacta de almacenamiento que necesita para los mensajes de registro depende de su instalación y configuración

**Navegadores soportados**
Satellite soporta versiones recientes de: Firefox y Google Chrome.


*El tamaño del tiempo de ejecución se midió con los repositorios de Red Hat Enterprise Linux 6, 7 y 8 sincronizados.

**Requerimientos de puertos y firewall**

Puertos para la comunicación de satélite a Red Hat CDN
| Puerto | Protocolo | Servicio | Requerido para |
| --- | --- | --- | --- |
| 443 | TCP |HTTPS|Servicios de administración de suscripción (access.redhat.com) y conexión a Red Hat CDN (cdn.redhat.com).|

Puertos para el acceso de la interfaz de usuario basada en navegador al satélite
| Puerto | Protocolo | Servicio | Requerido para |
| --- | --- | --- | --- |
| 443 | TCP |HTTPS|Acceso a la interfaz de usuario basada en navegador para Satellite.|
| 80 | TCP |HTTP|Redirección a HTTPS para acceder a la interfaz de usuario web a satélite (opcional).|

Puertos para la comunicación de cliente a satélite
| Puerto | Protocolo | Servicio | Requerido para |
| --- | --- | --- | --- |
| 80 | TCP |HTTP|Anaconda, yum, para obtener certificados, plantillas de Katello y para descargar el firmware de iPXE.|
| 443 | TCP |HTTPS|Servicios de administración de suscripción, yum, servicios de telemetría y para la conexión al agente de Katello.|
| 5646 | TCP |AMQP|El enrutador de despacho Capsule Qpid al enrutador de despacho Qpid en Satellite.|
| 5647 | TCP |AMQP|Agente de Katello para comunicarse con el enrutador de despacho Qpid de Satellite.|
| 8000 | TCP |HTTP|Anaconda para descargar plantillas kickstart a hosts y para descargar firmware iPXE.|
| 8140 | TCP |HTTPS|Conexiones de Puppet agent a Puppet master.|
| 9090 | TCP |HTTPS|Envío de informes SCAP a la cápsula integrada, para la imagen de descubrimiento durante el aprovisionamiento para comunicarse con Satellite Server y copiar las claves SSH para la configuración de ejecución remota (Rex).|
| 7 | TCP,UDP |ICMP|DHCP externo en una red de cliente a satélite, ICMP ECHO para verificar que la dirección IP esté libre (opcional).|
| 53 | TCP,UDP |DNS| Consultas de DNS del cliente al servicio de DNS cápsula integrado de un satélite (opcional).|
| 67 | UDP |DHCP| Transmisiones de cápsula integradas de cliente a satélite, transmisiones DHCP para aprovisionamiento de clientes desde una cápsula integrada de satélite (opcional).|
| 69 | UDP |TFTP| Clientes que descargan archivos de imagen de arranque PXE desde una cápsula integrada de satélites para aprovisionamiento (opcional).|
| 5000 | TCP|HTTPS| Connection to Katello for the Docker registry (Optional).|


Puertos para comunicación satélite a cápsula
| Puerto | Protocolo | Servicio | Requerido para |
| --- | --- | --- | --- |
| 443 | TCP |HTTPS|Conexiones al servidor Pulp en la cápsula.|
| 9090 | TCP |HTTPS|Conexiones al proxy en la cápsula.|
| 80| TCP |HTTP|Descarga de un disco de arranque (opcional)

Puertos de red opcionales
| Puerto | Protocolo | Servicio | Requerido para |
| --- | --- | --- | --- |
| 22 | TCP |SSH|Comunicaciones basadas en satélite y cápsula, para ejecución remota (Rex) y Ansible.|
| 443 | TCP |HTTPS|Comunicaciones basadas en satélites, para recursos informáticos de vCenter.|
| 5000| TCP |HTTP|Comunicaciones por satélite, para recursos informáticos en OpenStack o para ejecutar contenedores.|
|22,16514| TCP |SSH,SSL/TLS|Comunicaciones por satélite, para recursos informáticos en libvirt.|
|389,636|TCP|LDAP,LDAPS|Comunicaciones satellite, para LDAP y fuentes de autenticación LDAP seguras.|
|5900 to 5930|TCP|SSL/TLS|Comunicaciones satellite, para la consola NoVNC en la interfaz de usuario web a los hipervisores.|

# Instalación de Red Hat Satellite. (Demostración)
**Verificando conectividad y resolución DNS**
```
[root@satellite ~]# ping -c1 localhost
```
```
[root@satellite ~]# ping -c1 $(hostname -f)
```
```
[root@satellite ~]# ping -c1 $(hostname -s)
```
```
[root@satellite ~]# nslookup satellite.opennova.pe
Server:         192.168.0.120
Address:        192.168.0.120#53

Name:   satellite.opennova.pe
Address: 192.168.0.140
```
```
[root@satellite ~]# nslookup 192.168.0.140
140.0.168.192.in-addr.arpa      name = satellite.opennova.pe
```

Es buena idea indicar el el archivo /etc/hosts
<br>**\<IP\> \<FQDN Satellite\> \<Short name Satellite\>**
```
192.168.0.140 satellite.opennova.pe satellite
```
**Habilitación de conexiones de un cliente a un servidor satélite**
```
[root@satellite ~]# firewall-cmd \
--add-port="80/tcp" --add-port="443/tcp" \
--add-port="5647/tcp" --add-port="8000/tcp" \
--add-port="8140/tcp" --add-port="9090/tcp" \
--add-port="53/udp" --add-port="53/tcp" \
--add-port="67/udp" --add-port="69/udp" \
--add-port="5000/tcp"
```
```
[root@satellite ~]# firewall-cmd --runtime-to-permanent
```
```
[root@satellite ~]# firewall-cmd --list-all
```
<br>**Instalacion Online**
**Habilitación de los siguientes repositorios:**
```
[root@satellite ~]# subscription-manager repos --enable=rhel-7-server-rpms \
--enable=rhel-7-server-satellite-6.9-rpms \
--enable=rhel-7-server-satellite-maintenance-6-rpms \
--enable=rhel-server-rhscl-7-rpms \
--enable=rhel-7-server-ansible-2.9-rpms
```
**Borrar metadata yum**
```
[root@satellite ~]# yum clean all
```
**Verificar repositorios configurados**
``` 
[root@satellite ~]# yum repolist enabled
```

**Realizar una lista de paquetes necesarios para la administración de la maquina virtual.**
```
[root@satellite ~]# yum install sos git net-tools bind-utils vim mlocate chrony
```

**NOTA: Si necesita instalar algún paquete adicional como bash-completion, dig, net-tools, git, vim, entre otros necesarios para su administración realizarlo antes de la instalación y configuración del producto**

**Actualizar el sistema en conjunto y reiniciar**
```
[root@satellite ~]# yum update
```
```
[root@satellite ~]# reboot
```
**Instalar paquetes de instalación para Red Hat Satellite**
``` 
[root@satellite ~]# yum install satellite
```
**Instalar Red Hat Satellite**
```
[root@satellite ~]# satellite-installer --scenario satellite \
--foreman-initial-organization "initial_organization_name" \
--foreman-initial-location "initial_location_name" \
--foreman-initial-admin-username admin_user_name \
--foreman-initial-admin-password admin_password
```
```
satellite-installer --scenario satellite \
--foreman-initial-admin-username admin \
--foreman-initial-admin-password redhat
```

**Nota: Para evitar problemas de perdida de conectividad hacia la terminar virtual se recomienda ejecutar el procedimiento de instalación por screen**
<br>**Instalar screen**
```
[root@satellite ~]# yum install -y screen
```
**Generar un alias de conexión screen**
```
[root@satellite ~]# screen -S jaime 
```
**Listar conexión screen, identificar el id ejemplo: 3081**
```
[root@satellite ~]# screen -ls
There is a screen on:
        3081.jaime      (Attached)
1 Socket in /var/run/screen/S-root.
```
**En caso de des-conexión abrir otro terminal y ejecutar el comando indicado para restablecer la conexión, recordar poner el id que se genere en su terminal**
```
[root@satellite ~]# screen -r 3081
```

### **Instalacion offline**

Validar que el cliente tenga el repositorio local para Red Hat Enteprise Linux 7.9
```
[root@satellite ~]# cat /etc/yum.repos.d/rhel.repo
[rhel]
name=rhel
enabled=1
baseurl=ftp://classroom.opennova.pe/rhel7
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
[selinux]
name=selinux
enabled=1
baseurl=ftp://classroom.opennova.pe/selinux
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
```
```
[root@satellite ~]# yum repolist
```
Es buena idea indicar el el archivo /etc/hosts
<br>**\<IP\> \<FQDN Satellite\> \<Short name Satellite\>**
<br>**NOTA: Utilizar las ips y nombres dns asignados**
```
192.168.0.151 server01.opennova.pe server01
```

Instalar paquetes necesarios para su administracion
```
[root@satellite ~]# yum install sos wget git net-tools vim mlocate chrony screen bash-completion selinux-policy
[root@satellite ~]# systemctl start chronyd
[root@satellite ~]# systemctl enable chronyd
```

```
[root@satellite ~]# firewall-cmd \
--add-port="80/tcp" --add-port="443/tcp" \
--add-port="5647/tcp" --add-port="8000/tcp" \
--add-port="8140/tcp" --add-port="9090/tcp" \
--add-port="53/udp" --add-port="53/tcp" \
--add-port="67/udp" --add-port="69/udp" \
--add-port="5000/tcp"
```
```
[root@satellite ~]# firewall-cmd --runtime-to-permanent
```
```
[root@satellite ~]# firewall-cmd --list-all
```
```
[root@satellite ~]# rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-redhat-release
[root@satellite ~]# wget ftp://classroom.opennova.pe/sat69.iso
[root@satellite ~]# mkdir /mnt/sat69
[root@satellite ~]# mount /root/sat69.iso /mnt/sat69
[root@satellite ~]# cd /mnt/sat69; ./install_packages
[root@satellite ~]# satellite-installer --help
[root@satellite ~]# satellite-installer --scenario satellite \
--foreman-initial-admin-username admin \
--foreman-initial-admin-password redhat
```

Ingresar a la url `https://satellite.opennova.pe`
<br>usuario: **admin**
<br>password: **redhat**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat200.png?raw=true" width="800" height="400"></p>

Una vez indicada las credenciales podremos logearnos y accesar al dashboard de satellite
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat201.png?raw=true" width="800" height="400"></p>

**Instalar software adicional posterior a la instalacion**
```
[root@satellite ~]# foreman-maintain packages install bind-utils
```
NOTA: Foreman bloquea la instalación post-instalación para evitar que se instalen paquetes que hagan conflicto con satellite, pero si se necesita instalar alguna herramienta para la administración y/o resolución de problemas este lo hará con el comando indicado. Tomar en cuenta que cada instalación hará que satellite valide su integridad por lo que posterior a la instalación el reiniciara los servicios y verificara sus componentes.

<br>**Extras**
<br>**Hammer Authentication Session**
```
[root@satellite ~]# vim /root/.hammer/cli.modules.d/foreman.yml
```
<br>Agregar el parámetro **:use_sessions:** true como se muestra en la siguiente imagen
```
[root@satellite ~]# cat /root/.hammer/cli.modules.d/foreman.yml
:foreman:
  :use_sessions: true
  # Credentials. You'll be asked for the interactively if you leave them blank here
  :username: 'admin'
  :password: 'redhat'

  # Check API documentation cache status on each request
  :refresh_cache: false

  # API request timeout in seconds, set -1 for infinity
  :request_timeout: 120
```
```
[root@satellite ~]# hammer auth login basic
[Foreman] Username: admin
[Foreman] Password for admin:
Successfully logged in as 'admin'.
```
```
[root@satellite ~]# hammer auth status
Session exists, currently logged in as 'admin'.
```
```
[root@satellite ~]# hammer organization list
---|----------------------|----------------------|-------------|---------------------
ID | TITLE                | NAME                 | DESCRIPTION | LABEL
---|----------------------|----------------------|-------------|---------------------
1  | Default Organization | Default Organization |             | Default_Organization
3  | Opennova             | Opennova             |             | ON
---|----------------------|----------------------|-------------|---------------------
```
```
[root@satellite ~]# hammer settings list | grep ^idle_timeout
idle_timeout                                           | Idle timeout                                                | 60                                                                               | Log out idle users after a certain number of minutes
```
**Cambiar el tiempo de sesión de 60 minutos a 30 minutos**
```
[root@satellite ~]# hammer settings set --name idle_timeout --value 30
Setting [idle_timeout] updated to [30].
```
```
[root@satellite ~]# hammer settings list | grep ^idle_timeout
idle_timeout                                           | Idle timeout                                                | 30                                                                               | Log out idle users after a certain number of minutes
```
**Revisar el estado de los servicios principales o core de Satellite**
```
[root@satellite ~]# hammer ping
database:
    Status:          ok
    Server Response: Duration: 0ms
candlepin:
    Status:          ok
    Server Response: Duration: 16ms
candlepin_auth:
    Status:          ok
    Server Response: Duration: 14ms
pulp:
    Status:          ok
    Server Response: Duration: 51ms
pulp_auth:
    Status:          ok
    Server Response: Duration: 19ms
foreman_tasks:
    Status:          ok
    Server Response: Duration: 4ms
```

**Gestionar los servicios de red hat satellite**

Listar servicios Red Hat Satellite
```
[root@satellite ~]# satellite-maintain service list
```
Listar estado Red Hat Satellite
```
[root@satellite ~]# satellite-maintain service status
```
Parar servicios Red Hat Satellite
```
[root@satellite ~]# satellite-maintain service stop
```
Reiniciar servicios Red Hat Satellite
```
[root@satellite ~]# satellite-maintain service restart
```
Hacer una revision de salud de Red Hat Satellite
```
[root@satellite ~]# satellite-maintain health check
```

**Configurar mensaje personalizado para pagina de Login**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat202.png?raw=true"width="800" height="400"></p>

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat203.png?raw=true"width="800" height="400"></p>

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat204.png?raw=true"width="800" height="400"></p>

**Resetear el password del Administrador**
Generar una contraseña aleatoria
```
[root@satellite ~]# foreman-rake permissions:reset
Reset to user: admin, password: zaJxRftxb7Gbvca
```
**Ingresar con el password y cambiar por uno nuevo**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat205.png?raw=true"width="800" height="400"></p>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat206.png?raw=true"width="800" height="400"></p>

**Asignar una contraseña nueva**
```
[root@satellite ~]# foreman-rake permissions:reset password=redhat123
```

# Laboratorio: Instalando Red Hat Satellite

<br>**1. Instalar Red Hat Satellite utilizando el procedimiento INSTALACIÓN OFFLINE**
<br>- Utilizar el procedimiento indicado en la explicación.
<br>- Una vez finalizada la instalación logearse con el usuario: admin password: redhat
<br>- Post-instalación instalar el paquete bind-utils
<br>**2. Configurar el cliente hammer**
<br>- Configurar hammer para que utilice sesiones **:use_sessions:**
<br>- Logearse al satellite por la herramienta hammer utilizando **hammer auth login basic**
<br>- Setear el timeout de sesión a 30 minutos
<br>- Validar por hammer los servicios principales
<br>- Utilizar satellite-maintain service para listar, ver el estado y reiniciar los servicios de satellite.
<br>- Configurar un mensaje de inicio de sesión que diga la frase: "Red Hat Satellite Claro"
<br>- Cambiar la contraseña del usuario admin por los 2 métodos: Con el uso de clave autogeneradas luego cambiarlo por la GUI y luego cambiarla indicando el password exacto que debe tener.
