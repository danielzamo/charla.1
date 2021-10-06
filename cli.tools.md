# Herramientas utilidades para CLI

En este documento se enumeran algunas de los paquetes y/o herramientas para utilizar desde el CLI (command-line interface) de sistemas operatvivos orientados al comando, del tipo basados en Unix (WSL Windows, VM Fedora Linux, o similares). Se muestran algunos ejemplos.

## Laboratorio de prueba utilizado para este trabajo

Para este trabajo se ha desplegado [este laboratorio][laboratorio.1] de pruebas, sobre un anfitrion basado en tecnología VMWare, en un Windows 10. Se intenta aqui mostrar/debatir, una arquitectura que sirva de base a un despliegue comun o consensuado, y mostrar algunas sesiones de trabajo haciendo uso de un CLI Linux unificado o unico/comun.
La escritura de este articulo ha sido realizado en un despliegue llamador laboratorio 1, cuya represetnacion es mostrada [aquí][laboratorio.1].

![Laboratorio 1][laboratorio.1]

[laboratorio.1]: img/laboratorio.1.png

## Instalación paquetes sobre Fedora 34

`sudo dnf -y install htop rsync nmap`

## Instalación paquetes sobre WSL Ubuntu LTS 20.04

> Recordemos que WSL (principalmente la versión WSL 1, usada en este trabajo) esta basado en Hiper-V, y __*no es un kernel "puro" de Linux*__, esto ocaciona que algunos de los paquetes no funcionaran adecuadamente, como si fuese un contenedor o VM real Linux.  Paquetes como `netcat`, `tcpdump`, `systemctl` no se ejecutaran adecuadamente.
> 
> Los paquetes que se instalan a continuación, han sido probados sobre un Ubuntu 20.04 (expuesta en [este](./subsistema.windows.p.linux.md) documento), funcional sobre WSL ver. 1.

```bash
sudo apt update && sudo apt -y upgrade
sudo apt install htop rsync dnsutils htop lsof
```