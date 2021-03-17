Funciones predefinidas
======================

.. image:: /logos/logo-go.png
    :scale: 30%
    :alt: Logo GO
    :align: center

.. |date| date:: 
.. |time| date:: %H:%M
  

Funciones más usadas en GO

.. contents:: Índice

Manipulación de variables
#########################

Averiguar tipo de dato
**********************

.. code-block:: GO
    :linenos:

    ...

Validación
**********

.. code-block:: GO
    :linenos:

    ...

Destrucción
***********

.. code-block:: GO
    :linenos:

    ...

Manipulación de Strings
#######################

Longitud de un String 
*********************

.. code-block:: GO
    :linenos:

    ...

Conversión número a String 
**************************

.. code-block:: GO
    :linenos:

    ...

Conversión String a Array
*************************

.. code-block:: GO
    :linenos:

    ...

Reemplazar palabras
*******************

.. code-block:: GO
    :linenos:

    ...

Primera letra mayúscula
***********************

.. code-block:: GO
    :linenos:

    ...

Conversión a mayúsculas
***********************

.. code-block:: GO
    :linenos:

    ...

Conversión a minúsculas
***********************

.. code-block:: GO
    :linenos:

    ...

Manipulación de Números
#######################

Conversión Float a Integer
**************************

.. code-block:: GO
    :linenos:

    package main

    import "fmt"

    func main(){
        edad := 33.23
        edadNum := int(edad)

        fmt.Println(edadNum)
    }

Conversión String a Float
*************************

.. code-block:: GO
    :linenos:

    ...

Redondeo de decimales
*********************

.. code-block:: GO
    :linenos:

    ...

Manipulación de Arrays
######################

Imprimir contenido
******************

.. code-block:: GO
    :linenos:

    ...

Rango de números
****************

.. code-block:: GO
    :linenos:

    package main

    // importar la librería rand:
    import (
        "fmt"
        "math/rand"
    )

    func main() {
        // se establece el rango en la variable:
        aleatorio := rand.Int()

        fmt.Println("El número aleatorio es: ", aleatorio)
    }


Recuperar valor máximo
**********************

.. code-block:: GO
    :linenos:

    ...

Recuperar valor mínimo
**********************

.. code-block:: GO
    :linenos:

    ...

Suma total de todos los valores
*******************************

.. code-block:: GO
    :linenos:

    ...

Manipulación JSON
#################

Convertir Array en JSON 
***********************

.. code-block:: GO
    :linenos:

    ...

Convertir JSON en Array 
***********************

.. code-block:: GO
    :linenos:

    ...

.. attention::
    Para poder trabajar con curl hay que instalar la dependencia ``sudo apt install GO7.4-curl``

Manipulación de fechas 
######################

.. code-block:: GO
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

.. code-block:: GO
    :linenos:

    ...

Manipulación de archivos
************************

* Escritura de archivos:

.. code-block:: GO
    :linenos:

    ...

* Lectura de archivos:

.. code-block:: GO
    :linenos:

    ...

* Actualización de archivos:

.. code-block:: GO
    :linenos:

    ...

Manipulación de cabeceras
#########################

Redirección
***********

.. code-block:: GO
    :linenos:

    ...

Modificar el comportamiento de un script
****************************************

.. code-block:: GO
    :linenos:

    ...

* Lista de MIMES más comunes: https://developer.mozilla.org/es/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types

Descargar un archivo desde un script
************************************

.. code-block:: GO
    :linenos:

    ...

Tratamiento de CORS
*******************

.. code-block:: GO
    :linenos:

    ...
 
Manipulación del Sistema
########################

Averiguar el Sistema operativo
******************************

.. code-block:: GO 
    :linenos:

    ...

Averiguar la arquitectura
*************************

.. code-block:: GO
    :linenos:

    ...

