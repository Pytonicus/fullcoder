Análisis de datos
=================

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Análisis de datos con diferentes tecnologías

.. contents:: Índice

Anaconda 
########
* Para instalar Anaconda primero instalamos: ``sudo apt-get install libgl1-mesa-glx libegl1-mesa libxrandr2 libxrandr2 libxss1 libxcursor1 libxcomposite1 libasound2 libxi6 libxtst6``
* Vamos a https://www.anaconda.com/products/individual#Downloads descargamos e instalamos.
* Tras la instalación nos preguntará "Do you wish the installer to initialize Anaconda3
by running conda init?" -> decimos yes.
* Cerramos la terminal para que se actualicen los cambios.
* Ejecutamos en terminal: ``anaconda-navigator``
* Abrimos Jupyter y podemos trabajar con un cuaderno nuevo.

Pandas
######
Pandas es la librería para trabajar con DataFrames.

* Comprobar versión:

.. code-block:: python
    :linenos:

    # Se importa pandas como pd:
    import pandas as pd 

    # de pd se irá ejecutando las distintas funciones:
    pd.show_versions() # como ver la versión a detalle.


DataFrames
**********
Los dataframes son conjuntos de datos ordenados por filas y columnas:


Crear un DataFrame a partir de Listado de objetos
+++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    # Creamos un listado con varios diccionarios:
    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    # Con esta función se crea un dataframe:
    pd.DataFrame(amigos)

.. info::
    Pandas asocia las keys de cada diccionario como título de columna y cada diccionario es una fila en el DataFrame 

Crear un DataFrame a partir de archivo CSV
++++++++++++++++++++++++++++++++++++++++++

* Tenemos el siguiente archivo CSV llamado amigos.csv:

.. code:: 

    nombre,apellidos
    Alfredo,Ramirez Alberti
    Laura,Plutarco Pitágoras
    Ernesto,Granada Aferez

* Lo leemos con Pandas y este lo convierte a DataFrame:

.. code-block:: python
    :linenos:

    import pandas as pd 

    # Ejecutamos la lectura del csv:
    pd.read_csv(r'amigos.csv')

.. note::
    Se puede saltar filas añadiendo el parametro skiprows y el valor que queramos 
    pd.read_csv(r'amigos.csv', skiprows=3), esto vale para el resto de funciones read_*.

Ver información del DataFrame
+++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # mostrará una información detallada:
    tabla_amigos.info()

Averiguar dimensión dataframe
+++++++++++++++++++++++++++++
Para averiguar la dimensión de un dataframe:

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    # Se guarda el dataframe:
    tabla_amigos = pd.DataFrame(amigos)

    # Y ahora podemos medir su tamaño:
    tabla_amigos.shape

Esto devuelve 3 filas y 2 columnas.

Ver los primeros registros
++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # ver los 5 primeros:
    tabla_amigos.head()

    # ver los primeros que queramos:
    tabla_amigos.head(100)

Ver los últimos registros
+++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # ver los 5 últimos:
    tabla_amigos.tail()

    # ver los últimos que queramos:
    tabla_amigos.tail(25)

Ordenar Registros
+++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Ordenar los registros:
    tabla_amigos.sort_values(by=['nombre'])

    # Ordenar por varios criterios y en orden descendente:
    tabla_amigos.sort_values(by=['apellidos', 'nombre'], ascending=False)

Buscar registros por un valor 
+++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    # Recuperar todos los registros con el nombre alfredo:
    tabla_amigos[tabla_amigos['nombre'] == 'Alfredo']

Buscar registros por multiples valores 
++++++++++++++++++++++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    # Recuperar todos los registros con el nombre alfredo:
    tabla_amigos[(tabla_amigos['nombre'] == 'Alfredo') & (tabla_amigos['apellidos'] == 'Ramirez Alberti')]

Series
******
Las series son definidas en el DataFrame como las columnas de una tabla.

* Si queremos acceder a una columna:

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    # Se guarda el dataframe:
    tabla_amigos = pd.DataFrame(amigos)

    # se llama a la serie:
    tabla_amigos['nombre']

    # también se puede hacer con notación de punto:
    tabla_amigos.apellidos

    # O las series que queramos a la vez:
    tabla_amigos[['nombre','apellidos']]

Contar registros
++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Hará un desglose de cuantas veces se repite cada elemento en una Serie:
    tabla_amigos['nombre'].value_counts()

Ordenar Series
++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Ordenará una serie de datos:
    tabla_amigos['nombre'].sort_values()

Indexación booleana
+++++++++++++++++++

.. code-block:: python
    :linenos:

    import pandas as pd 

    amigos = [
        {'nombre': 'Alfredo', 'apellidos': 'Ramirez Alberti'},
        {'nombre': 'Laura', 'apellidos': 'Plutarco Pitágoras'},
        {'nombre': 'Ernesto', 'apellidos': 'Granada Aferez'}
    ]

    tabla_amigos = pd.DataFrame(amigos)

    # Mostrará la posición de la serie junto a True o False si coincide el valor buscado:
    tabla_amigos['nombre'] == 'Alfredo'

Gráficos
********

.. code-block:: python
    :linenos:

    import pandas as pd 

    .. buscar ejemplos