# 2. Creación y edición de archivos
![](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel003.png)

**Meta:**
  * Entender los conceptos necesarios para el manejo de archivos en linux.

**Objetivos:** 
  * Aprender a utilizar los programas de edición por línea de comando y atajos.

**Secciones:**
  * Utilizando editores de texto y atajos. (Teoría - practica)

**Laboratorio:**
  * Editando archivos de configuración utilizando atajos.

# Utilizando editores de texto y atajos ( Teoría – Practica)

**Objetivos**:
  Después de completar esta sección el estudiante estará preparado para:
* Manejo de vi,vim,nano para edición de archivos de configuración y conocer atajos para trabajar de forma eficiente.
# Vi-Vim Grafico comparativo (Teoria)
![Vi-Vim](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel004.png)

**El siguiente cuadro referencial indica en resumen la función de cada directorio del sistema de archivos linux**

| Editores | Descripción |
| --- | --- |
| vi | Significa Visual. Es un editor de texto que es un primer intento de un editor de texto visual. |
| vim | Son las siglas de Vi IMproved. Es una implementación del estándar Vi con muchas adiciones. Es la implementación del estándar más utilizada. |
| nano | Es un editor de texto para sistemas Unix basado en curses. |


# Editando archivos con Vi-Vim (Teoria)
Para poder utilizar el editor vi o vim debemos entender el siguiente flujo basico:
![Vi-Vim2](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel005.png)

**Modo normal**
  * Es el modo predeterminado.
  * Permite un movimiento rápido por el texto.
  * Modificación rápida de texto.
  * Cambiar a otros modos.

**Modo de inserción**
  * Modificar el archivo insertando nuevo texto

**Modo visual**
  * Seleccionar parte del texto para operar sobre él.

**Modo de comando o ejecución de comando**
  * Operación básica del editor (abrir, cerrar, escribir ...)
  * Edición masiva a través de `comandos ex`

# Atajos para Vim (Teoria)

**Atajos de Edición**
| Key | Descripción |
| --- | --- |
| i | Cambie al modo de inserción y comience a insertar antes de la posición actual del cursor.|
| I | Mueva el cursor al inicio de la línea actual y cambie al modo de inserción.|
| a | Cambie al modo de inserción y comience a insertar después de la posición actual del cursor.|
| A | Mueva el cursor al final de la línea actual y cambie al modo de inserción.|
| o | Abra una nueva línea debajo de la actual y cambie al modo de inserción.|
| O | Abra una nueva línea sobre la actual y cambie al modo de inserción.|
| R | Cambie al modo de reemplazo, comenzando en el carácter debajo del cursor.|

**Atajos de Movimiento**
| Key | Descripción |
| --- | --- |
| h | Mover el cursor hacia la izquierda.|
| j | Mover el cursor hacia abajo.|
| k | Mover el cursor hacia arriba.|
| l | Mover el cursor hacia la derecha.|
| H | Mover el cursor al inicio.|
| M | Mover el cursor al medio.|
| L | Mover el cursor al final.|
| gg | Mover el cursor al inicio.|
| G | Mover el cursor al final.|
| ^ | Mover el cursor al inicio de la linea.|
| $ | Mover el cursor al final de la linea.|

**Atajos para guardar**
| Key | Descripción |
| --- | --- |
| :wq | Guarde y salga del archivo actual.|
| :x | Guarde el archivo actual si hay cambios sin guardar, luego salga.|
| :w | Guarde el archivo actual y permanezca en el editor.|
| :w <filename> | Guarde el archivo actual con un nombre de archivo diferente.|
| :q | Salga del archivo actual (solo si no hay cambios sin guardar).|
| :q! | Salga del archivo actual, ignorando los cambios no guardados.|

**Atajos Varios**
| Key | Descripción |
| --- | --- |
| / | Buscar una palabra dentro de un archivo.|
| :set nu | Poner numeración a las lineas en un archivo.|
| :set nonu | Quitar numeración a las lineas en un archivo.|
| :\<numero_de _linea\> | Ir a una linea especifica.|
| ciw,caw | Cambiar una palabra.|
| cc,c$,C | Reemplazar una linea.|
| r | Reemplazar un carácter.|
| ~ | Cambiar de Lower a Upper Case y viceversa.|
| dd,D | Borrar una linea.|
| x | Borrar un caracter.|
| yy | Copiar una linea.|
| yiw,yaw | Copiar una palabra.|
| p | Pegar lineas o palabras copiadas.|
| u | Deshacer un cambio.|
| Ctrl + r | Recuperar un cambio.|
|:%s/\<old>\/\<new>\/g| Reemplazar una palabra por una nueva.|



# Laboratorio: Editando archivos de configuración utilizando atajos.
En el siguiente laboratorio tendrá que realizar las siguientes operaciones:
1. Editar el archivo sshd_config_template ubicado en el home del usuario root, entre al archive y coloque el modo de numeración de linea.
2. Modificar la directiva de #LoginGraceTime 2m yes a LoginGraceTime 5m  utilizando la función de buscar (/), luego edite y grabe sin salir del archivo.
3. Modificar la directiva #ListenAddress 0.0.0.0 a ListenAddress <ipv4_asignada> utilizando el modo de ejecución :%s/\<old\>/\<new\>/g
4. Copiar las primeras 10 lineas del archivo sshd_config_template y pegarlas al final del archivo.
5. Modificar la directiva #Banner none a Banner /etc/issue que se encuentra en la linea 123, utilizando el modo de ejecucion :\<number_line\> 
6. Grabar los cambios en un nuevo archivo que se llame sshd_config_template_final.

Solución:

1. Editar el archivo sshd_config_template ubicado en el home del usuario root, entre al archive y coloque el modo de numeración de linea.
```
[root@nova ~]# vim sshd_config_template
#       $OpenBSD: sshd_config,v 1.100 2016/08/15 12:32:04 naddy Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/local/bin:/usr/bin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.

# If you want to change the port on a SELinux system, you have to tell
# SELinux about this change.
# semanage port -a -t ssh_port_t -p tcp #PORTNUMBER
#
#Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::

HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_dsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key

# Ciphers and keying
#RekeyLimit default none

# Logging
#SyslogFacility AUTH
SyslogFacility AUTHPRIV
#LogLevel INFO

# Authentication:

#LoginGraceTime 2m
#PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

#PubkeyAuthentication yes
:set nu
```

2. Modificar la directiva de #LoginGraceTime 2m yes a LoginGraceTime 5m  utilizando la función de buscar (/), luego edite y grabe sin salir del archivo.
```
[root@nova ~]# vim sshd_config_template
 ...
 37 #LoginGraceTime 2m
 38 #PermitRootLogin yes
 39 #StrictModes yes
 40 #MaxAuthTries 6
 41 #MaxSessions 10
 42
 43 #PubkeyAuthentication yes
/LoginGraceTime       
```
Modificar como sigue:
```
 37 LoginGraceTime 5m
 38 #PermitRootLogin yes
 39 #StrictModes yes
 40 #MaxAuthTries 6
 41 #MaxSessions 10
 42
 43 #PubkeyAuthentication yes
/LoginGraceTime       
```
3. Modificar la directiva #ListenAddress 0.0.0.0 a ListenAddress <ipv4_asignada> utilizando el modo de ejecución :%s/\<old\>/\<new\>/g
```
[root@nova ~]# vim sshd_config_template
#Port 22
#AddressFamily any
#ListenAddress 0.0.0.0
#ListenAddress ::

HostKey /etc/ssh/ssh_host_rsa_key
#HostKey /etc/ssh/ssh_host_dsa_key
HostKey /etc/ssh/ssh_host_ecdsa_key
HostKey /etc/ssh/ssh_host_ed25519_key

# Ciphers and keying
#RekeyLimit default none

# Logging
#SyslogFacility AUTH
SyslogFacility AUTHPRIV
#LogLevel INFO

# Authentication:

#LoginGraceTime 2m
#PermitRootLogin yes
#StrictModes yes
#MaxAuthTries 6
#MaxSessions 10

#PubkeyAuthentication yes
:%s/#ListenAddress 0.0.0.0/ListenAddress 192.168.0.110/g
```
Validar resultado:

```
...
#Port 22
#AddressFamily any
ListenAddress 192.168.0.110
#ListenAddress ::
...
```
 
4. Copiar las primeras 10 lineas del archivo sshd_config_template y pegarlas al final del archivo.
En el modo normal digitar **10yy**, esto hará que al final del archivo se indique **10 lines yanked**, luego presionar **Shift + g (G)** y finalmente el caracter **p** para pegar.
```
[root@nova ~]# vim sshd_config_template
#       $OpenBSD: sshd_config,v 1.100 2016/08/15 12:32:04 naddy Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/local/bin:/usr/bin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
# default value.

# If you want to change the port on a SELinux system, you have to tell
# SELinux about this change.
# semanage port -a -t ssh_port_t -p tcp #PORTNUMBER
10 lines yanked                                         
```
Pegar al final:
```
...
KerberosAuthentication no
PubkeyAuthentication yes
UsePAM yes
AuthorizedKeysCommand /usr/bin/sss_ssh_authorizedkeys
GSSAPIAuthentication yes
ChallengeResponseAuthentication yes
AuthorizedKeysCommandUser nobody
#       $OpenBSD: sshd_config,v 1.100 2016/08/15 12:32:04 naddy Exp $

# This is the sshd server system-wide configuration file.  See
# sshd_config(5) for more information.

# This sshd was compiled with PATH=/usr/local/bin:/usr/bin

# The strategy used for options in the default sshd_config shipped with
# OpenSSH is to specify options with their default value where
# possible, but leave them commented.  Uncommented options override the
```
5. Modificar la directiva #Banner none a Banner /etc/issue que se encuentra en la linea 123, utilizando el modo de ejecucion :\<number_line\> 
```
[root@nova ~]# vim sshd_config_template
...
123 #Banner none
...
154 # The strategy used for options in the default sshd_config shipped with
155 # OpenSSH is to specify options with their default value where
156 # possible, but leave them commented.  Uncommented options override the
:123                                                                            
```
Modificar como sigue:
```
...
123 Banner /etc/issue
...
154 # The strategy used for options in the default sshd_config shipped with
155 # OpenSSH is to specify options with their default value where
156 # possible, but leave them commented.  Uncommented options override the
```
6. Grabar los cambios en un nuevo archivo que se llame sshd_config_template_final.
```
[root@nova ~]# vim sshd_config_template
...
149 # This is the sshd server system-wide configuration file.  See
150 # sshd_config(5) for more information.
151
152 # This sshd was compiled with PATH=/usr/local/bin:/usr/bin
153
154 # The strategy used for options in the default sshd_config shipped with
155 # OpenSSH is to specify options with their default value where
156 # possible, but leave them commented.  Uncommented options override the
:w /root/sshd_config_template_final
```