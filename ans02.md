<h1>Ansible Playbooks</h1>
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans100.png?raw=true"width="800" height="400"></p>
<p>
<strong>Meta:</strong>
<br>- Entendimiento Ansible Playbooks, Roles y Collecciones.
</p>
<p>
<strong>Objetivos:</strong>
<br>- Conceptos Playbooks, Roles y Collecciones (Teórico)
</p>
<p>
<strong>Secciones:</strong>
<br>- Ansible funcionamiento y comandos adhoc. (Teórico)
<br>- Que son Playbooks, Roles y Colecciones. (Teórico)
<br>- Trabajando con Ansible Playbooks y Roles. (Demostración) 
</p>
<p>
<strong>Laboratorio:</strong>
</p>

# Ansible funcionamiento y comandos adhoc. (Teórico)
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans203.png?raw=true"width="800" height="400"></p>

### **¿Cómo funciona Ansible?**
Ansible se conecta a los nodos y les inserta pequeños programas denominados módulos, los cuales permiten llevar a cabo tareas de automatización en la plataforma.

Esta ejecuta esos programas, los cuales funcionan como modelos de recursos del estado deseado de los sistemas, y, luego, los retira cuando finaliza la tarea.

Sin ellos, usted dependería de comandos específicos y de la creación de scripts para concretar una tarea. 

Como Ansible no necesita agentes, no se requiere instalar ningún software en los nodos que gestiona.

La plataforma lee información en el inventario para saber qué máquinas desea gestionar. Aunque Ansible cuenta con un archivo de inventario predeterminado, usted puede crear uno propio y definir los servidores que desea que administre. 

La plataforma utiliza el protocolo SSH para conectarse a los servidores y ejecutar las tareas. De forma predeterminada, utiliza claves y un agente SSH para conectarse a las máquinas virtuales con su nombre de usuario actual. No es necesario que inicie sesión como superusuario; puede hacerlo como cualquier otro y luego utilizar los comandos su o sudo para adquirir nuevos privilegios.

Una vez que Ansible se conecta, transfiere los módulos que requiere el comando o el playbook a la máquina remota para que los ejecute.

La plataforma utiliza plantillas YAML comprensibles para las personas, para que los usuarios no tengan que aprender un lenguaje de programación avanzado cuando deseen establecer la ejecución automática de tareas repetitivas.

---
### **Utilización de Ansible para comandos específicos (Adhoc commands)**

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans201.png?raw=true"></p>

Puede ejecutar comandos específicos con Ansible si ejecuta uno o llama a un módulo directamente desde la línea de comandos, lo cual implica que no es necesario que utilice playbooks. 

Aunque esta acción sirve para las tareas que ocurren por única vez, deberá usar un playbook de Ansible para las más complejas.

---
# Que son Playbooks, Roles y Colecciones
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans202.png?raw=true"></p>

### **Playbooks, Roles y Colecciones y YAML para Ansible**

<br>Los playbooks de Ansible se utilizan para organizar los procesos de TI. Un playbook es un archivo YAML que contiene por lo menos un play, y que sirve para definir el estado deseado de un sistema. No es lo mismo que un módulo de Ansible, el cual es un script independiente que se puede utilizar dentro de un playbook de Ansible. 

Los plays son un conjunto ordenado de tareas que se ejecutan en las selecciones del host desde el archivo de inventario de Ansible. 

Las tareas son los elementos que llaman a los módulos de Ansible y que conforman un play, y se ejecutan allí en el mismo orden en que se escribieron.  

Cuando Ansible comienza a funcionar, puede hacer un seguimiento del estado de un sistema. Si al hacerlo detecta que la descripción del playbook sobre el sistema no coincide con su estado real, la plataforma implementará todos los cambios necesarios para que se cumpla esta correspondencia. 

Ansible incluye un "modo de verificación" que le muestra lo que la plataforma podría hacer, pero sin que se implementen cambios concretos. De este modo, usted puede validar los playbooks y los comandos específicos antes de llevar a cabo una modificación en el estado del sistema. 

<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans204.png?raw=true"width="800" height="400"></p>

Los controladores en Ansible (handlers) sirven para ejecutar una tarea específica luego de que se haya realizado un cambio en el sistema. Los activan las tareas, y se ejecutan una sola vez, después de todos los demás plays del playbook. 

Las variables, que son un concepto de Ansible que le permite modificar la ejecución de los playbooks, sirven para explicar las diferencias entre los sistemas, como las versiones de los paquetes o las rutas de los archivos. Ansible posibilita la ejecución de playbooks en diferentes sistemas. 

Las variables de Ansible se deben definir en función de la tarea que esté realizando el playbook. 

Estas siguen un orden de prioridad que establece cuáles prevalecerán sobre otras, lo cual debe tener en cuenta a la hora de incluir variables en el playbook.

Para trabajar con Ansible, también tendrá que comprender de qué se tratan las colecciones. Las colecciones son un formato de distribución para el contenido de Ansible que puede incluir playbooks, funciones, módulos y plugins.

Las funciones de Ansible (Roles) son un tipo de playbook especial completamente autónomo y portátil que incluye las tareas, las variables, las plantillas de configuración y otros archivos de soporte que son necesarios para completar una organización compleja. 

Una colección puede contener varias funciones (Roles) y módulos específicos que no estan necesariamente en una instalación de ansible, lo cual posibilita el intercambio sencillo de contenido a través de Automation Hub y Ansible Galaxy. 
<br>
#### Con ansible podemos automatizar toda la infraestructura tecnológica.
<p align="left"><img src="https://github.com/gpulido-redhat/tecnologiasredhat/blob/master/ans/ans206.png?raw=true"width="600" height="500"></p>
<br>

---

# Trabajando con Playbooks y Roles Ansible. (Demostración)

1. Crear un playbook para instalación de HTTPD Server, revisar las directivas y discutirlas.

<br> Inicialmente para este playbook vamos a copiar la llave ssh del usuario ansible hacia el propio usuario ansible ya que vamos a utilizar un play de validación de apache una vez instalado y es necesario para que no nos de error.

```
[ansible@server09 ansible]$ ssh-copy-id -i ~/.ssh/id_rsa.pub ansible@server09.opennova.pe
```

<br> Crear el playbook de nombre **install_webserver.yaml** dentro del directorio de trabajo /home/ansible/ansible que contenga la siguiente informacion:

```
---
- name: Install HTTPD Server Playbook
  hosts: prod
  tasks:
    - name: "Install httpd package on prod servers"
      yum:
        name: httpd
        state: present

    - name: "Install firewalld package on prod servers"
      yum:
        name: firewalld
        state: present

    - name: "Create a custom index.html"
      copy:
        dest: "/var/www/html/index.html"
        content: "My first webserver deployed with ansible 2.9"

    - name: "Startup httpd service on prod servers"
      service:
        name: httpd
        state: started
        enabled: yes

    - name: "Startup firewalld service on prod servers"
      service:
        name: firewalld
        state: started
        enabled: yes

    - name: "Open port 80/tcp on firewalld"
      firewalld:
        service: http
        permanent: yes
        immediate: yes
        state: enabled

- name: "Test httpd access from workstation"
  hosts: control_node
  become: no
  tasks:
    - name: "Connect to prod webserver"
      uri:
        url: http://node91.opennova.pe/index.html
        return_content: yes
        status_code: 200
```

Revisar si no existe algún error de sintaxis con el siguiente comando:
```
[ansible@server09 ansible]$ ansible-playbook --syntax-check install_webserver.yaml

playbook: install_webserver.yaml
```

Ejecutar una prueba de corrida del playbook install_webserver.yaml
```
[ansible@server09 ansible]$ ansible-playbook --check install_webserver.yaml

PLAY [Install HTTPD Server Playbook] ****************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [node91.opennova.pe]

TASK [Install httpd package on prod servers] ********************************************************************************************************
changed: [node91.opennova.pe]

TASK [Install firewalld package on prod servers] ****************************************************************************************************
ok: [node91.opennova.pe]

TASK [Create a custom index.html] *******************************************************************************************************************
changed: [node91.opennova.pe]

TASK [Startup httpd service on prod servers] ********************************************************************************************************
changed: [node91.opennova.pe]

TASK [Startup firewalld service on prod servers] ****************************************************************************************************
ok: [node91.opennova.pe]

TASK [Open port 80/tcp on firewalld] ****************************************************************************************************************
changed: [node91.opennova.pe]

PLAY [Test httpd access from workstation] ***********************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [control_node]

TASK [Connect to prod webserver] ********************************************************************************************************************
skipping: [control_node]

PLAY RECAP ******************************************************************************************************************************************
control_node               : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
node91.opennova.pe         : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

Finalmente ejecutar el playbook con el comando **ansible-playbook install_webserver.yaml -v**
```
[ansible@server09 ansible]$ ansible-playbook install_webserver.yaml -v
Using /home/ansible/ansible/ansible.cfg as config file

PLAY [Uninstall HTTPD Server Playbook] **************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [node91.opennova.pe]

TASK [Remove index.html from HTTPD Server] **********************************************************************************************************
ok: [node91.opennova.pe] => {"changed": false, "path": "/var/www/html/index.html", "state": "absent"}

TASK [Uninstall httpd package on prod servers] ******************************************************************************************************
ok: [node91.opennova.pe] => {"changed": false, "msg": "Nothing to do", "rc": 0, "results": []}

TASK [Close port 80/tcp on firewalld] ***************************************************************************************************************
ok: [node91.opennova.pe] => {"changed": false, "msg": "Permanent and Non-Permanent(immediate) operation"}

PLAY RECAP ******************************************************************************************************************************************
node91.opennova.pe         : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[ansible@server09 ansible]$
[ansible@server09 ansible]$ ansible-playbook install_webserver.yaml -v
Using /home/ansible/ansible/ansible.cfg as config file

PLAY [Install HTTPD Server Playbook] ****************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [node91.opennova.pe]

TASK [Install httpd package on prod servers] ********************************************************************************************************
changed: [node91.opennova.pe] => {"changed": true, "msg": "", "rc": 0, "results": ["Installed: mod_http2-1.15.7-3.module+el8.4.0+8625+d397f3da.x86_64", "Installed: httpd-2.4.37-39.module+el8.4.0+9658+b87b2deb.x86_64"]}

TASK [Install firewalld package on prod servers] ****************************************************************************************************
ok: [node91.opennova.pe] => {"changed": false, "msg": "Nothing to do", "rc": 0, "results": []}

TASK [Create a custom index.html] *******************************************************************************************************************
changed: [node91.opennova.pe] => {"changed": true, "checksum": "5efd47647d19c5a7468391d339ef6bda4adc7612", "dest": "/var/www/html/index.html", "gid": 0, "group": "root", "md5sum": "a8f25fe770d5c51fc2d3018cdebc072b", "mode": "0644", "owner": "root", "secontext": "system_u:object_r:httpd_sys_content_t:s0", "size": 44, "src": "/home/ansible/.ansible/tmp/ansible-tmp-1635795670.2088788-24362-193577383267849/source", "state": "file", "uid": 0}

TASK [Startup httpd service on prod servers] ********************************************************************************************************
changed: [node91.opennova.pe] => {"changed": true, "enabled": true, "name": "httpd", "state": "started", "status": {"ActiveEnterTimestampMonotonic": "0", "ActiveExitTimestampMonotonic": "0", "ActiveState": "inactive", "After": "systemd-tmpfiles-setup.service -.mount system.slice nss-lookup.target network.target httpd-init.service systemd-journald.socket sysinit.target remote-fs.target tmp.mount var-tmp.mount basic.target var.mount", "AllowIsolate": "no", "AllowedCPUs": "", "AllowedMemoryNodes": "", "AmbientCapabilities": "", "AssertResult": "no", "AssertTimestampMonotonic": "0", "Before": "shutdown.target", "BlockIOAccounting": "no", "BlockIOWeight": "[not set]", "CPUAccounting": "no", "CPUAffinity": "", "CPUAffinityFromNUMA": "no", "CPUQuotaPerSecUSec": "infinity", "CPUQuotaPeriodUSec": "infinity", "CPUSchedulingPolicy": "0", "CPUSchedulingPriority": "0", "CPUSchedulingResetOnFork": "no", "CPUShares": "[not set]", "CPUUsageNSec": "[not set]", "CPUWeight": "[not set]", "CacheDirectoryMode": "0755", "CanFreeze": "yes", "CanIsolate": "no", "CanReload": "yes", "CanStart": "yes", "CanStop": "yes", "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon", "CollectMode": "inactive", "ConditionResult": "no", "ConditionTimestampMonotonic": "0", "ConfigurationDirectoryMode": "0755", "Conflicts": "shutdown.target", "ControlPID": "0", "DefaultDependencies": "yes", "DefaultMemoryLow": "0", "DefaultMemoryMin": "0", "Delegate": "no", "Description": "The Apache HTTP Server", "DevicePolicy": "auto", "Documentation": "man:httpd.service(8)", "DynamicUser": "no", "EffectiveCPUs": "", "EffectiveMemoryNodes": "", "Environment": "LANG=C", "ExecMainCode": "0", "ExecMainExitTimestampMonotonic": "0", "ExecMainPID": "0", "ExecMainStartTimestampMonotonic": "0", "ExecMainStatus": "0", "ExecReload": "{ path=/usr/sbin/httpd ; argv[]=/usr/sbin/httpd $OPTIONS -k graceful ; ignore_errors=no ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "ExecStart": "{ path=/usr/sbin/httpd ; argv[]=/usr/sbin/httpd $OPTIONS -DFOREGROUND ; ignore_errors=no ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "FailureAction": "none", "FileDescriptorStoreMax": "0", "FragmentPath": "/usr/lib/systemd/system/httpd.service", "FreezerState": "running", "GID": "[not set]", "GuessMainPID": "yes", "IOAccounting": "no", "IOSchedulingClass": "0", "IOSchedulingPriority": "0", "IOWeight": "[not set]", "IPAccounting": "no", "IPEgressBytes": "18446744073709551615", "IPEgressPackets": "18446744073709551615", "IPIngressBytes": "18446744073709551615", "IPIngressPackets": "18446744073709551615", "Id": "httpd.service", "IgnoreOnIsolate": "no", "IgnoreSIGPIPE": "yes", "InactiveEnterTimestampMonotonic": "0", "InactiveExitTimestampMonotonic": "0", "JobRunningTimeoutUSec": "infinity", "JobTimeoutAction": "none", "JobTimeoutUSec": "infinity", "KeyringMode": "private", "KillMode": "mixed", "KillSignal": "28", "LimitAS": "infinity", "LimitASSoft": "infinity", "LimitCORE": "infinity", "LimitCORESoft": "infinity", "LimitCPU": "infinity", "LimitCPUSoft": "infinity", "LimitDATA": "infinity", "LimitDATASoft": "infinity", "LimitFSIZE": "infinity", "LimitFSIZESoft": "infinity", "LimitLOCKS": "infinity", "LimitLOCKSSoft": "infinity", "LimitMEMLOCK": "65536", "LimitMEMLOCKSoft": "65536", "LimitMSGQUEUE": "819200", "LimitMSGQUEUESoft": "819200", "LimitNICE": "0", "LimitNICESoft": "0", "LimitNOFILE": "262144", "LimitNOFILESoft": "1024", "LimitNPROC": "7114", "LimitNPROCSoft": "7114", "LimitRSS": "infinity", "LimitRSSSoft": "infinity", "LimitRTPRIO": "0", "LimitRTPRIOSoft": "0", "LimitRTTIME": "infinity", "LimitRTTIMESoft": "infinity", "LimitSIGPENDING": "7114", "LimitSIGPENDINGSoft": "7114", "LimitSTACK": "infinity", "LimitSTACKSoft": "8388608", "LoadState": "loaded", "LockPersonality": "no", "LogLevelMax": "-1", "LogRateLimitBurst": "0", "LogRateLimitIntervalUSec": "0", "LogsDirectoryMode": "0755", "MainPID": "0", "MemoryAccounting": "yes", "MemoryCurrent": "[not set]", "MemoryDenyWriteExecute": "no", "MemoryHigh": "infinity", "MemoryLimit": "infinity", "MemoryLow": "0", "MemoryMax": "infinity", "MemoryMin": "0", "MemorySwapMax": "infinity", "MountAPIVFS": "no", "MountFlags": "", "NFileDescriptorStore": "0", "NRestarts": "0", "NUMAMask": "", "NUMAPolicy": "n/a", "Names": "httpd.service", "NeedDaemonReload": "no", "Nice": "0", "NoNewPrivileges": "no", "NonBlocking": "no", "NotifyAccess": "main", "OOMScoreAdjust": "0", "OnFailureJobMode": "replace", "PermissionsStartOnly": "no", "Perpetual": "no", "PrivateDevices": "no", "PrivateMounts": "no", "PrivateNetwork": "no", "PrivateTmp": "yes", "PrivateUsers": "no", "ProtectControlGroups": "no", "ProtectHome": "no", "ProtectKernelModules": "no", "ProtectKernelTunables": "no", "ProtectSystem": "no", "RefuseManualStart": "no", "RefuseManualStop": "no", "RemainAfterExit": "no", "RemoveIPC": "no", "Requires": "system.slice -.mount var-tmp.mount sysinit.target var.mount", "RequiresMountsFor": "/var/tmp", "Restart": "no", "RestartUSec": "100ms", "RestrictNamespaces": "no", "RestrictRealtime": "no", "RestrictSUIDSGID": "no", "Result": "success", "RootDirectoryStartOnly": "no", "RuntimeDirectoryMode": "0755", "RuntimeDirectoryPreserve": "no", "RuntimeMaxUSec": "infinity", "SameProcessGroup": "no", "SecureBits": "0", "SendSIGHUP": "no", "SendSIGKILL": "yes", "Slice": "system.slice", "StandardError": "inherit", "StandardInput": "null", "StandardInputData": "", "StandardOutput": "journal", "StartLimitAction": "none", "StartLimitBurst": "5", "StartLimitIntervalUSec": "10s", "StartupBlockIOWeight": "[not set]", "StartupCPUShares": "[not set]", "StartupCPUWeight": "[not set]", "StartupIOWeight": "[not set]", "StateChangeTimestampMonotonic": "0", "StateDirectoryMode": "0755", "StatusErrno": "0", "StopWhenUnneeded": "no", "SubState": "dead", "SuccessAction": "none", "SyslogFacility": "3", "SyslogLevel": "6", "SyslogLevelPrefix": "yes", "SyslogPriority": "30", "SystemCallErrorNumber": "0", "TTYReset": "no", "TTYVHangup": "no", "TTYVTDisallocate": "no", "TasksAccounting": "yes", "TasksCurrent": "[not set]", "TasksMax": "11383", "TimeoutStartUSec": "1min 30s", "TimeoutStopUSec": "1min 30s", "TimerSlackNSec": "50000", "Transient": "no", "Type": "notify", "UID": "[not set]", "UMask": "0022", "UnitFilePreset": "disabled", "UnitFileState": "disabled", "UtmpMode": "init", "Wants": "httpd-init.service", "WatchdogTimestampMonotonic": "0", "WatchdogUSec": "0"}}

TASK [Startup firewalld service on prod servers] ****************************************************************************************************
ok: [node91.opennova.pe] => {"changed": false, "enabled": true, "name": "firewalld", "state": "started", "status": {"ActiveEnterTimestamp": "Mon 2021-10-25 20:23:00 -05", "ActiveEnterTimestampMonotonic": "5325751", "ActiveExitTimestampMonotonic": "0", "ActiveState": "active", "After": "dbus.service dbus.socket polkit.service sysinit.target system.slice basic.target", "AllowIsolate": "no", "AllowedCPUs": "", "AllowedMemoryNodes": "", "AmbientCapabilities": "", "AssertResult": "yes", "AssertTimestamp": "Mon 2021-10-25 20:22:59 -05", "AssertTimestampMonotonic": "4906104", "Before": "shutdown.target multi-user.target network-pre.target", "BlockIOAccounting": "no", "BlockIOWeight": "[not set]", "BusName": "org.fedoraproject.FirewallD1", "CPUAccounting": "no", "CPUAffinity": "", "CPUAffinityFromNUMA": "no", "CPUQuotaPerSecUSec": "infinity", "CPUQuotaPeriodUSec": "infinity", "CPUSchedulingPolicy": "0", "CPUSchedulingPriority": "0", "CPUSchedulingResetOnFork": "no", "CPUShares": "[not set]", "CPUUsageNSec": "[not set]", "CPUWeight": "[not set]", "CacheDirectoryMode": "0755", "CanFreeze": "yes", "CanIsolate": "no", "CanReload": "yes", "CanStart": "yes", "CanStop": "yes", "CapabilityBoundingSet": "cap_chown cap_dac_override cap_dac_read_search cap_fowner cap_fsetid cap_kill cap_setgid cap_setuid cap_setpcap cap_linux_immutable cap_net_bind_service cap_net_broadcast cap_net_admin cap_net_raw cap_ipc_lock cap_ipc_owner cap_sys_module cap_sys_rawio cap_sys_chroot cap_sys_ptrace cap_sys_pacct cap_sys_admin cap_sys_boot cap_sys_nice cap_sys_resource cap_sys_time cap_sys_tty_config cap_mknod cap_lease cap_audit_write cap_audit_control cap_setfcap cap_mac_override cap_mac_admin cap_syslog cap_wake_alarm cap_block_suspend cap_audit_read cap_perfmon", "CollectMode": "inactive", "ConditionResult": "yes", "ConditionTimestamp": "Mon 2021-10-25 20:22:59 -05", "ConditionTimestampMonotonic": "4906103", "ConfigurationDirectoryMode": "0755", "Conflicts": "shutdown.target ip6tables.service ipset.service iptables.service nftables.service ebtables.service", "ControlGroup": "/system.slice/firewalld.service", "ControlPID": "0", "DefaultDependencies": "yes", "DefaultMemoryLow": "0", "DefaultMemoryMin": "0", "Delegate": "no", "Description": "firewalld - dynamic firewall daemon", "DevicePolicy": "auto", "Documentation": "man:firewalld(1)", "DynamicUser": "no", "EffectiveCPUs": "", "EffectiveMemoryNodes": "", "EnvironmentFiles": "/etc/sysconfig/firewalld (ignore_errors=yes)", "ExecMainCode": "0", "ExecMainExitTimestampMonotonic": "0", "ExecMainPID": "1058", "ExecMainStartTimestamp": "Mon 2021-10-25 20:22:59 -05", "ExecMainStartTimestampMonotonic": "4907908", "ExecMainStatus": "0", "ExecReload": "{ path=/bin/kill ; argv[]=/bin/kill -HUP $MAINPID ; ignore_errors=no ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "ExecStart": "{ path=/usr/sbin/firewalld ; argv[]=/usr/sbin/firewalld --nofork --nopid $FIREWALLD_ARGS ; ignore_errors=no ; start_time=[n/a] ; stop_time=[n/a] ; pid=0 ; code=(null) ; status=0/0 }", "FailureAction": "none", "FileDescriptorStoreMax": "0", "FragmentPath": "/usr/lib/systemd/system/firewalld.service", "FreezerState": "running", "GID": "[not set]", "GuessMainPID": "yes", "IOAccounting": "no", "IOSchedulingClass": "0", "IOSchedulingPriority": "0", "IOWeight": "[not set]", "IPAccounting": "no", "IPEgressBytes": "18446744073709551615", "IPEgressPackets": "18446744073709551615", "IPIngressBytes": "18446744073709551615", "IPIngressPackets": "18446744073709551615", "Id": "firewalld.service", "IgnoreOnIsolate": "no", "IgnoreSIGPIPE": "yes", "InactiveEnterTimestampMonotonic": "0", "InactiveExitTimestamp": "Mon 2021-10-25 20:22:59 -05", "InactiveExitTimestampMonotonic": "4907945", "InvocationID": "35faf3c33cdb476fac171da6ee82837d", "JobRunningTimeoutUSec": "infinity", "JobTimeoutAction": "none", "JobTimeoutUSec": "infinity", "KeyringMode": "private", "KillMode": "mixed", "KillSignal": "15", "LimitAS": "infinity", "LimitASSoft": "infinity", "LimitCORE": "infinity", "LimitCORESoft": "infinity", "LimitCPU": "infinity", "LimitCPUSoft": "infinity", "LimitDATA": "infinity", "LimitDATASoft": "infinity", "LimitFSIZE": "infinity", "LimitFSIZESoft": "infinity", "LimitLOCKS": "infinity", "LimitLOCKSSoft": "infinity", "LimitMEMLOCK": "65536", "LimitMEMLOCKSoft": "65536", "LimitMSGQUEUE": "819200", "LimitMSGQUEUESoft": "819200", "LimitNICE": "0", "LimitNICESoft": "0", "LimitNOFILE": "262144", "LimitNOFILESoft": "1024", "LimitNPROC": "7114", "LimitNPROCSoft": "7114", "LimitRSS": "infinity", "LimitRSSSoft": "infinity", "LimitRTPRIO": "0", "LimitRTPRIOSoft": "0", "LimitRTTIME": "infinity", "LimitRTTIMESoft": "infinity", "LimitSIGPENDING": "7114", "LimitSIGPENDINGSoft": "7114", "LimitSTACK": "infinity", "LimitSTACKSoft": "8388608", "LoadState": "loaded", "LockPersonality": "no", "LogLevelMax": "-1", "LogRateLimitBurst": "0", "LogRateLimitIntervalUSec": "0", "LogsDirectoryMode": "0755", "MainPID": "1058", "MemoryAccounting": "yes", "MemoryCurrent": "34750464", "MemoryDenyWriteExecute": "no", "MemoryHigh": "infinity", "MemoryLimit": "infinity", "MemoryLow": "0", "MemoryMax": "infinity", "MemoryMin": "0", "MemorySwapMax": "infinity", "MountAPIVFS": "no", "MountFlags": "", "NFileDescriptorStore": "0", "NRestarts": "0", "NUMAMask": "", "NUMAPolicy": "n/a", "Names": "firewalld.service", "NeedDaemonReload": "no", "Nice": "0", "NoNewPrivileges": "no", "NonBlocking": "no", "NotifyAccess": "none", "OOMScoreAdjust": "0", "OnFailureJobMode": "replace", "PermissionsStartOnly": "no", "Perpetual": "no", "PrivateDevices": "no", "PrivateMounts": "no", "PrivateNetwork": "no", "PrivateTmp": "no", "PrivateUsers": "no", "ProtectControlGroups": "no", "ProtectHome": "no", "ProtectKernelModules": "no", "ProtectKernelTunables": "no", "ProtectSystem": "no", "RefuseManualStart": "no", "RefuseManualStop": "no", "RemainAfterExit": "no", "RemoveIPC": "no", "Requires": "system.slice dbus.socket sysinit.target", "Restart": "no", "RestartUSec": "100ms", "RestrictNamespaces": "no", "RestrictRealtime": "no", "RestrictSUIDSGID": "no", "Result": "success", "RootDirectoryStartOnly": "no", "RuntimeDirectoryMode": "0755", "RuntimeDirectoryPreserve": "no", "RuntimeMaxUSec": "infinity", "SameProcessGroup": "no", "SecureBits": "0", "SendSIGHUP": "no", "SendSIGKILL": "yes", "Slice": "system.slice", "StandardError": "null", "StandardInput": "null", "StandardInputData": "", "StandardOutput": "null", "StartLimitAction": "none", "StartLimitBurst": "5", "StartLimitIntervalUSec": "10s", "StartupBlockIOWeight": "[not set]", "StartupCPUShares": "[not set]", "StartupCPUWeight": "[not set]", "StartupIOWeight": "[not set]", "StateChangeTimestamp": "Mon 2021-10-25 20:23:00 -05", "StateChangeTimestampMonotonic": "5325751", "StateDirectoryMode": "0755", "StatusErrno": "0", "StopWhenUnneeded": "no", "SubState": "running", "SuccessAction": "none", "SyslogFacility": "3", "SyslogLevel": "6", "SyslogLevelPrefix": "yes", "SyslogPriority": "30", "SystemCallErrorNumber": "0", "TTYReset": "no", "TTYVHangup": "no", "TTYVTDisallocate": "no", "TasksAccounting": "yes", "TasksCurrent": "2", "TasksMax": "11383", "TimeoutStartUSec": "1min 30s", "TimeoutStopUSec": "1min 30s", "TimerSlackNSec": "50000", "Transient": "no", "Type": "dbus", "UID": "[not set]", "UMask": "0022", "UnitFilePreset": "enabled", "UnitFileState": "enabled", "UtmpMode": "init", "WantedBy": "multi-user.target", "Wants": "network-pre.target", "WatchdogTimestamp": "Mon 2021-10-25 20:23:00 -05", "WatchdogTimestampMonotonic": "5325749", "WatchdogUSec": "0"}}

TASK [Open port 80/tcp on firewalld] ****************************************************************************************************************
changed: [node91.opennova.pe] => {"changed": true, "msg": "Permanent and Non-Permanent(immediate) operation, Changed service http to enabled"}

PLAY [Test httpd access from workstation] ***********************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [control_node]

TASK [Connect to prod webserver] ********************************************************************************************************************
ok: [control_node] => {"accept_ranges": "bytes", "changed": false, "connection": "close", "content": "My first webserver deployed with ansible 2.9", "content_length": "44", "content_type": "text/html; charset=UTF-8", "cookies": {}, "cookies_string": "", "date": "Mon, 01 Nov 2021 19:41:14 GMT", "elapsed": 0, "etag": "\"2c-5cfbf5be32cfa\"", "last_modified": "Mon, 01 Nov 2021 19:41:10 GMT", "msg": "OK (44 bytes)", "redirected": false, "server": "Apache/2.4.37 (Red Hat Enterprise Linux)", "status": 200, "url": "http://node91.opennova.pe/index.html"}

PLAY RECAP ******************************************************************************************************************************************
control_node               : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node91.opennova.pe         : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

2. Crear un playbook para desinstalar HTTPD Server, revisar las directivas y discutirlas.

<br> Crear el playbook de nombre **uninstall_webserver.yaml** dentro del directorio de trabajo /home/ansible/ansible que contenga la siguiente informacion:
```
---
- name: "Uninstall HTTPD Server Playbook"
  hosts: prod
  tasks:
    - name: "Remove index.html from HTTPD Server"
      file:
        path: /var/www/html/index.html
        state: absent
    - name: "Uninstall httpd package on prod servers"
      yum:
        name: httpd
        state: absent
    - name: "Close port 80/tcp on firewalld"
      firewalld:
        service: http
        permanent: yes
        immediate: yes
        state: disabled
```

<br> Ejecutarlo y validar que el webserver desplegado en prod no esta habilitado.
```
[ansible@server09 ansible]$ ansible-playbook uninstall_webserver.yaml

PLAY [Uninstall HTTPD Server Playbook] **************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [node91.opennova.pe]

TASK [Remove index.html from HTTPD Server] **********************************************************************************************************
changed: [node91.opennova.pe]

TASK [Uninstall httpd package on prod servers] ******************************************************************************************************
changed: [node91.opennova.pe]

TASK [Close port 80/tcp on firewalld] ***************************************************************************************************************
changed: [node91.opennova.pe]

PLAY RECAP ******************************************************************************************************************************************
node91.opennova.pe         : ok=4    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

Al ejecutar el comando curl no nos debe dar respuesta
```
[ansible@server09 ansible]$ curl -si http://node91.opennova.pe
```

3. Crear un playbook para instalación de HTTPD Server que utilice variables dentro del playbook, revisar las directivas y discutirlas.

<br> Crear el playbook de nombre **install_webserver_vars.yaml** dentro del directorio de trabajo /home/ansible/ansible que contenga la siguiente informacion:
```
---
- name: Install HTTPD Server Playbook
  hosts: prod
  vars:
    web_pkg: httpd
    web_svc: httpd
    web_fw_svc: http
    fw_pkg: firewalld
    fw_svc: firewalld
    py_pkg: python3-PyMySQL

  tasks:
    - name: "Install httpd package on prod servers"
      yum:
        name:
          - "{{ web_pkg }}"
          - "{{ py_pkg }}"
        state: present

    - name: "Install firewalld package on prod servers"
      yum:
        name: "{{ fw_pkg }}"
        state: present

    - name: "Create a custom index.html"
      copy:
        dest: "/var/www/html/index.html"
        content: "My first webserver deployed with ansible 2.9"

    - name: "Startup httpd service on prod servers"
      service:
        name: "{{ web_svc }}"
        state: started
        enabled: yes

    - name: "Startup firewalld service on prod servers"
      service:
        name: "{{ fw_svc }}"
        state: started
        enabled: yes

    - name: "Open port 80/tcp on firewalld"
      firewalld:
        service: "{{ web_fw_svc}}"
        permanent: yes
        immediate: yes
        state: enabled

- name: "Test httpd access from workstation"
  hosts: control_node
  become: no
  tasks:
    - name: "Connect to prod webserver"
      uri:
        url: http://node91.opennova.pe/index.html
        return_content: yes
        status_code: 200
```
Revisar si no existe algún error de sintaxis con el siguiente comando:
```
[ansible@server09 ansible]$ ansible-playbook --syntax-check install_webserver_vars.yaml

playbook: install_webserver_vars.yaml
```

Ejecutar una prueba de corrida del playbook install_webserver_vars.yaml
```
[ansible@server09 ansible]$ ansible-playbook --check install_webserver_vars.yaml

PLAY [Install HTTPD Server Playbook] ****************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [node91.opennova.pe]

TASK [Install httpd package on prod servers] ********************************************************************************************************
changed: [node91.opennova.pe]

TASK [Install firewalld package on prod servers] ****************************************************************************************************
ok: [node91.opennova.pe]

TASK [Create a custom index.html] *******************************************************************************************************************
changed: [node91.opennova.pe]

TASK [Startup httpd service on prod servers] ********************************************************************************************************
changed: [node91.opennova.pe]

TASK [Startup firewalld service on prod servers] ****************************************************************************************************
ok: [node91.opennova.pe]

TASK [Open port 80/tcp on firewalld] ****************************************************************************************************************
changed: [node91.opennova.pe]

PLAY [Test httpd access from workstation] ***********************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [control_node]

TASK [Connect to prod webserver] ********************************************************************************************************************
skipping: [control_node]

PLAY RECAP ******************************************************************************************************************************************
control_node               : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
node91.opennova.pe         : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

Ejecutar el playbook con el comando **ansible-playbook install_webserver_vars.yaml**
```
[ansible@server09 ansible]$ ansible-playbook install_webserver_vars.yaml

PLAY [Install HTTPD Server Playbook] ****************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [node91.opennova.pe]

TASK [Install httpd package on prod servers] ********************************************************************************************************
changed: [node91.opennova.pe]

TASK [Install firewalld package on prod servers] ****************************************************************************************************
ok: [node91.opennova.pe]

TASK [Create a custom index.html] *******************************************************************************************************************
changed: [node91.opennova.pe]

TASK [Startup httpd service on prod servers] ********************************************************************************************************
changed: [node91.opennova.pe]

TASK [Startup firewalld service on prod servers] ****************************************************************************************************
ok: [node91.opennova.pe]

TASK [Open port 80/tcp on firewalld] ****************************************************************************************************************
changed: [node91.opennova.pe]

PLAY [Test httpd access from workstation] ***********************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [control_node]

TASK [Connect to prod webserver] ********************************************************************************************************************
ok: [control_node]

PLAY RECAP ******************************************************************************************************************************************
control_node               : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node91.opennova.pe         : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

Validar con el comando curl que tengamos acceso al servidor web desplegado sobre produccion
```
[ansible@server09 ansible]$ curl -si http://node91.opennova.pe
HTTP/1.1 200 OK
Date: Mon, 01 Nov 2021 20:31:48 GMT
Server: Apache/2.4.37 (Red Hat Enterprise Linux)
Last-Modified: Mon, 01 Nov 2021 20:28:52 GMT
ETag: "2c-5cfc00672a52b"
Accept-Ranges: bytes
Content-Length: 44
Content-Type: text/html; charset=UTF-8

My first webserver deployed with ansible 2.9
```

4. Crear un playbook para instalación de HTTPD Server que utilice variables de archivos dentro del playbook, revisar las directivas y discutirlas.

<br> Crear el playbook de nombre **install_webserver_vars_file.yaml** dentro del directorio de trabajo /home/ansible/ansible que contenga la siguiente información: 
```
---
- name: Install HTTPD Server Playbook
  hosts: prod
  vars_files:
    - vars/webvars.yml
  tasks:
    - name: "Install httpd package on prod servers"
      yum:
        name:
          - "{{ web_pkg }}"
          - "{{ py_pkg }}"
        state: present

    - name: "Install firewalld package on prod servers"
      yum:
        name: "{{ fw_pkg }}"
        state: present

    - name: "Create a custom index.html"
      copy:
        dest: "/var/www/html/index.html"
        content: "My first webserver deployed with ansible 2.9"

    - name: "Startup httpd service on prod servers"
      service:
        name: "{{ web_svc }}"
        state: started
        enabled: yes

    - name: "Startup firewalld service on prod servers"
      service:
        name: "{{ fw_svc }}"
        state: started
        enabled: yes

    - name: "Open port 80/tcp on firewalld"
      firewalld:
        service: "{{ web_fw_svc}}"
        permanent: yes
        immediate: yes
        state: enabled

- name: "Test httpd access from workstation"
  hosts: control_node
  become: no
  tasks:
    - name: "Connect to prod webserver"
      uri:
        url: http://node91.opennova.pe/index.html
        return_content: yes
        status_code: 200
```

Crear el directorio vars con el archivos webvars.yml dentro del directorio de trabajo * /home/ansible/ansible/vars/webvars.yml
```
[ansible@server09 ansible]$ mkdir -p /home/ansible/ansible/vars/
```
Dentro de este directorio crear el archivo **webvars.yml** que contenga la siguiente informacion:
```
---
web_pkg: httpd
web_svc: httpd
web_fw_svc: http
fw_pkg: firewalld
fw_svc: firewalld
py_pkg: python3-PyMySQL
```

Revisar si no existe algún error de sintaxis con el siguiente comando:
```
[ansible@server09 ansible]$ ansible-playbook --syntax-check install_webserver_vars_file.yml

playbook: install_webserver_vars_file.yml
```

Ejecutar una prueba de corrida del playbook install_webserver_vars_file.yaml
```
[ansible@server09 ansible]$ ansible-playbook install_webserver_vars_file.yml

PLAY [Install HTTPD Server Playbook] ****************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [node91.opennova.pe]

TASK [Install httpd package on prod servers] ********************************************************************************************************
changed: [node91.opennova.pe]

TASK [Install firewalld package on prod servers] ****************************************************************************************************
ok: [node91.opennova.pe]

TASK [Create a custom index.html] *******************************************************************************************************************
changed: [node91.opennova.pe]

TASK [Startup httpd service on prod servers] ********************************************************************************************************
changed: [node91.opennova.pe]

TASK [Startup firewalld service on prod servers] ****************************************************************************************************
ok: [node91.opennova.pe]

TASK [Open port 80/tcp on firewalld] ****************************************************************************************************************
changed: [node91.opennova.pe]

PLAY [Test httpd access from workstation] ***********************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [control_node]

TASK [Connect to prod webserver] ********************************************************************************************************************
ok: [control_node]

PLAY RECAP ******************************************************************************************************************************************
control_node               : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node91.opennova.pe         : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

Validar con el comando curl que tengamos acceso al servidor web desplegado sobre produccion
```
[ansible@server09 ansible]$ curl -si http://node91.opennova.pe
HTTP/1.1 200 OK
Date: Mon, 01 Nov 2021 20:31:48 GMT
Server: Apache/2.4.37 (Red Hat Enterprise Linux)
Last-Modified: Mon, 01 Nov 2021 20:28:52 GMT
ETag: "2c-5cfc00672a52b"
Accept-Ranges: bytes
Content-Length: 44
Content-Type: text/html; charset=UTF-8

My first webserver deployed with ansible 2.9
```

5. Crear un playbook para instalación de VSFTPD Server  revisar las directivas y discutirlas.

<br> Crear el playbook de nombre **install_ftpserver.yaml** dentro del directorio de trabajo /home/ansible/ansible/ftp que contenga la siguiente información:

```
[ansible@server09 ansible]$ mkdir /home/ansible/ansible/ftp
[ansible@server09 ansible]$ cd /home/ansible/ansible/ftp/
```

Crear el archivo con install_ftpserver.yaml dentro de /home/ansible/ansible/ftp/ con la siguiente información:
```
---
- name: "Deploy FTP Server"
  hosts: dev,qa
  become: true
  become_method: sudo
  become_user: root
  vars:
    ftp_pkg: vsftpd
    ftp_svc: vsftpd
    fw_pkg: firewalld
    fw_svc: firewalld
    fw_svc_name: ftp
  tasks:
    - name: "Install FTP server"
      yum:
        name: "{{ ftp_pkg }}"
        state: present

    - name: "Startup and Enable FTP server"
      service:
        name: "{{ ftp_svc }}"
        state: started
        enabled: yes

    - name: "Install firewalld package on prod servers"
      yum:
        name: "{{ fw_pkg }}"
        state: present

    - name: "Startup firewalld service on prod servers"
      service:
        name: "{{ fw_svc }}"
        state: started
        enabled: yes

    - name: "Open ftp service port 21/tcp on firewalld"
      firewalld:
        service: "{{ fw_svc_name }}"
        permanent: yes
        immediate: yes
        state: enabled

    - name: "Configure anonymous access for vsftpd"
      replace:
        path: /etc/vsftpd/vsftpd.conf
        regexp: '^anonymous_enable=NO'
        replace: 'anonymous_enable=YES'
      notify: restart vsftpd

  handlers:
    - name: restart vsftpd
      service:
        name: vsftpd
        state: restarted
```

Ejecutar el playbook install_ftpserver.yaml

```[ansible@server09 ftp]$ ansible-playbook -i ~/ansible/inventory install_ftpserver.yaml

PLAY [Deploy FTP Server] ****************************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [node93.opennova.pe]
ok: [node92.opennova.pe]

TASK [Install FTP server] ***************************************************************************************************************************
changed: [node92.opennova.pe]
changed: [node93.opennova.pe]

TASK [Startup and Enable FTP server] ****************************************************************************************************************
changed: [node93.opennova.pe]
changed: [node92.opennova.pe]

TASK [Install firewalld package on prod servers] ****************************************************************************************************
ok: [node92.opennova.pe]
ok: [node93.opennova.pe]

TASK [Startup firewalld service on prod servers] ****************************************************************************************************
ok: [node93.opennova.pe]
ok: [node92.opennova.pe]

TASK [Open ftp service port 21/tcp on firewalld] ****************************************************************************************************
changed: [node93.opennova.pe]
changed: [node92.opennova.pe]

TASK [Configure anonymous access for vsftpd] ********************************************************************************************************
changed: [node92.opennova.pe]
changed: [node93.opennova.pe]

RUNNING HANDLER [restart vsftpd] ********************************************************************************************************************
changed: [node92.opennova.pe]
changed: [node93.opennova.pe]

PLAY RECAP ******************************************************************************************************************************************
node92.opennova.pe         : ok=8    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node93.opennova.pe         : ok=8    changed=5    unreachable=0    failed=0    skipped=0    rescued=0    ignored=
```

En el nodo de control instalar el cliente ftp para probar la conexión ftp hacia los nodos de los ambientes dev y qa.
```
[ansible@server09 ftp]$ sudo yum install -y ftp
Updating Subscription Management repositories.
Red Hat Ansible Engine 2.9 for RHEL 8 x86_64 (RPMs)                                                                   34 kB/s | 2.4 kB     00:00
Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)                                                                 29 kB/s | 2.4 kB     00:00
Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)                                                              38 kB/s | 2.8 kB     00:00
Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 (RPMs)                                                                  20 kB/s | 2.1 kB     00:00
Dependencies resolved.
=====================================================================================================================================================
 Package                  Architecture                Version                            Repository                                             Size
=====================================================================================================================================================
Installing:
 ftp                      x86_64                      0.17-78.el8                        rhel-8-for-x86_64-appstream-rpms                       70 k

Transaction Summary
=====================================================================================================================================================
Install  1 Package

Total download size: 70 k
Installed size: 112 k
Downloading Packages:
ftp-0.17-78.el8.x86_64.rpm                                                                                            60 kB/s |  70 kB     00:01
-----------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                 60 kB/s |  70 kB     00:01
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                             1/1
  Installing       : ftp-0.17-78.el8.x86_64                                                                                                      1/1
  Running scriptlet: ftp-0.17-78.el8.x86_64                                                                                                      1/1
  Verifying        : ftp-0.17-78.el8.x86_64                                                                                                      1/1
Installed products updated.
Uploading Tracer Profile

Installed:
  ftp-0.17-78.el8.x86_64

Complete!
```

Probar conexión a los nodos de los ambientes de dev y qa.
```
[ansible@server09 ftp]$ ftp node92.opennova.pe
Connected to node92.opennova.pe (192.168.10.92).
220 (vsFTPd 3.0.3)
Name (node92.opennova.pe:ansible): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> quit
```
```
[ansible@server09 ftp]$ ftp node93.opennova.pe
Connected to node93.opennova.pe (192.168.10.93).
220 (vsFTPd 3.0.3)
Name (node93.opennova.pe:ansible): anonymous
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> quit
221 Goodbye.
```

6. Crear un playbook para desinstalar VSFTPD Server, revisar las directivas y discutirlas.

<br> Crear el playbook de nombre **uninstall_ftpserver.yaml** dentro del directorio de trabajo /home/ansible/ansible/ftp que contenga la siguiente información:
```
---
- name: "Uninstall VSFTPD Server Playbook"
  hosts: dev,qa
  become: true
  become_method: sudo
  become_user: root
  tasks:
    - name: "Uninstall vsftpd package on prod servers"
      yum:
        name: vsftpd
        state: absent
    - name: "Close port 21/tcp on firewalld"
      firewalld:
        service: ftp
        permanent: yes
        immediate: yes
        state: disabled
```

Para desinstalar el servicio vsftpd ejecutar el siguiente comando:
```
[ansible@server09 ftp]$ pwd
/home/ansible/ansible/ftp

[ansible@server09 ftp]$ ansible-playbook -i ~/ansible/inventory uninstall_ftpserver.yaml

PLAY [Uninstall VSFTPD Server Playbook] **************************************************************************************************************

TASK [Gathering Facts] *******************************************************************************************************************************
ok: [node93.opennova.pe]
ok: [node92.opennova.pe]

TASK [Uninstall vsftpd package on prod servers] ******************************************************************************************************
changed: [node92.opennova.pe]
changed: [node93.opennova.pe]

TASK [Close port 21/tcp on firewalld] ****************************************************************************************************************
changed: [node92.opennova.pe]
changed: [node93.opennova.pe]

PLAY RECAP *******************************************************************************************************************************************
node92.opennova.pe         : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
node93.opennova.pe         : ok=3    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

Validar que no se pueda conectar al servicio ftp en los nodos de los grupos de dev y qa.
```
[ansible@server09 ftp]$ ftp node93.opennova.pe
ftp: connect: No route to host
ftp> quit
[ansible@server09 ftp]$ ftp node92.opennova.pe
ftp: connect: No route to host
ftp>
```

7. Crear un rol llamado apache y configurarlo con los siguientes archivos:
<br> Crear el directorio roles dentro del espacio de trabajo /home/ansible/ansible
```
[ansible@server09 ansible]$ pwd
/home/ansible/ansible
[ansible@server09 ansible]$ mkdir roles
[ansible@server09 ansible]$ cd roles/
```

Agregar la directiva roles_path dentro del archivo ansible.cfg del espacio de trabajo
```
[ansible@server09 ansible]$ pwd
/home/ansible/ansible
[ansible@server09 ansible]$ cat ansible.cfg
[defaults]
inventory = ./inventory
remote_user = ansible
ask_pass = False
roles_path = ./roles:/usr/share/ansible/roles:/etc/ansible/roles

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = False
```

Crear un rol de nombre apache dentro del espacio de trabajo /home/ansible/ansible/roles

```
[ansible@server09 ansible]$ cd roles/

[ansible@server09 roles]$ ansible-galaxy init apache
- Role apache was created successfully

[ansible@server09 roles]$ tree apache/
apache/
├── defaults
│   └── main.yml
├── files
├── handlers
│   └── main.yml
├── meta
│   └── main.yml
├── README.md
├── tasks
│   └── main.yml
├── templates
├── tests
│   ├── inventory
│   └── test.yml
└── vars
    └── main.yml
```

Dentro del directorio tasks agregar la siguiente información dentro del archivo main.yml:
```
- name: "Install httpd package on prod servers"
  yum:
    name: "{{ web_pkg }}"
    state: present

- name: "Install firewalld package on prod servers"
  yum:
    name: "{{ fw_pkg }}"
    state: present

- name: "Create a custom index.html from jinja2 template"
  template:
    src: index.j2
    dest: /var/www/html/index.html
    owner: apache
    group: apache
    mode: '0644'

- name: "Startup httpd service on prod servers"
  service:
    name: "{{ web_svc }}"
    state: started
    enabled: yes

- name: "Startup firewalld service on prod servers"
  service:
    name: "{{ fw_svc }}"
    state: started
    enabled: yes

- name: "Open port 80/tcp on firewalld"
  firewalld:
   service: "{{ fw_svc_name }}"
   permanent: yes
   immediate: yes
   state: enabled
```

Dentro del directorio templates agregar la siguiente informacion dentro del archivo index.j2:
```
Testing webserver on {{ ansible_facts.fqdn }} with ip address {{ ansible_facts.default_ipv4.address }}
```

Dentro del direcotio vars agregar la siguiente informacion dentro del archivo main.yml
```
web_pkg: httpd
web_svc: httpd
fw_pkg: firewalld
fw_svc: firewalld
fw_svc_name: http
```

Crear un playbook de nombre main_role_apache.yaml dentro del espacio de trabajo /home/ansible/ansible con la siguiente informacion:
```
---
- name: Install Apache from roles
  hosts: webservers
  roles:
    - role: apache
```

Ejecutar el playbook main_role_apache.yaml desde el espacio de trabajo /home/ansible/ansible
```
[ansible@server09 ansible]$ ansible-playbook main_role_apache.yaml

PLAY [Install Apache from roles] ********************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [node94.opennova.pe]

TASK [apache : Install httpd package on prod servers] ***********************************************************************************************
changed: [node94.opennova.pe]

TASK [apache : Install firewalld package on prod servers] *******************************************************************************************
ok: [node94.opennova.pe]

TASK [apache : Create a custom index.html from jinja2 template] *************************************************************************************
changed: [node94.opennova.pe]

TASK [apache : Startup httpd service on prod servers] ***********************************************************************************************
changed: [node94.opennova.pe]

TASK [apache : Startup firewalld service on prod servers] *******************************************************************************************
ok: [node94.opennova.pe]

TASK [apache : Open port 80/tcp on firewalld] *******************************************************************************************************
changed: [node94.opennova.pe]

PLAY RECAP ******************************************************************************************************************************************
node94.opennova.pe         : ok=7    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

Validar que el servicio web este accesible en el nodoX4 correspondiente y contenta el mensaje indicado en el template index.j2
```
[ansible@server09 ansible]$ curl -si http://node94.opennova.pe
HTTP/1.1 200 OK
Date: Tue, 02 Nov 2021 00:04:28 GMT
Server: Apache/2.4.37 (Red Hat Enterprise Linux)
Last-Modified: Tue, 02 Nov 2021 00:03:02 GMT
ETag: "5e-5cfc30462a921"
Accept-Ranges: bytes
Content-Length: 94
Content-Type: text/html; charset=UTF-8

Testing webserver on node94.opennova.pe.10.168.192.in-addr.arpa with ip address 192.168.10.94
```

8. Instalar roles del paquete rhel-system-roles los cuales habilitara algunos roles:
```
[ansible@server09 ansible]$ sudo yum install rhel-system-roles
Updating Subscription Management repositories.
Red Hat Ansible Engine 2.9 for RHEL 8 x86_64 (RPMs)                                                                   25 kB/s | 2.4 kB     00:00
Red Hat Enterprise Linux 8 for x86_64 - BaseOS (RPMs)                                                                 27 kB/s | 2.4 kB     00:00
Red Hat Enterprise Linux 8 for x86_64 - AppStream (RPMs)                                                              28 kB/s | 2.8 kB     00:00
Red Hat Satellite Tools 6.9 for RHEL 8 x86_64 (RPMs)                                                                  24 kB/s | 2.1 kB     00:00
Dependencies resolved.
=====================================================================================================================================================
 Package                             Architecture             Version                       Repository                                          Size
=====================================================================================================================================================
Installing:
 rhel-system-roles                   noarch                   1.0.1-1.el8                   rhel-8-for-x86_64-appstream-rpms                   1.1 M

Transaction Summary
=====================================================================================================================================================
Install  1 Package

Total download size: 1.1 M
Installed size: 7.0 M
Is this ok [y/N]: y
Downloading Packages:
rhel-system-roles-1.0.1-1.el8.noarch.rpm                                                                             836 kB/s | 1.1 MB     00:01
-----------------------------------------------------------------------------------------------------------------------------------------------------
Total                                                                                                                835 kB/s | 1.1 MB     00:01
Running transaction check
Transaction check succeeded.
Running transaction test
Transaction test succeeded.
Running transaction
  Preparing        :                                                                                                                             1/1
  Installing       : rhel-system-roles-1.0.1-1.el8.noarch                                                                                        1/1
  Verifying        : rhel-system-roles-1.0.1-1.el8.noarch                                                                                        1/1
Installed products updated.
Uploading Tracer Profile

Installed:
  rhel-system-roles-1.0.1-1.el8.noarch

Complete!
```
Validar que tengamos los roles accesibles
```
[ansible@server09 ansible]$ ansible-galaxy list
# /home/ansible/ansible/roles
- apache, (unknown version)
# /usr/share/ansible/roles
- linux-system-roles.certificate, (unknown version)
- linux-system-roles.crypto_policies, (unknown version)
- linux-system-roles.ha_cluster, (unknown version)
- linux-system-roles.kdump, (unknown version)
- linux-system-roles.kernel_settings, (unknown version)
- linux-system-roles.logging, (unknown version)
- linux-system-roles.metrics, (unknown version)
- linux-system-roles.nbde_client, (unknown version)
- linux-system-roles.nbde_server, (unknown version)
- linux-system-roles.network, (unknown version)
- linux-system-roles.postfix, (unknown version)
- linux-system-roles.selinux, (unknown version)
- linux-system-roles.ssh, (unknown version)
- linux-system-roles.sshd, (unknown version)
- linux-system-roles.storage, (unknown version)
- linux-system-roles.timesync, (unknown version)
- linux-system-roles.tlog, (unknown version)
- rhel-system-roles.certificate, (unknown version)
- rhel-system-roles.crypto_policies, (unknown version)
- rhel-system-roles.ha_cluster, (unknown version)
- rhel-system-roles.kdump, (unknown version)
- rhel-system-roles.kernel_settings, (unknown version)
- rhel-system-roles.logging, (unknown version)
- rhel-system-roles.metrics, (unknown version)
- rhel-system-roles.nbde_client, (unknown version)
- rhel-system-roles.nbde_server, (unknown version)
- rhel-system-roles.network, (unknown version)
- rhel-system-roles.postfix, (unknown version)
- rhel-system-roles.selinux, (unknown version)
- rhel-system-roles.ssh, (unknown version)
- rhel-system-roles.sshd, (unknown version)
- rhel-system-roles.storage, (unknown version)
- rhel-system-roles.timesync, (unknown version)
- rhel-system-roles.tlog, (unknown version)
# /etc/ansible/roles
```

Crear un playbook de nombre timesync.yaml que este en el espacio de trabajo /home/ansible/ansible/ que contenga la siguiente informacion:
```
---
- name: Use a RHEL system role
  hosts: servers
  vars:
    timesync_ntp_servers:
      - hostname: idm.opennova.pe
        iburst: yes
    timesync_ntp_provider: chrony
    timezone: UTC
  roles:
    - rhel-system-roles.timesync
  tasks:
    - name: "TIMEZONE CONFIGURATION"
      timezone:
        name: "{{ timezone }}"
      notify: restart crond
  handlers:
    - name: restart crond
      service:
        name: crond
        state: restarted
```

Ejecutar el playbook timesync.yaml y analizar la salida
```
[ansible@server09 ansible]$ ansible-playbook timesync.yaml

PLAY [Use a RHEL system role] ***********************************************************************************************************************

TASK [Gathering Facts] ******************************************************************************************************************************
ok: [node94.opennova.pe]
ok: [node93.opennova.pe]
ok: [node92.opennova.pe]
ok: [node91.opennova.pe]

TASK [rhel-system-roles.timesync : Check if only NTP is needed] *************************************************************************************
ok: [node91.opennova.pe]
ok: [node92.opennova.pe]
ok: [node93.opennova.pe]
ok: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Check if single PTP is needed] ***********************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Check if both NTP and PTP are needed] ****************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Determine current NTP provider] **********************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Select NTP provider] *********************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Install chrony] **************************************************************************************************
changed: [node91.opennova.pe]
changed: [node94.opennova.pe]
changed: [node93.opennova.pe]
changed: [node92.opennova.pe]

TASK [rhel-system-roles.timesync : Install ntp] *****************************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Install linuxptp] ************************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Run phc_ctl on PTP interface] ************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Check if PTP interface supports HW timestamping] *****************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Get chrony version] **********************************************************************************************
ok: [node91.opennova.pe]
ok: [node93.opennova.pe]
ok: [node94.opennova.pe]
ok: [node92.opennova.pe]

TASK [rhel-system-roles.timesync : Get ntp version] *************************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Generate chrony.conf file] ***************************************************************************************
changed: [node91.opennova.pe]
changed: [node93.opennova.pe]
changed: [node94.opennova.pe]
changed: [node92.opennova.pe]

TASK [rhel-system-roles.timesync : Generate chronyd sysconfig file] *********************************************************************************
changed: [node91.opennova.pe]
changed: [node94.opennova.pe]
changed: [node92.opennova.pe]
changed: [node93.opennova.pe]

TASK [rhel-system-roles.timesync : Generate ntp.conf file] ******************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Generate ntpd sysconfig file] ************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Generate ptp4l.conf file] ****************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Generate ptp4l sysconfig file] ***********************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Generate phc2sys sysconfig file] *********************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Generate timemaster.conf file] ***********************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Update network sysconfig file] ***********************************************************************************
changed: [node91.opennova.pe]
changed: [node92.opennova.pe]
changed: [node94.opennova.pe]
changed: [node93.opennova.pe]

TASK [rhel-system-roles.timesync : Disable chronyd] *************************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Disable ntpd] ****************************************************************************************************
fatal: [node93.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ntpd: host"}
...ignoring
fatal: [node94.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ntpd: host"}
...ignoring
fatal: [node91.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ntpd: host"}
...ignoring
fatal: [node92.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ntpd: host"}
...ignoring

TASK [rhel-system-roles.timesync : Disable ntpdate] *************************************************************************************************
fatal: [node94.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ntpdate: host"}
...ignoring
fatal: [node92.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ntpdate: host"}
...ignoring
fatal: [node93.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ntpdate: host"}
...ignoring
fatal: [node91.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ntpdate: host"}
...ignoring

TASK [rhel-system-roles.timesync : Disable sntp] ****************************************************************************************************
fatal: [node91.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service sntp: host"}
...ignoring
fatal: [node92.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service sntp: host"}
...ignoring
fatal: [node93.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service sntp: host"}
...ignoring
fatal: [node94.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service sntp: host"}
...ignoring

TASK [rhel-system-roles.timesync : Disable ptp4l] ***************************************************************************************************
fatal: [node91.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ptp4l: host"}
...ignoring
fatal: [node93.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ptp4l: host"}
...ignoring
fatal: [node94.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ptp4l: host"}
...ignoring
fatal: [node92.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service ptp4l: host"}
...ignoring

TASK [rhel-system-roles.timesync : Disable phc2sys] *************************************************************************************************
fatal: [node91.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service phc2sys: host"}
...ignoring
fatal: [node94.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service phc2sys: host"}
...ignoring
fatal: [node93.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service phc2sys: host"}
...ignoring
fatal: [node92.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service phc2sys: host"}
...ignoring

TASK [rhel-system-roles.timesync : Disable timemaster] **********************************************************************************************
fatal: [node91.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service timemaster: host"}
...ignoring
fatal: [node93.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service timemaster: host"}
...ignoring
fatal: [node94.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service timemaster: host"}
...ignoring
fatal: [node92.opennova.pe]: FAILED! => {"changed": false, "msg": "Could not find the requested service timemaster: host"}
...ignoring

TASK [rhel-system-roles.timesync : Enable chronyd] **************************************************************************************************
changed: [node91.opennova.pe]
changed: [node93.opennova.pe]
changed: [node94.opennova.pe]
changed: [node92.opennova.pe]

TASK [rhel-system-roles.timesync : Enable ntpd] *****************************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Enable ptp4l] ****************************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Enable phc2sys] **************************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [rhel-system-roles.timesync : Enable timemaster] ***********************************************************************************************
skipping: [node91.opennova.pe]
skipping: [node92.opennova.pe]
skipping: [node93.opennova.pe]
skipping: [node94.opennova.pe]

TASK [TIMEZONE CONFIGURATION] ***********************************************************************************************************************
ok: [node91.opennova.pe]
changed: [node94.opennova.pe]
changed: [node92.opennova.pe]
changed: [node93.opennova.pe]

RUNNING HANDLER [rhel-system-roles.timesync : restart chronyd] **************************************************************************************
changed: [node93.opennova.pe]
changed: [node94.opennova.pe]
changed: [node92.opennova.pe]

RUNNING HANDLER [restart crond] *********************************************************************************************************************
changed: [node94.opennova.pe]
changed: [node92.opennova.pe]
changed: [node93.opennova.pe]

PLAY RECAP ******************************************************************************************************************************************
node91.opennova.pe         : ok=17   changed=8    unreachable=0    failed=0    skipped=20   rescued=0    ignored=6
node92.opennova.pe         : ok=17   changed=8    unreachable=0    failed=0    skipped=20   rescued=0    ignored=6
node93.opennova.pe         : ok=17   changed=8    unreachable=0    failed=0    skipped=20   rescued=0    ignored=6
node94.opennova.pe         : ok=17   changed=8    unreachable=0    failed=0    skipped=20   rescued=0    ignored=6
```

En cualquiera siguiente comando adhoc para validar la sincronizacion.
```
[ansible@server09 ansible]$ ansible servers -m shell -a "chronyc sources -v"
node94.opennova.pe | CHANGED | rc=0 >>
210 Number of sources = 1

  .-- Source mode  '^' = server, '=' = peer, '#' = local clock.
 / .- Source state '*' = current synced, '+' = combined , '-' = not combined,
| /   '?' = unreachable, 'x' = time may be in error, '~' = time too variable.
||                                                 .- xxxx [ yyyy ] +/- zzzz
||      Reachability register (octal) -.           |  xxxx = adjusted offset,
||      Log2(Polling interval) --.      |          |  yyyy = measured offset,
||                                \     |          |  zzzz = estimated error.
||                                 |    |           \
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
^? idm.opennova.pe               0   8     0     -     +0ns[   +0ns] +/-    0ns
node92.opennova.pe | CHANGED | rc=0 >>
210 Number of sources = 1

  .-- Source mode  '^' = server, '=' = peer, '#' = local clock.
 / .- Source state '*' = current synced, '+' = combined , '-' = not combined,
| /   '?' = unreachable, 'x' = time may be in error, '~' = time too variable.
||                                                 .- xxxx [ yyyy ] +/- zzzz
||      Reachability register (octal) -.           |  xxxx = adjusted offset,
||      Log2(Polling interval) --.      |          |  yyyy = measured offset,
||                                \     |          |  zzzz = estimated error.
||                                 |    |           \
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
^? idm.opennova.pe               0   8     0     -     +0ns[   +0ns] +/-    0ns
node91.opennova.pe | CHANGED | rc=0 >>
210 Number of sources = 1

  .-- Source mode  '^' = server, '=' = peer, '#' = local clock.
 / .- Source state '*' = current synced, '+' = combined , '-' = not combined,
| /   '?' = unreachable, 'x' = time may be in error, '~' = time too variable.
||                                                 .- xxxx [ yyyy ] +/- zzzz
||      Reachability register (octal) -.           |  xxxx = adjusted offset,
||      Log2(Polling interval) --.      |          |  yyyy = measured offset,
||                                \     |          |  zzzz = estimated error.
||                                 |    |           \
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
^? idm.opennova.pe               0   8     0     -     +0ns[   +0ns] +/-    0ns
node93.opennova.pe | CHANGED | rc=0 >>
210 Number of sources = 1

  .-- Source mode  '^' = server, '=' = peer, '#' = local clock.
 / .- Source state '*' = current synced, '+' = combined , '-' = not combined,
| /   '?' = unreachable, 'x' = time may be in error, '~' = time too variable.
||                                                 .- xxxx [ yyyy ] +/- zzzz
||      Reachability register (octal) -.           |  xxxx = adjusted offset,
||      Log2(Polling interval) --.      |          |  yyyy = measured offset,
||                                \     |          |  zzzz = estimated error.
||                                 |    |           \
MS Name/IP address         Stratum Poll Reach LastRx Last sample
===============================================================================
^? idm.opennova.pe               0   8     0     -     +0ns[   +0ns] +/-    0ns
```

# Laboratorio: Trabajando con Ansible Playbooks y Roles

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
1. Dentro del espacio de trabajo **/home/ansible/ansible** crear los siguientes playbooks.
* Crear un playbook de nombre **install_webserver.yaml** que contenga la informacion del **punto 1**, modificar el parametro hosts y ejecutarlo en **webservers**
* Crear un playbook de nombre **uninstall_webserver.yaml** que contenga la informacion del **punto 2**, modificar el parametro hosts  y ejecutarlo en **dev**
* Crear un playbook de nombre **install_webserver_vars.yaml** que contenga la informacion del **punto 3**, modificar el paremtro hosts y ejecutarlo en **nodeX3.opennova.pe**, donde **X** es el numero de su usuario del **1 al 6**.
* Crear un playbook de nombre **install_webserver_vars_file.yaml** que contenga la informacion del **punto 4**, modificar el parametro hosts y ejecutarlo en **dev**.
* Crear un playbook de nombre **install_ftpserver.yaml** que contenga la informacino del **punto 5**, este playbook debera estar dentro del directorio **/home/ansible/ansible/ftp**, modificar el parametro hosts para ejecutarlo en **dev y qa**
* Crear un playbook de nombre **uninstall_ftpserver.yaml** que contenga la informacion del **punto 6**, este playbook debera estar dentro del directorio **/home/ansible/ansible/ftp**, modificar el parametro hosts para ejecutarlo en **dev**
* Crear un **rol** llamado **apache** utilizar el procedimiento del **punto 7**, para ejecutar este rol debemos crear un playbook llamado **main_role_apache.yaml** dentro del espacio de trabajo **/home/ansible/ansible**, ejecutar este playbook en **nodeX4.opennova.pe** donde **X** es el numero de su usuario del **1 al 6**.
*  Instalar el paquete **rhel-system-roles**, de tal manera que el contenido sea accesible al usuario ansible configurado (revisar la directiva **roles_path** en **ansible.cfg** de su espacio de trabajo), crear un playbook llamado **timesync.yaml** dentro del espacio de trabajo **/home/ansible/ansible** que contenga la informacion del **punto 8**, modificar el parametro hosts para ejecutarlo en el grupo **servers**.
