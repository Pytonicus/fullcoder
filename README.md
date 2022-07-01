# FullCoder Sphinx Site
Bienvenid@ al repositorio de FullCoder. Con esta guía podrás desplegar tu propio repositorio de documentación con todo el contenido disponible de FullCoder.

## Instalar dependencias
Para poder compilar FullCoder es necesario tener instalado __Python 3__ y añadir el paquete __Sphynx__: ``pip install -U Sphinx``

También debemos instalar el tema __faculty-sphinx-theme__: ``pip install faculty-sphinx-theme``

## Compilar el sitio web

LINUX: Para compilar la web nos vamos a la raiz del proyecto desde un terminal y ejecutamos ``make html``. 

WINDOWS: Para compilar la web en windows usamos el comando ``.\make.bat html``

NOTA: Alternativamente si no funciona la compilación a HTML se puede instalar sphinx del siguiente modo: ``sudo apt install python-sphinx``

NOTA 2: Si falla la nota anterior, instala: ``sudo apt install sphinx-common`` y también ``sudo apt install python3-stemmer``

En la carpeta ___build/html__ se encuentra la página compilada.

## Crear manuales
En el directorio template hay unos archivos base para clonar y crear nuevos manuales de forma estandar siguiendo estos pasos:

- Crear una nueva carpeta con el nombre del lenguaje de programación o tecnología.
- Copiar uno de los archivos y editar su contenido.
- ir al archivo index.rst y copiar la estructura que tienen los otros lenguajes eliminando las líneas que apunten a archivos que no existen en la nueva carpeta.