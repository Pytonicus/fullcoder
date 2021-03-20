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

    ...

Insertar registros
******************

.. code-block:: python 
    :linenos:

    ...

Inserciones y actualizaciones múltiples
***************************************

.. code-block:: python 
    :linenos:

    ...

Leer registros
**************

.. code-block:: python 
    :linenos:

    ...

Borrar registros
****************

.. code-block:: python 
    :linenos:

    ...

Actualizar registros
********************

.. code:: python 

    ...