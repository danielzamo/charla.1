# Introducción a los playbook de Ansible

## Objetivo

> En este laboratorio se introduce el uso de un simple playbook. El mismo instala _Cockpit_ sobre _CentOS 8 Stream_ (y/o derivados). Esto es, mediante la ejecución de un plan de jugada (playbook) de Ansible, sobre el host `my-kvm-centos8` del [laboratorio][laboratorio.ansible.1] se instalará la interface *consola web de administración __Cockpit__* . 
> 
> Estos mismos pasos deberían de funcionar sobre un RHEL 8 y/o derivados. 

_Nota:_ El playbook se ejecuta desde el WSL ubuntu 20.04 LTS. Pero debería ser funcional desde cualquier Ansible de versión similar al aquí utilizado.

## Representación del laboratorio

![Laboratorio Ansible 1][laboratorio.ansible.1]

[laboratorio.ansible.1]: img/laboratorio.ansible.1.png

## Instalar cockpit usando playbook de Ansible

1. Agregar el host al inventario (El inventario queda compartido en el repositorio privado, el mismo no es mostrado aquí).
2. Verificar que se llega al host target (destino), donde será instalada la __*"Web Admin Console"*__ Cockpit. Dicha verificación puede realizarse ejecutando:
  ```bash
  $ ansible all -i ../inventory.laboratorio.2 --limit my-kvm-centos8 -m ping
  ```
3. Se escribe el siguiente plan de jugada (playbook). Este es:

  ```bash
  $ cat install.cockpit.centos8.yml
  ---
- hosts: my-kvm-centos8
  tasks:
    - name: Install cockpit
      yum:
        name: "{{ item }}"
        state: present
      with_items:
      - cockpit
      - cockpit-ws # Cockpit Web Service
      - cockpit-pcp # Cockpit PCP integration
      - cockpit-selinux # Cockpit SELinux package
        #- cockpit-doc # Cockpit deployment and developer guide
      - cockpit-bridge # Cockpit bridge server-side component
        #- cockpit-dashboard # Cockpit remote servers and dashboard
        #- cockpit-docker # Cockpit user interface for Docker containers
      - cockpit-machines # Cockpit user interface for virtual machines
      - cockpit-kdump # Cockpit user interface for kernel crash dumping
      - cockpit-packagekit # Cockpit user interface for package updates
      - cockpit-sosreport # Cockpit user interface for diagnostic reports
        #- cockpit-kubernetes # Cockpit user interface for Kubernetes cluster
        #- cockpit-subscriptions # Cockpit subscription user interface package
      - cockpit-storaged # Cockpit user interface for storage, using Storaged
      - cockpit-networkmanager # Cockpit user interface for networking, using NetworkManager
      - cockpit-system # Cockpit admin interface package for configuring and troubleshooting a system
    #
    # start and enable cockpit
    #
    - name: start cockpit
      systemd:
        name: cockpit
        state: started
    - name: enable cockpit.socket
      systemd:
        name: cockpit.socket
        enabled: yes
    #
    # set firewall rules for cockpit
    #
    - name: Firewall rules
      firewalld:
        service: cockpit
        permanent: true
        state: enabled
        immediate: yes
  ```
4. Solo resta ejecutar el playbook. Se puede invocar ejecutando:
  ```bash
  ansible-playbook -i <PATH_INVENTORY>/<MY_INVENTORY> install.cockpit.centos8.yml
  ```

  _Nota:_ Al invocar `ansible...` se pueden utilizar opciones como:

  - `--step` --> las tareas realizadas paso a paso, solicitando confirmación por cada una de ellas.
  - `-vvv` --> se puede dar mayor nivel de verbose del propio comando. Esto sirve para dar mayor nivel de debug a nuestros playbook, para mejor depuración.
  
## Interface Cockpit
Para autenticarnos y utilizar Cockpit se puede ingresar en el navegador `https://my-kvm-centos8:9090` (En los ficheros host - en sis. basados en Windows en `C:\Windows\System32\drivers\etc\hosts` o en sis. op. MACOS y Linux en `/etc/hosts`-  ya he agregado el `IP` y `nombre de dns`). La pantalla de login se muestra [aquí][cockpit.login].

![Login Cockpit][cockpit.login]

[cockpit.login]: img/cockpit.login.png

En esta [captura][cockpit.my-kvm-centos8] se muestra una de las interfaces del gestor Cockpit, con el usuario root ya autenticado. La instación ha sido realizada sobre el host `my-kvm-centos8` y el servicio iniciado.

![Interface GUI Cockpit][cockpit.my-kvm-centos8]

[cockpit.my-kvm-centos8]: img/cockpit.my-kvm-centos8.png


