<h1>Introducción a Red Hat Satellite</h1>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat100.png?raw=true"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento de Red Hat Satellite como solución de administración, monitoreo y despliegue de Red Hat Enteprise Linux.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Identificación y planificación de componentes de Red Hat Satellite (Demostración)
</p>
<p>
<strong>Secciones:</strong>
<br>- Introducción a Red Hat Satellite. (Teórico)
<br>- Identificar componentes de Red Hat Satellite. (Teórico)
<br>- Planificar escenarios de despliegue. (Teórico)
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Introducción a Red Hat Satellite. (Teórico)
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat106.png?raw=true"></p>

**¿Que es Red Hat Satellite?**
<br>
<br>Red Hat Satellite es una solución de administración de sistemas que hace que la infraestructura de Red Hat sea más fácil de implementar, escalar, administrar y mantener en entornos físicos, virtuales y en la nube. Esta herramienta de administración ayuda a los usuarios a aprovisionar, configurar y actualizar sistemas para que sigan funcionando de manera eficiente, con seguridad y en cumplimiento con varios estándares. Al automatizar la mayoría de las tareas de mantenimiento del sistema, Red Hat Satellite ayuda a las organizaciones a aumentar la eficiencia, reducir los costos operativos y permitir que TI responda mejor a las necesidades comerciales estratégicas.

**¿Que es Red Hat Satellite Capsule Server?**
<br>
<br>Red Hat Satellite Capsule Server refleja el contenido de Red Hat Satellite Server para facilitar la federación de contenido en varias ubicaciones geográficas. Los sistemas host pueden extraer contenido del Capsule Server y no del Satellite Server central. Capsule Server también proporciona servicios localizados como Puppet Master, DHCP, DNS o TFTP. Los servidores cápsula lo ayudan a escalar su entorno de satélite a medida que aumenta el número de sus sistemas administrados

Los servidores cápsula reducen la carga en el servidor central, aumentan la redundancia y reducen el uso de ancho de banda

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat105.png?raw=true" width="400" height="400"></p>

### **Características y beneficios de Red Hat Satellite**
<br>Red Hat Satellite automatiza muchas tareas relacionadas con la administración del sistema y se integra fácilmente en los marcos de flujo de trabajo existentes. La consola centralizada ofrece a los administradores una ubicación única para acceder a los informes y para aprovisionar, configurar y actualizar sistemas.

**Gestión de contenido**
<br>
<br>Red Hat Satellite ayuda a garantizar la aplicación sistemática de contenido, incluidos los parches, en los sistemas implementados, en infraestructuras físicas, virtuales o en la nube, en todas las etapas. Este enfoque promueve una mayor consistencia y disponibilidad del sistema y libera a TI para responder más rápidamente a las necesidades y vulnerabilidades del negocio.

| Característica | Beneficio |
| --- | --- |
| Vistas de contenido | Las vistas de contenido son colecciones de RPM, módulos Puppet, contenido de contenedor o contenido de OSTree refinado con filtros y reglas. Se publican y promueven a lo largo de los entornos de ciclo de vida, lo que permite la gestión del sistema de un extremo a otro.|
| Integración de Red Hat Content Delivery Network (CDN) |Permite a los usuarios controlar la sincronización del contenido de Red Hat directamente desde la interfaz de usuario.|
|Gestión del ciclo de vida| Permite la distribución, aprovisionamiento, configuración y entrega de contenido a través de Red Hat Satellite Capsule Server.|
|Sincronización de contenido optimizada|Permite a los usuarios crear sistemas casi inmediatamente después de la instalación mientras el contenido se descarga en segundo plano.|

**Gestión de actualizaciones**
<br>
<br>Garantice un entorno operativo estándar (SOE) obteniendo actualizaciones sobre parches de seguridad, actualizaciones y mejoras. Además, mejore rápidamente la seguridad del sistema al parchear varios sistemas a la vez.

| Característica | Beneficio |
| --- | --- |
| Capacidad para definir y gestionar SOE | Garantice SOE obteniendo actualizaciones sobre parches de seguridad, actualizaciones y mejoras.|
| Parche automatizado |Mejore rápidamente la seguridad del sistema parcheando cientos o miles de sistemas a la vez.|
|Gestión del ciclo de vida| Permite la distribución, aprovisionamiento, configuración y entrega de contenido a través de Red Hat Satellite Capsule Server.|
|Implementación y seguimiento de software de Red Hat y software de terceros |Implemente toda la infraestructura de Red Hat, así como el software de terceros, extrayendo todos esos bits de software en Satellite. Una vez que Satellite tiene ese contenido, también realiza un seguimiento de él, lo que mejora la seguridad y garantiza un mejor seguimiento de lo que se implementa en cada sistema.|

**Gestión de Aprovisionamiento**
<br>
<br>Los administradores pueden aprovisionar en infraestructura virtualizada, bare metal y en entornos de nube pública o privada, todo desde una consola centralizada mediante un proceso simple

| Característica | Beneficio |
| --- | --- |
| Aprovisionamiento en bare metal | Aprovisione y actualice rápidamente toda su infraestructura básica.|
|Aprovisionamiento en Red Hat Virtualization, Red Hat OpenStack® Platform, VMware o varios proveedores de nube| Cree y administre fácilmente instancias en infraestructura virtualizada o en entornos de nube pública y privada.|
|Aprovisionamiento mediante plantillas| Cree escenarios complejos de Kickstart y Preboot Execution Environment (PXE) con poderosas variables y fragmentos.|
|System discovery|Descubra y busque en hosts no aprovisionados para una implementación rápida, incluso en entornos donde el Protocolo de configuración dinámica de host (DHCP) y PXE no están disponibles.|

**Gestión de Configuración**
<br>
<br>Analice y corrija automáticamente la desviación y el control de la configuración, y aplique el estado final del host deseado, todo desde la interfaz de usuario de Red Hat Satellite. Esta interfaz le permite configurar de manera eficiente los sistemas Red Hat Enterprise Linux® para una mayor agilidad.

| Característica | Beneficio |
| --- | --- |
| Ejecución remota | Automatiza los flujos de trabajo y permite a los usuarios realizar múltiples acciones contra grupos de sistemas, incluido el reinicio de un sistema después de la instalación de un parche y la realización de actualizaciones continuas en cientos de sistemas.|
|Integración de Red Hat Insights| Utiliza análisis avanzados para ayudar a detectar riesgos, permite la creación de un plan Insights para remediar los riesgos y ayuda a ejecutar los Playbooks de Ansible® a través de la misma interfaz de satélite.|
|Integración de Red Hat Ansible Automation Platform|Permite la ejecución remota, la gestión del estado deseado y la automatización de la gestión de la configuración.|

**Gestión de suscripciones**
<br>
<br>Genere informes y mapee fácilmente sus productos Red Hat a sistemas registrados para una visibilidad de consumo de suscripción de un extremo a otro.

| Característica | Beneficio |
| --- | --- |
| Gestión de suscripciones | Importe y administre fácilmente la distribución de suscripciones de software de Red Hat.|
|Motor de informes integrado| Informe y mapee los productos comprados a los sistemas registrados dentro de Red Hat Satellite para una visibilidad de uso de suscripción de un extremo a otro.|



# Identificar componentes de Red Hat Satellite. (Teórico)


Red Hat Satellite 6 consta de varios proyectos de código abierto que están integrados, verificados, entregados y respaldados como Satellite 6. 
<br>Consta de los siguientes proyectos de código abierto:

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat108.png?raw=true"width="700" height="280"></p>

### **Foreman**
Foreman es una aplicación de código abierto que se utiliza para el aprovisionamiento y la gestión del ciclo de vida de sistemas físicos y virtuales. Foreman configura automáticamente estos sistemas utilizando varios métodos, incluidos los módulos kickstart y Puppet. Foreman también proporciona datos históricos para informes, auditorías y resolución de problemas.

### **Katello**
Katello es un complemento de Foreman para la gestión de suscripciones y repositorios. Proporciona un medio para suscribirse a los repositorios de Red Hat y descargar contenido. Puede crear y administrar diferentes versiones de este contenido y aplicarlas a sistemas específicos dentro de las etapas definidas por el usuario del ciclo de vida de la aplicación.

### **Candlepin**
Candlepin es un servicio dentro de Katello que se encarga de la gestión de suscripciones.

### **Pulp**
Pulp es un servicio dentro de Katello que se encarga de la gestión de contenido y repositorios. Pulp asegura un espacio de almacenamiento eficiente al no duplicar los paquetes RPM incluso cuando lo solicitan Content Views en diferentes organizaciones.

### **Hammer**
Hammer es una herramienta CLI que proporciona equivalentes de línea de comandos y shell de la mayoría de las funciones de la interfaz de usuario web.

**REST API**
Red Hat Satellite 6 incluye un servicio de API RESTful que permite a los administradores y desarrolladores del sistema escribir scripts personalizados y aplicaciones de terceros que interactúan con Red Hat Satellite.

### **Puppet**
Red Hat Satellite 6 incluye paquetes Puppet compatibles. El programa de instalación permite a los usuarios instalar y configurar Puppet Masters como parte de Red Hat Satellite Capsule Servers. Un módulo Puppet, que se ejecuta en un Puppet Master en Red Hat Satellite Server o Satellite Capsule Server, también es compatible con Red Hat.

## Arquitecturas de cliente compatibles

**Soporte de gestión de contenido**

|Plataforma | Arquitecturas |
| --- | --- |
|Red Hat Enterprise Linux 8| x86_64, ppc_64, s390x |
|Red Hat Enterprise Linux 7| x86_64, ppc64 (BE), ppc64le, aarch64, s390x|
|Red Hat Enterprise Linux 6|x86_64, i386, s390x, ppc64 (BE)|
|Red Hat Enterprise Linux 5|x86_64, i386, s390x|

**Soporte de aprovisionamiento de host**

|Plataforma | Arquitecturas |
| --- | --- |
|Red Hat Enterprise Linux 8 | x86_64 |
|Red Hat Enterprise Linux 7 | x86_64 |
|Red Hat Enterprise Linux 6 | x86_64, i386 |
|Red Hat Enterprise Linux 5 | x86_64, i386 |

**Gestión de la configuración - Soporte Puppet 5**

|Plataforma | Arquitecturas |
| --- | --- |
|Red Hat Enterprise Linux 8 | x86_64, ppc_64, s390x|
|Red Hat Enterprise Linux 7 | x86_64, aarch64, ppc64le|
|Red Hat Enterprise Linux 6 | x86_64, i386|
|Red Hat Enterprise Linux 5 | x86_64, i386|

# Planificar escenarios de despliegue. (Teórico)
### **Arquitectura del sistema Red Hat Satellite 6**
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat101.png?raw=true" width="850" height="600"></p>


### **Topología de satélite con cápsula interna**
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat103.png?raw=true" width="850" height="600"></p>

### **Topología de satélite con cápsula aislada**
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/images/sat/sat102.png?raw=true" width="850" height="600"></p>