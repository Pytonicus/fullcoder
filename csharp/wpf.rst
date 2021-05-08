Interfaces gráficas: WPF
========================

.. image:: /logos/logo-csharp.png
    :scale: 80%
    :alt: Logo C#
    :align: center

.. |date| date:: 
.. |time| date:: %H:%M
 

Interfaces gráficas con WPF en C#

.. contents:: Índice 

Configurar Visual Studio
########################

* Abrir el Visual Studio Installer
* Añadir en carga de trabajos **Desarrollo de escritorio .NET**

Crear un Proyecto
*****************
* Para crear un nuevo proyecto seleccionamos la opción **APlicacion de WPF (.NET Framework)** y le ponemos el nombre que queramos.
* Cargará el proyecto con una ventana inicial.

.. note::
    Se puede trabajar tanto en la ventana como en el código.

.. note:: 
    A la izquierda podemos desplegar un **cuadro de herramientas** para añadir cosas a la ventana.

XAML
####

Es un lenguaje que permite escribir toda la interfaz de usuario.

Estructura básica
*****************

Al crear el proyecto tenemos el siguiente archivo principal llamado MainWindow.xaml

.. code-block:: XAML
    :linenos:

    <Window x:Class="wpf_01.MainWindow"
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
            xmlns:local="clr-namespace:wpf_01"
            mc:Ignorable="d"
            Title="MainWindow" Height="450" Width="800">
        <!-- Dentro de grid se agrega el contenido de la ventana -->
        <Grid>
            <!-- Cada etiqueta de elemento tiene dentro unos atributos que ajustan su estilo -->
            <Button Content="Botón de prueba" Height="30" Width="120"></Button>
        </Grid>
    </Window>

Tipos de contenedores
*********************

StackPanel
++++++++++

.. code-block:: XAML 
    :linenos:

    <!-- Stack panel apila elementos de arriba abajo y reemplaza al Grid: -->
    <StackPanel>
        <TextBlock HorizontalAlignment="Center" Margin="12">Tus videoconsolas</TextBlock>
        <ListBox Height="80" Width="500">
            <ListBoxItem Content="PlayStation" />
            <ListBoxItem Content="Gameboy" />
            <ListBoxItem Content="Nintendo DS" />
        </ListBox>
        <Button Content="Añadir consola" Margin="20" Click="Button_Click"></Button>
    </StackPanel>

Grid
++++

Button
******

Botón sencillo.

Estructura del elemento
+++++++++++++++++++++++

.. code-block:: XAML
    :linenos:

    <Button Height="30" Click="Lanzar_Mensaje">Texto</Button>

Atributos comunes
+++++++++++++++++

* Content: texto del botón, también se puede poner en entre etiquetas.
* Height: define el alto. Recibe valor numérico.
* Width: define el ancho. Recibe valor numérico.
* FontSize: Tamaño de fuente. Recibe valor numérico.
* Foreground: Color de fuente. Recibe color en texto o hexadecimal.
* HorizontalAlignment: Alineación horizontal. Valores Left, Center y Right.
* Margin: margen entre elementos externos. Recibe valor numérico.
* Click: Dispara un evento al pulsarlo. Recibe el nombre de la función que ejecutará.

TextBlock
*********

Bloque de texto.

Estructura del elemento
+++++++++++++++++++++++

.. code-block:: XAML
    :linenos:

    <TextBlock HorizontalAlignment="Center" Margin="12">Tus videoconsolas</TextBlock>

Atributos comunes
+++++++++++++++++

* Content: texto del botón, también se puede poner en entre etiquetas.
* Height: define el alto. Recibe valor numérico.
* Width: define el ancho. Recibe valor numérico.
* FontSize: Tamaño de fuente. Recibe valor numérico.
* Foreground: Color de fuente. Recibe color en texto o hexadecimal.
* HorizontalAlignment: Alineación horizontal. Valores Left, Center y Right.
* Margin: margen entre elementos externos. Recibe valor numérico.

ListBox y ListBoxItem
*********************

Listado de elementos y elementos internos del mismo.

Estructura del elemento
+++++++++++++++++++++++

.. code-block:: XAML
    :linenos:

    <ListBox Height="80" Width="500" >
        <ListBoxItem Content="PlayStation" />
        <ListBoxItem Content="Gameboy" />
        <ListBoxItem Content="Nintendo DS" />
    </ListBox>

Atributos comunes
+++++++++++++++++

* Content: texto del botón, también se puede poner en entre etiquetas.
* Height: define el alto. Recibe valor numérico.
* Width: define el ancho. Recibe valor numérico.
* FontSize: Tamaño de fuente. Recibe valor numérico.
* Foreground: Color de fuente. Recibe color en texto o hexadecimal.
* HorizontalAlignment: Alineación horizontal. Valores Left, Center y Right.
* Margin: margen entre elementos externos. Recibe valor numérico.

Lógica de WPF
#############

Si la estructura de una ventana en XAML se escribe en **MainWindow.xaml**:

.. code-block:: xaml 
    :linenos:

    <Window x:Class="wpf_01.MainWindow"
            xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
            xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
            xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
            xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
            xmlns:local="clr-namespace:wpf_01"
            mc:Ignorable="d"
            Title="MainWindow" Height="450" Width="800">
        <Grid>
            <Button Content="Lanzar mensaje" Width="200" Height="40" Click="Lanzar_Mensaje" ></Button>
        </Grid>
    </Window>


la lógica se añade en el archivo MainWindow.xaml.cs en código C#:

.. code-block:: C#
    :linenos:

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Windows;
    using System.Windows.Controls;
    using System.Windows.Data;
    using System.Windows.Documents;
    using System.Windows.Input;
    using System.Windows.Media;
    using System.Windows.Media.Imaging;
    using System.Windows.Navigation;
    using System.Windows.Shapes;

    namespace wpf_01
    {
        /// <summary>
        /// Lógica de interacción para MainWindow.xaml
        /// </summary>
        public partial class MainWindow : Window
        {
            public MainWindow()
            {
                InitializeComponent();
            }
            // método creado que se dispara al hacer clic en el botón
            private void Lanzar_Mensaje(object sender, RoutedEventArgs e)
            {
                // mostrar una ventana emergente:
                MessageBox.Show("Soy una ventana emergente");
            }
        }
    }
