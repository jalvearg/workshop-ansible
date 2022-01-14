# 6. Manejo básico de usuarios y grupos.

![](https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/rhel013.png)

**Meta:**
  * Entender los conceptos necesarios para la administración de usuarios y grupos.

**Objetivos:** 
  * Entender el procedimiento de creación de usuarios y grupos locales dentro del sistema operativo linux.

**Secciones:**
  * Administración de usuarios locales. (Teoría - Demostración)
  * Administración de grupos locales. (Teoría - Demostración)


**Laboratorio:**
  * Creación de usuarios y asignación de grupos locales.

# Administración de usuarios locales. (Teoría - Demostración)

**Objetivos**:
  Después de completar esta sección el estudiante estará preparado para:
* Crear usuarios locales y entender los archivos de configuración implicados.

# Usuarios Locales Linux (Teoría - Demostración)
Hay tres tipos principales de cuentas de usuario: **superusuario, usuarios del sistema y usuarios regulares.**

**Superusuario**
<br>
La cuenta de superusuario es para la administración del sistema. El nombre del superusuario es root y la cuenta tiene UID 0. 
El superusuario tiene acceso completo al sistema.
<br>
<br>
**Usuario de sistema o Usuario de servicio**
<br>
El sistema tiene cuentas de usuario del sistema que son utilizadas por procesos que brindan soporte servicios. Estos procesos, o demonios, generalmente no necesitan ejecutarse como superusuario. Son cuentas no privilegiadas asignadas que les permiten proteger sus archivos y otros recursos de entre sí y de los usuarios regulares del sistema. Los usuarios no inician sesión de forma interactiva mediante un sistema cuenta de usuario.
<br>
<br>
**Usuario o Usuario regular**
<br>
La mayoría de los usuarios tienen cuentas de usuario regulares que utilizan para su trabajo diario. Como sistema usuarios, los usuarios habituales tienen acceso limitado al sistema.
<br>
<br>
**UID ranges**
<br>
<br>
El **UID 0** siempre se asigna a la cuenta de superusuario, **root.**
<br>
<br>
El **UID 1-200** es un rango de **"usuarios del sistema"** **asignados estáticamente** a los procesos del sistema por **Red Hat.**
<br>
<br>
El **UID 201-999** es un rango de **"usuarios del sistema"** que **utilizan** los **procesos del sistema** que **no poseen archivos en el sistema de archivos.**
<br>
<br>
El **UID 1000+** es el rango disponible para su asignación a **usuarios regulares.**
<br>
<br>
**Archivo principal:** \/etc\/passwd
<br>**Formato:** user01: x :1000:1000:User One:\/home\/user01:\/bin\/bash
<br>
<br>
**Las columnas representan la siguiente informacion:**
| Columna | Descripción |
| --- | --- |
| 1 | Nombre del usuario.|
| 2 | Password encryptado en /etc/shadow.|
| 3 | Identificador de usuario uid. |
| 4 | Identificador de grupo guid.|
| 5 | Descripción o Gecos.|
| 5 | Directorio de trabajo.|
| 6 | Shell.|

# Creación de usuarios locales. (Teoría - Demostración)
**Comando para crear usuario**
<br>``useradd <opciones> <username>``
<br>**Comando para modificar usuario**
<br>``usermod <opciones> <username>``
<br>**Comando para borrar usuario**
<br>``userdel <opciones> <username>``
<br>**Comando para listar opciones**
<br>``useradd --help o usermod --help o userdel --help``
<br>
<br>**Ejemplos**
<br>Crear usuario con uid 1001 y shell /bin/bash
```
[root@nova ~]# useradd -u 1001 -s /bin/bash operador1001
```
<br>Asignar contraseña al usuario operador1001
```
[root@nova ~]# echo "redhat" | passwd --stdin operador1001
```
<br>Verificador los datos de uid,gid y grupos primarios y secundarios asociados a la cuenta
```
[root@nova ~]# id operador1001
uid=1001(operador1001) gid=1001(operador1001) groups=1001(operador1001)
```
<br>Modificar el nombre del usuario operador1001 por operador100
```
[root@nova ~]# usermod -l operador100 operador1001
```
<br>Eliminar la cuenta operador100
```
[root@nova ~]# userdel -r operador100
```
# Administración de grupos locales. (Teoría - Demostración)

**Objetivos**:
  Después de completar esta sección el estudiante estará preparado para:
* Crear grupos locales y entender los archivos de configuración implicados.

# Grupos Locales Linux (Teoría - Demostración)
Hay dos tipos de grupos: **grupos primarios, grupos secundarios o suplementarios.**
<br>
<br>**Grupos primarios**
<br>
Es el que provee el parámetro gid que es el identificador del grupo primario, por lo general cuando se crea un usuario este grupo se crea con el mismo nombre del usuario y sirve para asignar los permisos para ese usuario a los recursos del sistema.
<br>
<br>**Grupo secundario o suplementarios**
<br>
Son los grupos que sea crean con el propósito de agrupar usuarios que realizan tareas en conjunto con un cierto propósito. 
<br>Por ejemplo: developers,devops,netadmins,storageadmins, entre otros. Estos deben agregarse al usuario sin modificar su grupo primario.

**Archivo principal:** \/etc\/group
<br>**Formato:** group01: x: 10000: user01,user02,user03
<br>
<br>
**Las columnas representan la siguiente informacion:**
| Columna | Descripción |
| --- | --- |
| 1 | Nombre del grupo.|
| 2 | Password de grupo, valor teórico.|
| 3 | Identificador de grupo gid. |
| 4 | Lista de usuarios.|

# Creación de grupos locales. (Teoría - Demostración)
**Comando para crear grupo**
<br>``groupadd <opciones> <groupname>``
<br>**Comando para modificar grupo**
<br>``groupmod <opciones> <groupname>``
<br>**Comando para borrar grupo**
<br>``groupdel <opciones> <groupname>``
<br>**Comando para listar opciones**
<br>``groupadd --help o groupmod --help o groupdel --help``
<br>
<br>**Ejemplos**
<br>Crear grupo con gid 2000 y de nombre developers
```
[root@nova ~]# groupadd -g 2000 developers
```
<br>Verificador los datos del grupo
```
[root@nova ~]# grep developers /etc/group
developers:x:2000:
```
<br>Modificar el nombre del grupo developers por devops
```
[root@nova ~]# groupmod -n devops developers
```
<br>Eliminar el grupo devops
```
[root@nova ~]# groupdel devops
```
<br>Crear el usuario devops01 y agregar los grupos prod, dev y qa como grupos secundarios.
```
[root@nova ~]# useradd devops
[root@nova ~]# groupadd prod
[root@nova ~]# groupadd dev
[root@nova ~]# groupadd qa
[root@nova ~]# usermod -aG prod devops
[root@nova ~]# usermod -aG dev devops
[root@nova ~]# usermod -aG qa devops
[root@nova ~]# id devops
uid=1002(devops) gid=1002(devops) groups=1002(devops),2001(prod),2002(dev),2003(qa)

```
# Laboratorio: Explorando el sistema de archivos linux
En el siguiente laboratorio tendrá que realizar las siguientes operaciones:
1. Crear el grupo prod con identificador de grupo 2000
2. Crear el grupo dev con identificador de grupo 3000
3. Crear el grupo qa con identificador de grupo 4000
4. Crear los usuarios jonas, martha, claudia los cuales deberán pertenecer al grupo prod como grupo secundario
5. Crear los usuarios hannah, katharina, charlotte los cuales deberán pertenecer al grupo dev como grupo secundario.
6. Crear los usuarios noah, helge, peter los cuales deberán pertenecer al grupo qa como grupo secundario.
Nota: El password para todos los usuarios deberá ser ``redhat`` y deberán conservar su grupo primario.

Solución:

1. Crear el grupo prod con identificador de grupo 2000
```
[root@nova ~]# groupadd -g 2000 prod
```

2. Crear el grupo dev con identificador de grupo 3000
```
[root@nova ~]# groupadd -g 3000 dev
```
3. Crear el grupo qa con identificador de grupo 4000
```
[root@nova ~]# groupadd -g 4000 qa
```
4. Crear los usuarios jonas, martha, claudia los cuales deberán pertenecer al grupo prod como grupo secundario
```
[root@nova ~]# useradd jonas 
[root@nova ~]# useradd martha
[root@nova ~]# useradd claudia
[root@nova ~]# echo "redhat" | passwd --stdin jonas
[root@nova ~]# echo "redhat" | passwd --stdin martha
[root@nova ~]# echo "redhat" | passwd --stdin claudia
[root@nova ~]# usermod -aG prod jonas
[root@nova ~]# usermod -aG prod martha
[root@nova ~]# usermod -aG prod claudia
```
5. Crear los usuarios hannah, katharina, charlotte los cuales deberán pertenecer al grupo dev como grupo secundario.
```
[root@nova ~]# useradd hannah 
[root@nova ~]# useradd katharina
[root@nova ~]# useradd charlotte
[root@nova ~]# echo "redhat" | passwd --stdin hannah
[root@nova ~]# echo "redhat" | passwd --stdin katharina
[root@nova ~]# echo "redhat" | passwd --stdin charlotte
[root@nova ~]# usermod -aG dev hannah
[root@nova ~]# usermod -aG dev katharina
[root@nova ~]# usermod -aG dev charlotte
```
6. Crear los usuarios noah, helge, peter los cuales deberán pertenecer al grupo qa como grupo secundario.
```
[root@nova ~]# useradd noah
[root@nova ~]# useradd helge
[root@nova ~]# useradd peter
[root@nova ~]# echo "redhat" | passwd --stdin noah
[root@nova ~]# echo "redhat" | passwd --stdin helge
[root@nova ~]# echo "redhat" | passwd --stdin peter
[root@nova ~]# usermod -aG qa noah
[root@nova ~]# usermod -aG qa helge
[root@nova ~]# usermod -aG qa peter 
```