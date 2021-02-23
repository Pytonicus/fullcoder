Funciones predefinidas
======================

.. image:: /logos/logo-csharp.png
    :scale: 80%
    :alt: Logo C#
    :align: center

.. |date| date:: 
.. |time| date:: %H:%M
 

Funciones más usadas en C#

.. contents:: Índice

Información del servidor 
########################

En un archivo vacío se guarda la siguiente función:

.. code-block:: C#
    :linenos:

    ...

Manipulación de variables
#########################

Averiguar tipo de dato
**********************

.. code-block:: C#
    :linenos:

    ...

Validación
**********

.. code-block:: C#
    :linenos:

    ...

Destrucción
***********

.. code-block:: C#
    :linenos:

    ...

Manipulación de Strings
#######################

Longitud de un String 
*********************

.. code-block:: C#
    :linenos:

    static void Main(string[] args)
        {
            string nombre = "Guillermo";

            // devuelve un valor entero que se puede imprimir directamente: 
            int longitudNombre = nombre.Length;

            Console.WriteLine(longitudNombre);

            Console.Read();
        }

Conversión a String 
*******************

.. code-block:: C#
    :linenos:

    static void Main(string[] args)
        {
            int numero = 27;

            // convertir a string:
            string numeroStr = Convert.ToString(numero);

            Console.WriteLine(numeroStr);

            Console.Read();
        }

Conversión String a Array
*************************

.. code-block:: C#
    :linenos:

    ...

Reemplazar palabras
*******************

.. code-block:: C#
    :linenos:

    ...

Primera letra mayúscula
***********************

.. code-block:: C#
    :linenos:

    ...

Conversión a mayúsculas
***********************

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string nombre = "Guillermo";

            Console.WriteLine(nombre.ToUpper());

            Console.Read();
        }
    }

Conversión a minúsculas
***********************

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string nombre = "Guillermo";

            Console.WriteLine(nombre.ToLower());

            Console.Read();
        }
    }

Eliminar espacios en blanco a los lados
***************************************

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string frase = "   Esta frase esta mal formada   ";

            // imprimir quitando espacios a los lados:
            Console.WriteLine(frase.Trim());
            Console.Read();
        }
    }

Localizar posición de caracteres en cadena
******************************************

.. code-block:: C#
    :linenos:

    class Program
    {
        static void Main(string[] args)
        {
            string frase = "En esta frase se esconde Pepe";

            if (frase.Contains("Pepe"))
            {
                Console.WriteLine("Hemos encontrado a Pepe!");
                Console.Read();
            }
        }
    }

Formatear contenido de una variable con otras
*********************************************

.. code-block:: C#
    :linenos:
    
    class Program
    {
        static void Main(string[] args)
        {
            string frase;

            Console.Write("Introduce tu nombre: ");
            string nombre = Console.ReadLine();
            // con string format podemos usar el formateo:
            frase = String.Format("Te llamas {0}", nombre);

            Console.WriteLine(frase);
            Console.Read();
        }
    }

Manipulación de Números
#######################

Conversión String a Integer
***************************

.. code-block:: C#
    :linenos:

    static void Main(string[] args)
        {
            string edad = "33";

            // Parsing a entero:
            int total = Int32.Parse(edad);

            Console.WriteLine(total + 10);
            Console.ReadKey();
        }

Conversión String a Float
*************************

.. code-block:: C#
    :linenos:

    ...

Redondeo de decimales
*********************

.. code-block:: C#
    :linenos:

    ...

Manipulación de Arrays
######################

Imprimir contenido
******************

.. code-block:: C#
    :linenos:

    ...

Rango de números
****************

.. code-block:: C#
    :linenos:

    ...

Recuperar valor máximo
**********************

.. code-block:: C#
    :linenos:

    ...

Recuperar valor mínimo
**********************

.. code-block:: C#
    :linenos:

    ...

Suma total de todos los valores
*******************************

.. code-block:: C#
    :linenos:

    ...

Manipulación JSON
#################

Convertir Array en JSON 
***********************

.. code-block:: C#
    :linenos:

    ...

Convertir JSON en Array 
***********************

.. code-block:: C#
    :linenos:

    ...

.. attention::
    Para poder trabajar con curl hay que instalar la dependencia ``sudo apt install C#7.4-curl``

Manipulación de fechas 
######################

.. code-block:: C#
    :linenos:

    ...

* Códigos comunes para Fecha: 

+----------------------------------------------+---------+
| Tipo de valor                                | símbolo |
+==============================================+=========+
| Día en notación numeral                      | d       |
+----------------------------------------------+---------+
| Día por inicial                              | D       | 
+----------------------------------------------+---------+
| Día de la semana                             | l       |
+----------------------------------------------+---------+
| Dias transcurridos desde comienzos de año    | z       |
+----------------------------------------------+---------+
| Dias que tiene el mes corriente              | t       |
+----------------------------------------------+---------+
| Semanas transcurridas desde comienzos de año | W       |
+----------------------------------------------+---------+
| Mes actual en notación numeral               | m       |
+----------------------------------------------+---------+
| Mes actual en notación numeral sin cero      | n       |
+----------------------------------------------+---------+
| Iniciales del mes corriente                  | M       |
+----------------------------------------------+---------+
| Año corriente en notación numeral            | Y       |
+----------------------------------------------+---------+
| Año con notación numeral abreviada           | y       |
+----------------------------------------------+---------+
| Año bisiesto (devuelve 1 si es bisiesto)     | L       |
+----------------------------------------------+---------+
| Fecha en formato ISO-8601                    | c       |
+----------------------------------------------+---------+

* Códigos comunes para Hora:

+----------------------------------------------+---------+
| Tipo de valor                                | símbolo |
+==============================================+=========+
| Ver si la hora es AM o PM                    | a       |
+----------------------------------------------+---------+
| Ver si la hora es AM o PM en mayúsculas      | A       | 
+----------------------------------------------+---------+
| Hora en formato 12                           | g       |
+----------------------------------------------+---------+
| Hora en formato 24                           | G       |
+----------------------------------------------+---------+
| Hora en formato 12 con 0 inicial             | h       |
+----------------------------------------------+---------+
| Hora en formato 24 con 0 inicial             | H       |
+----------------------------------------------+---------+
| Minutos                                      | i       |
+----------------------------------------------+---------+
| Segundos                                     | s       |
+----------------------------------------------+---------+
| Microsegundos                                | u       |
+----------------------------------------------+---------+
| Zona Horaria                                 | e       |
+----------------------------------------------+---------+
| Horario de sol reducido                      | I       |
+----------------------------------------------+---------+
| Desfase meridiano de Greenwitch              | O       |
+----------------------------------------------+---------+
| Hora formato Swatch Internet Time            | B       |
+----------------------------------------------+---------+
| Hora formato UNIX                            | U       |
+----------------------------------------------+---------+


Tratamiento de archivos
#######################

Recuperar contenido de archivo 
******************************

.. code-block:: C#
    :linenos:

    ...

Manipulación de archivos
************************

* Escritura de archivos:

.. code-block:: C#
    :linenos:

    ...

* Lectura de archivos:

.. code-block:: C#
    :linenos:

    ...

* Actualización de archivos:

.. code-block:: C#
    :linenos:

    ...

Manipulación de cabeceras
#########################

Redirección
***********

.. code-block:: C#
    :linenos:

    ...

Modificar el comportamiento de un script
****************************************

.. code-block:: C#
    :linenos:

    ...

* Lista de MIMES más comunes: https://developer.mozilla.org/es/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types

Descargar un archivo desde un script
************************************

.. code-block:: C#
    :linenos:

    ...

Tratamiento de CORS
*******************

.. code-block:: C#
    :linenos:

    ...
 
Manipulación del Sistema
########################

Averiguar el Sistema operativo
******************************

.. code-block:: C# 
    :linenos:

    ...

Averiguar la arquitectura
*************************

.. code-block:: C#
    :linenos:

    ...