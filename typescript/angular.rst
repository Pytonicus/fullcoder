Framework: Angular
==================

.. image:: /logos/logo-angular.png
    :scale: 50%
    :alt: Logo Angular
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica de Angular 11

.. contents:: Índice
 
Configuraciones
###############  
 
Instalación de Angular CLI
**************************
Para gestionar Angular hay que instalar Angular CLI: ``npm install -g @angular/cli``

.. note::
    Para instalar en Linux utilizar el comando ``sudo npm install -g @angular/cli``

ANGULAR CLI
###########
Para ejecutar un comando de Angular CLI el prefijo que se utiliza es ``ng``:

* Crear proyecto: ``ng new nombre-proyecto``
* Levantar servidor y abrir navegador: ``ng serve -o`` (ruta por defecto: localhost:4200)
* Instalar todas las dependencias: ``npm install`` (no es un comando ng pero es importante recordarlo)


.. attention::
    Para ejecutar en Windows estos comandos CLI se usará la aplicación ``nodejs command prompt`` o ejecutar con el prefijo ``npm run ng``

Componentes
###########

Los componentes se encuentran en la carpeta **src**.
Cada componente se organizará en una carpeta con el siguiente contenido:
* Hoja de estilo CSS u otro tipo.
* Archivo HTML.
* Controlador Typescript.
* Modulo Typescript.

