Sintaxis Python
===============

.. image:: /logos/logo-python.png
    :scale: 25%
    :alt: Logo Python 
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Sintáxis básica de Python 3.8
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################
  
Instalación
***********
* Instalación: ``sudo apt install python3``
* Extensión de archivos: **.py**
 
Comentarios
***********

* Comentarios de una sola línea: 

.. code-block:: python
    :linenos:
 
    # Comentario de una sola línea

* Comentarios multilínea:

.. code-block:: python
    :linenos:

    """
    Este comentario 
    tiene más de una línea.
    Puede servir para escribir
    un manual u otras cosas.
    """

Entrada y salida estandar
*************************
 
.. code-block:: python 
    :linenos:

    # entrada estandar:
    dato = input('introduce un dato: ')

    # salida estandar:
    print(dato)

    # salida en una sola línea:
    for i in range(1,11):
        print("{}...".format(i), end="") 

Estructura en python
********************

.. code-block:: python
    :linenos:

    import random

    numero_aleatorio = random.randint(1, 20)

    print(numero_aleatorio)

.. attention::
    En Python no se hace uso de llaves ni de ; final

Concatenación
*************
Concatenación de variables y cadenas se realiza con **+**

.. code-block:: python 
    :linenos:

    # concatenación con +
    print("cadena concatenada a " + "otra cadena")

    variable = "Pepe"
    print("resultado en variable: " + variable)

    # usando format para colocar variables:
    nombre = "Guillermo"
    apellidos = "Granados Gómez"
    print("Me llamo {} y mis apellidos son {}.".format(nombre, apellidos))

Python-CLI - Comandos de python
*******************************

Comandos de python y pip:

* python3: abre la consola de python y con exit() se puede cerrar.
* python3 --version: versión usada
* python3 archivo.py: ejecuta un script python.

Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: python 
    :linenos:

    cadena = "Cadena de texto"
    entero = 27
    decimal = 23.27
    booleano = True # False
    lista = ['datos', 2, 3.2, False]
    tupla = ('dato uno', 2)
    diccionario = {
        'nombre': 'Pepe',
        'telefono': 753283723
    }

* Constantes:

.. code-block:: python
    :linenos:

    CONSTANTE = "soy una presunta constante"

.. attention:
    Las constantes no existen como tales en Python, pero si se utiliza la convención de declararlas en mayúsculas para recordar que es un dato que no debería ser mutable.

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: python 
    :linenos:

    sumar = 3 + 6
    restar = 7 * 9
    multiplicar = 11 * 6
    dividir = 13 / 20
    resto = 54 % 7
    potencia = 3 ** 5

* Asignar operación:

.. code-block:: python 
    :linenos:

    # la variable debe tener un valor asignado:
    resultado = 0

    resultado += 12
    resultado -= 16
    resultado *= 19
    resultado /= 6
    resultado **= 5

Operadores relacionales
***********************
Validación entre dos números.

* Mayor que: **>**.
* Menor que: **<**.
* Mayor o igual que: **>=**.
* Menor o igual que: **<=**.
* Igual que: **==**.

Operadores lógicos
******************
Expresiones de operaciones lógicas.

* and: **and**.
* or: **or**.
* not: **!**.

Estructuras de control
######################

Condicional if
**************

* if sencillo:

.. code-block:: python 
    :linenos:

    edad = 18;

    if edad >= 18:
        print("Eres mayor de edad")

* if / else:

.. code-block:: python 
    :linenos:

    edad = 15

    if edad >= 18:
        print("Eres mayor de edad")
    else:
        print("Eres menor de edad")

* else-if:

.. code-block:: python 
    :linenos:

    edad = 45

    if edad >= 65 :
        print("Eres un anciano")

    elif edad >= 18:
        print("Eres mayor de edad")
    else:
        print("Eres menor de edad")

* Operador ternario:

.. code-block:: python 
    :linenos:

    edad = int(input("Introduce tu edad: "))
    print("eres mayor de edad") if (edad >= 18) else print("Todavía eres menor de edad")


Condicional Switch
******************
No existe el condicional Switch en Python, su alternativa es usar **if-elif-else**

Bucle for
*********

* for básico:

.. code-block:: python 
    :linenos:

    for i in range(1,10):
        print("Repetición nº {} \n".format(i))

* for clave / valor:

.. code-block:: python 
    :linenos:

    electrodomesticos = {
        "producto": "Nevera",
        "modelo": "FX27",
        "marca": "Fagor",
        "precio": 783.23
    }

    for key, value in electrodomesticos.items():
        print("{}: {} \n".format(key, value))

Bucle while
***********

* While sencillo:

.. code-block:: python 
    :linenos:

    num = 0

    while num < 10:
        print("código de mensaje - {}".format(num))
        num += 1

* While infinito:

.. code-block:: python 
    :linenos:

    numero = 10
    # al añadir True hacemos un bucle infinito:
    while True:
        adivina = int(input('Adivinia el número >> '))

        if adivina == numero:
            print('Acertaste!')
            # Con exit() finalizamos el programa
            exit()

        print('Fallaste!')

Detener secuenda de script
**************************

.. code-block:: python
    :linenos:

    for i in range(10):
        if(i == 5):
            print("Ya has llegado a 5 y no irás más lejos")
            exit()

    print("Esta frase no se mostrará")

Tipos de datos avanzados
########################

Listas
******

.. code-block:: python 
    :linenos:

    lista = ["cadena", 20, 18.27, False, ["otra cadena", 23, 18.77]]

    # asignación:
    lista[3] = "Morcilla"

    # impresión:
    print(lista[3])

Tuplas
******

.. code-block:: python 
    :linenos:

    tupla = ("cadena", 20, 18.27, False, ["otra cadena", 23, 18.77])
    
    # impresión
    print(tupla[2])

.. attention:: 
    Las tuplas son inmutables por lo tanto no se pueden asignar valores

Diccionarios
************

.. code-block:: python 
    :linenos:

    operadores = [
        {"suma": "+"},
        {"resta": "-"},
        {"multiplicación": "*"},
        {"división": "/"},
        {"resto": "%"},
        {"potencia": "**"}
    ]

    # ejemplo recorrido en listado de diccionarios:
    for operador in operadores:
        for key, value in operador.items():
            print("{}: {}".format(key, value))

    # asignación:
    operadores[0]["suma"] = "Sumar"

    # impresión: 
    print(operadores[0]["suma"])

Control de errores
##################

.. code-block:: python
    :linenos:

    try:
        print(nombre)
    except NameError:
        print('No has escrito un nombre')


Programación modular
####################

Funciones
*********

* Procedimienos:

.. code-block:: python 
    :linenos:

    def saludar():
        print("Hola persona")

    saludar()

* funciones:

.. code-block:: python 
    :linenos:

    def saludar():
        return "Hola persona"

    print(saludar())

* uso de parámetros:

.. code-block:: python 
    :linenos:

    def saludar(nombre):
        return "Hola {}".format(nombre)

    print(saludar("Antonio"))

* Funciones anónimas:

.. code-block:: python 
    :linenos:

    tu_nombre = lambda nombre: "Hola {}".format(nombre)

    print(tu_nombre("Gabriel"))

* Ámbito global:

.. code-block:: python 
    :linenos:

    nombre = "Alberto"

    def saludar():
        return "¿Qué tal {}?".format(nombre)

    print(saludar())

.. note:: 
    Las variables en Python son por lo general de ámbito global

Programación orientada a objetos
################################

El ámbito de atributos y métodos de una clase en Python son globales.

Clases y objetos
****************

* Estructura clase:

.. code-block:: python 
    :linenos:

    class Videoconsola():
        # atributos:
        modelo = "Mega Drive"
        marca = "Sega"

        # los métodos reciben siempre self para hacer uso de los atributos de la clase:
        def descripcion(self):
            print("Es una {} {}".format(self.marca, self.modelo))


    # crear objeto:
    megaDrive = Videoconsola()

    # recuperar atributo:
    print(megaDrive.marca)

    # recuperar métodos:
    megaDrive.descripcion()


* Constructor:

.. code-block:: python 
    :linenos:

    class Videoconsola():
        # atributos:
        modelo = "Mega Drive"
        marca = "Sega"

        # El constructor recibe self y los parámetros que se pasan por el constructor:
        def __init__(self, modelo, marca):
            self.modelo = modelo 
            self.marca = marca

        def descripcion(self):
            print("Es una {} {}".format(self.marca, self.modelo))


    # crear objeto y pasar parámetros al constructor:
    megaDrive = Videoconsola("MegaDrive", "Sega")

    print(megaDrive.marca)

    megaDrive.descripcion()

* Herencia:

.. code-block:: python 
    :linenos:

    class Persona():
        nombre = ""
        genero = ""
        peso = 0
        estatura = 0

        def __init__(self):
            self.nombre = "Alfredo"
            self.genero = "Masculino"
            self.peso = 82
            self.estatura = 174

        def datos(self):
            print("Su nombre es {}, su género {}, pesa {} kilos y mide {}.".format(self.nombre, self.genero, self.peso, self.estatura))


    class Luis(Persona):
        def __init__(self):
            self.nombre = "Luis"
            self.genero = "Masculino"
            self.peso = 79
            self.estatura = 158

    luis = Luis()
    # y podemos acceder a los metodos del padre como a sus atributos:
    luis.datos()

Clases abstractas
*****************
Es posible trabajar con clases abstactas gracias a la librería **abc**

.. code-block:: python
    :linenos:

    # se importa la librería para abstracciones:
    from abc import ABC, abstractmethod

    # se le indica a la clase que es abstracta con abc:
    class Videoconsola(ABC):
        modelo = "Super Nintendo"
        marca = ""

        def __init__(self, modelo, marca):
            self.modelo = modelo
            self.marca = marca

            print("Se ha creado el objeto")

        def juegos():
            print("La consola dispone de alrededor de 700 títulos")


        # las funciones abstractas se deben usar obligatoriamente en la clase hija:
        # Utilizan un decorador de abc:
        @abstractmethod
        def precio():
            """ Texto convencional: este método muestra el precio """
            pass

    # clase a partir de clase abstracta:
    class SuperNintendo(Videoconsola):
        def __init__(self):
            self.modelo = "SNES"
            self.marca = "Nintendo"


        def precio(self):
            print("La consola cuesta 200 €")



    # uso de clase hija:
    superNintendo = SuperNintendo()
    print(superNintendo.modelo)

    superNintendo.precio()

    # Desestructuración de métodos:
    Videoconsola.juegos()


Interfaces
**********
Las interfaces como tales no existen en python pero hay un modo de trabajar de forma similar

.. code-block:: python 
    :linenos:

    class VideoconsolaInterface():
        # En una supuesta interfaz creamos los métodos y le pasamos el valor pass para dejarlos vacíos:
        def descripcion():
            """ Muestra una descripción de la consola """
            pass


    class NeoGeo(VideoconsolaInterface):
        modelo = ""
        marca = ""
        precio = ""

        def __init__(self, modelo, marca, precio):
            self.modelo = modelo
            self.marca = marca
            self.precio = precio
            print(self.precio)

        def descripcion(self):
            print("Es la consola de {} {}".format(self.modelo, self.marca))


    neoGeo = NeoGeo("Neo Geo Pocket", "SNK", "149.99")
    neoGeo.descripcion()

Importar y exportar
###################

Módulos y paquetes
******************
Podemos crear nuestros propios módulos en python para cortar partes del código específicas:

* Lo primero es crear un nuevo archivo.py y guardar ahí por ejemplo una clase.
* Luego creamos un segundo archivo que será el principal.py y para importarlo basta con escribir ``import archivo`` al comienzo del proyecto.

Si lo que queremos es guardar el módulo en una carpeta entonces estamos hablando de un Paquete:

* Los paquetes son archivos.py que guardamos en una carpeta.
* Dentro de esa carpeta creamos siempre un archivo llamado ``__init__.py`` para que el interprete lo considere un paquete.
* Luego en el archivo principal.py lo importamos con la línea ``from carpeta import archivo``

Y para poner un alias a un paquete o módulo de python ya sea estandar o personalizado utilizamos ``as``:

.. code-block:: python

    from carpeta import archivo as traductor