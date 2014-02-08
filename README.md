Ejercicios-Tema6-Gestión de configuraciones
===========================================

Ejercicios Antonio Melero de Infraestructura Virtual 13-14 


###Ejercicio 1

**Instalar chef en la máquina virtual que vayamos a usar**

Para este ejercicio se utilizará una maquina Kubuntu ( ya utlizada en la realización de la práctica 3):

Como uso una máquina tipo Ubuntu debemos instalar previamente Ruby y Ruby Gems que no ha sido instalado todavía:

    sudo apt-get install ruby1.9.1 ruby1.9.1-dev rubygems

![captura1]()

Una vez instalado, ya podemos instalar **chef** tecleando desde el terminal

    sudo gem install ohai chef

![captura2]()
