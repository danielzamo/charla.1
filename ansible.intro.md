# Una introducción a Ansible

Este documento incluye:

- <a href="#laboratorio-1">Presentación del laboratorio 1</a>
- <a href="#ansible-inst">Instalando Ansible</a>
- <a href="#ansible-modulos">Uso básico de Ansible - <i>(módulos)</i></a>

<h2 id="laboratorio-1">Presentacion del laboratorio 1</h2>

Para presentar un uso inicial básico de Ansible, es que se ha vuelto a utilizar el [laboratorio 1][laboratorio.1] de pruebas.

![Laboratorio 1][laboratorio.1]

[laboratorio.1]: img/laboratorio.1.png

<h2 id="ansible-inst">Instalando Ansible</h2>

### Instalando Ansible en WSL Ubuntu 20.04 LTS

```bash
apt update && apt -y upgrade
apt install ansible openssh-clients
```

### Instalando Ansible en Fedora 34

```bash
dnf -y upgrade
dnf -y install ansible 
```

### Configuración inicial e inventario

> Una vez instalado, ansible queda disponible de utilizar. Para el [laboratorio][laboratorio.1], se ha realizado una modificación menor a la configuración inicial del aplicativo (estas modificaciones no son mostradas aquí).
> 
> Por seguridad y privacidad de datos, en este trabajo no se muestran los inventarios utilizados, para las pruebas. Dichos ficheros de configuración, son compartidos en el repositorio privado donde se deja todo el material creado para estas prácticas.

### Confirmando configuración

```bash
# Mostrar los host definidos
ansible all --list-hosts
# Verificación a un grupo de host específico
ansible dz_in_anxo --list-hosts
```

<h2 id="ansible-modulos">Uso básico comando ansible - <i>(módulos)</i></h2>

En este apartado de muestra un uso básico e introductorio de Ansible.

El comando `ansible` tiene la siguiente sintaxis:

`ansible [Hosts de destino] [Opción] -m [Módulo] -a [Argumentos]`

En [este URL][ansible.modules] se documentan los muchos módulos que posee Ansible.

### El módulo ping

En esta captura se muestra la salida del comando

```bash
ansible dz_in_anxo -m ping
```

#### Invocando ping sobre un host en particular

En esta [captura][labo2.ansible.ping.limit] se muestra como limitar la ejecucion de el modulo `ping` sobre un _host_ en particular.

El comando ejecutado es:

```bash
ansible dz_in_anxo -i /etc/ansible/inventory.laboratorio.2 --limit=tpl-centos8-stream-n1 -m ping
```

![Ansible modulo ping, limitado a host][labo2.ansible.ping.limit]

[labo2.ansible.ping.limit]: img/laboratorio.2.ansible.ping.limit.png

### El módulo command

El siguiente comando, ejecuta `uptime` sobre todos los `hosts` que esten configurados en el inventario invocado.

```bash
ansible all -i /etc/ansible/inventory.laboratorio.2 -m command -a uptime
```

La salida del comando es mostrada [aquí][labo2.ansible.command]

![Ansible modulo command][labo2.ansible.command]

[labo2.ansible.command]: img/laboratorio.2.ansible.command.png

## Referencias

- Documentación [módulos de Ansible][ansible.modules].
- https://github.com/ansible-collections/community.vmware
- https://www.virtualizationhowto.com/2021/01/ansible-provisioning-vmware-with-vmware_guest-example/
- https://docs.ansible.com/ansible/latest/collections/community/vmware/vmware_host_module.html

[ansible.modules]: https://docs.ansible.com/ansible/latest/modules/modules_by_category.html
