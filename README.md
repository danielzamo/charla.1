# README

Este documento incluye los siguientes ficheros

- En [WSL Linux Sobre Windows 10](./subsistema.windows.p.linux.md) ([PDF aquí](pdf.out/subsistema.windows.p.linux.pdf)) se muestran algunos comentarios respecto a WSL versión 1 y uno de los metodos de instalación/activación.
- En el [vm.linux.md](./vm.linux.md) ([PDF aquí](pdf.out/vm.linux.pdf)) se enumeran unas pocas arquitecturas de virtualización completa, para el sistema operativo Windows 10/11. Mostrando ademas, la que se utilizará en el desarrollo de este este trabajo.
- El fichero [cli.tool.md](./cli.tools.md) ([PDF aquí](pdf.out/cli.tools.pdf)) incluye:
  - La representación del despliegue utilizado para el laboratorio 1. 
  - Se realizan todas las practicas y ejecucion de comandos (comandos presentados/usados: `sshpass`, `parallel-ssh`, `tmux`, ...)
- El [ansible.intro.md](./ansible.intro.md) ([PDF aquí](pdf.out/ansible.intro.pdf)) incluye:
  - Presentación _laboratorio 2_.
  - Instalacion de ansible en __*WSL - Ubuntu 20.04 LTS*__ y en __*Fedora 34*__.
  - Configuracion inicial y el primer inventario.
  - Uso de ansible basico. Modulos `ping` y `command`.
- En el fichero [ansible.playbook.intro.md][ansible.playbook.intro.md]  ([PDF aquí](pdf.out/ansible.playbook.intro.pdf)) se presenta un primer playbook que instala y pre configura Cockpit sobre una VM basada en CentOS 8 Stream.

---

## Contenido último

El último contenido de ficheros en el "directory work" original de este repositorio es:

```bash
.
├── README.md
├── ansible.intro.md
├── ansible.playbook.intro.md
├── charla.1.drawio
├── cli.tools.md
├── etc
│   └── ansible
│       ├── ansible.cfg
│       ├── hosts
│       ├── inventory.laboratorio.2
│       └── playbook
│           ├── ansible-kvm-vm
│           │   ├── LICENSE
│           │   ├── README.md
│           │   ├── defaults
│           │   │   └── main.yml
│           │   ├── files
│           │   │   └── README
│           │   ├── handlers
│           │   │   └── main.yml
│           │   ├── meta
│           │   │   └── main.yml
│           │   ├── tasks
│           │   │   ├── main.yml
│           │   │   └── teardown_kvm_vm.yml
│           │   ├── templates
│           │   │   └── ifcfg.j2
│           │   ├── test.yml
│           │   ├── tests
│           │   │   ├── inventory
│           │   │   └── test.yml
│           │   └── vars
│           │       └── main.yml
│           └── install.cockpit.centos8.yml
├── img
│   ├── activar.caract.windows_4.png
│   ├── activar.subsistema.windows.linux_5.png
│   ├── aplicaciones.y.caracteristicas_3.png
│   ├── aplicaciones_2.png
│   ├── cockpit.login.png
│   ├── cockpit.my-kvm-centos8.png
│   ├── ejecutar.powershell.png
│   ├── labo.tmux.png
│   ├── laboratorio.1.png
│   ├── laboratorio.2.ansible.command.png
│   ├── laboratorio.2.ansible.ping.limit.png
│   ├── laboratorio.ansible.1.png
│   ├── microsoft_store_6.png
│   ├── mount.w.png
│   ├── setting_1.png
│   ├── teminal.cli.png
│   ├── tmux.htop.png
│   ├── ubuntu.lts.iniciar_10.png
│   ├── ubuntu.lts.primer.login_11.png
│   ├── ubuntu.lts_7.png
│   ├── ubuntu.lts_8.png
│   ├── ubuntu.lts_9.png
│   └── vmware.workstation.player.png
├── pdf.out
│   ├── ansible.intro.pdf
│   ├── ansible.playbook.intro.pdf
│   ├── cli.tools.pdf
│   ├── subsistema.windows.p.linux.pdf
│   └── vm.linux.pdf
├── seguimiento.md
├── subsistema.windows.p.linux.md
├── vm.linux.md
└── vms
    └── laboratorio.1
        ├── fedora-xfce
        │   ├── my-fedora-xfce-disk1.vmdk
        │   ├── my-fedora-xfce.mf
        │   └── my-fedora-xfce.ovf
        └── windows.10
            ├── windows.10-disk1.vmdk
            ├── windows.10-file1.nvram
            ├── windows.10.mf
            └── windows.10.ovf
```

Nota del autor: no todos los ficheros son públicos en este repositorio.

---

