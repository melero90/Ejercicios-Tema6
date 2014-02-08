Ejercicios-Tema6-Gestión de configuraciones
===========================================

Ejercicios Antonio Melero de Infraestructura Virtual 13-14 


###Ejercicio 1

**Instalar chef en la máquina virtual que vayamos a usar**

Para este ejercicio se utilizará una maquina Kubuntu ( ya utlizada en la realización de la práctica 3):

Como uso una máquina tipo Ubuntu debemos instalar previamente Ruby y Ruby Gems que no ha sido instalado todavía:

    sudo apt-get install ruby1.9.1 ruby1.9.1-dev rubygems

![captura1](https://dl.dropbox.com/s/izmdghj35bp4vpx/t6_ej1.png)

![captura2](https://dl.dropbox.com/s/rcevf6kok2hqsnh/t6_ej1_2.png)

Una vez instalado, ya podemos instalar **chef** tecleando desde el terminal

    sudo gem install ohai chef

![captura3](https://dl.dropbox.com/s/nvv06nig2py4vvu/t6_ej1_3.png)


### Ejercicio 2

**Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.**

En primer lugar debemos crear los directorios para nuestras recetas:

    mkdir -p chef/cookbooks/geany/recipes
    mkdir -p chef/cookbooks/nginx/recipes

Ahora debemos configurar los ficheros que contendrán la recetas para instalar *geany*, por ejemplo, y *nginx*.

Para ello dentro de "chef/cookbooks/geany/recipes" creamos el fichero default.rb que contendrán la receta para instalar el editor geany y creará un directorio en "/home/antoniomelero/Documentos" y dentro de él un fichero.

    #!usr/bin/ruby

    package 'geany'
    directory "/home/antoniomelero/Documentos/prueba1"
        owner "antoniomelero"
        group "antoniomelero"
        mode 00544
        action :create
        content "Directorio"
    end

dentro de "chef/cookbooks/nginx/recipes" creamos el fichero default.rb que contendrán la receta para instalar nginx y creará un directorio en "/home/antoniomelero/Documentos" y dentro de él un fichero.

    #!usr/bin/ruby

    package 'nginx'
    directory "/home/francisco/Documentos/prueba"
        owner "francisco"
        group "francisco"
        mode 00544
        action :create
        content "Directorio"
    end

Lo siguiente es configurar el fichero *"node.json"* que incluirá las referencias a nuestras recetas:

    {
        "run_list":["recipe[geany]", "recipe[nginx]"]
    }

Por último debemos de configurar el fichero de configuración "solo.rb" de la siguiente forma:

    #!usr/bin/ruby

    file_cache_path "/home/antoniomelero/Documentos/chef"
    cookbook_path "/home/antoniomelero/Documentos/chef/cookbooks"
    json_attribs "/home/antoniomelero/Documentos/chef/node.json"

Ahora desde el directorio raíz podemos ejecutarlo:

    sudo chef-solo -c chef/solo.rb

#### Ejercicio 3

#### Ejercicio 4

#### Ejercicio 5

#### Ejercicio 6
