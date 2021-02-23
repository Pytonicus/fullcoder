Sintaxis C#
===========

.. image:: /logos/logo-csharp.png
    :scale: 80% 
    :alt: Logo C#
    :align: center

.. |date| date::
.. |time| date:: %H:%M


Sintáxis básica de C#
  
.. contents:: Índice

Elementos básicos del lenguaje 
##############################

Instalación
***********
* Instalación: Mediante Visual Studio o Unity.

* Instalación Visual Studio 2019:
    * Descargamos la versión comunity
    * En carga de trabajo seleccionamos Desarrollo de escritorio de .NET y Desarrollo de la plataforma universal de Windows
    * En la siguiente pestaña de componentes individuales seleccionamos la opción Herramientas de LINQ to SQL

* Extensión de archivos: **.cs**

Comentarios
***********

.. code-block:: C#
    :linenos:
 
    // comentario de una línea 

    /* Comentario 
    multilínea */

    /// <summary>
    /// Comentario de documentación XML </summary>

Entrada y salida estandar
*************************
Datos de entrada y salida a través de la consola y/o el navegador.


* Uso de la clase Console:

.. code-block:: C# 
    :linenos:

    static void Main(string[] args)
        {
            // Salida en consola:
            Console.Write("Mensaje - ");

            // Imprimir y saltar de línea:
            Console.WriteLine("Introduce un valor: ");

            // Leer valor y lo guarda en formato string:
            Console.Write("Escribe tu nombre: ");
            string leerOtroValor = Console.ReadLine();
            Console.WriteLine("Te llamas {0}", leerOtroValor);

            // Leer valor de consola y guardar en variable en formato ASCII:
            int leerValor = Console.Read();
            Console.WriteLine("El valor introducido es: {0}", leerValor);

            // Toma un solo caracter:
            Console.ReadKey();
        }

Estructura en C#
*****************

* Crear proyecto: Abrimos VS y pinchamos en Crear un proyecto, luego elegimos Aplicación de consola (.NET Framework o la opción .NET Core si no esta la primera), cambiamos el nombre del proyecto y creamos.

* Código C# puro:

.. code-block:: C#
    :linenos:

    using System;

    namespace HolaMundo
    {
        class Program
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hola FullCoder!");
            }
        }
    }

Concatenación
*************
Concatenación de variables y cadenas se realiza con **+**

.. code-block:: C# 
    :linenos:

    static void Main(string[] args)
        {
            string nombre = "Guillermo";
            int edad = 33;

            // uso de +:
            Console.WriteLine("Me llamo " + nombre + " y tengo " + edad + " años");

            // uso de template:
            Console.WriteLine("Me llamo {0} y tengo {1} años.", nombre, edad);

            Console.ReadKey();
        }
    

C#-CLI - Comandos de C#
***********************
Al trabajar con C# es poco probable el uso de CLI, así que por ahora se omitirá este apartado.

Variables y tipos de datos
##########################

* Declaración, asignación y tipo:

.. code-block:: C# 
    :linenos:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;

    namespace Tipos
    {
        class Program
        {
            static void Main(string[] args)
            {
                // declaración:
                int numero;


                // asignación de valores:
                int numeroEntero = 10;
                double comaFlotante = 2.832;
                float otroFlotante = 3.2f;
                string cadena = "cadena de texto";
                bool interruptor = true;

                // Impresión de valores::
                Console.WriteLine("Valor del número: " + numeroEntero);

                // dejamos el read abierto para que no se cierre la consola:
                Console.Read();
            }
        }
    }


* Constantes:

.. code-block:: C#
    :linenos:

    class Program
    {
        // se declara usando const y además se añade el tipo:
        const int fechaNacimiento = 1987;
        static void Main(string[] args)
        {
            Console.WriteLine(fechaNacimiento);
            Console.Read();
        }
    }

Operadores
##########

Operadores aritméticos
**********************

* Operaciones aritméticas:

.. code-block:: C# 
    :linenos:

    static void Main(string[] args)
        {
            int operacion;

            int sumar = 2 + 2;
            int restar = 2 - 2;
            int multiplicar = 3 + 5;
            int dividir = 2 / 2;
            int resto = 2 % 1;
        }

* Incremento y decremento:

.. code-block:: C# 
    :linenos:

    static void Main(string[] args)
        {
            int valor = 10;

            valor = valor++;
            valor = ++valor;
            valor = valor--;
            valor = --valor;
        }

* Asignar operación:

.. code-block:: C# 
    :linenos:

    static void Main(string[] args)
        {
            int valor = 10;

            valor += 10;
            valor -= 5;
            valor *= 22;
            valor /= 11;
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

.. code-block:: C# 
    :linenos:

    ...

* if / else:

.. code-block:: C# 
    :linenos:

    ...

* else-if:

.. code-block:: C# 
    :linenos:

    ...

* if alternativo:

.. code-block:: C# 
    :linenos:

    ...

* Operador ternario:

.. code-block:: C# 
    :linenos:

    ...

Condicional Switch
******************
Estructura de un switch:

.. code-block:: C# 
    :linenos:

    ...

Bucle for
*********

* for básico:

.. code-block:: C# 
    :linenos:

    ...

* foreach:

.. code-block:: C# 
    :linenos:

    ...

* foreach clave / valor:

.. code-block:: C# 
    :linenos:

    ...

Bucle while
***********

* While sencillo:

.. code-block:: C# 
    :linenos:

    ...

* do-while:

.. code-block:: C# 
    :linenos:

    ...

Punteros
########

.. code-block:: GO 
    :linenos:

    ...

Tipos de datos avanzados
########################

Arrays
******

- Declaración tradicional:

.. code-block:: C# 
    :linenos:

    ...

- Declaración con función array():

.. code-block:: C# 
    :linenos:

    ...

- Array multidimensional:

.. code-block:: C# 
    :linenos:

    ...

* Imprimir y asignar valores:

.. code-block:: C# 
    :linenos:

    ...

Arrays asociativos
******************

- Declaración tradicional:

.. code-block:: C# 
    :linenos:

    ...

- Declaración con función array():

.. code-block:: C# 
    :linenos:

    ...

- Array multidimensional:

.. code-block:: C# 
    :linenos:

    ...

- Imprimir y asignar valores:

.. code-block:: C# 
    :linenos:

    ...

Control de errores
##################

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Por favor introduce un número: ");
            string num = Console.ReadLine();
            // vamos a evitar caracteres no válidos:
            try
            {
                // convertimos el resultado a entero, de modo que si se introduce una letra habrá una excepción:
                int resultado = int.Parse(num);
                Console.WriteLine("El valor es: " + resultado);
            }
            catch (Exception)
            {
                Console.WriteLine("El valor introducido no es un número.");
            }
            Console.Read();
        }
    }

Programación modular
####################
El paradigma de programación de C# es POO, sin embargo es interesante ver en esta sección como crear métodos y llamarlos desde Main.

Métodos
*******

* Método void:

.. code-block:: C# 
    :linenos:

    class Program
    {
        // En la clase principal existe un método principal:
        static void Main(string[] args)
        {
            // ejecutamos el método:
            Mensaje(); // para poder llamarlo debe tener acceso static
            Console.Read(); 
        }

        // este es un método que no devuelve nada (void):
        public static void Mensaje()
        {
            Console.WriteLine("Este método devuelve un mensaje");
        }
    }

* uso de parámetros:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            // pasamos los parámetros:
            Sumar(10, 15); 
            Console.Read(); 
        }

        // se define el tipo de parámetro:
        public static void Sumar(int numUno, int numDos)
        {
            int resultado = numUno + numDos;
            Console.WriteLine("El resultado de {0} + {1} es: {2}", numUno, numDos, resultado);
        }
    }

* retorno de valores:

.. code-block:: C# 
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            // Guardamos la operación en una variable:
            string resultado = Sumar(12, 26);

            Console.WriteLine(resultado);
            Console.Read(); 
        }

        // Se utiliza string en lugar de void para devolver una cadena:
        public static string Sumar(int numUno, int numDos)
        {
            int resultado = numUno + numDos;
            // usamos return y aprovechamos el String.Format en este caso:
            return String.Format("El resultado de {0} + {1} es: {2}", numUno, numDos, resultado);
        }
    }

* Ámbito global o atributos estáticos:

.. code-block:: C# 
    :linenos:

    class Program
    {
        // Los atributos declarados estáticos podemos usarlos en Main:
        public static int num1;
        public static int num2;
        static void Main(string[] args)
        {
            // asignamos valores y usamos con el método Sumar:
            num1 = 10;
            num2 = 73;
            string resultado = Sumar(num1, num2);

            Console.WriteLine(resultado);
            Console.Read(); 
        }

        public static string Sumar(int numUno, int numDos)
        {
            int resultado = numUno + numDos;
            return String.Format("El resultado de {0} + {1} es: {2}", numUno, numDos, resultado);
        }
    }

Programación orientada a objetos
################################

Los elementos de una clase se definen con ámbito **public**, **private** y **protected**. 
Adicionalmente se puede agregar el modificador **static** para poder acceder a los atributos y métodos sin crear un objeto.

Clases y objetos
****************

* Estructura clase:

.. code-block:: C# 
    :linenos:

    ...


* Constructor:

.. code-block:: C# 
    :linenos:

    ...

* Get y Set:

.. code-block:: C# 
    :linenos:

    ...

* Herencia:

.. code-block:: C# 
    :linenos:

    ...

Clases abstractas y resolución de ámbito
****************************************

- uso de clases no instanciables:

.. code-block:: C# 
    :linenos:

    ...

Interfaces
**********

.. code-block:: C# 
    :linenos:

    ...

Importar y exportar
###################

include y require
*****************

* Importar archivos C#:

.. code-block:: C# 
    :linenos:

    ...

Namespace
*********

* Exportar (videojuegos.C#):

    .. code-block:: C# 
        :linenos:

        ...
    
    * Importar namespace (index.C#):

    .. code-block:: C# 
        :linenos:

        ...