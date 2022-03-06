Framework: Angular
==================

.. image:: /logos/logo-angular.png
    :scale: 50%
    :alt: Logo Angular
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica de Angular 12

.. contents:: Índice
 
Configuraciones
###############  
  
Instalación de Angular CLI
**************************
Para gestionar Angular hay que instalar Angular CLI: ``npm install -g @angular/cli``

.. note::
    Para instalar en Linux utilizar el comando ``sudo npm install -g @angular/cli``

ANGULAR CLI y otros comandos 
############################
Para ejecutar un comando de Angular CLI el prefijo que se utiliza es ``ng``:

* Comprobar versión de angular/cli: ``ng --version``
* Crear proyecto: ``ng new nombre-proyecto``
* Levantar servidor y abrir navegador: ``ng serve -o`` (ruta por defecto: localhost:4200)
* Levantar en otro puerto: ``ng serve -o --port 4500``
* Crear un componente:  ``ng generate component nombre_componente``

Otros comandos útiles de npm
****************************
* Instalar todas las dependencias: ``npm install`` (no es un comando ng pero es importante recordarlo)


.. attention::
    Para ejecutar en Windows estos comandos CLI se usará la aplicación ``nodejs command prompt`` o ejecutar con el prefijo ``npm run ng``

Estructura del proyecto 
#######################

Partes importantes del proyecto:
* package.json: archivo con las dependencias del proyecto.
* angular.json: se encuentra la configuración del proyecto.
* e2e: Carpeta test de integración 
* src: carpeta del proyecto en la cual vemos: 
  * index.html: pagina de entrada de la aplicación. 
  * main.ts: es donde se cargan los módulos.
  * style.css: estilos a nivel global.
  * test.ts: archivo para realizar tests.
  * enviorments: carpeta para variables de entornos.
  * assets: carpeta de archivos estáticos como imágenes.
  * app: carpeta del módulo principal donde se irá añadiendo el resto de componentes.

Componentes
###########

Los componentes se encuentran en la carpeta **src**.
Es ideal crear una carpeta **components** dentro de **src** para ordenarlos ya que se van a reutilizar en distintos módulos.
Cada componente se organizará en una carpeta con el siguiente contenido:
* Hoja de estilo CSS u otro tipo.
* Archivo HTML.
* Controlador Typescript.
* Modulo Typescript.

Crear un componente 
*******************

Para crear un componente se ejecuta el comando: ``ng generate component nombre_componente``
Crear componente dentro de una carpeta **components**: ``ng generate component components/menu``
* Lo primero que vamos a hacer es borrar el contenido del archivo **app.component.html** y lo reemplazamos por:

.. code-block:: html 
    :linenos:

    <div>
        <h1>Componente principal</h1>
        <hr>
        <app-menu></app-menu>
    </div>

* Ahora editamos el contenido de **menu.component.html**:

.. code-block:: html 
    :linenos:

    <div id="menu">
        <h2>Soy el menú</h2>
    </div>

* Y de paso editamos el css de menu en **menu.component.css**:

.. code-block:: css 
    :linenos:

    h2{
        color: red;
    }

Esto mostrará el título del módulo y el subtítulo del componente menú de color rojo.

.. atention::
    Mover la carpeta de un componente de forma manual causará fallos en la aplicación ya que no coincidirán las 
    rutas.


Data Binding
############

Atributos 
*********

* Crear y asignar en componente **app.component.ts**:

.. code-block:: Typescript
    :linenos:

    import { Component } from '@angular/core';

    @Component({
        selector: 'app-root',
        templateUrl: './app.component.html',
        styleUrls: ['./app.component.css']
    })
    export class AppComponent {
        // crear una variable en el componente:
        mensaje: string = "Mensaje desde el componente app";
    }

* Utilizar variable en plantilla **app.template.html**:

.. code-block:: html 
    :linenos:

    <h1>{{mensaje}}</h1>


Métodos
*******

Retornar datos de un método:

.. code-block:: Typescript
    :liinenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
    selector: 'app-interpolation',
    templateUrl: './interpolation.component.html',
    styleUrls: ['./interpolation.component.css']
    })
    export class InterpolationComponent implements OnInit {
    // vamos a crear un objeto mixto sin interface:
    consola: any = {
        marca: 'Sony',
        modelo: 'PlayStation',
        lanzamiento: new Date(1995, 9, 29)
    }

    constructor() { }

    ngOnInit(): void {
    }

    // para averiguar la edad creamos un método:
    getEdad(): number {
        const edad = (new Date().getTime() - this.consola.lanzamiento.getTime()) / (365 * 24 * 60 * 60 * 1000);
        return Math.ceil(edad);
    }

    }

Uso en el template:

.. code-block:: html 
    :linenos:

    <div class="card">
        <p>Consola: {{consola.marca}} {{consola.modelo}}</p>
        <p>Edad: {{getEdad()}} años</p>
    </div>

Assets
******

* Tratamiento estático de assets en templates:

.. code-block:: html 
    :linenos:

    <div class="card">
        <img src="/assets/img/imagen-prueba.jpg">
    </div>

* Asignación de assets en componentes:

.. code-block:: Typescript
    :linenos:

    imagen: string = '/assets/img/prueba-imagen.jpg';


Atributos dinámicos
*******************

* En el controlador existe un atributo con una ruta, se carga la variable en el template:

.. code-block:: html 
    :linenos:

    <img [src]="imagen">

.. note:: 
    Esto vale para cargar información en cualquier atributo de la etiqueta.


Eventos del DOM (event binding)
*******************************

Angular dispone de todos los métodos tácticos del DOM usados en HTML para dispara acciones:

* En el componente se crea un método:

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-saludar',
        templateUrl: './saludar.component.html',
        styleUrls: ['./saludar.component.css']
    })
    export class SaludarComponent implements OnInit {
        // se crea un atributo para el HTML:
        public saludo: string;

        constructor() {
            // Se inicializa el atributo con un mensaje o nada:
            this.saludo = "";
        }

        ngOnInit(): void {
        }

        // este método dispara el saludo:
        startSaludo(): void{
            this.saludo = "Hola amigo, ¿quién eres?";
        }

    }


* Este método ahora se puede disparar al hacer click en el botón:

.. code-block:: html 
    :linenos:

    <div class="card">
        <h1>Ejemplo de saludo</h1>
        <hr>
        <p>{{ saludo }}</p>
        <button (click)="startSaludo()">Saludar</button>
    </div>


Recuperar valores de plantilla (Two Way binding)
************************************************
Para recuperar valores de la plantilla como datos de un formulario se hace lo siguiente:

1. Se carga el modulo de formularios en **app.module.ts**:

.. code-block:: Typescript
    :linenos:

    import { NgModule } from '@angular/core';
    import { BrowserModule } from '@angular/platform-browser';

    import { AppComponent } from './app.component';
    import { MenuComponent } from './components/menu/menu.component';
    import { InterpolationComponent } from './components/interpolation/interpolation.component';
    import { PropertyBindingComponent } from './components/property-binding/property-binding.component';
    import { EventBindingComponent } from './components/event-binding/event-binding.component';
    import { SaludarComponent } from './components/saludar/saludar.component';
    import { TwowaybindingComponent } from './components/twowaybinding/twowaybinding.component';
    import { FormsModule } from '@angular/forms'; // se importan los forms.

    @NgModule({
    declarations: [
        AppComponent,
        MenuComponent,
        InterpolationComponent,
        PropertyBindingComponent,
        EventBindingComponent,
        SaludarComponent,
        TwowaybindingComponent
    ],
    imports: [
        BrowserModule,
        FormsModule // se carga en los imports el modulo de forms para todos los componentes de app
    ],
    providers: [],
    bootstrap: [AppComponent]
    })
    export class AppModule { }

2. Ahora pasamos al componente con el que se quiere trabajar:

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

        @Component({
        selector: 'app-twowaybinding',
        templateUrl: './twowaybinding.component.html',
        styleUrls: ['./twowaybinding.component.css']
        })
        export class TwowaybindingComponent implements OnInit {
        // crear objeto donde se va a guardar los datos.
        consola: any = {
            marca: null,
            modelo: null
        }

        constructor() { }

        ngOnInit(): void {
        }

    }


3. Y por último se prepara el template:

.. code-block:: html 
    :linenos:

    <div class="card">
        <h1>Datos consola</h1>
        <hr>
        <p>Consola: {{consola.marca}} {{consola.modelo}}</p>
        <!-- se le pasa los campos con la directiva ngModel: -->
        <input type="text" placeholder="marca" [(ngModel)]="consola.marca">
        <input type="text" placeholder="modelo" [(ngModel)]="consola.modelo">
    </div>

Ciclo de vida 
#############

El ciclo de vida va en el siguiente orden:
* Constructor
* ngOnChanges
* ngOnInit
* ngDoCheck
* ngAfterContentInit
* ngAfterContentChecked
* ngAfterViewInit
* ngAfterViewChecked
* ngOnDestroy

Constructor - Cargar métodos y datos que construyen la aplicación
*****************************************************************
La primera acción que se ejecuta en el componente es el constructor y es muy útil para 
cargar la información antes de disparar cualquier evento como NgOnInit():

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-event-binding',
        templateUrl: './event-binding.component.html',
        styleUrls: ['./event-binding.component.css']
    })
    export class EventBindingComponent implements OnInit {

        // se crea un elemento, si no se inicializa dará error el linter:
        public hora: string;

        constructor() {
            // establecemos la hora con el setHora:
            this.hora = this.setHora();
        }

        ngOnInit(): void {
        }

        // creamos un seteador para la hora:
        setHora(): string {
            // recuperamos hora, minutos y segundos actuales:
            const hh = ('0' + new Date().getHours()).slice(-2);
            const mm = ('0' + new Date().getHours()).slice(-2);
            const ss = ('0' + new Date().getHours()).slice(-2);
            // cargamos el tiempo en hora:
            return hh + ':' + mm + ':' + ss;
        }

    }


ngOnInit() - Cargar método cuando se inicialice el componente
*************************************************************

.. code-block:: Typescript
    :linenos:

    import { Component, OnInit } from '@angular/core';

    @Component({
        selector: 'app-property-binding',
        templateUrl: './property-binding.component.html',
        styleUrls: ['./property-binding.component.css']
    })
    export class PropertyBindingComponent implements OnInit {

        imagen: string = '/assets/img/prueba-imagen.jpg';

        constructor() { }

        ngOnInit(): void {
            // lo cargamos en el DOM al inicializar el componente para que se ejecute:
            this.cambiarImagen();
        }

        // crear metodo que cambia imagen:
        cambiarImagen(): void {
            const logoRojo = '/assets/img/logo-rojo.jpg';
            const logoBlanco = '/assets/img/logo-blanco.jpg';
            setInterval(()=> {
            this.imagen === logoRojo ? this.imagen = logoBlanco : this.imagen = logoRojo;
            }, 1000);
        }

    }


Pipes
#####




Módulos
#######


Interfaces en Angular 
#####################


Servicios
#########
