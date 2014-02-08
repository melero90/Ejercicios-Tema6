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
    
![captura4](https://dl.dropbox.com/s/42eni81w9s62igu/t6_ej2_1.png)

Ahora debemos configurar los ficheros que contendrán la recetas para instalar *geany*, por ejemplo, y *nginx*.

Para ello dentro de "chef/cookbooks/geany/recipes" creamos el fichero default.rb que contendrán la receta para instalar el editor geany y creará un directorio en "/home/antoniomelero/Documentos" y dentro de él un fichero.

    #!usr/bin/ruby

    package 'geany'
    directory "/home/Documents/prueba1"
        owner "antoniomelero"
        group "antoniomelero"
        mode 00544
        action :create
        content "Directorio"
    end

dentro de "chef/cookbooks/nginx/recipes" creamos el fichero default.rb que contendrán la receta para instalar nginx y creará un directorio en "/home/antoniomelero/Documentos" y dentro de él un fichero.

    #!usr/bin/ruby

    package 'nginx'
    directory "/home/Documents/prueba"
        owner "antoniomelero"
        group "antoniomelero"
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

    file_cache_path "/home/Documents/chef"
    cookbook_path "/home/Documents/chef/cookbooks"
    json_attribs "/home/Documents/chef/node.json"

Ahora desde el directorio raíz podemos ejecutarlo:

    sudo chef-solo -c chef/solo.rb
    
![captura5](https://dl.dropbox.com/s/ao321y50vkkkrj3/t6_ej2_3.png)

![captura6](https://dl.dropbox.com/s/kisb9w1x1aeq5xp/t6_ej2_2.png)

#### Ejercicio 3

**Escribir en YAML la siguiente estructura de datos en JSON: { uno: "dos",tres: [ 4, 5, "Seis", { siete: 8, nueve: [ 10, 11 ] } ] }**

Esta estructura de datos JSON traducida a YAML sería la siguiente:

    uno : "dos"
    tres :
    - 4
    - 5
    - "Seis"
    -
        siete : 8
        nueve : 
            - 10
            - 11


#### Ejercicio 4

**Desplegar los fuentes de la aplicación de DAI o cualquier otra aplicación que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.**

#### Ejercicio 5

**Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.**

#### Ejercicio 6

**Instalar una máquina virtual Debian usando Vagrant y conectar con ella.**
