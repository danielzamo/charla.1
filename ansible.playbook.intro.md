# Introducción a los playbook de Ansible

## Objetivo

> En este laboratorio se instala Cockpit sobre CentOS 8 Stream (y/o derivados), mediante la ejecución de un plan de jugada (playbook) de Ansible, en el host `my-kvm-centos8` del [laboratorio][laboratorio.ansible.1]. Estos mismos pasos deberían de funcionar sobre un RHEL 8 y derivados.
> El playbook se ejecuta desde el WSL ubuntu 20.04 LTS.

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

En esta [captura][check.cockpit.my-kvm-centos8] se muestra una de las interfaces del gestor Cockpit, con el usuario root ya autenticado. La instación ha sido realizada sobre el host `my-kvm-centos8` y el servicio iniciado.

![Interface GUI Cockpit][check.cockpit.my-kvm-centos8]

[check.cockpit.my-kvm-centos8]: img/check.cockpit.my-kvm-centos8.png


