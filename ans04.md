<h1>Qué es Ansible Tower</h1>
<p>
<strong>Meta:</strong>
<br>- Entender el proceso de instalación de la solución Red Hat Ansible Tower así como el diseño sugerido para una correcta implementación.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Instalación de Red Hat Ansible(Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>-  .(Teórico - Practico)
<br>- Validación de pre-requisitos para la instalación de Red Hat Ansible Tower.(Teórico)
<br>- Instalación de Red Hat Ansible. (Demostración)
</p>
<p>
<strong>Laboratorios:</strong>
<br>- Instalación de Red Hat Ansible Tower
</p>

# Validación de pre-requisitos para la instalación de Red Hat Ansible Tower

Ansible Tower tiene los siguientes requisitos:

Sistemas operativos compatibles:

Red Hat Enterprise Linux 6 de 64 bits

Red Hat Enterprise Linux 7 de 64 bits

Red Hat Enterprise Linux 8 de 64 bits

CentOS 6 de 64 bits

CentOS 7 de 64 bits

CentOS 8 de 64 bits

Ubuntu 12.04 LTS de 64 bits

Ubuntu 14.04 LTS de 64 bits



La última versión estable de Ansible


2 GB de RAM como mínimo (se recomiendan más de 4 GB de RAM)

2 GB de RAM (mínimo y recomendado para instalaciones de prueba de Vagrant)
Se recomiendan 4 GB de RAM por cada 100 bifurcaciones
Disco duro de 20 GB

Se requiere soporte de 64 bits (kernel y tiempo de ejecución)



Para Amazon EC2:

Tamaño de instancia de m3. Mediano o mayor
Un tamaño de instancia de m3.xlarge o mayor si hay más de 100 hosts
Para configuraciones HA MongoDB:

Si planea ejecutar MongoDB, las siguientes pautas proporcionan una estimación aproximada de la cantidad de espacio requerido. El cálculo básico es:

(number of hosts in inventory) * (number of scans) * (average module fact size) * (number of modules scanning)

Por ejemplo:

hosts = 1,000

número de escaneos = 365 (1 escaneo por día durante un año)

tamaño medio de los hechos del módulo = 100 kb

número de módulos = 4 (ansible, paquetes, servicios, archivos)

= 146 GB

La operación de escaneo predeterminada tiene los cuatro (4) módulos enumerados, pero puede agregar los suyos propios. Dependiendo de los tipos de módulos y del tamaño de los datos que esté recopilando, ese tamaño puede ser mayor.

**Requerimientos de puertos y firewall**

Puertos para la comunicación de satélite a Red Hat CDN
| Puerto | Protocolo | Servicio | Requerido para |
| --- | --- | --- | --- |
| 80 | TCP |HTTP|Servicios de administración web|
| 443 | TCP |HTTPS|Servicios de administración web seguro|
| 22| TCP |SSH|Servicios de administración remota via ssh|
| 5432| TCP | DB |Servicios de conexion a la base de datos|



# Instalación de Red Hat Ansible Tower. (Demostración)
**Verificando conectividad y resolución DNS**
```
[root@server08 ~]# ping -c1 localhost
```
```
[root@server08 ~]# ping -c1 $(hostname -f)
```
```
[root@server08 ~]# ping -c1 $(hostname -s)
```
```
[root@server08 ~]# nslookup server08.opennova.pe
Server:         192.168.10.178
Address:        192.168.10.120#53

Name:   server08.opennova.pe
Address: 192.168.10.178
```
```
[root@server08 ~]# nslookup 192.168.10.178
178.10.168.192.in-addr.arpa      name = server08.opennova.pe
```

Es buena idea indicar el el archivo /etc/hosts
<br>**\<IP\> \<FQDN Ansiblee\> \<Short name Ansible\>**
```
192.168.10.178 server08.opennova.pe server08
```
**Habilitación de conexiones de un cliente a un servidor satélite**
```
[root@server08 ~]# firewall-cmd \
--add-port="80/tcp" --add-port="443/tcp" \
--add-port="22/tcp" --add-port="5432/tcp"
```
```
[root@server08 ~]# firewall-cmd --runtime-to-permanent
```
```
[root@server08 ~]# firewall-cmd --list-all
```
<br>**Instalacion**

Registrar el servidor a un sistema que permita el acceso a repositorios de paquetes como Satellite
```
[root@server08 ~]# curl --insecure --output katello-ca-consumer-latest.noarch.rpm https://satellite.opennova.pe/pub/katello-ca-consumer-latest.noarch.rpm
[root@server08 ~]# yum localinstall katello-ca-consumer-latest.noarch.rpm
[root@server08 ~]# subscription-manager register --org="OpenNova" --activationkey="RHEL8"
[root@server08 ~]# subscription-manager attach --auto
[root@server08 ~]# subscription-manager repos --enable=ansible-2.9-for-rhel-8-x86_64-rpms
```
**Borrar metadata yum**
```
[root@server08 ~]# yum clean all
```
**Verificar repositorios configurados**
``` 
[root@server08 ~]# yum repolist enabled
```

Validamos que el sistema tenga al menos los siguientes repositorios

ansible-2.9-for-rhel-8-x86_64-rpms

rhel-8-for-x86_64-appstream-rpms

rhel-8-for-x86_64-baseos-rpms


**Realizar una lista de paquetes necesarios para la administración de la maquina virtual.**

```
[root@server08 ~]# yum install ansible git
```


**Actualizar el sistema en conjunto y reiniciar**

```
[root@server08 ~]# yum update
```

```
[root@server08 ~]# reboot
```

**Instalar Red Hat Ansible Tower**

Descargamos desde el ftp del salon el instalador de Ansible Tower y descomprimirlo

<br>`[root@server08 ~]# wget ftp://classroom.opennova.pe/ansible-automation-platform-setup-bundle-1.2.5-1.tar.gz`
<br>`[root@server08 ~]# tar -xzvf ansible-automation-platform-setup-bundle-1.2.5-1.tar.gz`
<br>`[root@server08 ~]# cd ansible-automation-platform-setup-bundle-1.2.5-1`

Modificar el archivo inventory para que pueda uztomizar las claves de admin y de awx a redhat

<br>`[root@server08 ~]# vi inventory`


Ejecutar el instalador con

<br>`[root@server08 ~]# ./setup.sh`

**Nota: Para evitar problemas de perdida de conectividad hacia la terminar virtual se recomienda ejecutar elprocedimiento de instalación por screen**
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
[root@server08 ~]# screen -r 3081
```

**Abrir puertos de firewall**

Abrir los puertos del firewall correspondiente al acceso HTTP, HTTPS y SSH, opcionalmente el puerto 5432 es necesario solo si se trabaja con bases de datos externas

```
[root@server08 ~]# firewall-cmd \
--add-port="80/tcp" --add-port="443/tcp" \
--add-port="22/tcp" --add-port="5432/tcp"
```

En este punto indicar a su instructor que active la plataforma de Ansible Tower con una suscripcion de prueba, luego ingresar con un navegador web para validar su instalacion
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans02.png?raw=true"></p>



# Laboratorio: Instalando Red Hat Ansible Tower

<br>**1. Instalar Red Hat Ansible Tower utilizando el procedimiento INSTALACIÓN**
<br>- Utilizar el procedimiento indicado en la explicación.
<br>- Solicite a su instructor la activacion de su instalacion.
<br>- Una vez finalizada la instalación logearse con el usuario: admin password: redhat

