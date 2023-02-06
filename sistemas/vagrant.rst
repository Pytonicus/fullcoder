=======
Vagrant
=======

.. image:: /logos/docker-logo.png
    :scale: 20%
    :alt: Logo Docker
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Última edición el día |date| a las |time|. 

Esta es la documentación que he recopilado para instalar y configurar vagrant en sistemas linux. 
 
.. contents:: Índice
 
Configuración e instalaciones   
#############################

Instalaciones
*************

- Instalar Virtualbox: ``sudo apt install virtualbox``
- Instalar Vagrant: ``sudo apt install vagrant``

Crear máquina virtual con Virtualbox
************************************

- Paso 1: Descargar un sistema operativo ej. Ubuntu server: https://ubuntu.com/download/server
- Paso 2: Abrimos Virtualbox y creamos una nueva máquina virtual:
    - Seleccionamos el sistema operativo.
    - Ponemos 2048MB o 1024MB de memoria si no tenemos demasiada en nuestro equipo.
    - Creamos un disco virtual: elegimos la opción VMDK, espacio "Reservado dinámicamente" y el espacio 10GB.
- Paso 3: Arrancamos la máquina virtual y en Dispositivos seleccionamos la opción Unidades Opticas y cargamos la imagen de instalación de Ubuntu.
- Paso 4: Reiniciamos la máquina e instalamos el sistema operativo.
- Paso 5: Una vez instalado, ejecutamos la máquina.

Crear máquina virtual con vagrant
*********************************

- Paso 1: Crear directorio: ``mkdir pruebaVagrant``
- Paso 2: Acceder a la raiz del nuevo directorio en el terminal y ejecutar: ``vagrant init ubuntu/xenial64`` (el nombre del sistema lo provee de un repositorio propio de Vagrant)
- Paso 3: Arrancar la máquina: ``vagrant up``
- Paso 4: En la carpeta raiz del proyecto creamos un archivo, ejemplo **hola.txt**
- Paso 5: Acceder a la máquina virtual: ``vagrant ssh``
- Paso 6: En la línea de comando de la máquina virtual, ejecutamos ``cd /`` y el comando ``ls vagrant`` y veremos listado el archivo **hola.txt**.
- Paso 7: Para cerrar máquina virtual en la raiz del proyecto (no en la terminal de la máquina virtual) ejecutar: ``vagrant halt``

.. note::
    Puedes ver que imágenes cargar con **vargant init** en: https://app.vagrantup.com/boxes/search


Archivo Vagrantfile
*******************

Vagrantfile es el archivo de configuración del proyecto cuando se crea un proyecto por defecto tiene la siguiente configuración si eliminamos los COMENTARIOS:

.. code-block:: ruby

    # -*- mode: ruby -*-
    # vi: set ft=ruby :

    # dentro de un bucle que recorre todos los datos:
    Vagrant.configure("2") do |config|
        # se define por defecto cual es la imagen del sistema operativo usado, si la cambiamos hará un clon si existe del repositorio principal:
        config.vm.box = "ubuntu/xenial64"

        config.vm.provider "virtualbox" do |vb|
        #   # con este comando se ejecutará virtualbox en modo gráfico al cargar una imagen
            vb.gui = true
            #
            # Cambiamos la cantidad de memoria usada para la maquina:
            vb.memory = "2048"
            # Y el número de cpus a 2
            vb.cpus = 2
        end

    end

- Ejecutamos ``vagrant up`` para arrancar la máquina y nos abrirá virtualbox, si vemos el menu donde aparece la imagen nos mostrará que ahora tiene 2 cores y 2048MB.

.. note::
    Hay una serie de comandos comentados que se irán editando y habilitando según necesidad.

Comandos de Vagrant 
###################

Comandos básicos 
****************

- ``vagrant init ubuntu/xenial64``: Crear nueva máquina virtual.
- ``vagrant up``: Arrancar la máquina virtual.
- ``vagrant ssh``: Acceder vía ssh a la máquina virtual.
- ``vagrant halt``: Apagar máquina virtual.


Comandos de box 
***************
