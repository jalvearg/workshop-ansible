# 1. Sistema de archivos linux
![](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel002.png)

**Meta:**
  * Entender los conceptos necesarios para la administración del sistema de archivos linux.

**Objetivos:** 
  * Describir como se organizan los archivos en Linux, y cual es el propósito de cada directorio en la jerarquía del sistema de archivos.

**Secciones:**
  * Describiendo el sistema de archivos linux conceptos. (Teoría - Quiz)

**Laboratorio:**
  * Explorando el sistema de archivos linux.

# Describiendo el sistema de archivos linux conceptos (Teoría)

**Objetivos**:
  Después de completar esta sección el estudiante estará preparado para:
* Describir la jerarquía de sistema de archivos linux.
* Desplazarse e interactuar sobre el sistema de archivos linux.

# Sistema de archivos linux conceptos (Teoría - Quiz)

![Linux FS](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel001.png)

**El siguiente cuadro referencial indica en resumen la función de cada directorio del sistema de archivos linux**

| Directorio | Descripción |
| --- | --- |
| / | Jerarquía Principal, conocida como raíz |
| /bin | Binarios y/o programas y/o ejecutables de usuarios regulares |
| /boot | Ejecutables, drivers, archivos de configuración de arranque |
| /dev | Dispositivos físicos y lógicos |
| /etc | Archivos de configuración del sistema operativo |
| /home | Espacio de trabajo de usuarios regulares |
| /lib | Librerías 32 bits |
| /lib64 | Librerías 64 bits |
| /mnt | Directorio sugerido para montar recursos de tipo NAS como cliente |
| /opt | Directorio sugerido para instalación de software de terceros |
| /run | Directorio de datos relevantes de procesos en ejecución (se destruye y recrea al reinicio) |
| /usr | Jerarquía secundaria, destinada a usuarios |
| /root | Espacio de trabajo del usuario root |
| /sbin | Binarios y/o programas y/o ejecutables de super usuario |
| /srv | Data para servicios provistas por el sistema |
| /media | Montaje para dispositivos como usb, cdrom, dvd |
| /sys | Directorio de archivos virtual, exporta información sobre dispositivos y sus controladoras |
| /tmp | Archivos temporales |
| /proc | Directorio de archivos virtual, documenta el kernel y estado de procesos como archivos de texto |
| /var | Archivos Variables |

# Describiendo el sistema de archivos linux conceptos (Test)
1. ¿Que directorio contiene información sobre dispositivos lógicos?
<br> a) /tmp
<br> b) /boot
<br> c) /devs
<br> d) /dev

2. ¿Que directorio contiene archivos de configuración persistentes?
<br> a) /root
<br> b) /etc
<br> c) /mnt
<br> d) /sbin

3. ¿Que directorio contiene la información de logs del sistema?
<br> a) /tmp
<br> b) /srv
<br> c) /var/cache
<br> d) /var/log

4. ¿Que directorio contiene información de procesos en ejecución?
<br> a) /root
<br> b) /opt
<br> c) /ran
<br> d) /run

5. ¿Que directorio es utilizado para la instalación de software de terceros?
<br> a) /bin
<br> b) /opt
<br> c) /media
<br> d) /usr

6. ¿Cuales de los siguientes directorios son temporales?
<br> a) /tmp ; /var/tmp
<br> b) /var/cache ; /var
<br> c) /proc ; /sys
<br> d) /mnt ; /srv

7. ¿Que directorio contiene información de arranque del sistema?
<br> a) /proc
<br> b) /boot
<br> c) /etc
<br> d) /usr/local

8. ¿Que directorio contiene los binarios del super usuario?
<br> a) /var
<br> b) /bin
<br> c) /sbin
<br> d) /dev

9. ¿Que directorio es considerado la raíz del sistema?
<br> a) /
<br> b) /root
<br> c) /home
<br> d) /boot

10. ¿Que directorio es utilizado como sugerencia para publicar recursos de servicios?
<br> a) /srv
<br> b) /mnt
<br> c) /opt
<br> d) /media

Solucionario:
| Pregunta| Alternativa |
| --- | --- |
| 1 | d |
| 2 | b |
| 3 | d |
| 4 | d |
| 5 | b |
| 6 | a |
| 7 | b |
| 8 | c |
| 9 | a |
| 10 | a |

# Laboratorio: Explorando el sistema de archivos linux
En el siguiente laboratorio tendrá que realizar las siguientes operaciones:
1. Identificar la ruta donde se encuentran los dispositivos asociados a los discos duros de la maquina virtual.
2. Identificar la ruta donde se encuentra el archivo de configuración del servicio SSH.
3. Identificar la ruta donde se encuentran los archivos de log: messages y secure.
4. Identificar la ruta donde se encuentran los archivos de booteo: vmlinuz y initramfs.
5. Identificar la ruta donde se encuentran los archivos de configuraciones por defecto.

Solución:

1. Identificar la ruta donde se encuentran los dispositivos asociados a los discos duros de la maquina virtual.
```
[root@nova ~]# ls -l /dev/nvme*
crw-------. 1 root root 243, 0 Aug 30 20:49 /dev/nvme0
brw-rw----. 1 root disk 259, 0 Aug 30 20:49 /dev/nvme0n1
brw-rw----. 1 root disk 259, 1 Aug 30 20:49 /dev/nvme0n1p1
brw-rw----. 1 root disk 259, 2 Aug 30 20:49 /dev/nvme0n1p2
```

2. Identificar la ruta donde se encuentra el archivo de configuración del servicio SSH.
```
[root@nova ~]# ls -l  /etc/ssh/sshd_config
-rw-------. 1 root root 4120 Aug  7 02:25 /etc/ssh/sshd_config 
```
3. Identificar la ruta donde se encuentran los archivos de log: messages y secure.
```
[root@nova ~]# ls -l /var/log/messages
-rw-------. 1 root root 1695 Aug 23 15:01 /var/log/messages
[root@nova ~]# ls -l /var/log/secure
-rw-------. 1 root root 372 Aug 23 15:00 /var/log/secure
```
4. Identificar la ruta donde se encuentran los archivos de booteo: vmlinuz y initramfs.
```
[root@nova ~]# ls -l /boot/vmlinuz-4.18.0-193.el8.x86_64
-rwxr-xr-x. 1 root root 8913760 Mar 27 09:48 /boot/vmlinuz-4.18.0-193.el8.x86_64
[root@nova ~]# ls -l /boot/initramfs-4.18.0-193.el8.x86_64.img
-rw-------. 1 root root 29600719 Aug 22 14:58 /boot/initramfs-4.18.0-193.el8.x86_64.img
```
5. Identificar la ruta donde se encuentran los archivos de configuraciones por defecto.
```
[root@nova ~]# ls -l /usr/lib/
total 156
drwxr-xr-x.  2 root root  4096 Feb 20  2018 binfmt.d
drwxr-xr-x.  3 root root  4096 Dec 14  2017 debug
drwxr-xr-x.  4 root root  4096 Aug  6 20:18 dracut
drwxr-xr-x.  8 root root  4096 Aug  6 20:17 firewalld
drwxr-xr-x. 83 root root 16384 Aug  6 20:19 firmware
dr-xr-xr-x.  2 root root  4096 Dec 14  2017 games
drwxr-xr-x.  3 root root  4096 Aug  6 20:17 grub
drwxr-xr-x.  2 root root  4096 Aug  7 02:18 hsqldb
drwxr-xr-x.  2 root root  4096 Aug  7 02:17 java
drwxr-xr-x.  2 root root  4096 Jul  2  2015 java-1.5.0
drwxr-xr-x.  2 root root  4096 Jul  2  2015 java-1.6.0
drwxr-xr-x.  2 root root  4096 Jul  2  2015 java-1.7.0
drwxr-xr-x.  2 root root  4096 Jul  2  2015 java-1.8.0
drwxr-xr-x.  2 root root  4096 Jul  2  2015 java-ext
drwxr-xr-x.  3 root root  4096 Aug  7 02:17 jvm
drwxr-xr-x.  2 root root  4096 Jul  2  2015 jvm-commmon
drwxr-xr-x.  3 root root  4096 Aug  7 02:17 jvm-exports
drwxr-xr-x.  4 root root  4096 Aug  7 02:17 jvm-private
drwxr-xr-x.  6 root root  4096 Aug  6 20:18 kbd
drwxr-xr-x.  2 root root  4096 Aug  6 20:18 kdump
drwxr-xr-x.  3 root root  4096 Feb 20  2018 kernel
drwxr-xr-x.  2 root root  4096 Aug  6 20:18 locale
drwxr-xr-x.  2 root root  4096 Aug  6 20:18 modprobe.d
drwxr-xr-x.  3 root root  4096 Aug  6 20:18 modules
drwxr-xr-x.  2 root root  4096 Feb 20  2018 modules-load.d
drwxr-xr-x.  4 root root  4096 Aug  6 20:18 NetworkManager
drwxr-xr-x.  2 root root  4096 Aug  6 20:18 polkit-1
drwxr-xr-x.  3 root root  4096 Aug  6 20:18 python2.7
drwxr-xr-x.  5 root root  4096 Aug  7 02:17 rpm
lrwxrwxrwx.  1 root root    30 Aug  6 20:19 sendmail -> /etc/alternatives/mta-sendmail
lrwxrwxrwx.  1 root root    24 Aug  6 20:18 sendmail.postfix -> ../sbin/sendmail.postfix
dr-xr-xr-x.  2 root root  4096 Dec 14  2017 sse2
drwxr-xr-x.  2 root root  4096 Aug  7 02:18 sysctl.d
drwxr-xr-x. 13 root root  4096 Aug  7 02:17 systemd
drwxr-xr-x.  2 root root  4096 Aug  7 02:18 tmpfiles.d
drwxr-xr-x. 12 root root  4096 Aug  6 20:18 tuned
drwxr-xr-x.  4 root root  4096 Aug  6 20:18 udev
drwxr-xr-x.  2 root root  4096 Aug  6 20:18 yum-plugins 
```
