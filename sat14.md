<h1>Ejemplo de casos de soporte y acceso a la documentación oficial</h1>

<p>
<strong>Meta:</strong>
<br>Conocer el flujo de creación de un caso de soporte
</p>
<p>
<strong>Objetivos:</strong>
<br>- Generar sosreport
<br>- Utilizar el tool de soporte
</p>
<p>
<strong>Secciones:</strong>
<br>- Gestión de incidentes
</p>
<p>
<strong>Laboratorios:</strong>
<br><strong>- Registrar un sistema RHEL a la plataforma Satellite</strong>
<br><strong>- Ejercicio propuesto 01</strong>
<br><strong>- Tool de soporte de Red Hat</strong>
<br><strong>- Ejercicio propuesto 02</strong>
</p>

<strong>Requisitos:</strong>
<br><strong>- RHEL client</strong>

<h3><br><strong>## Instalar el sosreport</strong></h3>

El comando sosreport es una herramienta que recoge información sobre la configuración, información del sistema e información diagnóstica de un sistema Red Hat Enterprise Linux system. Por ejemplo: la versión de kernel que está corriendo, los módulos cargados y los archivos de configuración del sistema y de los servicios. El comando también corre programas externos para recoger más información y almacena el resultado en un archivo.

El resultado del comando sosreport es el punto de partida común para los ingenieros de soporte de Red Hat support cuando realizan el análisis inicial de un caso referido a un sistema Red Hat Enterprise Linux.

Para instalar el comando sosreport instalamos el paquete 
<br>`# yum install sos`

Cuando aperturamos un caso de soporte, el sistema de Red Hat nos genera un codigo de atencion, es recomendable ejecutar el comando sosreport referenciando ese numero de caso de soporte, por ejemplo si reportamos un incidente y el sistema nos genera el codigo 20091983 entonces usamos el siguiente procedimiento para empaquetar todos los archivos importantes via sosreport

<br>`# sosreport`
<br>`Press ENTER to continue, or CTRL-C to quit.`
<br>`Please enter the case id that you are generating this report for []: <strong>20091983</strong>`
<br>`Your sosreport has been generated and saved in: <strong>/var/tmp/sosreport-client01-20091983-2020-08-29-ezrwzxn.tar.xz</strong>`

<br><h3><strong>Ejercicio propuesto 01:</strong></h3>
Usted aperturo un nuevo caso de soporte desde la pagina de Red Hat, siendo asignado para usted el Cogido 20202020NumeroDeAlumno, desde su cliente satellite, cree un sosreport para adjuntarlo en el caso

<h3><br><strong>## Tool de soporte</strong></h3>

En caso desee subir el archivo sosreport directamente desde el sistema suscrito, puede apoyarse en el tool de soporte, instalelo con
<br>`# yum install redhat-support-tool`

Luego ejecute el comando donde se indica el nro de caso de soporte despues de -c y el archivo sosreport despues de -f
<br>`# redhat-support-tool addattachment -c 0000000 -f  /var/tmp/sosreport-00000.tar.xz`

Deberá ingresar el sus credenciales de su cuenta de Red Hat para subir el archivo, el instructor hará una demostración

<br><h3><strong>Ejercicio propuesto 02:</strong></h3>
Si tiene una cuenta de Red Hat, cree un caso de soporte del tipo consulta, identifique el numero de caso, ejecute un sosreport y subalo a su caso desde el terminal de Linux, valide que el archivo sosreport este cargado y luego cierre el caso de soporte


<p><br><a href="sat">volver</a></p>