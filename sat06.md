<h1>Entendimiento y gestión de usuarios</h1>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat100.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento de la gestión de organizaciones y ubicaciones en Red Hat Satellite.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Identificación y planificación de Organizaciones y Ubicaciones en Red Hat Satellite (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Crear Usuarios en Satellite por GUI. (Demostrativo)
<br>- Crear Usuarios en Satellite por CLI hammer. (Demostrativo)
<br>- Crear Grupos en Satellite por GUI. (Demostrativo)
<br>- Crear Grupos en Satellite por CLI hammer. (Demostrativo)
<br>- Crear Roles en Satellite por GUI. (Demostrativo)
<br>- Crear Roles en Satellite por CLI hammer. (Demostrativo)
<br>- Laboratorio: Creando usuarios, grupos y roles en Red Hat Satellite por GUI y CLI
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Crear usuarios en Satellite por GUI. (Demostrativo)
La siguiente demostración tiene como finalidad aprender a crear usuarios por la herramienta gráfica.

**Administrar > Usuarios**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat600.png?raw=true"width="800" height="400"></p>

En la pagina de Usuarios darle click al boton **Crear usuario**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat601.png?raw=true"width="800" height="400"></p>

Ingresar los datos como se muestra en la imagen y darle click al boton **Enviar**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat602.png?raw=true"width="800" height="400"></p>

Verificar que el nuevo usuario se haya creado de manera satisfactoria en la pagina **Usuarios**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat603.png?raw=true"width="800" height="400"></p>

Seleccionar en la lista de la **columna acciones** la opción **Impersonate** para validar los accesos efectivos

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat603_00.png?raw=true"width="800" height="400"></p>

Verificar que se ha cambiado al usuario temporalmente de manera satisfactoria

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat603_01.png?raw=true"width="800" height="400"></p>

Marcar el símbolo de Impersonate y confirmar para salir del modo

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat603_02.png?raw=true"width="800" height="400"></p>

Hacer click en el **nombre del usuario** para modificar sus propiedades y adicionarle el **rol de administrador**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat603_04.png?raw=true"width="800" height="400"></p>

Dentro del las opciones de **roles** marcar la **casilla de Administrador** y presionar el botón **Enviar**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat603_05.png?raw=true"width="800" height="400"></p>

Verificar que el usuario ahora tenga en la **columna Administrador** el check **activado**.

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat603_06.png?raw=true"width="800" height="400"></p>

Salir temporalmente de la cuenta de administrador para validar el acceso a nivel administrador para el usuario

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat603_07.png?raw=true"width="800" height="400"></p>

Ingresar las credenciales

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat603_08.png?raw=true"width="800" height="400"></p>

Validar el acceso y rol Administrador

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat603_09.png?raw=true"width="800" height="400"></p>

# Crear usuarios en Satellite por CLI hammer. (Demostrativo)
Autenticarse utilizando la herramienta hammer
```
[root@satellite ~]# hammer auth login basic
[Foreman] Username: admin
[Foreman] Password for admin:
Successfully logged in as 'admin'.
```
Crear usuario con los datos que se muestran en la siguiente salida.

```
[root@satellite ~]# hammer user create --login andy.reyes --firstname Andy --lastname Reyes --mail andy.reyes@opennova.pe --default-organization 'Default Organization' --default-location 'Default Location' --password redhat --auth-source 'Internal' --admin true
```
NOTA: Para identificar la información de organización,ubicación y fuente de autenticación utilizar las salidas indicadas.
```
[root@satellite ~]# hammer organization list
---|----------------------|----------------------|-------------------------------------|---------------------
ID | TITLE                | NAME                 | DESCRIPTION                         | LABEL
---|----------------------|----------------------|-------------------------------------|---------------------
16 | Aplicaciones         | Aplicaciones         | Servidores del área de aplicaciones | apps
1  | Default Organization | Default Organization |                                     | Default_Organization
4  | Global Bank          | Global Bank          | Organización Principal              | principal
3  | Opennova             | Opennova             |                                     | ON
---|----------------------|----------------------|-------------------------------------|---------------------
[root@satellite ~]# hammer location list
---|------------------|------------------|--------------------
ID | TITLE            | NAME             | DESCRIPTION
---|------------------|------------------|--------------------
2  | Default Location | Default Location |
6  | Lima             | Lima             | Sede Sucursal
8  | Panamá           | Panamá           | Sede Principal
14 | San Isidro       | San Isidro       | Data Center Level 3
---|------------------|------------------|--------------------
[root@satellite ~]# hammer auth-source list
---|----------|--------------------
ID | NAME     | TYPE OF AUTH SOURCE
---|----------|--------------------
1  | Internal | AuthSourceInternal
---|----------|--------------------
```

Listar los usuarios para validar
```
[root@satellite ~]# hammer user list
---|---------------|---------------|---------------------------|-------|---------------------|--------------
ID | LOGIN         | NAME          | EMAIL                     | ADMIN | LAST LOGIN          | AUTHORIZED BY
---|---------------|---------------|---------------------------|-------|---------------------|--------------
4  | admin         | Admin User    | root@opennova.pe          | yes   | 2020/08/29 16:38:26 | Internal
8  | andy.reyes    | Andy Reyes    | andy.reyes@opennova.pe    | yes   |                     | Internal
5  | jaime.zamudio | Jaime Zamudio | jaime.zamudio@opennova.pe | yes   | 2020/08/29 02:01:47 | Internal
---|---------------|---------------|---------------------------|-------|---------------------|--------------
```

Autenticarse por linea de comandos con el usuario andy.reyes y realizar consultas.
```
[root@satellite ~]# hammer auth login basic --username andy.reyes --password redhat
Successfully logged in as 'andy.reyes'.
[root@satellite ~]# hammer organization list
---|----------------------|----------------------|-------------------------------------|---------------------
ID | TITLE                | NAME                 | DESCRIPTION                         | LABEL
---|----------------------|----------------------|-------------------------------------|---------------------
16 | Aplicaciones         | Aplicaciones         | Servidores del área de aplicaciones | apps
1  | Default Organization | Default Organization |                                     | Default_Organization
4  | Global Bank          | Global Bank          | Organizacion Principal              | principal
3  | Opennova             | Opennova             |                                     | ON
---|----------------------|----------------------|-------------------------------------|---------------------
[root@satellite ~]# hammer location list
---|------------------|------------------|--------------------
ID | TITLE            | NAME             | DESCRIPTION
---|------------------|------------------|--------------------
2  | Default Location | Default Location |
6  | Lima             | Lima             | Sede Sucursal
8  | Panamá           | Panamá           | Sede Principal
14 | San Isidro       | San Isidro       | Data Center Level 3
---|------------------|------------------|--------------------
[root@satellite ~]# hammer user list
---|---------------|---------------|---------------------------|-------|---------------------|--------------
ID | LOGIN         | NAME          | EMAIL                     | ADMIN | LAST LOGIN          | AUTHORIZED BY
---|---------------|---------------|---------------------------|-------|---------------------|--------------
4  | admin         | Admin User    | root@opennova.pe          | yes   | 2020/08/29 16:38:26 | Internal
8  | andy.reyes    | Andy Reyes    | andy.reyes@opennova.pe    | yes   |                     | Internal
5  | jaime.zamudio | Jaime Zamudio | jaime.zamudio@opennova.pe | yes   | 2020/08/29 02:01:47 | Internal
---|---------------|---------------|---------------------------|-------|---------------------|--------------
```

Validar el acceso por GUI

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat618.png?raw=true"width="800" height="400"></p>

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat617.png?raw=true"width="800" height="400"></p>

Actualizar la contraseña del usuario andy.reyes
```
[root@satellite ~]# hammer user update --password redhat123 --login andy.reyes
[Foreman] Username: andy.reyes
[Foreman] Password for andy.reyes:
User [andy.reyes] updated.
```
Validar que ahora acepte la nueva contraseña
```
[root@satellite ~]# hammer auth login basic --username andy.reyes --password redhat
Invalid credentials, continuing with session for 'andy.reyes'.
[root@satellite ~]# hammer auth login basic --username andy.reyes --password redhat123
Successfully logged in as 'andy.reyes'.
[root@satellite ~]# hammer user list
---|---------------|---------------|---------------------------|-------|---------------------|--------------
ID | LOGIN         | NAME          | EMAIL                     | ADMIN | LAST LOGIN          | AUTHORIZED BY
---|---------------|---------------|---------------------------|-------|---------------------|--------------
4  | admin         | Admin User    | root@opennova.pe          | yes   | 2020/08/29 16:38:26 | Internal
8  | andy.reyes    | Andy Reyes    | andy.reyes@opennova.pe    | yes   | 2020/08/29 17:14:23 | Internal
5  | jaime.zamudio | Jaime Zamudio | jaime.zamudio@opennova.pe | yes   | 2020/08/29 02:01:47 | Internal
---|---------------|---------------|---------------------------|-------|---------------------|--------------
```

Borrar el usuario andy.reyes
```
[root@satellite ~]# hammer user delete --login andy.reyes
User [andy.reyes] deleted.
```
Listar las organizaciones para validar
```
[root@satellite ~]# hammer user list
---|---------------|---------------|---------------------------|-------|---------------------|--------------
ID | LOGIN         | NAME          | EMAIL                     | ADMIN | LAST LOGIN          | AUTHORIZED BY
---|---------------|---------------|---------------------------|-------|---------------------|--------------
4  | admin         | Admin User    | root@opennova.pe          | yes   | 2020/08/29 16:38:26 | Internal
5  | jaime.zamudio | Jaime Zamudio | jaime.zamudio@opennova.pe | yes   | 2020/08/29 02:01:47 | Internal
---|---------------|---------------|---------------------------|-------|---------------------|--------------
```

# Crear Grupos de usuarios en Satellite por GUI. (Demostrativo)
**Administrar > Grupos de usuario**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat604.png?raw=true"width="800" height="400"></p>

En la pagina de Grupos de usuario darle click al botón **Crear grupos de usuario**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat605.png?raw=true"width="800" height="400"></p>

Ingresar los datos como se muestra en la imagen y darle click al boton **Enviar**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat606.png?raw=true"width="800" height="400"></p>

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat607.png?raw=true"width="800" height="400"></p>

Verificar y editar el grupo de usuarios

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat608_00.png?raw=true"width="800" height="400"></p>

En la opción de **roles** seleccionar la **casilla de Administrar** y darle al botón **Enviar**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat608_01.png?raw=true"width="800" height="400"></p>

# Crear Grupos de usuario en Satellite por CLI hammer. (Demostrativo)
Autenticarse utilizando la herramienta hammer
```
[root@satellite ~]# hammer auth login basic
[Foreman] Username: admin
[Foreman] Password for admin:
Successfully logged in as 'admin'.
```
Crear el grupo de usuario dba_admins con los datos que se muestran en la siguiente salida.
```
[root@satellite ~]# hammer user-group create --name dba_admins --organization "Default Organization" --location "Default Location" --admin true --users andy.reyes
User group [dba_admins] created.
```
Listar los grupos de usuario para validar
```
[root@satellite ~]# hammer user-group list
---|-------------|------
ID | NAME        | ADMIN
---|-------------|------
1  | apps_admins | yes
2  | dba_admins  | yes
---|-------------|------
```
Listar la información del grupo de usuario dba_admins

```
[root@satellite ~]# hammer user-group info --name dba_admins
Id:                   2
Name:                 dba_admins
Admin:                yes
Users:
    andy.reyes
User groups:

External user groups:

Roles:

Created at:           2020/08/29 18:11:53
Updated at:           2020/08/29 18:11:53
```
Listar la información del usuario y verificar que tiene el grupo asociado
```
[root@satellite ~]# hammer user info --login andy.reyes
Id:                    9
Login:                 andy.reyes
Name:                  Andy Reyes
Email:                 andy.reyes@opennova.pe
Admin:                 yes
Last login:            2020/08/29 18:45:40
Authorized by:         Internal
Effective admin:       yes
Locale:                default
Timezone:              default
Description:
Default organization:  Default Organization
Default location:      Default Location
Roles:

User groups:
 1) Usergroup: dba_admins
    Roles:
Inherited User groups:

Created at:            2020/08/29 17:05:52
Updated at:            2020/08/29 18:45:25
```

Agregar un nuevo usuario al grupo dba_admins
```
[root@satellite ~]# hammer user-group add-user --user jaime.zamudio --name dba_admins
The user has been associated.
[root@satellite ~]# hammer user-group info --name dba_admins
Id:                   2
Name:                 dba_admins
Admin:                yes
Users:
    andy.reyes
    jaime.zamudio
User groups:

External user groups:

Roles:

Created at:           2020/08/29 18:11:53
Updated at:           2020/08/29 18:11:53
```

Modificar el nombre del grupo de usuarios a dbas_admin
```
[root@satellite ~]# hammer user-group update --name dba_admins --new-name dbas_admins
User group [dbas_admins] updated.
[root@satellite ~]# hammer user-group list
---|-------------|------
ID | NAME        | ADMIN
---|-------------|------
1  | apps_admins | yes
2  | dbas_admins | yes
---|-------------|------
[root@satellite ~]# hammer user-group info --name dbas_admins
Id:                   2
Name:                 dbas_admins
Admin:                yes
Users:
    andy.reyes
    jaime.zamudio
User groups:

External user groups:

Roles:

Created at:           2020/08/29 18:11:53
Updated at:           2020/08/29 19:20:02
```


Borrar el grupo de usuarios **dbas_admin**
```
[root@satellite ~]# hammer user-group delete --name dbas_admins
User group [dbas_admins] deleted.
```
Listar el grupo de usuario para validar
```
[root@satellite ~]# hammer user-group list
---|-------------|------
ID | NAME        | ADMIN
---|-------------|------
1  | apps_admins | yes
---|-------------|------
```
# Crear Roles en Satellite por GUI. (Demostrativo)
**Administrar > Roles**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat609.png?raw=true"width="800" height="400"></p>

En la pagina de Roles darle click al botón **Crear rol**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat610.png?raw=true"width="800" height="400"></p>

Ingresar los datos como se muestra en la imagen y darle click al botón **Enviar**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat611.png?raw=true"width="800" height="400"></p>

Verificar que el rol se haya creado de manera satisfactoria y darle click al botón **Filtros**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat612.png?raw=true"width="800" height="400"></p>

En la pagina de filtros darle click al botón **Crear filtro**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat613.png?raw=true"width="800" height="400"></p>

Ingresar los datos como se muestra en la imagen y darle click al botón **Enviar**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat614.png?raw=true"width="800" height="400"></p>

Verificar que el filtro se haya creado de manera satisfactoria

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat615.png?raw=true"width="800" height="400"></p>

Validar en el perfil de un usuario si en la opción de **roles** ahora se pueda buscar el rol Application Admins como muestra la imagen

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat616.png?raw=true"width="800" height="400"></p>

# Crear Roles en Satellite por CLI hammer. (Demostrativo)
Autenticarse utilizando la herramienta hammer
```
[root@satellite ~]# hammer auth login basic
[Foreman] Username: admin
[Foreman] Password for admin:
Successfully logged in as 'admin'.
```
Crear el rol **Database Admins** con los datos que se muestran en la siguiente salida.
```
[root@satellite ~]# hammer role create --name 'Database Admins' --description 'Administradores de Base de Datos' --organization 'Default Organization' --location 'Default Location'
User role [Database Admins] created.
```
Listar los roles para validar
```
[root@satellite ~]# hammer role list
---|--------------------------------|--------
ID | NAME                           | BUILTIN
---|--------------------------------|--------
27 | Access Insights Admin          | no
26 | Access Insights Viewer         | no
16 | Ansible Roles Manager          | no
17 | Ansible Tower Inventory Reader | no
32 | Application Admins             | no
11 | Auditor                        | no
10 | Bookmarks manager              | no
24 | Boot disk access               | no
29 | Compliance manager             | no
28 | Compliance viewer              | no
30 | Create ARF report              | no
33 | Database Admins                | no
1  | Default role                   | yes
19 | Discovery Manager              | no
18 | Discovery Reader               | no
7  | Edit hosts                     | no
5  | Edit partition tables          | no
2  | Manager                        | no
3  | Organization admin             | no
25 | Red Hat Access Logs            | no
20 | Register hosts                 | no
15 | Remote Execution Manager       | no
14 | Remote Execution User          | no
9  | Site manager                   | no
4  | System admin                   | no
12 | Tasks Manager                  | no
13 | Tasks Reader                   | no
8  | Viewer                         | no
6  | View hosts                     | no
22 | Virt-who Manager               | no
21 | Virt-who Reporter              | no
23 | Virt-who Viewer                | no
---|--------------------------------|--------
```
También se puede simplificar la vista con el siguiente comando
```
[root@satellite ~]# hammer role list --search 'Database Admins'
---|-----------------|--------
ID | NAME            | BUILTIN
---|-----------------|--------
33 | Database Admins | no
---|-----------------|--------
```
Listar el permiso **access dashboard**
```
[root@satellite ~]# hammer filter available-permissions --search 'access_dashboard'
---|------------------|----------------
ID | NAME             | RESOURCE
---|------------------|----------------
35 | access_dashboard | (Miscellaneous)
---|------------------|----------------

```
Asociar permiso **access_dashboard** a rol **Database Admins**
```
[root@satellite ~]# hammer filter create --permissions 'access_dashboard' --role 'Database Admins'
```

Listar el filtro asociado al rol 'Database Admins'
```
[root@satellite ~]# hammer filter list --search 'Database Admins'
----|-----------------|--------|------------|-----------|-----------------|-----------------
ID  | RESOURCE TYPE   | SEARCH | UNLIMITED? | OVERRIDE? | ROLE            | PERMISSIONS
----|-----------------|--------|------------|-----------|-----------------|-----------------
321 | (Miscellaneous) | none   | yes        | no        | Database Admins | access_dashboard
----|-----------------|--------|------------|-----------|-----------------|-----------------
```

Asignar el rol 'Database Admins' al usuari 'dbasuser'
```
[root@satellite ~]# hammer user add-role --role 'Database Admins' --login 'dbasuser'
```


Modificar el nombre del rol 'Database Admins' a 'Oracle Database Admins'
```
[root@satellite ~]# hammer role update --new-name 'Oracle Database Admins' --name 'Database Admins'
User role [Oracle Database Admins] updated.
```

Validamos que el cambio conserve el permiso **access_dashboard** hacia el rol **'Oracle Database Admins'**
```
[root@satellite ~]# hammer filter list --search 'Oracle Database Admins'
----|-----------------|--------|------------|-----------|------------------------|-----------------
ID  | RESOURCE TYPE   | SEARCH | UNLIMITED? | OVERRIDE? | ROLE                   | PERMISSIONS
----|-----------------|--------|------------|-----------|------------------------|-----------------
321 | (Miscellaneous) | none   | yes        | no        | Oracle Database Admins | access_dashboard
----|-----------------|--------|------------|-----------|------------------------|-----------------
```
Borrar el rol 'Oracle Database Admins'
```
[root@satellite ~]# hammer role delete --name 'Oracle Database Admins'
User role [Oracle Database Admins] deleted.
```

# Laboratorio de la Unidad
<br>El siguiente laboratorio se realizara en el servidor Satellite instalado en el capitulo anterior
<br>
### <br>**1. Crear un usuario, grupo y rol utilizando la GUI**
<br>**Crear una usuario con los siguiente datos:**
<br> Login: **appsuser** 
<br> Nombre: Administrador
<br> Apellido: Aplicaciones
<br> Correo: appsuser@redhat.com
<br> Autorizado por: INTERNAL
<br> Contraseña: redhat
<br> Verificar: redhat
<br> Habilitar al usuario como Administrador de Satellite.

<br>**Crear una grupo de usuarios con los siguiente datos:**
<br>Nombre: **apps_admins**
<br> Asociar el usuario appsuser al grupo apps_admins
<br> Marcar al grupo como administrador
<br> 

<br>**Crear un rol con los siguiente datos:**
<br> Nombre: **Application Admins**
<br> Ubicacion y Organizacion: Default Location, Default Organization
<br> Aplicar el filtro de access_dashboard
<br> Asociar el rol al usuario appsuser 
<br>

### 2. Crear un usuario, grupo y rol utilizando la CLI hammer.
<br>**Crear una usuario con los siguiente datos:**
<br> Login: **dbasuser** 
<br> Nombre: Administrador
<br> Apellido: Base de Datos
<br> Correo: dbasuser@redhat.com
<br> Autorizado por: INTERNAL
<br> Contraseña: redhat
<br> Verificar: redhat
<br> Habilitar al usuario como Administrador de Satellite.

<br>**Crear una grupo de usuarios con los siguiente datos:**
<br>Nombre: **dbas_admins**
<br> Asociar el usuario dbasuser al grupo dbas_admins
<br> Marcar al grupo como administrador
<br> 

<br>**Crear un rol con los siguiente datos:**
<br> Nombre: **Database Admins**
<br> Ubicacion y Organizacion: Default Location, Default Organization
<br> Aplicar el filtro de access_dashboard
<br> Asociar el rol al usuario dbasuser 
<br>