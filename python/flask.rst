Microframework: Flask 
=====================

.. image:: /logos/logo-flask.png
    :scale: 10%
    :alt: Logo Flask
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica para trabajar con el Microframework Flask

.. contents:: Índice
 
Configuraciones
###############  
 
Creación del proyecto
*********************

* Crear un Directorio para el proyecto y acceder al mismo.
* Crear un entorno virtual.
* Instalar flask: `pip install flask`.
* Dentro del directorio creamos un directorio llamado templates y un archivo llamado main.py

Archivo principal
*****************

El archivo principal básico:

.. code-block:: python
    :linenos:

    # importamos flask y creamos el objeto con flask:
    from flask import Flask
    app = Flask(__name__)

    # Con un decorador definimos la ruta raiz y dentro una función que devuelve un mensaje.
    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    # creamos la condición para arrancar la aplicación flask:
    if __name__ == "__main__":
        # le pasamos la ejecución de la app y por parámetros la ruta del host y si esta en modo depuración o no.
        app.run(host='localhost', debug=True)

* Arrancar el servidor: ``python main.py``
* Abrir en navegador: http://localhost:5000


Rutas
#####

Rutas principales (main.py)
***************************
Las rutas se suelen añadir en el archivo principal del proyecto:

.. code-block:: python
    :linenos: 

    from flask import Flask
    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    # despues de la / creamos otra ruta:
    @app.route('/otra_ruta')
    def hola():
        return 'Acceso a otra ruta!'

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

* En el navegador abrir: http://localhost:5000/otra_ruta

rutas con parámetros 
********************

* Las rutas con parámetros:

.. code-block:: python
    :linenos:

    from flask import Flask
    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    # con los símbolos mayor-menor podemos capturar un parámetro por defecto tipo cadena:
    @app.route('/nombre/<persona>')
    def nombre(persona):
        return 'Te llamas {}'.format(persona)

    # Podemos definir que sea un entero o coma flotante:
    @app.route('/edad/<int:edad>')
    def edad(edad):
        return 'Tienes: {} años'.format(edad)

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

* La ruta que recibe parámetros por ejemplo sería: http://localhost:5000/nombre/Guillermo


Rutas por uno o más métodos
***************************
Es posible estipular uno o varios métodos permitidos en una ruta:

.. code-block:: python
    :linenos:

    from flask import Flask
    # importamos la librería request que funciona igual que en django:
    from flask import request

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    # el decorador recibe una lista de métodos permitidos:
    @app.route('/metodos', methods=['GET', 'POST'])
    def login():
        # preguntamos si el método es GET que nos abra sesion y si no que nos mande de vuelta al formulario:
        if request.method == 'GET':
            return 'Recibido ' + request.method
        else:
            print("Es otro método")

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

Redirecciones
*************

.. code-block:: python
    :linenos:

    # cargar librerías redirect y url_for:
    from flask import Flask, render_template, redirect, url_for


    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        # Redireccionar a otra ruta usando el nombre de su función:
        return redirect(url_for('saludar'))


    @app.route('/saludar', methods=['GET'])
    def saludar(nombre=None): 
        return 'Hola desde otra ruta'


    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

Error 404
+++++++++
Procedimiento común para redirección 404:

* Crear en **templates** archivo **error.html**:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>ERROR 404</title>
    </head>
    <body>
        <h1>ERROR 404</h1>
        <p>La página solicitada no existe</p>
    </body>
    </html>

* Crear error 404 cuando introducimos rutas incorrectas:

.. code-block:: python
    :linenos:

    from flask import Flask, render_template, redirect, url_for

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return redirect(url_for('saludar'))


    @app.route('/saludar', methods=['GET'])
    def saludar(nombre=None): 
        return 'Hola desde otra ruta'

    # cargamos la ruta de error cuando no se encuentre página:
    @app.errorhandler(404)
    def error(error): # este recibe un parámetro 
        return render_template('error.html'), 404

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

Vistas
######

Las vistas en Flask no suelen usarse, en su lugar se visualizan los templates con Jinja

Templates (Jinja2)
#################

Jinja2 es el motor de plantillas que se utiliza de serie en Flask.

* En la carpeta templates se crea un archivo por ejemplo prueba.html:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Prueba con Flask</title>
    </head>
    <body>
        <h1>Plantillas Jinja2</h1>
        <p>primera toma de contacto con Flask</p>
    </body>
    </html>

* De vuelta a main.py se renderiza el template:

.. code-block:: python
    :linenos:
 
    # importamos render_template para gestionar plantillas:
    from flask import Flask, render_template

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    @app.route('/prueba')
    def prueba(nombre=None): 
        # Renderizamos el archivo prueba:
        return render_template('prueba.html') 

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)


Template Tags
*************

Los Template Tags son un tipo de etiquetas especiales en Jinja2 que se utilizan en las plantillas para ejecutar respuestas backend.

Estas etiquetas suelen tener dos tipos de estructuras: ``{% instrucción %}`` o ``{{ datos }}`` según el tipo de tarea que vayamos a ejecutar.

Template tag base
+++++++++++++++++

Una buena práctica para no repetir código en plantillas es coger todo el contenido común y almacenarlo en una plantilla base:

* En **templates** crear un archivo llamado **base.html**:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Prueba con Flask</title>
    </head>
    <body>
        {% block cuerpo %}{% endblock %}
    </body>
    </html>

* En el resto de archivos html se elimina todo lo que contemple fuera del body del siguiente modo:

.. code-block:: html 
    :linenos: 

    {% extends 'base.html' %}

    {% block cuerpo %}
    <form method="POST" action="/subir" enctype="multipart/form-data">
        <label for="documento">Subir archivo</label>
        <br>
        <input type="file" name="documento">
        <br><br>
        <input type="submit">
    </form>
    {% endblock %}


Template tag static
+++++++++++++++++++

* En la raiz del proyecto crear carpeta llamada static.
* Crear archivo style.css:

.. code-block:: css
    :linenos:

    body{
        background: yellow;
        color: green;
    }

* En el template se vincula:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Prueba con Flask</title>
        <!-- Para añadir un archivo css utilizamos url for en una etiqueta jinja2 -->
        <link rel="stylesheet" href="{{ url_for('static', filename='style.css') }}">
    </head>
    <body>
        <h1>Plantillas Jinja2</h1>
        <p>primera toma de contacto con Flask</p>
    </body>
    </html>


Template tag de datos
+++++++++++++++++++++

Los template tags de datos muestran información que enviamos desde la vista al template.

* Si nos vamos a views.py para añadir un dato:

.. code-block:: python
    :linenos:

    from flask import Flask, render_template

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola!!!'


    @app.route('/hola')
    def saludar(): 
        nombre = "Guillermo"
        return render_template('hola.html', nombre=nombre)


    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

* Ahora que tenemos un dato, podemos mostrarlo en cualquier template de nuestra app:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <p>Hola {{nombre}}</p>
    </body>
    </html>

Template tag for
++++++++++++++++

* Se crea un listado en **main.py**:

.. code-block:: python
    :linenos: 

    from flask import Flask, render_template

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola!!!'


    @app.route('/hola')
    def saludar(): 
        personas = ["Guillermo", "Antonio", "Josefa", "Adrián"]
        return render_template('hola.html', personas=personas)


    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

* Y ahora podemos recorrer el diccionario en nuestro template con el template tag for:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <ul>
            {% for persona in personas %}
                <li>{{ persona }}</li>
            {% endfor %}
        </ul>
    </body>
    </html>

Template tag if
+++++++++++++++

Con el template tag if podemos establecer condiciones dentro de los templates, retomando el ejemplo de for vamos a pintar de verde uno de los registros:

* Template condicional que recibe un parámetro:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Prueba con Flask</title>
    </head>
    <body>
        {% if nombre %}
            <h1>Hola {{ nombre }}</h1>
        {% else %}
            <h1>Hola mundo</h1>
        {% endif %}
    </body>
    </html>

* Cargar el template y pasarle parámetro:

.. code-block:: python
    :linenos:

    from flask import Flask, render_template

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'


    @app.route('/saludos/<nombre>')
    def saludos(nombre=None):
        return render_template('saludos.html', nombre=nombre) # le pasamos el template y la variable con la clave nombre

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)

Formularios
###########

En Django podemos crear formularios individuales y reutilizables.

Formularios via POST
********************

* Se crea el archivo por ejemplo **form.html**:

.. code-block:: html 
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
    </head>
    <body>
        <form method="POST">
            <input type="text" name="nombre" placeholder="Tu nombre">
            <input type="text" name="apellidos" placeholder="Tus apellidos">
            <input type="submit" value="Saludar">
        </form>
    </body>
    </html>

* Lo siguiente es registrar las rutas en Flask:

.. code-block:: python
    :linenos: 

    from flask import Flask, render_template, redirect, url_for, request

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return redirect(url_for('saludar'))


    @app.route('/saludar', methods=['GET'])
    def saludar(): 
        return render_template('form.html')

    @app.route('/saludar', methods=['POST'])
    def saludo(): 
        nombre = request.form['nombre']
        apellidos = request.form['apellidos']
        return 'Te llamas ' + nombre + " " + apellidos


    if __name__ == "__main__":
        app.run(host='localhost', debug=True)


Recuperar archivos en Flask
***************************

De este modo se gestionaría la subida de un archivo desde un formulario:

* Crear en la raiz un directorio llamado **subidas**
* Crear en **templates** un archivo llamado **subidas.html**:

.. code-block:: html
    :linenos:

    <!DOCTYPE html>
    <html lang="es">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Prueba con Flask</title>
    </head>
    <body>
        <form method="POST" action="/subir" enctype="multipart/form-data">
            <label for="documento">Subir archivo</label>
            <br>
            <input type="file" name="documento">
            <br><br>
            <input type="submit">
        </form>
    </body>
    </html>

* Por último registrar dos rutas en **main.py**:

.. code-block:: python
    :linenos:

    from flask import Flask, render_template, request
    # añadimos también una utilidad para generar nombres seguros de archivos:
    from werkzeug.utils import secure_filename

    app = Flask(__name__)

    @app.route('/')
    def hello_workd():
        return 'Hola Mundo!!!'

    # Ruta del form:
    @app.route('/subir', methods=['GET'])
    def hola(nombre=None): 
        return render_template('subidas.html') 

    # Ruta para procesar la petición:
    @app.route('/subir', methods=['POST'])
    def subir():
        if request.method == 'POST':
            # recuperamos el archivo del parametro files:
            f = request.files['documento']
            # ahora guardamos el archivo con un nombre seguro:
            f.save('./subidas/{}'.format(secure_filename(f.filename)))
            return 'Se ha subido correctamente'

    if __name__ == "__main__":
        app.run(host='localhost', debug=True)
