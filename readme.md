# Estructura de carpetas
## Host: Pop_os!, Debian Linux Distro
Se utilizó la siguiente estructura de carpetas en la maquina host tipo linux
    wm_ubuntu/
    ├── .vagrant/ 
    │   └── bundler/
    │   └── machines/
    │   └── ...
    ├── .gitignore
    ├── readme.md
    ├── ubuntu-bionic-18.04-cloudimg-console.log
    ├── ubuntu.yml
    └── Vagrantfile

En el caso de *.vagrant* y *ubuntu-bionic-18.04-cloudimg-console.log* no se cargaron al repositorio ya que se generan durante la ejeución. 


## VM: Bionic Ubuntu for Vbox, Debian Linux Distro
Se utilizó la siguiente estructura de carpetas en la maquina host tipo linux
home/
└── tux/
│   └── ...
└── ubuntu/
│   └── ...
└── vagrant/
    └── partido.txt


# Instalción de componentes
## Vagrant
### Instalación distro linux debian (pop_os!)
La instalación se basa en la descargar desde hashicorp la versión adecuada al entorno, en este caso [vagrant_2.4.1-1_amd64.deb] a través de **wget https://releases.hashicorp.com/vagrant/2.4.1/vagrant_2.4.1-1_amd64.deb**.
La instalción con carga de dependencias automaticas es **sudo apt instal ./vagrant_2.4.1-1_amd64.deb**, recuerde colocar el ./ antes del .deb para que lo identifique como un ejecutable. 

### Vagran Cloud (boxes)
En lugar de iniciar direcatamente con init, se recomienda agregar la imagen para saber que todo el box se ha descargado correctamente, comenzamos por **vagrant box add <image_name>** y elegir la opcion de vbox, hyper-v, docker, etc. En este caso se utilizó [ubuntu/bionic64].
El inventario que imagenes descargadas de vagrant cloud **vagrant box list**

## Ansible
Instalción **sudo apt update** y **sudo apt install ansible -y** y validación **ansible --version**

## Vbox
Se extrae del proveedor la liga correposoiente, por ejempo, *echo "deb [arch=amd64] https://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib" | sudo tee -a /etc/apt/sources.list.d/virtualbox.list*, 
```
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -

sudo apt update
sudo apt install virtualbox-7.0 -y
sudo apt install virtualbox-ext-pack
virtualbox --version
```

# Ejecución, terminal de bash
Para comenzar se descarga la imagen requerida **vagrant init ubuntu/bionic64**, se edita el vagrantfile y se agrega el playbook que puede ser verificada su sintáxis con **ansible-playbook path/to/playbook.yml --syntax-check**.

Con **vagrant up** se inicia la ejeución y con la impresión del nombre de las tareas, en conjunto con .log es posible verificar contenido y de ser necesario hacer debugging.

Es posible re-ejecutar los cambios del pĺaybook.yml utilzando **vagrant provision**, en caso de iniciar de vuelta se puede hacer con **vagran reload** o en el caso de re-desplegar la VM, usar **vagrant destroy -f** y aprovisionar de vuelta con **vagrant up**.

Cuando la maquina virtual de Ubuntu este ejecutando correctamente, es posible acceder con **vagrant ssh** e imprmir contenido ejecutando *cat /vagrant/partido.txt*.

Con *exit* se corta la comunicación con la VM y **vagrant halt** se apaga sin destruirlo. Cualquier estatus puede ser verificado simultanemaente con la terminal o el gestor grafico de vbox 



# Ligas de interes
Sitio de descarga de vagrant *https://releases.hashicorp.com/vagrant/2.4.1/*
Sitio de descarga de virtualbox *https://www.virtualbox.org/wiki/Linux_Downloads*

Sincronización con usuarios windows *https://www.youtube.com/watch?v=7Di0twyxw1M&t=553s*
Ejecución con kernel *https://www.youtube.com/watch?v=V6jujUTkJJ8*
