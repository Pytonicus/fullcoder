Bases de datos
==============

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Trabajando con bases de datos en Python 

.. contents:: Índice

Conexión SQLITE 3
#################

.. code-block:: python 
    :linenos:
 
    # importar modulo sqlite 3:
    import sqlite3

    # Seleccionar archivo de conexión:
    conexion = sqlite3.connect("prueba.db")

    # Realizar conexión con un cursor:
    cursor = conexion.cursor()

    # Guardar operacion:
    conexion.commit()

    # Cerar conexion:
    conexion.close()


Conexión MySQL
##############

Pasos iniciales:

* Paso x...

.. code-block:: python 
    :linenos:

    ... 

Operaciones CRUD
################

Crear base de datos
*******************

.. code-block:: python 
    :linenos:

    ...


Crear una tabla
***************

.. code-block:: python 
    :linenos:

    import sqlite3

    conexion = sqlite3.connect("prueba.db")
    cursor = conexion.cursor()

    # Crear una tabla:
    cursor.execute('CREATE TABLE usuario(nombre VARCHAR(100), edad INTEGER, email VARCHAR(100))')

    conexion.commit()

    conexion.close()

Insertar registros
******************

.. code-block:: python 
    :linenos:

    import sqlite3

    conexion = sqlite3.connect("prueba.db")
    cursor = conexion.cursor()

    # creamos una lista con varias tuplas:
    usuarios = [
        ('Luis', 20, 'luis@luiser.com'),
        ('Mira', 27, 'mira@ynomira.com'),
        ('Juan', 90, 'ju@n.com')
    ]
    # ahora podemos ejecutar la consulta que introduce varios registros a la vez:
    cursor.executemany("INSERT INTO usuario VALUES (?,?,?)", usuarios)
    conexion.commit()

    conexion.close()

Leer registros
**************

.. code-block:: python 
    :linenos:

    import sqlite3

    conexion = sqlite3.connect("prueba.db")
    cursor = conexion.cursor()

    # Realizar consulta:
    cursor.execute('SELECT * FROM usuario')
    usuarios = cursor.fetchall() # recuperamos con este metodo una lista de registros.

    print(usuarios)

    # recorremos todos los registros:
    for usuario in usuarios:
        print("Nombre: {} \nEdad: {} \nEmail: {}\n\n".format(usuario[0], usuario[1], usuario[2]))

    conexion.close()

Borrar registros
****************

.. code-block:: python 
    :linenos:

    import sqlite3

    conexion = sqlite3.connect("prueba.db")
    cursor = conexion.cursor()

    # Realizar consulta:
    cursor.execute('DELETE FROM usuario WHERE nombre="Luis"')

    conexion.commit()

    conexion.close()

Actualizar registros
********************

.. code:: python 

    import sqlite3

    conexion = sqlite3.connect("prueba.db")
    cursor = conexion.cursor()

    # Realizar consulta:
    cursor.execute('UPDATE usuario SET nombre="Alberto" WHERE nombre="Juan"')

    conexion.commit()

    conexion.close()