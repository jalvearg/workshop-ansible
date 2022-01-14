# 4. Compresión de archivos y búsquedas.
![](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel010.png)

**Meta:**
  * Entender los conceptos necesarios para la compresión de archivos y búsquedas 

**Objetivos:** 
  * Describir como se realizan las compresiones y búsquedas dentro del sistema operativo linux.

**Secciones:**
  * Describiendo la herramienta de compresión tar. (Teoría - Demostración)
  * Describiendo las opciones de búsqueda de archivos. (Teoría - Demostración)

**Laboratorio:**
  * Respaldo de directorios y búsqueda de archivos.
  * Generación de SOS Report.

# Describiendo la herramienta de compresión tar. (Teoría - Demostración)

**Objetivos**:
  Después de completar esta sección el estudiante estará preparado para:
* Gestionar la compresión de archivos con tar en sus diferentes formatos mas utilizados.

# Compresión de archivos TAR (Teoría - Demostración).
![tar1](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel011.png)
<br>
**Tar** es una herramienta de línea de comando utilizada para crear y manipular archivos de almacenamiento en sistemas Linux y Unix.

**El siguiente cuadro referencial indica en resumen de las opciones y funciones de **tar**.**

| Opción | Descripción |
| --- | --- |
| -c, --create | Crea un nuevo archivo.|
| -x, --extract | Extrae de un archivo existente.|
| -t, --list | Lista la tabla de contenido de un archivo.|
| -v, --verbose | Muestra que archivos son archivados o extraidos|
| -f, --file= | Nombre del archivo.|
| -p, --preserve-permissions | Preserva los permisos de los archivos cuando estos son extraidos.|
| -z, --gzip | Usa gzip para compresion (.tar.gz).|
| -j, --bzip2 | Usa bzip2 para compresion (.tar.bz2). |
| -J, --xz | Usa xz para compresion (.tar.xz).|

**Ejemplos .tar**
<br>
<br>
**Crear archivo .tar**
```
[root@nova ~]# tar -cvf etc.tar /etc
[root@nova ~]# ls -l /root/etc.tar
```
**Listar archivo .tar**
```
[root@nova ~]# tar -tvf /root/etc.tar
```
**Extraer archivo .tar**
```
[root@nova ~]# tar -xvf etc.tar
```
**Ejemplo .tar.gz**
<br>
<br>
**Crear archivo .tar.gz**
```
[root@nova ~]# tar -zcvf etc.tar.gz /etc
[root@nova ~]# ls -l /root/etc.tar.gz
```
**Listar archivo .tar.gz**
```
[root@nova ~]# tar -tvf /root/etc.tar.gz
```
**Extraer archivo .tar.gz**
```
[root@nova ~]# tar -zxvf etc.tar.gz
```
**Ejemplos .tar.bz2**
**NOTA:Validar que el paquete bzip2 este instalado**
<br>
<br>
**Crear archivo .tar.bz2**
```
[root@nova ~]# tar -jcvf etc.tar.bz2 /etc
[root@nova ~]# ls -l /root/etc.tar.bz2
```
**Listar archivo .tar.bz2**
```
[root@nova ~]# tar -tvf /root/etc.tar.bz2
```
**Extraer archivo .tar.bz2**
```
[root@nova ~]# tar -jxvf etc.tar.gz
```

**Ejemplos .tar.xz**
<br>
<br>
**Crear archivo .tar.xz**
```
[root@nova ~]# tar -Jcvf etc.tar.xz /etc
[root@nova ~]# ls -l /root/etc.tar.xz
```
**Listar archivo .tar.xz**
```
[root@nova ~]# tar -tvf /root/etc.tar.xz
```
**Extraer archivo .tar.xz**
```
[root@nova ~]# tar -Jxvf etc.tar.xz
```
**Verificar los pesos para determinar cual tiene mejor compresion**
```
[root@nova ~]# du -sh etc.*
21M     etc.tar
3.6M    etc.tar.bz2
5.0M    etc.tar.gz
3.1M    etc.tar.xz
```
**Instalando sosreport para recolectar datos para soporte**
```
[root@nova ~]# yum install sos -y
[root@nova ~]# sosreport

sosreport (version 3.8)

This command will collect diagnostic and configuration information from
this Red Hat Enterprise Linux system and installed applications.

An archive containing the collected information will be generated in
/var/tmp/sos.kh8e48bc and may be provided to a Red Hat support
representative.

Any information provided to Red Hat will be treated in accordance with
the published support policies at:

  https://access.redhat.com/support/

The generated archive may contain data considered sensitive and its
content should be reviewed by the originating organization before being
passed to any third party.

No changes will be made to system configuration.

Press ENTER to continue, or CTRL-C to quit.

Please enter the case id that you are generating this report for []: 100203040

 Setting up archive ...
 Setting up plugins ...
[plugin:networking] skipped command 'ip -s macsec show': required kernel modules or services not present (kmods=[macsec] services=[]). Use '--allow-system-changes' to enable collection.
[plugin:networking] skipped command 'ss -peaonmi': required kernel modules or services not present (kmods=[tcp_diag,udp_diag,inet_diag,unix_diag,netlink_diag,af_packet_diag] services=[]). Use '--allow-system-changes' to enable collection.
 Running plugins. Please wait ...

  Finishing plugins              [Running: yum]                                           ]
  Finished running plugins
Creating compressed archive...

Your sosreport has been generated and saved in:
  /var/tmp/sosreport-nova-100203040-2020-08-24-whaaabp.tar.xz

The checksum is: e51bed0ebdbc593f2dc1802bc336bcb7

Please send this file to your support representative.
```
# Describiendo las opciones de búsqueda de archivos. (Teoría - Demostración)
**Objetivos**:
  Después de completar esta sección el estudiante estará preparado para:
* Utilizar los comandos de búsqueda locate y find.

# Búsquedas con locate y find (Teoría - Demostración).
![tar1](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel012.png)

**locate**, es un utilitario que permite hacer búsquedas rápidas dentro del sistema operativo.
Para utilizar locate debemos tener instalado el paquete mlocate.
```
[root@nova ~]# yum install -y mlocate
```
```
[root@nova ~]# updatedb
[root@nova ~]# locate sshd_config
/etc/ssh/sshd_config
/root/etc/ssh/sshd_config
/usr/share/man/man5/sshd_config.5.gz
```
Con la opcion **-i** podemos ignorar el case-sensitive
```
[root@nova ~]# locate -i message
...
/usr/share/vim/vim80/lang/zh_TW.UTF-8/LC_MESSAGES
/usr/share/vim/vim80/lang/zh_TW.UTF-8/LC_MESSAGES/vim.mo
/usr/share/vim/vim80/syntax/messages.vim
/usr/share/vim/vim80/syntax/msmessages.vim
```

**find**, es un utilitario que permite hacer búsquedas avanzadas dentro del sistema operativo.
**Su estructura es:**
<br>
**find \<startingdirectory\> \<options\> \<search term\>**

**Ejemplos:**
**Búsqueda en directorios específicos en tiempo real**
```
[root@nova ~]# find /etc -name sshd_config
/etc/ssh/sshd_config
```
**Ingorar case-sensitive**
```
[root@nova ~]# find / -iname message
/var/log/MESSAGE
/usr/lib/modules/4.18.0-193.el8.x86_64/kernel/drivers/message
/usr/share/mime/message
```
**Busqueda basada en propietario**
<br>
**user**
```
[root@nova ~]# find / -user nova 2> /dev/null
/var/spool/mail/nova
/home/nova
/home/nova/.bash_logout
/home/nova/.bash_profile
/home/nova/.bashrc
```
**group**
```
[root@nova ~]# find / -group nova 2> /dev/null
/home/nova
/home/nova/.bash_logout
/home/nova/.bash_profile
/home/nova/.bashrc
```
**uid**
```
[root@nova ~]# find / -uid 1000 2> /dev/null
/var/spool/mail/nova
/home/nova
/home/nova/.bash_logout
/home/nova/.bash_profile
/home/nova/.bashrc
```
**gid**
```
[root@nova ~]# find / -gid 1000 2> /dev/null
/home/nova
/home/nova/.bash_logout
/home/nova/.bash_profile
/home/nova/.bashrc
```
**user and group**
```
[root@nova ~]# find / -user root -group mail 2> /dev/null
```

**Busquedas basadas en permisos**
<br>
**perm**
```
[root@nova ~]# find /root/find -perm 600
/root/find/file600
[root@nova find]# ls -l /root/find/file600
-rw-------. 1 root root 0 Aug 24 02:16 /root/find/file600
```
```
[root@nova ~]# find /root/find -perm -644
/root/find
/root/find/file644
/root/find/file664
[root@nova find]# ls -l
total 0
-rw-------. 1 root root 0 Aug 24 02:16 file600
-rw-r--r--. 1 root root 0 Aug 24 02:16 file644
-rw-rw-r--. 1 root root 0 Aug 24 02:17 file664
[root@nova find]# ls -ld /root/find/
drwxr-xr-x. 2 root root 51 Aug 24 02:20 /root/find/
```
```
[root@nova ~]# find /root/find -perm /004
/root/find
/root/find/file644
/root/find/file664
[root@nova find]# ls -ld /root/find/
drwxr-xr-x. 2 root root 51 Aug 24 02:20 /root/find/
```
**Busquedas basadas en tamaño**
<br>
**size**
```
[root@nova ~]# dd if=/dev/urandom of=/root/find/size10M bs=1M count=10
```
```
[root@nova ~]# find /root/find -size 10M
/root/find/size10M
```
```
[root@nova ~]# find /root/find -size -10M
/root/find
/root/find/file600
/root/find/file644
/root/find/file664
```
```
[root@nova ~]# find /root/find -size +10M
[root@nova ~]#
```
**Busquedas basadas en minutos**
<br>
**mmin**
```
[root@nova ~]# find / -mmin 60
```
```
[root@nova ~]# find / -mmin -60
```
```
[root@nova ~]# find / -mmin +60
```

**Busquedas basadas en tipo**
<br>
**f - file**
```
[root@nova find]# find /etc -name sshd -type f
/etc/pam.d/sshd
/etc/sysconfig/sshd
```
**d - directory**
```
[root@nova find]# find /etc -name ssh -type d
/etc/ssh
```
**b - bloque**
```
[root@nova find]# find /dev -type b
/dev/sda2
/dev/sda1
/dev/sda
```

# Laboratorio: Explorando el sistema de archivos linux
En el siguiente laboratorio tendrá que realizar las siguientes operaciones:
1. Ubicar archivos que tengan la palabra sshd en todo el sistema.
2. Ubicar archivos que tengan la palabra networkmanager.conf y que ignoren el case-sensitive.
3. Ubicar dentro de /dev los dispositivos de tipo bloque.
4. Ubicar los archivos que le pertenecen al usuario nova.
5. Ubicar en /etc los archivos que tengan la extensión .repo.
6. Crear un respaldo con tar del directorio /etc el formato de compresión utilizado sera xz. El respaldo deberá ser guardado en /root.
7. Crear un sosreport para atención del caso de soporte 1000203040. Una vez creado desempaquetar e inspeccionar.

Solución:

1. Ubicar archivos que tengan la palabra sshd en todo el sistema.
```
[root@nova find]# locate sshd
/etc/pam.d/sshd
/etc/ssh/sshd_config
/etc/sysconfig/sshd
/etc/systemd/system/multi-user.target.wants/sshd.service
/usr/lib/systemd/system/sshd-keygen.target
/usr/lib/systemd/system/sshd-keygen@.service
/usr/lib/systemd/system/sshd.service
/usr/lib/systemd/system/sshd.socket
/usr/lib/systemd/system/sshd@.service
/usr/lib64/fipscheck/sshd.hmac
/usr/libexec/openssh/sshd-keygen
/usr/sbin/sshd
/usr/share/man/man5/sshd_config.5.gz
/usr/share/man/man8/sshd.8.gz
/usr/share/vim/vim80/syntax/sshdconfig.vim
/var/empty/sshd 
```

2. Ubicar archivos que tengan la palabra networkmanager.conf y que ignoren el case-sensitive.
```
[root@nova find]# locate -i networkmanager.conf
/etc/NetworkManager/NetworkManager.conf
/etc/dbus-1/system.d/org.freedesktop.NetworkManager.conf
/usr/share/man/man5/NetworkManager.conf.5.gz
```
3. Ubicar dentro de /dev los dispositivos de tipo bloque.
```
[root@nova find]# find /dev -type b
/dev/loop0
/dev/dm-1
/dev/dm-0
/dev/sr0
/dev/sda2
/dev/sda1
/dev/sda
```
4. Ubicar los archivos que le pertenecen al usuario nova.
```
[root@nova find]# find / -user nova 2> /dev/null
/var/spool/mail/nova
/home/nova
/home/nova/.bash_logout
/home/nova/.bash_profile
/home/nova/.bashrc 
```
5. Ubicar en /etc los archivos que tengan la extensión .repo.
```
[root@nova ~]# find /etc -name *.repo
/etc/yum.repos.d/redhat.repo
/etc/yum.repos.d/rhel82.repo
```
6. Crear un respaldo con tar del directorio /etc el formato de compresión utilizado sera xz. El respaldo deberá ser guardado en /root.
```
[root@nova ~]# tar -Jcvf /root/etc.tar.xz /etc
```
7. Crear un sosreport para atención del caso de soporte 1000203040. Una vez creado desempaquetar e inspeccionar.
```
[root@nova tmp]# sosreport

sosreport (version 3.8)

This command will collect diagnostic and configuration information from
this Red Hat Enterprise Linux system and installed applications.

An archive containing the collected information will be generated in
/var/tmp/sos.hgmmj0x2 and may be provided to a Red Hat support
representative.

Any information provided to Red Hat will be treated in accordance with
the published support policies at:

  https://access.redhat.com/support/

The generated archive may contain data considered sensitive and its
content should be reviewed by the originating organization before being
passed to any third party.

No changes will be made to system configuration.

Press ENTER to continue, or CTRL-C to quit.

Please enter the case id that you are generating this report for []: 1000203040
...
[root@nova tmp]# cd /var/tmp
[root@nova tmp]# tar -Jxvf sosreport-nova-1000203040-2020-08-25-evmdnig.tar.xz
[root@nova tmp]# cd sosreport-nova-1000203040-2020-08-25-evmdnig
```