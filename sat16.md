<h1>Actualización de un sistema cliente</h1>

<p>
<strong>Meta:</strong>
<br>Conocer el flujo de actualización de un sistema cliente
</p>
<p>
<strong>Objetivos:</strong>
<br>- Registar un sistema RHEL cliente
<br>- Aplicar actualizaciones del sistema RHEL cliente
</p>
<p>
<strong>Secciones:</strong>
<br>- Gestión de clientes de satellite
</p>
<p>
<strong>Laboratorios:</strong>
<br><strong>- Registrar un sistema RHEL a la plataforma Satellite</strong>
<br><strong>- Gestión de actualizaciones de un sistema cliente</strong>
<br><strong>- Ejercicio propuesto 01</strong>
<br><strong>- Ejercicio propuesto 02</strong>
<br><strong>- Ejercicio propuesto 03</strong>
</p>

<strong>Requisitos:</strong>
<br><strong>- Satellite</strong>
<br><strong>- RHEL client</strong>

<h3><br><strong>## Registrar un sistema RHEL a la plataforma Satellite</strong></h3>

Desde la linea de comandos descargamos los requisitos para registrar el sistema cliente
<br>`# curl --insecure --output katello-ca-consumer-latest.noarch.rpm https://satellite.opennova.pe/pub/katello-ca-consumer-latest.noarch.rpm`
<br>`# yum localinstall katello-ca-consumer-latest.noarch.rpm`

Registramos el sistema usando el Activation Key `rhel8` que ya fue creador por el administrador
<br>`# subscription-manager register --org="OpenNova" --activationkey="rhel8" --force`
<br>`# subscription-manager attach --auto`

Debera validar que tenga al menos 3 repostorios: Base, AppStream y Tools de Satellite con el comando
<br>`# yum repolist`

En caso de no tener los repositorios activados, hacerlo manualmente con:
<br>`# subscription-manager repos --enable=rhel-8-for-x86_64-appstream-rpms`
<br>`# subscription-manager repos --enable=rhel-8-for-x86_64-baseos-rpms`
<br>`# subscription-manager repos --enable=satellite-tools-6.7-for-rhel-8-x86_64-rpms`

Instalamos los agentes de katello
<br>`# yum -y install katello-host-tools`
<br>`# yum -y install katello-host-tools-tracer`
<br>`# yum -y install katello-agent`

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
Haga un análisis del kernel instalado  y proponga una actualización con sustento para luego ejecutarla

<br><h3><strong>Ejercicio propuesto 02:</strong></h3>
El desarrollador de la pagina web requiere gestionar el contenido del portal, por ello le pide instalar el siguiente RPM desde el servidor FTP del salón, instalelo con el comando:
<br>`# yum install git-2.18.2-1.el8_1.x86_64`

Por linea de comandos intente hacer un análisis y proponga la actualización de ser necesario

<br><h3><strong>Ejercicio prepuesto 03:</strong></h3>
El mismo desarrallador ahora requiere contar con librerías del navegador firefox, por ello le pide instalar el paquete desde el recurso FTP con el comando
<br>`# yum install firefox-68.6.0-1.el8_1.x86_64`

Por interface gráfica intente hacer un análisis y proponga la actualización de ser necesario

<p><br><a href="sat">volver</a></p>
