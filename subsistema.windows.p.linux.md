# WSL Linux sobre Windows 10

## Introducción

### Qué es el Subsistema de Windows para Linux?

WSL, Windows Subsystem for Linux, o Subsistema de Windows para Linux:

- Característica introducida en Windows 10
- Permite instalar (simular) un Kernel Linux directamente sobre el sistema operativo de Microsoft. Con este vamos a poder tener acceso a muchos (si no todos) los comandos y programas de terminal de este sistema operativo, desde uan ventana CLI.
- Tener acceso al shell Bash Linux sobre Windows, con una sencilla configuracion inicial. 

__*Ventajas de WSL*__

El _Subsistema de Windows para Linux_ puede ser útil para por ejemplo: Pruebas y/o implementacion de scripting (basadso en algun shell o lenguajes interpretados), edición/pruebas de script de orquestacion basados en Ansible o similar, ejecucion de comandos sobre varios sistemas remotos mediante coneccion ssh o similar, programacion de tareas programadas mediante crontab, etc. Permiti

> La finalidad principal de WSL es permitir a los administradores de sistemas, y a los programadores, usar todas las herramientas y servicios de Linux directamente desde Windows, sin tener que virtualizar, o montar una infrastructura mas complicada (como una VM o contenedor Docker).

__*Inconvenientes y limitaciones*__

- Una de las principales limitaciones de WSL es que no es un Kernel nativo. También debemos tener en cuenta que WSL1 no tiene soporte para kernel-level, por lo que algunos programas, como Docker, no funcionarán. 
- La conectividad de red funciona en WSL, pero debe pasar por varias capas.

## Instalar

### Metodo 1: Instalación desde pantallas

_[1]_ Configuración Windows

![Configuración - setting][setting_1]

_[2]_ - Aplicaciones

![Aplicaciones][aplicaciones_2]

_[3]_ - Aplicaciones y características

![Aplicaciones][aplicaciones.y.caracteristicas]

_[4]_ - Activar o desactivar las características de Windows

![Activar o desac. las caract. de Windows][activar.desac.caract.windows]

_[5]_ - Subsistema de Windows para Linux

![Activar subsistema Windows para Linux][activar.subsistema.windows.linux_5]

> Se recomienda que todo lo de Hyper-V (virtualización de Microsoft Windows) este desactivado.
>
> Si Windows solicita reiniciar, aceptar.

_[7]_ Instalación de Ubuntu LTS

En el Microsoft Store, buscar la última versión de LTS (Long Term Support).

En la siguiente secuencia se instala la ultima estable desde el Microsoft Store.

_[7.1]_ Buscar Ubuntu

![Ubuntu 20.04 LTS][ubuntu.lts_7]

_[7.2]_ Obtener Ubuntu 20.04 LTS

![Elegir Ubuntu 20.04 LTS][ubuntu.lts_8]

No es obligatorio iniciar sesión (la APP es gratuita)

![No se necesita iniciar sesión][ubuntu.lts_9]

_[8]_ Primera ejecución de Ubuntu

Al finalizar la instalación, se puede ingresar desde [aquí][ubuntu.lts.iniciar_10].

![Iniciar WSL Ubuntu 20.04 LTS][ubuntu.lts.iniciar_10]

_[9]_ Primer inicio

Sobre el primer inicio Ubuntu solicita establecer las credenciales de un primer usuario. Esto se muestra en [esta][ubuntu.lts.primer.login_11] captura.

![Primer inicio de WSL - Ubuntu LTS][ubuntu.lts.primer.login_11]

[setting_1]: img/setting_1.png
[aplicaciones_2]: img/aplicaciones_2.png
[aplicaciones.y.caracteristicas]: img/aplicaciones.y.caracteristicas_3.png
[activar.desac.caract.windows]: img/activar.caract.windows_4.png
[activar.subsistema.windows.linux_5]: img/activar.subsistema.windows.linux_5.png
[ubuntu.lts_7]: img/ubuntu.lts_7.png
[ubuntu.lts_8]: img/ubuntu.lts_8.png
[ubuntu.lts_9]: img/ubuntu.lts_9.png
[ubuntu.lts.iniciar_10]: img/ubuntu.lts.iniciar_10.png
[ubuntu.lts.primer.login_11]: img/ubuntu.lts.primer.login_11.png

---

## Algunas notas respecto al estado actual de WSL
- En la [esta][comparacion.wsl.1.2] referencia se enumeran algunas comparaciones de WSL 1 vs WSL 2.
- Referir comandos. Por ejemplo afectados por la capa de red o el propio Kernel (WSL no es un kernel Linux puro)
- Ventajas respecto a clientes ssh sobre Windows (MobaXterm, putty, Bitvise SSH Client, mRemoteNG) y/o utilidades CygWin. .... 
  - Ejecucion paralela sobre varios sistemas remotos
  - Desarrollo, prueba y ejecucion de scripting desde un CLI, mediantes comandos mas propios de sistemas basados en Unix (Linux)
- El fichero `/etc/hosts` y `C:\Windows\System32\drivers\etc\hosts`

---

## Tip

- Montar una unidad de red sobre WSL
  - Ejemplo: El siguiete ejemplo monta una unidad de red Windows (nativos de samba o red Windows o CIFS) al filesystem de WSL. Ver [esta figura] (En este ejemplo se cre el directorio donde se monta. Revisar, sobre el equipo que se replique la prueba, que no este ocupado o que no exista.)

  ![Montar unidad W][mount.w]

  [mount.w]: img/mount.w.png

  ```bash
  sudo mkdir -pv /mnt/testing-charla
  sudo mount -t drvfs '\\<IP>\<NAME_SHARE>' /mnt/testing-charla
  ```
  
  Nota: desde el `cmd` de Windows con `net view \\<IP>/all`  se puede ver que comparte el host.

---

## Configuración inicial básica/recomendada de WSL Ubuntu

_[1]_ Actualizar

```bash
sudo apt update && sudo apt -y upgrade
```

_[2]_ Instalación/configuracion inicial de vim

```bash
apt install vim ctags vim-scripts
```

_[2.1]_ Configuración inicial basica

Se agregan las siguientes configuraciones.

```bash
cat /etc/vim/vimrc
" Add to presentation
"...
set nocompatible
set encoding=utf-8
set fileencodings=utf-8
set fileformats=unix,dos
set ignorecase
set smartcase
"set list
set showmatch
set binary noeol
"set autoindent
syntax on
highlight Comment ctermfg=LightCyan
set wrap
set cursorline
```

_[3]_ Instalación de paquetes/herramientas

```bash
apt install rsync dnsutils
```

## Referencias

- [Instalación de WSL][inst.wsl] 
- [Install Windows Subsytem Linux Windwos 10][inst.wsl.win]
- [Ubuntu 20.04 vs. Windows 10 WSL/WSL2 Performance In 170+ Benchmarks][comparative.wsl.vs.ubuntu]
- [Comparación de WSL 1 con WSL 2][comparacion.wsl.1.2] 

[comparacion.wsl.1.2]: https://docs.microsoft.com/es-es/windows/wsl/compare-versions

[inst.wsl]: https://docs.microsoft.com/es-es/windows/wsl/install "Instalación de WSL en Windows 10"
[inst.wsl.win]: https://www.windowscentral.com/install-windows-subsystem-linux-windows-10
[comparative.wsl.vs.ubuntu]: https://www.phoronix.com/scan.php?page=article&item=wsl-wsl2-tr3970x&num=1

---

