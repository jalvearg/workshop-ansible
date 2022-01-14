<h1>Entendimiento y gestión de organizaciones</h1>
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
<br>- Crear Organizaciones en Satellite por GUI. (Demostrativo)
<br>- Crear Organizaciones en Satellite por CLI hammer. (Demostrativo)
<br>- Crear Ubicaciones en Satellite por GUI. (Demostrativo)
<br>- Crear Ubicaciones en Satellite por CLI hammer. (Demostrativo)
<br>- Laboratorio: Creando Organizaciones y Ubicaciones en Red Hat Satellite por GUI y Hammer
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Crear Organizaciones en Satellite por GUI. (Demostrativo)
La siguiente demostración tiene como finalidad aprender a crear organizaciones por la herramienta gráfica.

**Administrar > Organizaciones**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat500.png?raw=true"width="800" height="400"></p>

En la pagina de Organziaciones darle click al boton **Nueva organización**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat501.png?raw=true"width="800" height="400"></p>

Ingresar los datos como se muestra en la imagen y darle click al boton **Enviar**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat502.png?raw=true"width="800" height="400"></p>

Verificar que la nueva organización se haya creado de manera satisfactoria en la pagina **Organizaciones**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat503.png?raw=true"width="800" height="400"></p>

# Crear Organizaciones en Satellite por CLI hammer. (Demostrativo)
Autenticarse utilizando la herramienta hammer
```
[root@satellite ~]# hammer auth login basic
[Foreman] Username: admin
[Foreman] Password for admin:
Successfully logged in as 'admin'.
```
Crear la organización **Aplicaciones** con etiqueta **apps** y descripción **'Servidores del área de aplicaciones'**
```
[root@satellite ~]# hammer organization create  --name Aplicaciones --label apps --description 'Servidores del área de aplicaciones'
```
Listar las organizaciones para validar
```
[root@satellite ~]# hammer organization list
---|----------------------|----------------------|-------------------------------------|---------------------
ID | TITLE                | NAME                 | DESCRIPTION                         | LABEL
---|----------------------|----------------------|-------------------------------------|---------------------
12 | Aplicaciones         | Aplicaciones         | Servidores del área de aplicaciones | apps
1  | Default Organization | Default Organization |                                     | Default_Organization
4  | Global Bank          | Global Bank          | Organización Principal              | principal
3  | Opennova             | Opennova             |                                     | ON
---|----------------------|----------------------|-------------------------------------|---------------------
```

Borrar la organización **Aplicaciones**
```
[root@satellite ~]# hammer organization delete --name Aplicaciones
[....................................................................................................................................................] [100%]
```
Listar las organizaciones para validar
```
[root@satellite ~]# hammer organization list
---|----------------------|----------------------|------------------------|---------------------
ID | TITLE                | NAME                 | DESCRIPTION            | LABEL
---|----------------------|----------------------|------------------------|---------------------
1  | Default Organization | Default Organization |                        | Default_Organization
4  | Global Bank          | Global Bank          | Organización Principal | principal
3  | Opennova             | Opennova             |                        | ON
---|----------------------|----------------------|------------------------|---------------------
```

# Crear Ubicaciones en Satellite por GUI. (Demostrativo)
**Administrar > Ubicaciones**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat504.png?raw=true"width="800" height="400"></p>

En la pagina de Ubicaciones darle click al boton **Nueva ubicacion**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat505.png?raw=true"width="800" height="400"></p>

Ingresar los datos como se muestra en la imagen y darle click al boton **Enviar**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat506.png?raw=true"width="800" height="400"></p>

Verificar que la nueva ubicacion se haya creado de manera satisfactoria en la pagina **Ubicaciones**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat507.png?raw=true"width="800" height="400"></p>

Asociar la nueva ubicación Panamá a la organización Global Bank

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat508.png?raw=true"width="800" height="400"></p>

En la pagina de Organizaciones darle click al boton **Editar**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat512.png?raw=true"width="800" height="400"></p>

**Ubicaciones > Panamá y darle click al símbolo de las flechas**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat509.png?raw=true"width="800" height="400"></p>

Luego darle click al botón **Enviar**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat510.png?raw=true"width="800" height="400"></p>

En la parte superior izquierda en la parte oscura validar que exista la **organización Global Bank** y **la ubicación Panamá**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat511.png?raw=true"width="800" height="400"></p>

# Crear Ubicaciones en Satellite por CLI hammer. (Demostrativo)
Autenticarse utilizando la herramienta hammer
```
[root@satellite ~]# hammer auth login basic
[Foreman] Username: admin
[Foreman] Password for admin:
Successfully logged in as 'admin'.
```
Crear la ubicación **'San Isidro'** con la descripción 'Data Center Level 3'
```
[root@satellite ~]# hammer location create --name 'San Isidro' --description 'Data Center Level 3'
Location created.
```
Listar las ubicaciones para validar
```
[root@satellite ~]# hammer location list
---|------------------|------------------|--------------------
ID | TITLE            | NAME             | DESCRIPTION
---|------------------|------------------|--------------------
2  | Default Location | Default Location |
6  | Lima             | Lima             | Sede Sucursal
8  | Panamá           | Panamá           | Sede Principal
13 | San Isidro       | San Isidro       | Data Center Level 3
---|------------------|------------------|--------------------
```
Borrar la ubicación **'San Isidro'**
```
[root@satellite ~]# hammer location delete --name 'San Isidro'
Location deleted.
```
Listar las ubicaciones para validar
```
[root@satellite ~]# hammer location list
---|------------------|------------------|---------------
ID | TITLE            | NAME             | DESCRIPTION
---|------------------|------------------|---------------
2  | Default Location | Default Location |
6  | Lima             | Lima             | Sede Sucursal
8  | Panamá           | Panamá           | Sede Principal
---|------------------|------------------|---------------
```

Crear la organización y ubicación eliminadas en los pasos anteriores
```
[root@satellite ~]# hammer organization create  --name Aplicaciones --label apps --description 'Servidores del área de aplicaciones'
[root@satellite ~]# hammer location create --name 'San Isidro' --description 'Data Center Level 3'
```
Asignar la ubicación **'San Isidro'** a la organización **Aplicaciones**
```
[root@satellite ~]# hammer organization add-location --help
Usage:
    hammer organization add-location [OPTIONS]

Options:
 --id ID                         Organization ID
 --location LOCATION_NAME        Location name
 --location-id LOCATION_ID
 --location-title LOCATION_TITLE Location title
 --name NAME                     Organization name
 --title TITLE                   Organization title
 -h, --help                      Print help
```
```
[root@satellite ~]# hammer organization list
---|----------------------|----------------------|-------------------------------------|---------------------
ID | TITLE                | NAME                 | DESCRIPTION                         | LABEL
---|----------------------|----------------------|-------------------------------------|---------------------
15 | Aplicaciones         | Aplicaciones         | Servidores del area de aplicaciones | apps
1  | Default Organization | Default Organization |                                     | Default_Organization
4  | Global Bank          | Global Bank          | Organizacion Principal              | principal
3  | Opennova             | Opennova             |                                     | ON
---|----------------------|----------------------|-------------------------------------|---------------------
```
```
[root@satellite ~]# hammer location list
---|------------------|------------------|--------------------
ID | TITLE            | NAME             | DESCRIPTION
---|------------------|------------------|--------------------
2  | Default Location | Default Location |
6  | Lima             | Lima             | Sede Sucursal
8  | Panamá           | Panamá           | Sede Principal
14 | San Isidro       | San Isidro       | Data Center Level 3
---|------------------|------------------|--------------------
```
```
[root@satellite ~]# hammer organization add-location --name Aplicaciones --location 'San Isidro'
The location has been associated.
```
```
[root@satellite ~]# hammer organization info --name Aplicaciones | tail -n 10

Locations:
    San Isidro
Created at:             2020/08/28 06:20:53
Updated at:             2020/08/28 06:20:53
Label:                  apps
Description:            Servidores del area de aplicaciones
Red Hat Repository URL: https://cdn.redhat.com
Service Levels:
```
# Laboratorio de la Unidad
<br>El siguiente laboratorio se realizara en el servidor Satellite instalado en el capitulo anterior
<br>
### <br>**1. Crear una Organización y Ubicaciones utilizando la GUI**
<br>**Crear una Organización con los siguiente datos:**
<br>Nombre: **Aplicaciones**
<br>Label: **apps**
<br>
<br>**Crear una Ubicación con los siguiente datos:**
<br>Nombre: **Panamá**
<br>Descripción: **'Sede Principal'**
<br>**Asociar la Ubicación Panamá a la Organización Aplicaciones**
<br>
### 2. Crear una Organización y Ubicación utilizando la CLI hammer.**
<br>**Crear una Organización con los siguiente datos:**
<br>Nombre: **Cajeros**
<br>Label: **caj**
<br>Descripción: **'Servidores de la Organización Cajeros'** 
<br>
<br>**Crear una Ubicación con los siguiente datos:**
<br>Nombre: **Lima** 
<br>Descripción: **'Sede Sucursal'**
<br>
<br>**Asociar la Ubicación Lima a la Organización Cajeros**

<br>Utilizar la demostración previa como solucionario para este laboratorio. 
<br>Si tiene dudas o consultas escriba a los instructores a cargo por el chat.