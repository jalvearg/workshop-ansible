<h1>Validación de los reportes sacados por RH Satellite</h1>

<p>
<strong>Meta:</strong>
<br>Conocer los reportes de Satellite
</p>
<p>
<strong>Objetivos:</strong>
<br>- Registrar una vista nueva dentro de un entorno customizado

</p>
<p>
<strong>Secciones:</strong>
<br>- Gestión de reportes
</p>

<strong>Requisitos:</strong>
<br><strong>- Satellite</strong>

Una de las características interesantes de la versión Red Hat Satellite 6 es el nuevo motor de informes. El servidor satélite suele ser un punto focal del entorno de Red Hat de una organización, y el motor de informes permite a los usuarios de satélite crear informes que se pueden exportar. Estos informes pueden incluir detalles sobre los hosts del cliente Satellite, suscripciones, erratas aplicables, etc. El motor de informes utiliza el lenguaje Ruby (ERB) incorporado.

Satellite 6.5 incluye varios informes predefinidos proporcionados por Red Hat, a la vez que proporciona un motor de informes que los usuarios de Satellite pueden utilizar para personalizar los informes incluidos o para crear sus propios informes personalizados.

Los informes incluidos en Satellite 6 utilizan el formato de valores separados por comas (CSV); sin embargo, en esta publicación también exploraremos la creación de un informe personalizado que utilice formato HTML.

<h3><strong>Descripción general de los informes incluidos con Satellite 6</strong></h3>

Satellite incluye diferentes informes como:
<br>- El informe de erratas aplicables muestra una lista de erratas que se aplican a los hosts de contenido (opcionalmente se puede filtrar por hosts o erratas).
<br>- El informe de estados de host muestra el estado de sus hosts satélite (opcionalmente puede filtrar por hosts).
<br>- El informe de hosts registrados muestra información sobre sus hosts de satélite, como la dirección IP, la versión del sistema operativo y las suscripciones adjuntas (opcionalmente, puede filtrar por hosts).
<br>- El informe de suscripciones muestra información sobre las suscripciones, como la cantidad, el número disponible y el SKU (opcionalmente se puede filtrar por parámetros de suscripción).
<br>- Otros


Para generar un informe, vaya al menú Monitor y seleccione Plantillas de informes . En este punto, haga clic en el botón Generar a la derecha del informe que le gustaría generar. El informe solicitará la entrada del usuario para filtrar opcionalmente los resultados del informe. Deje el filtro en blanco para ver todos los resultados, o puede escribir un filtro para limitar los resultados del informe.

El instructor demostrara la generación de informes con las plantillas que Red Hat entrega en la solución de Satellite.

<h3><strong>Ejercicio propuesto</strong></h3>
Clone el reporte que creo el instructor y genere el archivo de reporte que pueda exportar a un servidor web

<h3><strong>Solución<strong></h3>

Ubique el reporte del instructor y clonelo, el nombre del reporte clonado deberá ser: Reporte_User_X, donde x es el numero de su usuario del 1 al 6.
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat901.png?raw=true"></p>

Genere su reporte personal utilizando el reporte clonado: **Reporte_User_X**, donde x es el numero de su usuario del 1 al 6, con el formato HTML y visualícelo.
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat902.png?raw=true"></p>

<br> Como opcional:
<br>Instale un servidor web en su equipo asignado y carge el reporte de su cliente
<br>`# yum install httpd -y`
<br>`# systemctl enable httpd`
<br>`# systemctl start httpd`
<br>`# firewall-cmd --permanent --add-service=http`
<br>`# firewall-cmd --permanent --add-service=https`
<br>`# firewall-cmd --reload`
<br>`# cd /var/www/html/`
<br>Cargue el archivo de reporte en su equipo asignado
<br>`# ln -s Instructor-2020-09-01.html  index.html`
<br>Validar la pagina por un navegador



<p><br><a href="sat">volver</a></p>
