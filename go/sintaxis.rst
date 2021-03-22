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

    package main

    import "fmt"

    func main() {
        var edad int

        fmt.Print("¿Qué edad tienes? \n>>> ")
        fmt.Scan(&edad)

        if edad >= 18 {
            fmt.Println("Eres mayor de edad")
        }
    }


* if / else:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        var edad int

        fmt.Print("¿Qué edad tienes? \n>>> ")
        fmt.Scan(&edad)

        if edad >= 18 {
            fmt.Println("Eres mayor de edad")
        } else {
            fmt.Println("Todavía eres menor de edad")
        }
    }


* else-if:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        var edad int

        fmt.Print("¿Qué edad tienes? \n>>> ")
        fmt.Scan(&edad)

        if edad >= 65 {
            fmt.Println("Eres un anciano")
        } else if edad >= 18 {
            fmt.Println("Eres mayor de edad")
        } else {
            fmt.Println("Todavía eres menor de edad")
        }
    }


Condicional Switch
******************
Estructura de un switch:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        var operacion string

        fmt.Print("¿Qué quieres saber? \n>>> ")
        fmt.Scan(&operacion)

        switch operacion {
        case "nombre":
            fmt.Println("Me llamo Guillermo")
        case "apellidos":
            fmt.Println("Mis apellidos son Granados Gómez")
        case "edad":
            fmt.Println("Tengo 33 años")
        default:
            fmt.Println("No reconozco el comando...")
        }
    }

.. attention::
    Se pueden validar más de un valor en case añadiéndolos con comas: **case 'a','e','i','o','u'**

Bucle for
*********

* for básico:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {

        for i := 0; i <= 10; i++ {
            fmt.Println("Repetición nº", i)
        }
    }

* for condicional:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        num := 0

        for num <= 10 {
            num++
            fmt.Println("Se ha sumado el número, su valor actual es:", num)
        }
    }

* for infinito:

.. code-block:: GO
    :linenos:

    package main

    import "fmt"

    func main() {
        var repetir string

        repeticion := 0

        for {
            repeticion++

            fmt.Println("Repetición nº", repeticion)

            fmt.Print("¿Repetir otra vez? (s/n): ")
            fmt.Scan(&repetir)

            if repetir == "n" {
                break
            }
        }
    }

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
No existe el bucle While en GO, lo más párecido a esta estructura de control es el for condicional o el for infinito.

Punteros
########

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        // un puntero se define con un asterisco:
        var num *int

        numero := 5

        // hacer que el apuntador no apunte a nada con nil:
        num = nil

        // apuntar el puntero a una variable:
        num = &numero

        fmt.Println("El identificador del puntero es:", num)
        fmt.Println("El valor apuntado es:", *num)
    }


Tipos de datos avanzados
########################

Arrays
******

- Declaración tradicional:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main() {
        // dclaración de array con tipo definido:
        var array [5]int
        array[2] = 7
        fmt.Println(array[2])

        // asignar valores al array:

        // asignación directa:
        array2 := [3]string{"Paco", "Pepe", "Adolfo"}
        fmt.Println(array2[2])

        // array de tamaño dinámico:
        array3 := [...]string{"Galletas", "Fresas", "Aceite", "Tomates"}
        fmt.Println(array3[2])
    }


- Array multidimensional:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    func main(){
        // declarar array multidimensional:
        var arrayMulti [4][4]int

        // asignar un valor a una posición:
        arrayMulti[2][1] = 11

        // utilizar el valor asignado:
        fmt.Println(arrayMulti[2][1])
    }

ME QUEDÉ EN LAS PORCIONES
#########################

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

    package main

    import "fmt"

    // declarar una función:
    func saludar() {
        fmt.Println("Saludo desde función")
    }

    func main() {
        // utilizar una función:
        saludar()
    }


* funciones:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    // las funciones retornan un valor que se debe definir:
    func saludar() string {
        return "Saludo desde función"
    }

    func main() {

        // utilizar una función:
        fmt.Println(saludar())
    }


* uso de parámetros:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    // los parametros se reciben con un valor definido::
    func saludar(nombre string) string {
        saludo := "Hola " + nombre
        return saludo
    }

    func main() {

        // pasar un parámetro:
        fmt.Println(saludar("Guillermo"))
    }


* Retorno múltiple:

.. code-block:: GO 
    :linenos:

    package main

    package main

    import "fmt"

    // se define entre parentesis el tipo de devolución de varios valores:
    func nombreCompleto(nombre string, apellidos string) (string, string) {
        // se devuelven dos valores:
        return nombre, apellidos
    }

    func main() {
        // asignamos los valores a las variables:
        n, m := nombreCompleto("Guillermo", "Granados Gómez")

        // asignar un elemento con retorno múltiple:
        soloNombre, _ := nombreCompleto("Guillermo", "Granados Gómez")

        fmt.Println("Me llamo", n, m)
        fmt.Println("Solo mi nombre es:", soloNombre)
    }

* Funciones anónimas:

.. code-block:: GO 
    :linenos:

    package main

    import "fmt"

    // se crea la función:
    func sumar(a, b int) int {
        return a + b
    }

    func main() {
        // se crea una variable con las caracteristicas de la función:
        var operacion func(int, int) int

        // y se asigna la función anterior a la declaración anterior:
        operacion = sumar

        fmt.Println(operacion(20, 15))
    }

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