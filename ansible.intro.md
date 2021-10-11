# Una introducción a Ansible

## Presentacion del laboratorio 2

Para presentar un uso inicial básico de Ansible, es que se ha desplegado [este laboratorio][laboratorio.2] de pruebas.

![Laboratorio 2][laboratorio.2]

[laboratorio.2]: img/laboratorio.2.png

## Instalando Ansible en WSL Ubuntu 20.04 LTS

```bash
apt update && apt -y upgrade
apt install ansible openssh-clients
```

## Instalando Ansible en Fedora 34

```bash
dnf -y upgrade
dnf -y install ansible 
```

## Configuración inicial e inventario

> Una vez instalado, ansible queda disponible de utilizar. Para el laboratorio 2, se ha realizado una modificación menor a la configuración inicial del aplicativo.
> 
> Por seguridad y privacidad de datos, en este trabajo no se muestran los inventarios utilizados, para las pruebas. Dichos ficheros de configuración, son compartidos en el repositorio privado donde se deja todo el material creado para estas prácticas.

## Confirmando configuración

```bash
# Mostrar los host definidos
ansible all --list-hosts
# Verificacion a un grupo de host especifico
ansible dz_in_anxo --list-hosts
```

## Uso básico comando ansible (invocando modulos)

En este apartado de muestra un uso básico de Ansible.

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

[ansible.modules]: https://docs.ansible.com/ansible/latest/modules/modules_by_category.html
