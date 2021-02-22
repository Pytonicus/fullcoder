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

Manipulación del Sistema
########################

Averiguar el Sistema operativo
******************************

.. code-block:: GO 
    :linenos:

    package main

    // cargamos la librería runtime:
    import (
        "fmt"
        "runtime"
    )

    func main() {
        // se averigua usando la variable runtime:
        fmt.Println("Sistema operativo: ", runtime.GOOS)
    }


Averiguar la arquitectura
*************************

.. code-block:: GO
    :linenos:

    package main

    // cargamos la librería runtime:
    import (
        "fmt"
        "runtime"
    )

    func main() {
        // se averigua usando la variable runtime:
        fmt.Println("Arquitectura: ", runtime.GOARCH)
    }

