<h1>Ansible Automation</h1>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans100.png?raw=true"width="800" height="400"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento Ansible Automation y Red Hat Automation Platform.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Conceptos de Ansible y Arquitectura (Teórico)
</p>
<p>
<strong>Secciones:</strong>
<br>- Introducción a Ansible. (Teórico)
<br>- Introducción a Red Hat Ansible Automation Platform. (Teórico)
<br>- Planificar setup inicial Ansible. (Demostración) 
</p>
<p>
<strong>Laboratorios:</strong>
</p>

# Introducción a Ansible. (Teórico)
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans100.jpg?raw=true"width="800" height="400"></p>

### **¿Qué es la Automatizacion de TI?**
<br>La automatización de TI o automatización de infraestructura consiste en utilizar un software para crear políticas y procesos que reduzcan o reemplacen la interacción manual con sistemas de TI.

Beneficios:
- Ahorro de costos operativos.
- Mitigar el error humano.
- Simplificar tareas repetitivas.
- Facilitar despliegues e integraciones.
- Reducción del tiempo de ejecución de tareas.
---

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans101.png?raw=true"width="600" height="400"></p>

### **¿Qué es Infraestructura como código?**
<br>
<br>La infraestructura como código (IaC) es un enfoque para la gestión de infraestructuras de sistemas de TI que se basa en el uso de archivos de configuración repetibles para generar entornos de implementación consistentes para el desarrollo de CI/CD

Tipos de IaC:
- [Terraform](https://www.terraform.io)
- [CloudFormation](https://aws.amazon.com/es/cloudformation)
- [Azure ARM](https://azure.microsoft.com/es-es/services/arm-templates/)
- [Ansible](https://www.ansible.com)
- [Chef](https://www.chef.io/products/chef-infra)
- [Puppet](https://puppet.com)
- [Saltstack](https://saltproject.io)
- otros
---
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans105.png?raw=true"width="500" height="230"></p>

### **¿Qué es Ansible?**
<br>**Ansible** es una plataforma de automatización de código abierto. Es un lenguaje de automatización simple que puede describir perfectamente una infraestructura de aplicaciones de TI en Ansible Playbooks.

- Ansible es simple.
- Ansible es potente.
- Ansible no necesita agentes.
<br>

**Arquitectura Ansible**
<br>
<br>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans103.jpg?raw=true"width="700" height="400"></p>

---

# Introducción a Red Hat Ansible Automation Platform. (Teórico)

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans102.jpg?raw=true"width="800" height="400"></p>

### **¿Qué es Red Hat Ansible Automation Platform?**
Ansible Automation Platform ofrece un marco empresarial para diseñar y gestionar la automatización de la TI según sea necesario. Además, proporciona un panel visual, control de acceso basado en funciones y herramientas de automatización que incluyen sistemas de análisis y contenido certificado y reutilizable, para que los usuarios puedan centralizar y controlar su infraestructura.

Ansible Automation Platform utiliza YAML, un lenguaje de automatización comprensible para las personas que permite que los usuarios de una empresa compartan, evalúen y gestionen el contenido de automatización. Colabore con todos los equipos y ponga en marcha sus sistemas rápidamente, gracias a los conjuntos de funciones y módulos creados previamente en los que se pueden realizar búsquedas, para que cualquier persona logre implementar la automatización.

### **Características y Beneficios**
Red Hat Ansible Automation Platform ayuda a las organizaciones a adoptar una cultura de automatización colaborativa al brindar una experiencia coherente en todas partes, basada en características adaptadas a las necesidades de todo el equipo de TI. Con la plataforma de automatización Ansible:

- Los administradores y arquitectos de TI pueden expandir más fácilmente la automatización en toda la empresa, mientras administran la política de automatización y el gobierno con el catálogo de servicios de automatización y obtienen informes en tiempo real en toda la pila con Red Hat Insights for Ansible Automation Platform.

- Los desarrolladores conservan la libertad de construir, sin la sobrecarga operativa de mantener muchas herramientas y marcos. Los entornos de ejecución brindan una experiencia consistente similar a un contenedor para la automatización de construcción y escalado, con nuevas herramientas incluidas para ayudar a construirlos y administrarlos. Las colecciones de contenido de Ansible ofrecen contenido de automatización prediseñado de más de 100 socios certificados, con soluciones disponibles para casi todos los casos de uso.

- Los administradores y operadores tienen herramientas poderosas en el controlador de automatización y el centro de automatización para administrar y compartir proyectos de automatización de manera más eficiente, con un lenguaje común y una combinación ampliamente accesible de interfaces de línea de comandos (CLI), interfaces gráficas de usuario (GUI) y interfaces de usuarios basados ​​en texto (TUI).

- Su organización puede abordar los desafíos de automatización, desde la automatización de la seguridad y la red, hasta el aprovisionamiento de infraestructura en la nube, la gestión de la configuración, la integración continua y la entrega continua (CI / CD), contenedores y más.

| Componentes de la plataforma  | Usos y beneficios |
| --- | --- |
| Ansible Core| Ansible Automation Platform está alineada con la comunidad global detrás del proyecto Ansible, con capacidades fundamentales adicionales y garantía de Red Hat que ayudan a su empresa a adoptar cómodamente la automatización en toda la organización a cualquier escala. |
| Automation controller| El plano de control de Ansible Automation Platform se denomina controlador de automatización (renombrado Ansible Tower). Incluye una interfaz de usuario (UI), control de acceso basado en roles (RBAC), flujos de trabajo y CI / CD para ayudar a su equipo a escalar. El controlador de automatización ayuda a estandarizar cómo se implementa, inicia, delega y audita la automatización. Administre el inventario, inicie y programe flujos de trabajo, realice un seguimiento de los cambios e integre en los informes, todo desde una interfaz de usuario centralizada y una interfaz de programación de aplicaciones (API) RESTful. |
| Automation execution environments| Empaquetados como contenedores, los entornos de ejecución de automatización (que reemplazan a Ansible Engine) son entornos definidos, consistentes y portátiles para ejecutar playbooks y roles de Ansible. Los entornos de ejecución ofrecen una forma sencilla y flexible de crear, reutilizar y escalar contenido de automatización.|
| Ansible Content Collections| Las colecciones de contenido de Ansible facilitan a los creadores y desarrolladores de contenido de Ansible poner en marcha la automatización más rápido. Las colecciones de contenido certificadas de Ansible están respaldadas por Red Hat y un sólido ecosistema de socios. Son bloques de construcción de contenido de automatización flexibles y confiables para una variedad de casos de uso.|
| Automation hub| El centro de automatización proporciona un lugar para que los clientes de Ansible Automation Platform encuentren, usen y extiendan rápidamente contenido que sea compatible con Red Hat y sus socios tecnológicos, para brindar tranquilidad adicional en los entornos más exigentes. El centro de automatización privado también está disponible y ofrece a los clientes un repositorio de imágenes de contenedor de sus entornos de ejecución como una instancia local de centro de automatización. |
| Ansible content tools | Ansible Automation Platform 2 incluye dos nuevas herramientas diseñadas para ayudar a que la creación y la implementación de entornos de ejecución sean una experiencia de creación más fluida. Se incluirán herramientas de contenido adicionales de Ansible en futuras versiones de la plataforma. El generador de entornos de ejecución (ansible-builder) es una herramienta de línea de comandos que ayuda a construir entornos Ansible en contenedores usando podman. Permite a los creadores y operadores de automatización crear entornos de ejecución personalizados con el contenido exacto de Ansible necesario para su automatización. El navegador de contenido de automatización (ansible-navigator) proporciona una interfaz de plataforma de nivel superior (a través de CLI o TUI) para los creadores de automatización de Ansible. Proporciona una experiencia de creación de contenido de automatización de nivel superior más coherente, coherente y predecible, diseñada para ayudar al desarrollador empresarial de Ansible. |
| Red Hat Insights for Ansible Automation Platform| Red Hat Insights for Ansible Automation Platform permite a los arquitectos rastrear y solucionar problemas de éxito en el trabajo y medir cómo los equipos coordinan los procesos de automatización en los dominios de TI. También ayuda a los operadores y administradores a mantener Red Hat Ansible Automation Platform funcionando de manera eficiente y óptima, a identificar dónde fallan trabajos específicos e informar sobre proyectos de automatización en toda la infraestructura de un extremo a otro.|
| Automation services catalog| El catálogo de servicios de automatización es un medio para que los usuarios administren, aprovisionen y retiren los recursos de automatización, para facilitar el modelado y la entrega. Brinda a los creadores de automatización y usuarios comerciales acceso de autoservicio en entornos físicos, virtuales, en la nube y de contenedores, lo que facilita la ejecución de proyectos de automatización. Simultáneamente brinda a los usuarios de automatización empresarial y de línea de negocios la gobernanza que necesitan para cumplir con los requisitos de cumplimiento y adquisiciones.|

---

# Planificar setup inicial Ansible. (Demostración)

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans106.png?raw=true"width="800" height="400"></p>
<p>

## **Requerimientos previos**

### **Control Node**

- Suscripcion valida de Red Hat Ansible Automation Platform.
- Registrarse al canal **ansible-2-for-rhel-8-x86_64-rpms** e instalar el paquete ansible con **yum install ansible**.
- Python:2 (version:2.7 o superior) o Python:3 (version:3.5 o superior), para Red Hat Enterprise Linux 8 se puede utilizar **"yum install platform-python"** del AppStream.

### **Managed Node**

- Suscripcion valida de Red Hat Enterprise Linux.
- Python:2 (version:2.6 o superior) o Python:3 (version:3.5 o superior), para Red Hat Enterprise Linux 8 se puede utilizar **"yum install platform-python"**. También se puede utilizar **"yum module install python36"**.
- Si, selinux esta habilitado en los managed nodes asegurarse que el paquete **python3-libselinux** esta instalado.

---
## **Instalar Ansible en el Control Node**

1. Listar repositorios disponibles y validar que contamos con ansible-2.9-for-rhel-8-x86_64-rpms

```
[root@server09 ~]# subscription-manager repos --list
+----------------------------------------------------------+
    Available Repositories in /etc/yum.repos.d/redhat.repo
+----------------------------------------------------------+
Repo ID:   rhel-8-for-x86_64-baseos-rpms
Repo Name: Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)
Repo URL:  https://satellite.opennova.pe/pulp/repos/OpenNova/Library/content/dist/rhel8/$releasever/x86_64/baseos/os
Enabled:   1

Repo ID:   satellite-tools-6.9-for-rhel-8-x86_64-rpms
Repo Name: Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 (RPMs)
Repo URL:  https://satellite.opennova.pe/pulp/repos/OpenNova/Library/content/dist/layered/rhel8/x86_64/sat-tools/6.9/os
Enabled:   1

Repo ID:   ansible-2.9-for-rhel-8-x86_64-rpms
Repo Name: Red Hat Ansible Engine 2.9 for RHEL 8 x86_64 (RPMs)
Repo URL:  https://satellite.opennova.pe/pulp/repos/OpenNova/Library/content/dist/layered/rhel8/x86_64/ansible/2.9/os
Enabled:   0

Repo ID:   rhel-8-for-x86_64-appstream-rpms
Repo Name: Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)
Repo URL:  https://satellite.opennova.pe/pulp/repos/OpenNova/Library/content/dist/rhel8/$releasever/x86_64/appstream/os
Enabled:   1
```

2. Habilitar en el nodo de control el repositorio **ansible-2.9-for-rhel-8-x86_64-rpms**
```
[root@server09 ~]# subscription-manager repos --enable=ansible-2.9-for-rhel-8-x86_64-rpms
Repository 'ansible-2.9-for-rhel-8-x86_64-rpms' is enabled for this system.

[root@server09 ~]# yum repolist
Updating Subscription Management repositories.
repo id                                                   repo name
ansible-2.9-for-rhel-8-x86_64-rpms                        Red Hat Ansible Engine 2.9 for RHEL 8 x86_64 (RPMs)
rhel-8-for-x86_64-appstream-rpms                          Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)
rhel-8-for-x86_64-baseos-rpms                             Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)
satellite-tools-6.9-for-rhel-8-x86_64-rpms                Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 (RPMs)
```

3. Instalar Python en el nodo de control
```
[root@server09 ~]# yum install platform-python -y
Updating Subscription Management repositories.
Red Hat Ansible Engine 2.9 for RHEL 8 x86_64 (RPMs)                                                                  7.9 MB/s | 2.0 MB     00:00
Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)                                                                 26 kB/s | 2.4 kB     00:00
Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)                                                              43 kB/s | 2.8 kB     00:00
Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 (RPMs)                                                                  25 kB/s | 2.1 kB     00:00
Package platform-python-3.6.8-37.el8.x86_64 is already installed.
Dependencies resolved.
=====================================================================================================================================================
 Package                           Architecture             Version                            Repository                                       Size
=====================================================================================================================================================
Upgrading:
 platform-python                   x86_64                   3.6.8-38.el8_4                     rhel-8-for-x86_64-baseos-rpms                    84 k
 python3-libs                      x86_64                   3.6.8-38.el8_4                     rhel-8-for-x86_64-baseos-rpms                   7.8 M

Transaction Summary
=====================================================================================================================================================
Upgrade  2 Packages

Total download size: 7.9 M
Downloading Packages:
(1/2): platform-python-3.6.8-38.el8_4.x86_64.rpm                                                                     818 kB/s |  84 kB     00:00
(2/2): python3-libs-3.6.8-38.el8_4.x86_64.rpm                                                                         55 MB/s | 7.8 MB     00:00
-----------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                 55 MB/s | 7.9 MB     00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                             1/1
  Upgrading        : platform-python-3.6.8-38.el8_4.x86_64                                                                                       1/4
  Running scriptlet: platform-python-3.6.8-38.el8_4.x86_64                                                                                       1/4
  Upgrading        : python3-libs-3.6.8-38.el8_4.x86_64                                                                                          2/4
  Cleanup          : python3-libs-3.6.8-37.el8.x86_64                                                                                            3/4
  Cleanup          : platform-python-3.6.8-37.el8.x86_64                                                                                         4/4
  Running scriptlet: platform-python-3.6.8-37.el8.x86_64                                                                                         4/4
  Verifying        : python3-libs-3.6.8-38.el8_4.x86_64                                                                                          1/4
  Verifying        : python3-libs-3.6.8-37.el8.x86_64                                                                                            2/4
  Verifying        : platform-python-3.6.8-38.el8_4.x86_64                                                                                       3/4
  Verifying        : platform-python-3.6.8-37.el8.x86_64                                                                                         4/4
Installed products updated.
Uploading Tracer Profile

Upgraded:
  platform-python-3.6.8-38.el8_4.x86_64                                      python3-libs-3.6.8-38.el8_4.x86_64

Complete!
```

4. Instalar ansible en el nodo de control
```
[root@server09 ~]# yum install -y ansible
Updating Subscription Management repositories.
Red Hat Ansible Engine 2.9 for RHEL 8 x86_64 (RPMs)                                               28 kB/s | 2.4 kB     00:00
Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)                                             29 kB/s | 2.4 kB     00:00
Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)                                          37 kB/s | 2.8 kB     00:00
Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 (RPMs)                                              29 kB/s | 2.1 kB     00:00
Dependencies resolved.
=================================================================================================================================
 Package                         Architecture      Version                   Repository                                     Size
=================================================================================================================================
Installing:
 ansible                         noarch            2.9.26-1.el8ae            ansible-2.9-for-rhel-8-x86_64-rpms             17 M
Installing dependencies:
 python3-babel                   noarch            2.5.1-5.el8               rhel-8-for-x86_64-appstream-rpms              4.8 M
 python3-cffi                    x86_64            1.11.5-5.el8              rhel-8-for-x86_64-baseos-rpms                 238 k
 python3-cryptography            x86_64            3.2.1-4.el8               rhel-8-for-x86_64-baseos-rpms                 559 k
 python3-jinja2                  noarch            2.10.1-2.el8_0            rhel-8-for-x86_64-appstream-rpms              538 k
 python3-markupsafe              x86_64            0.23-19.el8               rhel-8-for-x86_64-appstream-rpms               39 k
 python3-ply                     noarch            3.9-9.el8                 rhel-8-for-x86_64-baseos-rpms                 111 k
 python3-pycparser               noarch            2.14-14.el8               rhel-8-for-x86_64-baseos-rpms                 109 k
 python3-pytz                    noarch            2017.2-9.el8              rhel-8-for-x86_64-appstream-rpms               54 k
 python3-pyyaml                  x86_64            3.12-12.el8               rhel-8-for-x86_64-baseos-rpms                 193 k
 sshpass                         x86_64            1.06-3.el8ae              ansible-2.9-for-rhel-8-x86_64-rpms             27 k
Installing weak dependencies:
 python3-jmespath                noarch            0.9.0-11.el8              rhel-8-for-x86_64-appstream-rpms               45 k

Transaction Summary
=================================================================================================================================
Install  12 Packages

Total download size: 24 M
Installed size: 124 M
Downloading Packages:
(1/12): sshpass-1.06-3.el8ae.x86_64.rpm                                                          288 kB/s |  27 kB     00:00
(2/12): python3-pyyaml-3.12-12.el8.x86_64.rpm                                                    1.7 MB/s | 193 kB     00:00
(3/12): python3-pycparser-2.14-14.el8.noarch.rpm                                                 2.4 MB/s | 109 kB     00:00
(4/12): python3-cffi-1.11.5-5.el8.x86_64.rpm                                                     5.2 MB/s | 238 kB     00:00
(5/12): python3-cryptography-3.2.1-4.el8.x86_64.rpm                                               14 MB/s | 559 kB     00:00
(6/12): python3-ply-3.9-9.el8.noarch.rpm                                                         2.6 MB/s | 111 kB     00:00
(7/12): python3-jmespath-0.9.0-11.el8.noarch.rpm                                                 1.4 MB/s |  45 kB     00:00
(8/12): python3-pytz-2017.2-9.el8.noarch.rpm                                                     1.6 MB/s |  54 kB     00:00
(9/12): python3-markupsafe-0.23-19.el8.x86_64.rpm                                                897 kB/s |  39 kB     00:00
(10/12): python3-jinja2-2.10.1-2.el8_0.noarch.rpm                                                 12 MB/s | 538 kB     00:00
(11/12): ansible-2.9.26-1.el8ae.noarch.rpm                                                        52 MB/s |  17 MB     00:00
(12/12): python3-babel-2.5.1-5.el8.noarch.rpm                                                     45 MB/s | 4.8 MB     00:00
---------------------------------------------------------------------------------------------------------------------------------
Total                                                                                             64 MB/s |  24 MB     00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                         1/1
  Installing       : python3-markupsafe-0.23-19.el8.x86_64                                                                  1/12
  Installing       : python3-pytz-2017.2-9.el8.noarch                                                                       2/12
  Installing       : python3-babel-2.5.1-5.el8.noarch                                                                       3/12
  Installing       : python3-jinja2-2.10.1-2.el8_0.noarch                                                                   4/12
  Installing       : python3-jmespath-0.9.0-11.el8.noarch                                                                   5/12
  Installing       : python3-ply-3.9-9.el8.noarch                                                                           6/12
  Installing       : python3-pycparser-2.14-14.el8.noarch                                                                   7/12
  Installing       : python3-cffi-1.11.5-5.el8.x86_64                                                                       8/12
  Installing       : python3-cryptography-3.2.1-4.el8.x86_64                                                                9/12
  Installing       : python3-pyyaml-3.12-12.el8.x86_64                                                                     10/12
  Installing       : sshpass-1.06-3.el8ae.x86_64                                                                           11/12
  Installing       : ansible-2.9.26-1.el8ae.noarch                                                                         12/12
  Running scriptlet: ansible-2.9.26-1.el8ae.noarch                                                                         12/12
  Verifying        : ansible-2.9.26-1.el8ae.noarch                                                                          1/12
  Verifying        : sshpass-1.06-3.el8ae.x86_64                                                                            2/12
  Verifying        : python3-pyyaml-3.12-12.el8.x86_64                                                                      3/12
  Verifying        : python3-pycparser-2.14-14.el8.noarch                                                                   4/12
  Verifying        : python3-cffi-1.11.5-5.el8.x86_64                                                                       5/12
  Verifying        : python3-cryptography-3.2.1-4.el8.x86_64                                                                6/12
  Verifying        : python3-ply-3.9-9.el8.noarch                                                                           7/12
  Verifying        : python3-jmespath-0.9.0-11.el8.noarch                                                                   8/12
  Verifying        : python3-pytz-2017.2-9.el8.noarch                                                                       9/12
  Verifying        : python3-markupsafe-0.23-19.el8.x86_64                                                                 10/12
  Verifying        : python3-jinja2-2.10.1-2.el8_0.noarch                                                                  11/12
  Verifying        : python3-babel-2.5.1-5.el8.noarch                                                                      12/12
Installed products updated.
Uploading Tracer Profile

Installed:
  ansible-2.9.26-1.el8ae.noarch               python3-babel-2.5.1-5.el8.noarch         python3-cffi-1.11.5-5.el8.x86_64
  python3-cryptography-3.2.1-4.el8.x86_64     python3-jinja2-2.10.1-2.el8_0.noarch     python3-jmespath-0.9.0-11.el8.noarch
  python3-markupsafe-0.23-19.el8.x86_64       python3-ply-3.9-9.el8.noarch             python3-pycparser-2.14-14.el8.noarch
  python3-pytz-2017.2-9.el8.noarch            python3-pyyaml-3.12-12.el8.x86_64        sshpass-1.06-3.el8ae.x86_64

Complete!
```

Adicionalmente instalar las herramientas de trabajo con las que este familiarizado incluir vim y wget para el laboratorio.
```
[root@server09 ~]# yum install net-tools bash-completion bind-utils git vim tree wget -y
```

## **Instalar Requerimientos en el Managed Node**
1. Instalar Python en el nodo administrado
```
[root@node91 ~]# yum install platform-python -y
Updating Subscription Management repositories.
Red Hat Ansible Engine 2.9 for RHEL 8 x86_64 (RPMs)                                                                  7.9 MB/s | 2.0 MB     00:00
Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)                                                                 26 kB/s | 2.4 kB     00:00
Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)                                                              43 kB/s | 2.8 kB     00:00
Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 (RPMs)                                                                  25 kB/s | 2.1 kB     00:00
Package platform-python-3.6.8-37.el8.x86_64 is already installed.
Dependencies resolved.
=====================================================================================================================================================
 Package                           Architecture             Version                            Repository                                       Size
=====================================================================================================================================================
Upgrading:
 platform-python                   x86_64                   3.6.8-38.el8_4                     rhel-8-for-x86_64-baseos-rpms                    84 k
 python3-libs                      x86_64                   3.6.8-38.el8_4                     rhel-8-for-x86_64-baseos-rpms                   7.8 M

Transaction Summary
=====================================================================================================================================================
Upgrade  2 Packages

Total download size: 7.9 M
Downloading Packages:
(1/2): platform-python-3.6.8-38.el8_4.x86_64.rpm                                                                     818 kB/s |  84 kB     00:00
(2/2): python3-libs-3.6.8-38.el8_4.x86_64.rpm                                                                         55 MB/s | 7.8 MB     00:00
-----------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                 55 MB/s | 7.9 MB     00:00
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                             1/1
  Upgrading        : platform-python-3.6.8-38.el8_4.x86_64                                                                                       1/4
  Running scriptlet: platform-python-3.6.8-38.el8_4.x86_64                                                                                       1/4
  Upgrading        : python3-libs-3.6.8-38.el8_4.x86_64                                                                                          2/4
  Cleanup          : python3-libs-3.6.8-37.el8.x86_64                                                                                            3/4
  Cleanup          : platform-python-3.6.8-37.el8.x86_64                                                                                         4/4
  Running scriptlet: platform-python-3.6.8-37.el8.x86_64                                                                                         4/4
  Verifying        : python3-libs-3.6.8-38.el8_4.x86_64                                                                                          1/4
  Verifying        : python3-libs-3.6.8-37.el8.x86_64                                                                                            2/4
  Verifying        : platform-python-3.6.8-38.el8_4.x86_64                                                                                       3/4
  Verifying        : platform-python-3.6.8-37.el8.x86_64                                                                                         4/4
Installed products updated.
Uploading Tracer Profile

Upgraded:
  platform-python-3.6.8-38.el8_4.x86_64                                      python3-libs-3.6.8-38.el8_4.x86_64

Complete!
```
Repetir los pasos del **1 al 3** para los clientes: **nodeX2, nodeX3, nodeX4**. Donde **X** es el **numero del usuario** asignado del 1 al 6. 


## **Configurar espacio de trabajo y recursos en el nodo de control**

Se debe definir un usuario de automatización para toda la infraestructura, en nuestro taller el usuario ansible será el usuario de automatización, el mismo requiere cierta configuración tanto en el nodo de control como en los nodos administrador.

1. Crear el usuario ansible en el nodo de control y asignarle el password redhat
```
[root@server09 ~]# useradd ansible
[root@server09 ~]# id ansible
uid=1000(ansible) gid=1000(ansible) groups=1000(ansible)

[root@server09 ~]# echo "redhat" | passwd --stdin ansible
```

2. Configurarle permisos sudo al usuario ansible en el nodo de control
```
[root@server09 ~]# echo "ansible ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/ansible

[root@server09 ~]# cat /etc/sudoers.d/ansible
ansible ALL=(ALL)       NOPASSWD: ALL
```

3. Crear par de llaves ssh para el usuario ansible
```
[root@server09 ~]# su - ansible
[root@server09 ~]# ssh-keygen -t rsa -f ~/.ssh/id_rsa -N ""
```

4. Configurar editor vim y crear espacio de trabajo
```
[ansible@server09 ~]$ echo "autocmd filetype yaml setlocal ai ts=2 sw=2 et" > ~/.vimrc

[ansible@server09 ~]$ mkdir ansible
[ansible@server09 ~]$ cd ansible/

[ansible@server09 ~]$ wget ftp://classroom.opennova.pe/ansible/inventory-template
[ansible@server09 ~]$ wget ftp://classroom.opennova.pe/ansible/inventory.yml
[ansible@server09 ~]$ wget ftp://classroom.opennova.pe/ansible/ansible.cfg
```

Nota: Una vez descargado el archivo inventory-template renonmbrarlo a inventory y reemplazar donde indique X con el numero de su usuario asignado del 1 al 6.

```
[ansible@server09 ansible]$ mv inventory-template inventory
```

5. Hacer un login inicial del usuario ansible desde el nodo de control hacia el usuario root de los nodos administrados, para que se haga un primer reconocimiento del archivos known_hosts en el nodo de control.
```
[ansible@server09 ~]$ ssh root@node91.opennova.pe
root@node91.opennova.pe's password: <ingresar credencial>
[root@node91 ~]# exit
logout
Connection to node91.opennova.pe closed.
```
Repetir el paso 5 para los clientes: **nodeX2, nodeX3, nodeX4**. Donde **X** es el **numero del usuario** asignado del 1 al 6. 

6. Revisar en la sesión el archivo inventory, inventory.yml y ansible.cfg para entender su función en el setup inicial. De la misma manera inspeccionar los archivos de configuración por defecto **/etc/ansible/ansible.cfg** y **/etc/ansible/hosts**

```
[ansible@server09 ~]$ cat /etc/ansible/ansible.cfg
[ansible@server09 ~]$ cat /etc/ansible/hosts
```

Luego inspeccionar los archivos inventory y ansible.cfg en el espacio de trabajo del usuario ansible.

```
[ansible@server09 ~]$ cat /home/ansible/ansible/inventory
[ansible@server09 ~]$ cat /home/ansible/ansible/ansible.cfg
```

Para entender algunas directivas de configuración de ansible.cfg revisar la siguiente tabla:

Ansible Configuration
|Directiva | Descripción |
| --- | --- |
|inventory | Especifica la ruta al archivo de inventario.|
|remote_user | El nombre del usuario para iniciar sesión en los hosts administrados. Si no especificado, se utiliza el nombre del usuario actual.|
|ask_pass | Si solicita o no una contraseña SSH. Puede ser false si usa autenticación de clave pública SSH.|
|become | Ya sea para cambiar de usuario automáticamente en el host administrado (normalmente a root) después de conectarse. Esto también puede ser especificado en el playbook.|
|become_method | Cómo cambiar de usuario (normalmente sudo, que es el predeterminado, pero su es una opción).|
|become_user | El usuario al que cambiar en el host administrado (normalmente root, que es el predeterminado).|
|become_ask_pass | Ya sea para solicitar una contraseña para su become_method. El valor predeterminado es false.|

7. Adicional al inventario la siguiente información:

-  Agregar el grupo deploy el cual deberá contener los nodos: nodeX1, nodeX2, nodeX3, nodeX4. Donde **X** es el **numero del usuario** asignado del 1 al 6. 

<br> Opción 01
```
[ansible@server09 ansible]$ pwd
/home/ansible/ansible

[ansible@server09 ansible]$ vim inventory
...
[deploy]
node91.opennova.pe
node92.opennova.pe
node93.opennova.pe
node94.opennova.pe
...
```
<br> Opción 02

```
[ansible@server09 ansible]$ pwd
/home/ansible/ansible

[ansible@server09 ansible]$ vim inventory
...
[deploy]
node9[1:4].opennova.pe
...
```

- Agregar el grupo webservers el cual deberá contener los nodos: nodeX1, nodeX2. Donde **X** es el **numero del usuario** asignado del 1 al 6. 

<br> Opción 01

```
[ansible@server09 ansible]$ pwd
/home/ansible/ansible

[ansible@server09 ansible]$ vim inventory
...
[webservers]
node91.opennova.pe
node92.opennova.pe
...
```
<br> Opción 02
```
[ansible@server09 ansible]$ pwd
/home/ansible/ansible

[ansible@server09 ansible]$ vim inventory
...
[webservers]
node9[1:2].opennova.pe
...
```

- Agregar el grupo anidado o nested group infra el cual deberá contener los grupos: webservers y servers.

```
[ansible@server09 ansible]$ pwd
/home/ansible/ansible

[ansible@server09 ansible]$ vim inventory
...
[infra:children]
webservers
servers
...
```

8. Verificar el inventario configurado de tal manera que se pueda validar los nodos y grupos configurados. Nota: como inicialmente las credenciales tanto para el usuario de conexión como para el usuario de escalamiento de privilegios es root utilizar esas credenciales iniciales.
```
[ansible@server09 ansible]$ ansible all --list-hosts
SSH password: <ingresar contraseña>
BECOME password[defaults to SSH password]: < ingresar contraseña>

[ansible@server09 ansible]$ ansible ungrouped --list-hosts
SSH password: <ingresar contraseña>
BECOME password[defaults to SSH password]: < ingresar contraseña>

[ansible@server09 ansible]$ ansible prod --list-hosts
SSH password: <ingresar contraseña>
BECOME password[defaults to SSH password]: < ingresar contraseña>

[ansible@server09 ansible]$ ansible dev --list-hosts
SSH password: <ingresar contraseña>
BECOME password[defaults to SSH password]: < ingresar contraseña>

[ansible@server09 ansible]$ ansible qa --list-hosts
SSH password: <ingresar contraseña>
BECOME password[defaults to SSH password]: < ingresar contraseña>

[ansible@server09 ansible]$ ansible deploy --list-hosts
SSH password: <ingresar contraseña>
BECOME password[defaults to SSH password]: < ingresar contraseña>

[ansible@server09 ansible]$ ansible webservers --list-hosts
SSH password: <ingresar contraseña>
BECOME password[defaults to SSH password]: < ingresar contraseña>

[ansible@server09 ansible]$ ansible servers --list-hosts
SSH password: <ingresar contraseña>
BECOME password[defaults to SSH password]: < ingresar contraseña>

[ansible@server09 ansible]$ ansible infra --list-hosts
SSH password: <ingresar contraseña>
BECOME password[defaults to SSH password]: < ingresar contraseña>
```

9. Consultar los módulos disponibles en ansible y revisar el modulo ping para utilizarlo en pruebas de conectividad iniciales. Realizar la prueba de conectividad vía el modulo ping al grupo deploy.
```
[ansible@server09 ansible]$ ansible-doc -l

[ansible@server09 ansible]$ ansible-doc ping
```

```
[ansible@server09 ansible]$ ansible deploy -m ping
SSH password:
BECOME password[defaults to SSH password]:
node93.opennova.pe | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
node94.opennova.pe | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
node92.opennova.pe | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
node91.opennova.pe | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": false,
    "ping": "pong"
}
```

10. Validar que el modulo shell con el comando df -h se pueda ejecutar en los nodos del grupo deploy
```
[ansible@server09 ansible]$ ansible deploy -m shell -a "df -h"
SSH password:
BECOME password[defaults to SSH password]:
```

## **Configurar nodos administrados para trabajar con usuario ansible vía llaves ssh(Procedimiento manual clientes)**
1. Crear usuario ansible en el nodo administrado
```
[root@node91 ~]# useradd ansible
[root@node91 ~]# id ansible
uid=1000(ansible) gid=1000(ansible) groups=1000(ansible)

[root@node91 ~]# echo "redhat" | passwd --stdin ansible
```

2. Configurarle permisos sudo al usuario ansible en el nodo administrador
```
[root@node91 ~]# echo "ansible ALL=(ALL)       NOPASSWD: ALL" > /etc/sudoers.d/ansible

[root@node91 ~]# cat /etc/sudoers.d/ansible
ansible ALL=(ALL)       NOPASSWD: ALL
```

3. Copiar llaves ssh del usuario ansible del nodo de control hacia el usuario ansible del nodo administrado y validar que podamos logearnos sin contraseña.
```
[ansible@server09 ~]$ ssh-copy-id -i /home/ansible/.ssh/id_rsa.pub ansible@node91.opennova.pe
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/ansible/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
ansible@node91.opennova.pe's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'ansible@node91.opennova.pe'"
and check to make sure that only the key(s) you wanted were added.

[ansible@server09 ~]$ ssh 'ansible@node91.opennova.pe'
Last login: Wed Oct 27 15:50:39 2021
[ansible@node91 ~]$ exit
```

Para validar la operación de prueba del procedimiento manual, modificar la configuración del /home/ansible/ansible/ansible.cfg del espacio de trabajo del usuario ansible como sigue:
<br> Cambiar de:
```
[ansible@server09 ansible]$ cat ansible.cfg
[defaults]
inventory = ./inventory
remote_user = root
ask_pass = True

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = True
```

A esta configuración:
```
[ansible@server09 ansible]$ cat ansible.cfg
[defaults]
inventory = ./inventory
remote_user = ansible
ask_pass = False

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = False
```

Posteriormente tratar de ejecutar el comando remoto **df -h** con el **modulo shell** en el **grupo prod** y validar que ahora **no solicite credenciales**.
```
[ansible@server09 ansible]$ ansible prod -m shell -a "df -h"
```

Una vez validado que el nodo de control puede ejecutar comandos remotos utilizando el usuario ansible como usuario de conexión sin contraseña y elevarse a root sin contraseña devolver la configuración de /home/ansible/ansible/ansible.cfg a su estado original para proceder a configurar todos los nodos del grupo deploy

<br> Validar que la configuración quede como:
```
[ansible@server09 ansible]$ cat ansible.cfg
[defaults]
inventory = ./inventory
remote_user = root
ask_pass = True

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = True
```

## **Configurar nodos administrados para trabajar con usuario ansible vía llaves ssh(Procedimiento vía nodo de control)**

Nota: Antes de comenzar validar que el usuario ansible y el archivo /etc/sudoers.d/ansible no existan en los nodos administrados. En este caso como estamos trabajando con el nodox1.opennova.pe, validar que no existan estos recursos.
```
[root@node91 ~]# userdel -r ansible
[root@node91 ~]# rm -rf /etc/sudoers.d/ansible
```

1. En el nodo de control validar que el usuario ansible tenga el par de llaves ssh generadas. Este procedimiento lo debe ejecutar en su server0X, donde X es numero de su usuario asignado del 1 al 6.
```
[ansible@server09 ~]$ ls -l /home/ansible/.ssh/
total 12
-rw-------. 1 ansible ansible 2622 Oct 25 20:17 id_rsa
-rw-r--r--. 1 ansible ansible  582 Oct 25 20:17 id_rsa.pub
-rw-r--r--. 1 ansible ansible  776 Oct 25 20:55 known_hosts
```

2. Inspeccionar y discutir la operación de los siguientes comando add-hoc, como prueba inicial utilizar el grupo prod como referencia de ejecución. Para este procedimiento inspeccionar los módulos user, shell, copy, authorized_key.
```
[ansible@server09 ansible]$ ansible-doc user
[ansible@server09 ansible]$ ansible prod -m user -a "name=ansible uid=1000 shell=/bin/bash state=present"
SSH password: <ingresar_contraseña>
BECOME password[defaults to SSH password]: <ingresar_contraseña>

[ansible@server09 ansible]$ ansible-doc shell
[ansible@server09 ansible]$ ansible prod -m shell -a "echo redhat | passwd --stdin ansible"
SSH password: <ingresar_contraseña>
BECOME password[defaults to SSH password]: <ingresar_contraseña>

[ansible@server09 ansible]$ ansible-doc copy
[ansible@server09 ansible]$ ansible prod -m copy -a "content='ansible ALL=(ALL) NOPASSWD: ALL' dest=/etc/sudoers.d/ansible"
SSH password: <ingresar_contraseña>
BECOME password[defaults to SSH password]: <ingresar_contraseña>

[ansible@server09 ansible]$ ansible-doc authorized_key
[ansible@server09 ansible]$ansible prod -m authorized_key -a "user=ansible state=present key={{ lookup('file', '/home/ansible/.ssh/id_rsa.pub') }}"
SSH password: <ingresar_contraseña>
BECOME password[defaults to SSH password]: <ingresar_contraseña>
```

Para validar la operación de prueba, modificar la configuración del /home/ansible/ansible/ansible.cfg del espacio de trabajo del usuario ansible como sigue:
<br> Cambiar de:
```
[ansible@server09 ansible]$ cat ansible.cfg
[defaults]
inventory = ./inventory
remote_user = root
ask_pass = True

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = True
```

A esta configuración:
```
[ansible@server09 ansible]$ cat ansible.cfg
[defaults]
inventory = ./inventory
remote_user = ansible
ask_pass = False

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = False
```

Posteriormente tratar de ejecutar el comando remoto **df -h** con el **modulo shell** en el **grupo prod** y validar que ahora **no solicite credenciales**.
```
[ansible@server09 ansible]$ ansible prod -m shell -a "df -h"
```

Una vez validado que el nodo de control puede ejecutar comandos remotos utilizando el usuario ansible como usuario de conexión sin contraseña y elevarse a root sin contraseña devolver la configuración de /home/ansible/ansible/ansible.cfg a su estado original para proceder a configurar todos los nodos del grupo deploy

<br> Validar que la configuración quede como:
```
[ansible@server09 ansible]$ cat ansible.cfg
[defaults]
inventory = ./inventory
remote_user = root
ask_pass = True

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = True
```

3. Crear en el espacio de trabajo /home/ansible/ansible un script en bash de nombre setup-adhoc.sh contenga lo siguiente:
```
[ansible@server09 ansible]$ vim setup-adhoc.sh
#!/bin/bash
#Create ansible user
ansible deploy -m user -a "name=ansible uid=1000 shell=/bin/bash state=present"

#Set ansible user password
ansible deploy -m shell -a "echo redhat | passwd --stdin ansible"

#Setup sudo privileges for ansible user
ansible deploy -m copy -a "content='ansible ALL=(ALL) NOPASSWD: ALL' dest=/etc/sudoers.d/ansible"

#Copy ssh key from ansible user in control node to ansible user in managed nodes
ansible deploy -m authorized_key -a "user=ansible state=present key={{ lookup('file', '/home/ansible/.ssh/id_rsa.pub') }}"
```

4. Ejecutar y validar el correcto funcionamiento del script setup-adhoc.sh
```
[ansible@server09 ansible]$ bash setup-adhoc.sh
SSH password: <ingresar_contraseña>
BECOME password[defaults to SSH password]: <ingresar_contraseña>
node92.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1000,
    "home": "/home/ansible",
    "name": "ansible",
    "shell": "/bin/bash",
    "state": "present",
    "system": false,
    "uid": 1000
}
node94.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1000,
    "home": "/home/ansible",
    "name": "ansible",
    "shell": "/bin/bash",
    "state": "present",
    "system": false,
    "uid": 1000
}
node93.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1000,
    "home": "/home/ansible",
    "name": "ansible",
    "shell": "/bin/bash",
    "state": "present",
    "system": false,
    "uid": 1000
}
node91.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": "",
    "create_home": true,
    "group": 1000,
    "home": "/home/ansible",
    "name": "ansible",
    "shell": "/bin/bash",
    "state": "present",
    "system": false,
    "uid": 1000
}

SSH password: <ingresar_contraseña>
BECOME password[defaults to SSH password]: <ingresar_contraseña>
node91.opennova.pe | CHANGED | rc=0 >>
Changing password for user ansible.
passwd: all authentication tokens updated successfully.
node92.opennova.pe | CHANGED | rc=0 >>
Changing password for user ansible.
passwd: all authentication tokens updated successfully.
node94.opennova.pe | CHANGED | rc=0 >>
Changing password for user ansible.
passwd: all authentication tokens updated successfully.
node93.opennova.pe | CHANGED | rc=0 >>
Changing password for user ansible.
passwd: all authentication tokens updated successfully.

SSH password: <ingresar_contraseña>
BECOME password[defaults to SSH password]: <ingresar_contraseña>
node93.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "checksum": "0e2acb1172a2aab3688a29dd3a644e77f3c6e53e",
    "dest": "/etc/sudoers.d/ansible",
    "gid": 0,
    "group": "root",
    "md5sum": "94f8e667bc58a8600e3f092631926055",
    "mode": "0644",
    "owner": "root",
    "secontext": "system_u:object_r:etc_t:s0",
    "size": 31,
    "src": "/root/.ansible/tmp/ansible-tmp-1635369761.0412073-14725-228162569873209/source",
    "state": "file",
    "uid": 0
}
node94.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "checksum": "0e2acb1172a2aab3688a29dd3a644e77f3c6e53e",
    "dest": "/etc/sudoers.d/ansible",
    "gid": 0,
    "group": "root",
    "md5sum": "94f8e667bc58a8600e3f092631926055",
    "mode": "0644",
    "owner": "root",
    "secontext": "system_u:object_r:etc_t:s0",
    "size": 31,
    "src": "/root/.ansible/tmp/ansible-tmp-1635369761.038752-14726-12846207559701/source",
    "state": "file",
    "uid": 0
}
node91.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "checksum": "0e2acb1172a2aab3688a29dd3a644e77f3c6e53e",
    "dest": "/etc/sudoers.d/ansible",
    "gid": 0,
    "group": "root",
    "md5sum": "94f8e667bc58a8600e3f092631926055",
    "mode": "0644",
    "owner": "root",
    "secontext": "system_u:object_r:etc_t:s0",
    "size": 31,
    "src": "/root/.ansible/tmp/ansible-tmp-1635369761.0361688-14722-40549305685145/source",
    "state": "file",
    "uid": 0
}
node92.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "checksum": "0e2acb1172a2aab3688a29dd3a644e77f3c6e53e",
    "dest": "/etc/sudoers.d/ansible",
    "gid": 0,
    "group": "root",
    "md5sum": "94f8e667bc58a8600e3f092631926055",
    "mode": "0644",
    "owner": "root",
    "secontext": "system_u:object_r:etc_t:s0",
    "size": 31,
    "src": "/root/.ansible/tmp/ansible-tmp-1635369761.0319064-14723-201151924444824/source",
    "state": "file",
    "uid": 0
}

SSH password: <ingresar_contraseña>
BECOME password[defaults to SSH password]: <ingresar_contraseña>
node92.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": null,
    "exclusive": false,
    "follow": false,
    "key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCneAf/+wPKW09WT4Yfc9ot+oP2By4ovKjMg1G0bkE81wiehd+JNv/HwzwN5xxO1fPMhJ+yisYgCZm/kRHvX4xeuEfjCu3MriSviNpb5/HmVdi/7fhyLDLEjpkwQ8a32QscFp8e+kmDqeBzFSBX4ne4IhOYFNSQSYbqU9ST7MYCUQtRZkLRXx5eQ+EpmWnSTDbIx4RKjElNDgZj4p+ylP9sPQprcAIct1HsPWQvy7OuOS3OZAVQk0wwcQjZsgwjE2XN8R+QuKSTd/JgPMz0RHfIpcti2TWbqh/SlC6YrML4KEWS1wNks33vAadIx7aW9R2UWQviUHqkqfRmOsgpHPq3MbSB6ieMU1K2izjFeLvgAJTJ4eTp+armp7761Ht7w6CwIbubofJQ1SlqJ3vK4V6oz2oEyrXTspMmp8uOHnveIhoUZ26waDowQ00WFqhJ2RseBXzLT6MtSm0j5frDVTfQGwbYnjvpLr2Neraw7GW+uyYrr00kXXhQfS5AFvw55OM= ansible@server09.opennova.pe",
    "key_options": null,
    "keyfile": "/home/ansible/.ssh/authorized_keys",
    "manage_dir": true,
    "path": null,
    "state": "present",
    "user": "ansible",
    "validate_certs": true
}
node94.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": null,
    "exclusive": false,
    "follow": false,
    "key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCneAf/+wPKW09WT4Yfc9ot+oP2By4ovKjMg1G0bkE81wiehd+JNv/HwzwN5xxO1fPMhJ+yisYgCZm/kRHvX4xeuEfjCu3MriSviNpb5/HmVdi/7fhyLDLEjpkwQ8a32QscFp8e+kmDqeBzFSBX4ne4IhOYFNSQSYbqU9ST7MYCUQtRZkLRXx5eQ+EpmWnSTDbIx4RKjElNDgZj4p+ylP9sPQprcAIct1HsPWQvy7OuOS3OZAVQk0wwcQjZsgwjE2XN8R+QuKSTd/JgPMz0RHfIpcti2TWbqh/SlC6YrML4KEWS1wNks33vAadIx7aW9R2UWQviUHqkqfRmOsgpHPq3MbSB6ieMU1K2izjFeLvgAJTJ4eTp+armp7761Ht7w6CwIbubofJQ1SlqJ3vK4V6oz2oEyrXTspMmp8uOHnveIhoUZ26waDowQ00WFqhJ2RseBXzLT6MtSm0j5frDVTfQGwbYnjvpLr2Neraw7GW+uyYrr00kXXhQfS5AFvw55OM= ansible@server09.opennova.pe",
    "key_options": null,
    "keyfile": "/home/ansible/.ssh/authorized_keys",
    "manage_dir": true,
    "path": null,
    "state": "present",
    "user": "ansible",
    "validate_certs": true
}
node93.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": null,
    "exclusive": false,
    "follow": false,
    "key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCneAf/+wPKW09WT4Yfc9ot+oP2By4ovKjMg1G0bkE81wiehd+JNv/HwzwN5xxO1fPMhJ+yisYgCZm/kRHvX4xeuEfjCu3MriSviNpb5/HmVdi/7fhyLDLEjpkwQ8a32QscFp8e+kmDqeBzFSBX4ne4IhOYFNSQSYbqU9ST7MYCUQtRZkLRXx5eQ+EpmWnSTDbIx4RKjElNDgZj4p+ylP9sPQprcAIct1HsPWQvy7OuOS3OZAVQk0wwcQjZsgwjE2XN8R+QuKSTd/JgPMz0RHfIpcti2TWbqh/SlC6YrML4KEWS1wNks33vAadIx7aW9R2UWQviUHqkqfRmOsgpHPq3MbSB6ieMU1K2izjFeLvgAJTJ4eTp+armp7761Ht7w6CwIbubofJQ1SlqJ3vK4V6oz2oEyrXTspMmp8uOHnveIhoUZ26waDowQ00WFqhJ2RseBXzLT6MtSm0j5frDVTfQGwbYnjvpLr2Neraw7GW+uyYrr00kXXhQfS5AFvw55OM= ansible@server09.opennova.pe",
    "key_options": null,
    "keyfile": "/home/ansible/.ssh/authorized_keys",
    "manage_dir": true,
    "path": null,
    "state": "present",
    "user": "ansible",
    "validate_certs": true
}
node91.opennova.pe | CHANGED => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/libexec/platform-python"
    },
    "changed": true,
    "comment": null,
    "exclusive": false,
    "follow": false,
    "key": "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCneAf/+wPKW09WT4Yfc9ot+oP2By4ovKjMg1G0bkE81wiehd+JNv/HwzwN5xxO1fPMhJ+yisYgCZm/kRHvX4xeuEfjCu3MriSviNpb5/HmVdi/7fhyLDLEjpkwQ8a32QscFp8e+kmDqeBzFSBX4ne4IhOYFNSQSYbqU9ST7MYCUQtRZkLRXx5eQ+EpmWnSTDbIx4RKjElNDgZj4p+ylP9sPQprcAIct1HsPWQvy7OuOS3OZAVQk0wwcQjZsgwjE2XN8R+QuKSTd/JgPMz0RHfIpcti2TWbqh/SlC6YrML4KEWS1wNks33vAadIx7aW9R2UWQviUHqkqfRmOsgpHPq3MbSB6ieMU1K2izjFeLvgAJTJ4eTp+armp7761Ht7w6CwIbubofJQ1SlqJ3vK4V6oz2oEyrXTspMmp8uOHnveIhoUZ26waDowQ00WFqhJ2RseBXzLT6MtSm0j5frDVTfQGwbYnjvpLr2Neraw7GW+uyYrr00kXXhQfS5AFvw55OM= ansible@server09.opennova.pe",
    "key_options": null,
    "keyfile": "/home/ansible/.ssh/authorized_keys",
    "manage_dir": true,
    "path": null,
    "state": "present",
    "user": "ansible",
    "validate_certs": true
}
```

5. Para validar la operación, modificar la configuración del /home/ansible/ansible/ansible.cfg del espacio de trabajo del usuario ansible como sigue:
<br> Cambiar de:
```
[ansible@server09 ansible]$ cat ansible.cfg
[defaults]
inventory = ./inventory
remote_user = root
ask_pass = True

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = True
```

A esta configuración:
```
[ansible@server09 ansible]$ cat ansible.cfg
[defaults]
inventory = ./inventory
remote_user = ansible
ask_pass = False

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = False
```

Posteriormente tratar de ejecutar el comando remoto **df -h** con el **modulo shell** en el **grupo deploy** y validar que ahora **no solicite credenciales**.
```
[ansible@server09 ansible]$ ansible deploy -m shell -a "df -h"
```

Con esto ya tenemos el setup inicial de nuestro laboratorio configurado para ejecutar tareas de configuración.

# Laboratorio: Setup Inicial Ansible

NOTA: 
- Las tareas a ejecutarse en el nodo de control serán en la estación server0X.opennova.pe, donde X es el numero de usuario del 1 al 6 respectivamente. 
- Las tareas a ejecutarse en los nodos administrados serán en las estaciones: nodeX1.opennova.pe, nodeX2.opennova.pe, nodeX3.opennova.pe, nodeX4.opennova.pe, donde X es el numero de usuario del 1 al 6 respectivamente. 
- Si al probar la conectividad via el modulo ping de ansible hacia los nodos administrador le sale el siguiente mensaje:
```
[ansible@server09 ansible]$ ansible -m ping prod
SSH password:
BECOME password[defaults to SSH password]:
node91.opennova.pe | FAILED! => {
    "msg": "Using a SSH password instead of a key is not possible because Host Key checking is enabled and sshpass does not support this.  Please add this host's fingerprint to your known_hosts file to manage this host."
}
```

Debe establecer la conexión ssh inicial desde el nodo de control hacia los nodos administrador como indica el **punto 5**. de la seccion **Configurar espacio de trabajo y recursos en el nodo de control**

**Requerimientos:**
1. Instalar y/o Actualizar Python en el nodo de control.
2. Instalar ansible en el nodo de control asignado.
3. Instalar y/o Actualizar Python en los nodos administrados.
4. En el nodo de control realizar lo siguiente:
- Crear el usuario ansible.
- Asignar la contraseña redhat.
- Crear un directorio de trabajo de nombre ansible.
- Configurar el editor vim para que pueda interpretar correctamente ansible. (Sino tiene vim instalado puede instalarlo)
- En el directorio de trabajo ansible descargar de ftp://classroom.opennova.pe los archivos: inventory-template, ansible.cfg.
5. Al inventario agregarle los siguientes grupos:
- Agregar el grupo webservers el cual debe contener los nodos: nodeX1.opennova.pe  y nodeX2.opennova.pe. (Revisar la nota inicial).
- Agregar el grupo deploy en cual debe contener los nodos: nodeX1.opennova.pe, nodeX2.opennova.pe, nodeX3.opennova.pe, nodeX4.opennova.pe.(Revisar la nota inicial).
- Agregar el grupo anidado infra el cual debe contener los grupos: webservers y deploy.
- Modificar el inventario de tal manera que todos los objetos ya pre configurados correspondan a su ambiente de laboratorio. Cambiar nodeX1.opennova.pe, nodeX2.opennova.pe, nodeX3.opennova.pe, nodeX4.opennova.pe por sus respectivos recursos asignados. (Revisar la nota inicial).
- Mover el recurso desagrupado nodeX4.opennova.pe dentro del grupo qa. (Revisar la nota inicial).
- Actualizar las direcciones ip del nodo4 y del nodo de control de su entorno, con los datos proporcionados en el taller. 
6. Listar los host que pertenecen a los grupos: prod, dev, qa, webservers, deploy, servers, infra, all y ungrouped y verificar que estan de acorde al inventario.
7. Para el nodoX1.opennova.pe realizar el procedimiento de **Configurar nodos administrados para trabajar con usuario ansible vía llaves ssh(Procedimiento manual clientes)**.
8. Para los nodos del grupo deploy realizar el procedimiento de **Configurar nodos administrados para trabajar con usuario ansible vía llaves ssh(Procedimiento vía nodo de control)**. 
9. Al final de este punto usted deberá tener su ambiente de ansible configurado de tal modo que el usuario de conexión hacia todos los nodos sea ansible sin solicitud de contraseña y el usuario de escalamiento de privilegios sea root sin solicitud de contaseña.
Al ejecutar estos comando en sus nodos de control correspondientes, todos los nodos administrados deberían responder sin solicitar contraseña.
```
[ansible@server09 ansible]$ ansible deploy -m ping 
```

```
[root@server09 ~]# ansible deploy -m shell -a "df -h"
```








