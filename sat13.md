<h1>Tareas de Mantenimiento</h1>

<p>
<strong>Meta:</strong>
<br>Realizar operaciones de mantenimiento sobre la plataforma RH Satellite
</p>
<p>
<strong>Objetivos:</strong>
<br>- Respaldar la solucion
</p>
<p>
<strong>Secciones:</strong>
<br>- Respaldo FULL e INCREMENTAL
</p>
<p>
<strong>Laboratorios:</strong>
<br><strong>- Respaldo de la plataforma</strong>
<br><strong>- Restauracion de la plataforma</strong>
<br><strong>- Ampliando discos</strong>
</p>

<strong>Requisitos:</strong>
<br><strong>- Satellite</strong>

<h3><br><strong>## Respaldo y restauracion del sistema Satellite</strong></h3>

Para respaldar el sistema, usamos el comando foreman-maintain backup, por temas de laboratorio usamos el comando de bakcup sin respaldar los datos de pulp, estos datos ocupan mucho espacio, por ello para temas de laboratorio usamos la directiva --skip-pupl-content

<br>`# foreman-maintain backup offline --skip-pulp-content /var/satellite-backup/`

En caso hagamos un backup full y luego deseamos crear respaldos incrementales sobre ese backup full usamos

<br>`# satellite-maintain backup offline --incremental /var/backup_directory/full_backup  /var/backup_directory`

Podemos crear algunos usuarios o registros en la plataforma de Satellite y ejecutar un respaldo, luego borrar el registro o usuario y ejecutar un restore con
<br>`# satellite-maintain restore -w restore-installer-reset,pulp-migrate /var/backup_directory/full_backup`

En caso de alertas de error, pueden omitirse ya que los backup y restores son parciales por la directiva --skip-pulp-content, ignore esos errores y recuerde que en un ambiente de produccion el respaldo de pulp si esta presente.

<h3><br><strong>## Ampliando espacios en discos</strong></h3>

Muchas veces, los discos del sistema se quedan sin espacio disponible, en estos casos podemos ampliarlos de forma dinamica en linea ya que usan el sistema LVM, para ellos necesitamos usar el comando fdisk con algun disco lire y particionarlo, en este ejemplo usamos el disco sdb

<br>`# fdisk /dev/sdb`
<br>`Partition type:`
<br>`   p   primary (0 primary, 0 extended, 4 free)`
<br>`   e   extended`
<br>`Select (default p): p`
<br>`Partition number (1-4, default 1): 1`
<br>`First sector (2048-209715199, default 2048):`
<br>`Using default value 2048`
<br>`Last sector, +sectors or +size{K,M,G} (2048-209715199, default 209715199):`
<br>`Using default value 209715199`
<br>`Partition 1 of type Linux and of size 100 GiB is set`
<br>`Command (m for help): w`

Una vez particionado el disco, lo mapeamos como pv
<br>`# pvcreate /dev/sdb1`

Agregamos el PV al VG rhel
<br>`# vgextend rhel /dev/sdb1`

Con el comando anterior extendemos la capacidad del VG y podemos agregar espacional a los volumenes, por ejemplo ampliamos en 10GB el volumen /var de 20GB a 30GB
<br>`# lvresize -L +10G /dev/rhel/var`

Aplicamos el cambio en el filesystem con
<br>`# xfs_growfs /dev/rhel/var`

Finalmente validamos el nuevo espacio con
<br>`# df -h`

<h3><br><strong>## Gestión de actualizaciones de un sistema cliente</strong></h3>

Validamos la cantidad de erratas descubiertas en el servidor, tome nota de estos datos
<br>`# yum list-security`

Si queremos validar el detalle de esas actualizaciones usamos
<br>`# yum list-security info`

Seleccionamos una actualizacion del tipo bugfix para corregirlas
<br>`# yum update --advisory=RHBA-2020:3009`

Vuelva a validar la cantidad de erratas descubiertas en el servidor y compare con el dato anterior
<br>`# yum list-security`

Este mismo procedimiento puede ser realizado con la interface gráfica, logueese en la plataforma y en Hosts de contenido busque su sistema cliente
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1601.png?raw=true"></p>

En el TAB de Errata busque una actualización que considere critica para el sistema, tome nota del codigo
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1602.png?raw=true"></p>

Seleccione la actualización y aplíquela
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1603.png?raw=true"></p>

Espere que que termine de actualizarse, vuelva a examinar el servidor y busque si la actualizacion aun esta por aplicar
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1604.png?raw=true"></p>



<h3><br><strong>Ejercicio propuesto 01:</strong></h3>
Crear un usuario nuevo llamado UserX para luego realizar un procedimiento de backup full.
Eliminar el UserX
Restaurar el sistema a partir del backup-full realizado en pasos previos
Validar la infraestructura

<br><h3><strong>Ejercicio propuesto 02:(OPCIONAL)</strong></h3>
El desarrollador de la pagina web requiere gestionar el contenido del portal, por ello le pide instalar el siguiente RPM desde el servidor FTP del salón, instalelo con el comando:
<br>`# yum install git-2.18.2-1.el8_1.x86_64`

Por linea de comandos intente hacer un análisis y proponga la actualización de ser necesario

<br><h3><strong>Ejercicio prepuesto 03(OPCIONAL):</strong></h3>
El mismo desarrallador ahora requiere contar con librerías del navegador firefox, por ello le pide instalar el paquete desde el recurso FTP con el comando
<br>`# yum install firefox-68.6.0-1.el8_1.x86_64`

Por interface gráfica intente hacer un análisis y proponga la actualización de ser necesario




<p><br><a href="sat">volver</a></p>