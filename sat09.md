<h1>Gestión de Vistas</h1>

<p>
<strong>Meta:</strong>
<br>Conocer las vistas de recursos de Satellite
</p>
<p>
<strong>Objetivos:</strong>
<br>- Registrar una vista nueva dentro de un entorno customizado

</p>
<p>
<strong>Secciones:</strong>
<br>- Gestión de vistas
</p>
<p>
<strong>Laboratorios:</strong>
<br><strong>- Crear un nuevo entorno</strong>
<br><strong>- Crear y publicar una vista en el entorno</strong>
</p>

<strong>Requisitos:</strong>
<br><strong>- Satellite</strong>


<h3><br><strong>Crear un nuevo entorno</strong></h3>
Para crear un nuevo entorno, nos dirigimos a la seccion Content > Lifecycle Environments  y le damos crear un nuevo entorno de ciclo de vida.
<br>
<br>

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat10101R.jpg?raw=true"width="800" height="400"></p>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat10102R.jpg?raw=true"width="800" height="400"></p>
En la pestaña de nuevo entorno colocar:<br>
Nombre: <strong>Build</strong><br>
Label: <strong>Build</strong><br> 
Descripción: <strong>Build Environment</strong><br>
<br>
Luego darle click al boton <strong>Save</strong><br>
<br>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat10103R.jpg?raw=true"></p>
<br>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat10104R.jpg?raw=true"width="800" height="400"></p>
Crear un nuevo entorno llamado Test que este a continuacion de Build<br>
Nombre: <strong>Test</strong><br>
Label: <strong>Test</strong><br> 
Prior Environment: <strong>Build</strong><br>
<br>
Luego darle click al boton <strong>Save</strong><br>
<br>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat10105R.jpg?raw=true"></p>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat10106R.jpg?raw=true"></p>
Crear un nuevo entorno llamado Test que este a continuacion de Build<br>
Nombre: <strong>Deploy</strong><br>
Label: <strong>Deploy</strong><br> 
Prior Environment: <strong>Test</strong><br>
<br>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat10107R.jpg?raw=true"></p>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat10108R.jpg?raw=true"></p>
<br><h3><strong>Crear y publicar una vista en el entorno</strong></h3>

Ahora que tenemos un nuevo entorno, podemos crear una nueva vista en la seccion Content > Content Views 
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1003.png?raw=true"></p>

Nombramos la vista nueva
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1004.png?raw=true"></p>

En el vista nueva, seleccionamos el repositorio Base del canal de RHEL8 para incluirlo
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1005.png?raw=true"></p>

Ahora podemos publicar la vista
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1006.png?raw=true"></p>

Guardamos la version 1 de nuestra vista
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1007.png?raw=true"></p>

Cuando termine de publicar, con le damos click al boton promover
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1008.png?raw=true"></p>

Ahora le damos check a nuestro entorno para que la vista sea promovida en ella
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1009.png?raw=true"></p>

Podemos ingresar a la seccion de Hosts > Todos los hosts y editar las propiedades del host
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1010.png?raw=true"></p>

Editamos las propiedades para que este host pertenesca a nuestro entorno y vista customizada
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1011.png?raw=true"></p>

Ahora regresamos a la vista de contenidos y los recursos empezaran a registrarse en el entorno a medida que sean registrados y puedas ser enviados a futuros reportes

## Laboratorio de la Unidad
<br>1. Cree un nuevo entorno de ciclo de vida que contengo lo siguiente: **DesarrolloX**, **CertificacionX**, **ProduccionX**. Donde **X** es reemplazado por el numero de estación de cada asistente que va del **1** al **6**. Ejemplo: Desarrollo9, Certificacion9, Produccion9.
<br>
<br>2. Cree una vista de contenido llamado BaseX, en la versión inicial solamente adicione el repositorio yum: Red Hat Enterprise Linux 8 for x86_64 - BaseOS RPMs 8 y publíquelo. Una vez publicado promuévalo a los ambientes **DesarrolloX, CertificacionX y ProduccionX**.
<br>
<br>3. Genere una nueva versión 2.0 de la vista de contenido Base que incluya los repositorios: **Red Hat Enterprise Linux 8 for x86_64 - AppStream RPMs 8** y **Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 RPMs**  y promuevalo a los ambientes: **DesarrolloX, CertificacionX y ProduccionX**.
<br>
<br>4. Genere una llave de activación para realizar un re-registro del clienteX de su laboratorio, utilizar los siguientes datos:
       ActivationKey Name: **AK_BASE_RHEL8_USER_X**.<br>
       En ambiente seleccionar: **ProduccionX**<br>
       Vista de Contenido: **BaseX**<br>
       Tab de suscripciones: **Agregarle una Suscripcion disponible**<br>
       Tab de Juego de repositorios: **Habilitar los repositorios correspondientes**<br>
       Finalmente Registrar el cliente correspondiente utilizando la llave de activación creada: <br>
       **subscription-manager register --org="Opennova" --activationkey="AK_USERX_BASE_PROD"**<br>
       verificar que dispone de los repositorios configurados en la vista de contenido. Pruebe instalar el paquete **zsh**.
<br>




<p><br><a href="sat">volver</a></p>
