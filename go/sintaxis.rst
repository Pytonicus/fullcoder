Sintaxis GO
===========

.. image:: /logos/logo-go.png
    :scale: 30%
    :alt: Logo GO
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Sintáxis básica de GO
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################

Instalación
***********
* Instalación: ``sudo apt install golang``
* Extensión de archivos: **.go**

Comentarios
***********

* Comentarios de una sola línea: 

.. code-block:: GO
    :linenos:
 
    // Esto es un comentario de una línea

* Comentarios multilínea:

.. code-block:: GO
    :linenos:

    /*
    Comentarios de 
    tipo multilínea 
    */

Entrada y salida estandar
*************************
Datos de entrada y salida a través de la consola y/o el navegador.

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        // declarar valor entrada:
        var edad int

        // salida estandar:
        fmt.Print("¿Qué edad tienes?: ")
        
        // entrada estandar:
        fmt.Scan(&edad)

        // impresión con salto de línea:
        fmt.Println("Tienes", edad, "años")

        // Introducir múltiples valores:
        var nombre, apellidoUno, apellidoDos string

        fmt.Print("¿Cómo te llamas?: ")
        fmt.Scanf("%v %v %v", &nombre, &apellidoUno, &apellidoDos)

        fmt.Printf("Te llamas %v %v %v", nombre, apellidoUno, apellidoDos)
    }

Estructura en GO
*****************

* Código GO puro:

.. code-block:: GO
    :linenos:

    package main

    import "fmt"

    // Función principal:
    func main(){
        // imprimir un saludo:
        fmt.Println("Hola a full!")
    }


Concatenación
*************
Concatenación de variables y cadenas se realiza con **+**

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        nombre := "Guillermo"

        // concatenar:
        fmt.Println("Me llamo " + nombre)

        // se puede ir agregando variables y dejará espacios:
	    fmt.Println("Hola", "amigo mío, tienes", 33, "años")

        // impresión usando verbos:
        nombre := "Guillermo"
        apellidos := "Granados Gómez"
        edad := 33

        // cada %v devolverá el valor de una variable según el orden:
        fmt.Printf("Te llamas %v %v y tienes %v años", nombre, apellidos, edad)
    }

GO-CLI - Comandos de GO
***********************

Comandos de GO:

* go version: versión de go instalada.
* go build: se ejecuta en la raiz del proyecto para generar un ejecutable.
* go build archivo.go: genera un ejecutable de un script.
* GOOS=windows GOARCH=386 go build archivo.go: genera un ejecutable para otro sistema.
* go run archivo.go: ejecuta un script de go.
* godoc: Abre un servidor web en la dirección http://localhost:6000
* go get: permite descargar bibliotecas y utilidades de terceros.
* go mod: permite gestionar los proyectos locales.

Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        // declaración, que se puede hacer así o de una vez:
        var otroTexto string
        otroTexto = "Soy otra cadena"
        var numero int = -15
        var numeroSinSimbolo uint = 15
        var decimal float32 = 2.35
        var decimalLargo float64 = 32.23423423
        var booleano bool = true


        // declaracion con operador de inicialización:
        texto := "Cadena de texto \n - separada por una línea"

        fmt.Println(otroTexto)
    }

.. attention::
    Las variables declaradas deben usarse o dará error a la hora de compilar. Se recomienda también declarar en la medida de lo posible usando el operador :=

* Constantes:

.. code-block:: GO
    :linenos:

    package main

    import "fmt"

    func main(){
        // definición de constante:
        const PI = 3.1416
        fmt.Println(PI)

        // definir múltiples constantes:
        const (
            nombre = "Guillermo"
            apellidos = "Granados Gómez"
            edad = 33
        )
        fmt.Print(edad)
    }

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        suma := 2 + 2
        resta := 2 - 2
        multiplicacion := 2 * 2
        division := 2 / 2
        resto := 2 % 2
    }

* Incremento y decremento:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        numero := 5

        // incremento y decremento:
        numero++
        ++numero
        numero--
        --numero
    }

* Asignar operación:

.. code-block:: GO 
    :linenos:

        package main

    import "fmt"

    func main(){
        numero := 5

        numero += 10
        numero -= 11
        numero *= 2
        numero /= 7
        numero %= 2
    }
    

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

* and: **&&**.
* or: **||**.
* not: **!**.

Estructuras de control
######################

Condicional if
**************

* if sencillo:

.. code-block:: GO 
    :linenos:

    ...

* if / else:

.. code-block:: GO 
    :linenos:

    ...

* else-if:

.. code-block:: GO 
    :linenos:

    ...

* if alternativo:

.. code-block:: GO 
    :linenos:

    ...

* Operador ternario:

.. code-block:: GO 
    :linenos:

    ...

Condicional Switch
******************
Estructura de un switch:

.. code-block:: GO 
    :linenos:

    ...

Bucle for
*********

* for básico:

.. code-block:: GO 
    :linenos:

    ...

* foreach:

.. code-block:: GO 
    :linenos:

    ...

* foreach clave / valor:

.. code-block:: GO 
    :linenos:

    ...

Bucle while
***********

* While sencillo:

.. code-block:: GO 
    :linenos:

    ...

* do-while:

.. code-block:: GO 
    :linenos:

    ...

Tipos de datos avanzados
########################

Arrays
******

- Declaración tradicional:

.. code-block:: GO 
    :linenos:

    ...

- Declaración con función array():

.. code-block:: GO 
    :linenos:

    ...

- Array multidimensional:

.. code-block:: GO 
    :linenos:

    ...

* Imprimir y asignar valores:

.. code-block:: GO 
    :linenos:

    ...

Arrays asociativos
******************

- Declaración tradicional:

.. code-block:: GO 
    :linenos:

    ...

- Declaración con función array():

.. code-block:: GO 
    :linenos:

    ...

- Array multidimensional:

.. code-block:: GO 
    :linenos:

    ...

- Imprimir y asignar valores:

.. code-block:: GO 
    :linenos:

    ...

Control de errores
##################

.. code-block:: GO
    :linenos:

    ...

Programación modular
####################

Funciones
*********

* Procedimienos:

.. code-block:: GO 
    :linenos:

    ...

* funciones:

.. code-block:: GO 
    :linenos:

    ...

* uso de parámetros:

.. code-block:: GO 
    :linenos:

    ...

* Funciones anónimas:

.. code-block:: GO 
    :linenos:

    ...

* Ámbito global:

.. code-block:: GO 
    :linenos:

    ...

Programación orientada a objetos
################################

Los elementos de una clase se definen con ámbito **public**, **private** y **protected**. 
Adicionalmente se puede agregar el modificador **static** para poder acceder a los atributos y métodos sin crear un objeto.

Clases y objetos
****************

* Estructura clase:

.. code-block:: GO 
    :linenos:

    ...


* Constructor:

.. code-block:: GO 
    :linenos:

    ...

* Get y Set:

.. code-block:: GO 
    :linenos:

    ...

* Herencia:

.. code-block:: GO 
    :linenos:

    ...

Clases abstractas y resolución de ámbito
****************************************

- uso de clases no instanciables:

.. code-block:: GO 
    :linenos:

    ...

Interfaces
**********

.. code-block:: GO 
    :linenos:

    ...

Importar y exportar
###################

include y require
*****************

* Importar archivos GO:

.. code-block:: GO 
    :linenos:

    ...

Namespace
*********

* Exportar (videojuegos.GO):

    .. code-block:: GO 
        :linenos:

        ...
    
    * Importar namespace (index.GO):

    .. code-block:: GO 
        :linenos:

        ...