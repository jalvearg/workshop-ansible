<h1>Realizar por lo menos una tarea automatizada con puppet y/o ansible</h1>

<p>
<strong>Meta:</strong>
<br>Conocer las herramientas de automatización de Satellite
</p>
<p>
<strong>Objetivos:</strong>
<br>- Automatizar operaciones con puppet
<br>- Automatizar operaciones con ansible
</p>
<p>
<strong>Secciones:</strong>
<br>- Gestión de operaciones
</p>
<p>
<strong>Laboratorios:</strong>
<br><strong>- Registrar un sistema RHEL a la plataforma Satellite</strong>
<br><strong>- Instalar un paquete vía Satellite</strong>
<br><strong>- Registrar clases de puppet</strong>
<br><strong>- Registrar clientes de puppet</strong>
<br><strong>- Configuración de parámetros de CHRONY con puppet</strong>

</p>

<strong>Requisitos:</strong>
<br><strong>- Satellite</strong>
<br><strong>- RHEL client</strong>

<h3><br><strong>## Registrar un sistema RHEL a la plataforma Satellite</strong></h3>

Desde la linea de comandos descargamos los requisitos para registrar el sistema cliente
<br>`# curl --insecure --output katello-ca-consumer-latest.noarch.rpm https://satellite.opennova.pe/pub/katello-ca-consumer-latest.noarch.rpm`
<br>`# yum localinstall katello-ca-consumer-latest.noarch.rpm`

Registramos el sistema usando el Activation Key `rhel8` que ya fue creador por el administrador
<br>`# subscription-manager register --org="OpenNova" --activationkey="rhel8"`
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

<h3><br><strong>## Instalar un paquete vía Satellite</strong></h3>

La plataforma de satellite permite instalar un paquete a los clientes registrados, intentemos instalar el paquete CHRONY al cliente satellite, antes de iniciar la instalación ingrese al terminal del cliente satellite y valide que no tenga el rpm de chrony instalado

<br>`# rpm -q chrony`
<br>`package chrony is not installed`

Ingresamos al cliente en la sección de Hosts > Hosts de contenido y seleccionamos el cliente
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1512.png?raw=true"></p>

En la sección de Paquetes le damos a Acciones
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1513.png?raw=true"></p>

Ejecutamos la accion de instalar el paquete chrony
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1514.png?raw=true"></p>

Esperamos que la tarea termine de ejecutar con exito
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1515.png?raw=true"></p>

Volvemos a ejecutar el comando de verificación en el cliente
<br>`# rpm -q chrony`

Ahora el paquete esta instalado sin embargo el servicio no esta activo
<br>`# systemctl status chronyd`

Tampoco esta configurado con algun servidor que provea la hora
<br>`# cat /etc/chrony.conf | grep server`

Satellite nos ayuda a instalar el paquete y para la configuracion de los sistema nos apoyaremos en puppet.

<h3><br><strong>## Registrar clases de puppet(Solo el instructor)</strong></h3>

Las clases de puppet a través de los módulos de puppet facilitan la configuración de servicios a través del uso de parámetros, estos modulos pueden ser cargados por la linea de comandos o por entorno gráfico, a continuación el instructor cargara el modulo de puppet CHRONY para los siguientes laboratorios

Para buscar modulos relacionados con el servicio chrony
<br>`# puppet module search chrony`

Una vez identificado el modulo lo instalamos con
<br>`# puppet module install aboe-chrony`

Se importa las clases del modulo en el ambiente producción
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1501.png?raw=true"></p>

Se habilita la customización de parámetros de la clase chrony y la infraestructura que lista para que pueda enviar la configuración en el siguiente laboratorio

<h3><br><strong>## Registrar clientes de puppet</strong></h3>

Para la ejecución de las tareas de puppet primero se debe registrar el cliente de puppet en el servidor cliente de satellite, para ello primero validamos que el cliente tenga el repositorio de `satellite-tools-6.7-for-rhel-8-x86_64-rpms` con 
<br>`# yum repolist`

Luego instalamos el cliente con
<br>`# yum install -y puppet`

Ahora modificamos el archivo de configuración `/etc/puppetlabs/puppet/puppet.conf` para que incluya la linea
<br>`server=satellite.opennova.pe`

Validamos la configuración del cliente
<br>`# puppet agent --test --noop`

Se creo una petición de certificado digital pero esta pendiente de aprobación, para ello vamos a la sección de Infraestructura > Capsulas inteligentes y seleccionamos el servidor satellite
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1502.png?raw=true"></p>

En la sección de CA Puppet se vera una alerta de certificado, ingresamos
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1503.png?raw=true"></p>

Buscamos nuestro cliente de satellite y le damos registrar
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1504.png?raw=true"></p>

Validamos de nuevo el cliente y verificamos que no aparezcan errores (ejecutar 2 veces)
<br>`# puppet agent --test --noop`

Notamos que el cliente esta registrado en el ambiente Produccion y no hay operaciones por validar, se encuentra listo para enviar la configuración deseada

<h3><br><strong>## Configuración de parámetros de CHRONY con puppet</strong></h3>

Con el cliente listo y la clase de puppet habilitada por el instructor podemos crear nuestro grupo de configuración personalizado para enviar parámetros de configuración del servidor NTP/CHRONY, el objetivo de crear un grupo de configuración es segmentar la cantidad de servidores que requieren esa configuración especifica, el primer paso es ir a la sección Configurar > Grupos de configuración y creamos un grupo nuevo
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1505.png?raw=true"></p>

Nombramos el grupo con un nombre que nos identifique e incluimos la clase CHRONY a nuestro grupo nuevo
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1506.png?raw=true"></p>

En la sección de Hosts > Todos los hosts, seleccionamos nuestro cliente satellite
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1507.png?raw=true"></p>

Editamos el cliente
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1508.png?raw=true"></p>

Nos aseguramos que los parámetros de puppet del cliente estén configurados
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1509.png?raw=true"></p>

En Clases de Puppet añadimos nuestro grupo de configuracion
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1510.png?raw=true"></p>

Aceptamos la configuración y volvemos a ingresar a Editar, ahora vamos a la sección de Parámetros y sobrescribimos los parámetros
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1511.png?raw=true"></p>

En el cliente satellite ejecutamos el comando del verificacion del agente y analizamos la salida
<br>`# puppet agent --test --noop`

Como vera el comando puppet valida que no esta el servicio activo y que no tiene configuraciones de servidores de hora, para aplicar estas nuevas configuración usamos el comando
<br>`# puppet agent --test`

Ahora validamos los servicios de chrony con
<br>`# systemctl status chronyd`
<br>`# cat /etc/chrony.conf | grep server`

<h3><strong>## Ejercicio propuesto 01</strong></h3>
Con lo aprendido sobre clases de puppet implemente un nuevo grupo llamado <strong>Nro de Alumno</strong>-TUNED el cual implementara el perfil de afinamiento del sistema orientado a servicios de redes
<br>- El paquete tuned ya viene implementado en los RHEL8
<br>- El comando para listar los perfiles disponibles es <strong>tuned-adm list</strong> y el comando para validar el perfil actual es  <strong>tuned-adm active</strong>
<br>- El instructor ya habilito la clase tuned para que pueda ejecutar la configuración</strong>

<br>- <strong>Solucion </strong>

Con el cliente listo y la clase de puppet habilitada por el instructor podemos crear nuestro grupo de configuración personalizadoTESTX-TUNED para enviar parámetros de configuración del perfil de tuned, el objetivo de crear un grupo de configuración es segmentar la cantidad de servidores que requieren esa configuración especifica, el primer paso es ir a la sección Configurar > Grupos de configuración y creamos un grupo nuevo

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet01.png?raw=true"></p>

Creamos el grupo TUNED y asignamos la clase de tunes
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet02.png?raw=true"></p>

Regresamos a la secciond e HOSTS > Todos los Host y seleccionamos nuestro cliente de prueba
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet03.png?raw=true"></p>

Editamos las propiedades del cliente de prueba
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet04.png?raw=true"></p>

En clases de puppet, añadimos el grupo de configuracion nuevo con opciones de tunes
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet05.png?raw=true"></p>

Ahora podemos editar el perfil del sistema cliente
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet06.png?raw=true"></p>

Para verificar el perfil actual de tuned usamos
<br>`# tuned-adm active`

Para verificar los perfiles de tuned disponible usamos
<br>`# tuned-adm list`

Realice algunas modificaciones al perfil de tuned y ejecutelo inmediatamente con el comando
<br>`# puppet agent --test `


<h3><strong>## Ejercicio propuesto 02</strong></h3>
El auditor de la empresa considera que el login via SSH con el usuario ROOT es inseguro sugiere deshabilitar esa caracteristica en los servidores, utilizando lo aprendido realice las siguientes operaciones en secuencia:

<br>- Cree un usuario personal en su sistema cliente
<br>- Cree un nuevo grupo de configuración llamado <strong>Nro de Alumno</strong>-SSH
<br>- Habilite la política de seguridad que bloquea el acceso ssh para el usuario root, validelo con un intento de conexión con root
<br>- Loguese con su usuario personal y realice el cambio a root con el comando <strong>su - root</strong>
<br>- Modifique la política para que vuelva a permitir el acceso remoto ssh para root y certifique la politica para responder al informe de auditoria
<br>- El instructor ya habilito la clase sshd_config para que pueda modificar la configuración del archivo /etc/ssh/sshd_config 


<strong>Solucion</strong>
Creamos el usuario remote
<br>`# useradd remote`

Cambiamos la clave de remote
<br>`# passwd remote`

Creamos un nuevo grupo de configuracion 
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet01.png?raw=true"></p>

Nombramos el grupo de configuracion y añadimos la clase de ssh
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet07.png?raw=true"></p>

Volvemos a seleccionar nuestro cliente
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet02.png?raw=true"></p>

Editamos el cliente
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet03.png?raw=true"></p>

Agregamos el grupo de configuracion al cliente
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet08.png?raw=true"></p>

Modificamos el parametro de acceso remoto como root de yes a no
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet09.png?raw=true"></p>

Aplicamos los cambios en el sistema cliente
<br>`# puppet agent --test `

Intentemos crear una nueva session SSH con el usuario root, en caso de no poder crearla el ejercicio es correcto, podemos regresar a la configuracion anterior con el usuario remote


<h3><br><strong>## Otras opciones para programación de tareas</strong></h3>

Satellite ademas de puppet cuenta con diferentes opción de integración con otra herramientas de ejecución de tareas, entre ellas ansible o incluso lo mas simple como comandos SSH, en el siguiente ejemplo ejecutamos la tarea remota de copia de un log importante

En la sección de Todos los hosts, seleccionamos nuestro cliente de satellite
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1516.png?raw=true"></p>

Programamos un trabajo remoto
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1517.png?raw=true"></p>

Definimos el trabajo remoto
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1518.png?raw=true"></p>

Definimos las credenciales del usuario a ejecutar y sobre todo la opción de ejecutar ahora
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1519.png?raw=true"></p>

El programa debe finalizar con exito
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat1520.png?raw=true"></p>

Ingresamos al cliente satellite y validamos si se ejecuto la tarea

<h3><strong>## Ejercicio propuesto 04</strong></h3>
Es importante respaldar la configuración de un sistema, por buena practica estas confifuraciones se realizan en /etc, ejecute una tarea remota via satellite que permita este respaldo bajo las siguiente condiciones:
<br>- El archivo de respaldo debe guardarse en la carpeta /tmp
<br>- El archivo de respaldo debe tener el formato backup_config_DiaMesAño.tar.gz
<br>- El respaldo debe realizarse de forma programada pero no inmediatamente sino 2 minutos después de la creación de la tarea

<br>Tips de Linux
<br>- el comando <strong>tar -czvf carpeta.tar.gz carpeta/</strong> permite crear el archivo comprimido
<br>- el comando <strong>date '+%d%m%Y%H%M%S'</strong> entrega la fecha en formato DiaMesAñoHoraMinutoSegundo


<strong>Solucion</strong>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet10.png?raw=true"></p>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/puppet11.png?raw=true"></p>


<p><br><a href="sat">volver</a></p>
