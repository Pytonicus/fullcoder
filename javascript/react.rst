Framework: ReactJS  
==================

.. image:: /logos/logo-react.png
    :scale: 35%
    :alt: Logo Angular
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica de ReactJS 

.. contents:: Índice
  
Configuraciones
###############  

Instalar React
**************

Paso 1: Tener instalado NodeJS desde su página oficial: https://nodejs.org/es/
Paso 2: Instalar React con npx desde la carpeta del proyecto: ``npx create-react-app nombre-proyecto``
Paso 3: Acceder a la carpeta del proyecto y ejecutarlo: ``npm start``
Paso 4: Se abre el navegador con la ruta: ``http://localhost:3000``

.. attention::
    npx viene instalado con npm y es su versión en la nube. De modo que si necesitas un paquete y no deseas instalarlo en tu máquina utiliza npx en lugar de npm.

Herramientas de desarrollo 
**************************

Existen una serie de herramientas útiles que se pueden instalar desde la tienda de tu navegador:

- React Developer Tools 

También existe una herramienta muy útil para Visual Studio Code:

- ES7 React/Redux/GraphQL/React-Native snippets

Importar React desde CDN
************************
Existe la opción de importar react desde un cdn en lugar de crear un proyecto con node:

.. code-block::  
    :linenos:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>React prueba</title>
    
    </head>
    <body>
        <div id="raiz"></div>

        <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
        <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
        <!-- React utiliza babel para poder trabajar con JSX -->
        <script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/7.18.13/babel.min.js"></script>
        <!-- Definimos que el tipo de script será de babel: -->
        <script type="text/babel">
            const raiz = document.querySelector('#raiz');
            const nombre = "Guillermo";
            // Las llaves nos permiten incrustar código JSX:
            const titulo = <h1>Te llamas {nombre}</h1>;

            ReactDOM.render(titulo, raiz);
        </script>
    </body>
    </html>

Estructura proyecto React 
*************************

- Carpeta Public: Aquí irá todo los archivos públicos como imágenes, iconos y algún que otro html.
- Carpeta src: aquí viene el contenido del proyecto. 
    - index.js: Archivo de inicio principal de la aplicación. Tiene su homónimo css disponible para los estilos globales.
    - App.js: Componente principal de la aplicación donde se irán cargando el resto de componentes.

Dentro de src podemos crear la siguiente estructura de subcarpetas basado en Atomic Design:

    - common: para componentes que se van a reutilizar en distintos sitios de la aplicación.
    - templates: para componentes que pintan diferentes páginas en la aplicación.
    - Router.js: para los componentes que se relacionan con el enrutamiento (React Router).
    - pages: para los componentes que pintan vistas, dentro de esta carpeta se crean otras subcarpetas
    para componentes como Index, Login, Shop.. y dentro cada uno de sus componentes de un solo uso.
    - requests: para los archivos que consumen servicios rest.


Preparar App.js 
***************

Se borra el contenido de **App.js** y **App.css** dentro de la carpeta src y se edita **App.js**:

.. code-block::  
    :linenos:

    // Se importa el css si existe:
    import './App.css';

    // se crea una función:
    function App() {
    // esta función retorna un nodo con todas las etiquetas html:
    return (
        <h1>Soy un componente de prueba</h1>
    );
    }

    // se exporta el componente como un módulo:
    export default App;

.. note::
    **index.js** se queda vinculado como nodo principal hacia el archivo **index.html** el resto irán ligados a **app.js**


Componentes
###########

Los componentes basados en funciones son los más modernos y recomendados para uso de **hooks**.

Crear un componente  
*******************

Crear un componente: en **src** crear un archivo llamado **Prueba.js**:

.. code-block:: 
    :linenos:

    // se crea una función con el componente:
    function Prueba(){
        // el retorno del componente será el contenido html:
        return(
            <div>
                <h1>Componente de prueba</h1>
            </div>
        );
    }

    export default Prueba;

.. attention::
    Por convención el nombre del componente comienza en Mayúscula y el contenido html de return irá siempre envuelto en etiquetas **<div>**

Crear css del componente 
************************

Además del css principal de **App.css** cada componente lleva su propio archivo css con el mismo nombre **Prueba.css**:

.. code-block:: css 
    :linenos:

    h1{
        color: blue;
    }

Utilizar componente 
*******************

Para utilizar el componente, es necesario cargarlo en otro componente que este funcionando, actualmente **App.js**:

.. code-block:: 
    :linenos:

    import './App.css';
    // importar componente:
    import Prueba from './Prueba';

    function App() {
    return (
        <div>
        <h1>Recuerda usar contenedores div sino dará errores</h1>
        {/* cargar componente (metodo para hacer comentarios en el return): */}
        <Prueba />
        </div>
    );
    }
 
    export default App;

Uso de fragment
***************

Fragment te permite cargar varios nodos sin tener que añadir al DOM etiquetas div:

.. code-block::  
    :linenos:

    // importar fragment:
    import {Fragment} from 'react';
    import './App.css';
    import Prueba from './Prueba';

    function App() {
    return (
        <Fragment>
        <h1>El tag fragment omite el uso de divs</h1>
        <Prueba />
        </Fragment>
    );
    }

    export default App;

Props: Comunicación de padre a hijo
***********************************

Los props permiten enviar datos desde componentes padre a hijos

Enviando propiedades
++++++++++++++++++++

- Editar el componente padre (en este ejemplo **App.js**):

.. code-block::  
    :linenos:

    import {Fragment} from 'react';
    import './App.css';
    import Prueba from './Prueba';

    function App() {
    return (
        <Fragment>
        <h1>Listado de consolas: </h1>
        <Prueba marca="Nintendo" modelo="Wii" />
        <Prueba marca="Nintendo" modelo="Switch" />
        <Prueba marca="Nintendo" modelo="Gamecube" />
        </Fragment>
    );
    }

    export default App;

Recuperando propiedades 
+++++++++++++++++++++++

Recuperar propiedades en el componente hijo (en este caso **Prueba.js**):

.. code-block::  
    :linenos:

    import './Prueba.css';

    import './Prueba.css';

    // cargar propiedades (o bien escribimos props y sacamos props.marca, props.modelo o desestructuramos como en este caso):
    function Prueba({marca, modelo}){

        return(
            <div>
                {/* Cargar la información: */}
                <h1>- {marca} {modelo}</h1>
            </div>
        );
    }

    export default Prueba;

Propiedades por defecto (default props)
+++++++++++++++++++++++++++++++++++++++

Cuando no se reciben propiedades se pueden establecer algunas por defecto en el componente que completan uno o varios campos no recibidos:

.. code-block::  
    :linenos:

    import './Prueba.css';

    function Prueba({marca, modelo}){
        return(
            <div>
                <p> {marca} {modelo}</p>
            </div>
        );
    }

    // si el componente no recibe propiedades añade estas:
    Prueba.defaultProps = {marca: "Genérica", modelo: "estandar"}

    export default Prueba;

Validar propiedades (PropTypes)
+++++++++++++++++++++++++++++++

Se pueden validar los campos recibidos, de manera que cuando uno no cumpla con el formato establecido nos avise por consola:

.. code-block::  
    :linenos:

    // importar PropTypes:
    import PropTypes from 'prop-types';
    import './Prueba.css';

    function Prueba({marca, modelo, lanzamiento}){
        return(
            <div>
                <p> {marca} {modelo} de {lanzamiento}</p>
            </div>
        );
    }

    // crear validador:
    Prueba.propTypes = {
        marca: PropTypes.string.isRequired,
        modelo: PropTypes.string,
        lanzamiento: PropTypes.number
    }

    export default Prueba;

Comunicación de hijo a padre 
****************************

1. Desde el componente hijo tenemos lo siguiente:

.. code-block:: 
    :linenos:

    // importar el hook:
    import {useState} from 'react';
    import './Prueba.css';

    // la función recibe un hook con los valores:
    function Prueba({setJuegos}){
        // crear un nuevo hook para cambiar el estado del actual:
        const [nuevoJuego, setNuevoJuego] = useState('');

        // el hook tendra un handle para cambiar su estado:
        const handleNuevoJuego = (e) => {
            setNuevoJuego(e.target.value);
        }

        // crear un handle que añadira el juego nuevo:
        const handleJuegos = (e) => {
            // recuerda prevenir refresco de pantalla:
            e.preventDefault();
            // utilizar el hook del padre para añadir el valor del hook del hijo a una lista:
            setJuegos(juego => [...juego, nuevoJuego]);
            // regresar a su estado vacio el hook del hijo:
            setNuevoJuego('');
        }

        // retornar el input donde introducir nuevos valores:
        return(
            <form onSubmit={handleJuegos}>
                <input type="text" value={nuevoJuego} onChange={handleNuevoJuego} />
            </form>
        )
    }

    export default Prueba;

2. Y desde el padre:

.. code-block::  
    :linenos:

    import {Fragment} from 'react';
    // importar el hook:
    import {useState} from 'react';
    // importar el hijo:
    import Prueba from './Prueba.js';
    import './App.css';

    function App() {
    // tenemos el hook principal con los juegos:
    const [juegos, setJuegos] = useState(['Zelda', 'Mario', 'Yoshi']);

    // en el return añadimos el componente al formulario y le pasamos el hook de juegos haciendo el cambio de estado:
    return(
        <Fragment>
        <Prueba setJuegos={setJuegos} />
        <ul>
            {
            juegos.map((juego, index) => {
                return <li key={index}>{juego}</li>
            })
            }
        </ul>
        </Fragment>
    )

    }

    export default App;

.. note::
    Se puede añadir un valor index en los mapeos para evitar errores de duplicate key 

JSX 
###

JSX es una combinación de la sintaxis de javascript con XML, similar a HTML.

Imprimir datos en JSX
*********************

.. code-block::  
    :linenos:

    import './Prueba.css';

    // cargar propiedades (o bien escribimos props y sacamos props.marca, props.modelo o desestructuramos como en este caso):
    function Prueba(){
        // crear una variable:
        const consola = {
            marca: "Nintendo",
            modelo: "DS"
        }

        return(
            <div>
                {/* Cargar la información: */}
                <h1>- {consola.marca} {consola.modelo}</h1>
            </div>
        );
    }

    export default Prueba;

Mostrar contenido de un objeto
******************************

.. code-block::  
    :linenos:

    import './Prueba.css';

    function Prueba(){
        const consola = {
            marca: "Nintendo",
            modelo: "DS",
            lanzamiento: 2001
        }

        return(
            <div>
                <h1>Ver todos los valores de un objeto:</h1>
                {/* ver valores del objeto (objeto, campos, cantidad de espacios): */}
                <pre>{JSON.stringify(consola, null, 3)}</pre>
                <hr/>
                <h1>Ver solo campos determinados:</h1>
                <pre>{JSON.stringify(consola, ['marca', 'modelo'], 5)}</pre>
            </div>
        );
    }

    export default Prueba;

Condicionales en JSX 
********************
Si es necesario hacer una validación dentro del return se hace del siguiente modo:

Condicional simple 
******************

.. code-block:: 
    :linenos:

    import './Prueba.css';

    function Prueba(){
        const consola = {
            marca: "Nintendo",
            modelo: "DS",
            lanzamiento: 2001
        }

        return(
            <div>
                {consola.marca === "Nintendo" &&
                    <p>La consola es de Nintendo</p>
                }
            </div>
        );
    }

    export default Prueba;

Condicional ternaria 
********************

.. code-block:: 
    :linenos:

    import './Prueba.css';

    function Prueba(){
        const consola = {
            marca: "Nintendo",
            modelo: "DS",
            lanzamiento: 2001
        }

        return(
            <div>
                {consola.marca === "Nintendo" ? (
                    <p>La consola es de Nintendo</p>
                ) : (
                    <p>La consola es otra marca</p>
                )}
            </div>
        );
    }

    export default Prueba;

Estilos y clases
****************

Añadir estilos manualmente con **style**
++++++++++++++++++++++++++++++++++++++++

.. code-block:: 
    :linenos:

    import './Prueba.css';

    function Prueba(){
        // Utilizar la notación CamelCase en lugar de kebab-case para estilos:
        const estilo = {
            color: "red",
            backgroundColor: "black"
        }

        return(
            <div>
                {/* cargar datos de estilo: */}
                <p style={estilo}>Nintendo Switch</p>
            </div>
        );
    }

    export default Prueba;

uso de clases con className
***************************

En JSX se reemplaza el atributo class por className:

.. code-block::  
    :linenos:

    import './Prueba.css';

    function Prueba(){
        const lanzamiento = 2017;

        return(
            <div>
                {/* implementar clase: */}
                <p className={"switch"}>Nintendo Switch</p>
                {/* uso ternario de clases condicionales: */}
                <p className={lanzamiento ? 'showLanzamiento' : 'hideLanzamiento'}>Lanzamiento: {lanzamiento}</p>
            </div>
        );
    }

    export default Prueba;

Recorrer array con map
**********************

.. code-block::  
    :linenos:

    import './Prueba.css';

    function Prueba(){
        const consolas = ["Nintendo Switch", "Gameboy", "Master System", "Playstation"];

        return(
            <div>
                {/* recorrer elementos con map (importante añadir una key): */}
                <ol>
                    {
                        consolas.map( consola =>{
                            return <li key={consola}>{consola}</li>
                        })
                    }
                </ol>
            </div>
        );
    }

    export default Prueba;

Recorrer array de objetos con map 
*********************************

.. code-block::  
    :linenos:

    import './Prueba.css';

    function Prueba(){
        const consolas = [
            {marca: "Nintendo", modelo: "Switch"},
            {marca: "Sega", modelo: "Master System"},
            {marca: "Sony", modelo: "PlayStation"}
        ];

        return(
            consolas.map( consola =>{
                return(
                    <div key={consola.modelo}>
                        <ul>
                            <li>{consola.marca}</li>
                            <li>{consola.modelo}</li>
                        </ul>
                    </div>
                )
            })
        );
    }

    export default Prueba;

.. note:: 
    Hemos añadido un segundo return para poder añadir más de una línea de JSX dentro del bucle.

.. note:: 
    Se puede desestructurar el elemento **consola** en **({marca, modelo})**.


Eventos y Hooks 
###############

Tipos de Eventos 
****************

PORTAPAPELES
++++++++++++

- onCopy
- onCut
- onPaste

TECLADO
+++++++

- onKeyDown
- onKeyUp
- onKeyPress

RATÓN
+++++

- onClick
- onContextMenu
- onDoubleClick
- onDrag
- onDragEnd
- onDragEnter
- onDragExit
- onDragLeave
- onDragOver
- onDragStart
- onDrop
- onMouseDown
- onMouseEnter
- onMouseLeave
- onMouseMove
- onMouseOut
- onMouseOver
- onMouseUp

FORMULARIOS
+++++++++++

- onChange
- onInput
- onInvalid
- onReset
- onSubmit

mas eventos en: https://es.reactjs.org/docs/events.html

Uso de eventos 
**************

Eventos sin retorno 
+++++++++++++++++++

.. code-block::  
    :linenos:

    import {Fragment} from 'react';
    import './App.css';

    function App() {
    // función que dispara el evento:
    const mensaje = (e) => {
        // lanzar mensaje con alguna propiedad del botón:
        alert(`se ha pulsado ${e.target.innerText}`);
    }

    return (
        <Fragment>
        {/* botón con el evento click: */}
        <button onClick={mensaje}>Disparar mensaje de alerta</button>
        </Fragment>
    );
    }

    export default App;


Eventos con retorno y parámetros
++++++++++++++++++++++++++++++++

.. code-block::  
    :linenos:

    import {Fragment} from 'react';
    import './App.css';

    function App() {
    // se recibén en el callback los parámetros:
    const consola = (marca, modelo) => {
        // los eventos que retornan algo también reciben algo:
        return (e) => {
        // ahora hay dos tipos de parámetros, los que se recibén de la función y el evento que se recibe en este caso en el return:
        
        // parametros recibidos:
        alert(`${marca} ${modelo}`);
        // evento recibido por return:
        alert(`se ha pulsado ${e.target.innerText}`);

        }
    }

    return (
        <Fragment>
        {/* el evento recibe la función con los parámetros:: */}
        <button onClick={consola('Nintendo','Switch')}>Averiguar videoconsola</button>
        </Fragment>
    );
    }

    export default App;


Hooks 
*****

Los hooks se utilizan en React para cambiar el estado de un componente, los más comunes son:

useState
++++++++

Devuelve un valor con estado y una función para actualizarlo:

.. code-block::  
    :linenos:

    import {Fragment} from 'react';
    // importar el hook:
    import {useState} from 'react';
    import './App.css';

    function App() {
    // el elemento consola será un hook con un valor por defecto:
    const [consola, setConsola] = useState("ej. Gameboy");

    // a continuación se usará una función que ejecute el cambio de estado:
    const consolaChange = (e) => {
        // recuperar el valor del input:
        setConsola(e.target.value);
    }

    return (
        <Fragment>
        <h1>¿Cuál es tu videoconsola favorita?</h1>
        <input type="text" onChange={consolaChange} />
        <p>Mi videoconsola favorita es: {consola}</p>
        </Fragment>
    );
    }

    export default App;

useEffect
+++++++++

Realiza la ejecución de código después de renderizar la pantalla. Muy útil para subscribirse a servicios rest:

.. code-block::  
    :linenos:

    // se importa useEffect:
    import {useState, useEffect} from 'react';

    function App() {
        // se declara el hook tipo useState:
        const [mensaje, setMensaje] = useState(0);

        // el código de useEffect se ejecuta una vez renderizado el componente:
        useEffect(
            () => {
                // modificación de estado:
                window.setTimeout(()=>{
                    setMensaje(mensaje + 1);
                }, 1000);
            }, [mensaje] // este valor se dispara cuando detecta un cambio de estado
        )

        return <p>{mensaje}</p>;
    }

    export default App;

useContext
++++++++++

Crea un contexto por el que se pueden enviar propiedades a cualquier componente sin tener que enviarlo por parámetros:

1. Archivo que recibe el contexto **message.js**:

.. code-block::  
    :linenos:

    // importar en el archivo React y el hook:
    import React, {useContext} from 'react';
    // crear un mensaje:
    const mensaje = "Mensaje genérico";
    // cargar en el contexto de React:
    const MensajeContext = React.createContext(mensaje);

2. Uso del contexto:

.. code-block::  
    :linenos:

    function App() {
    // utilizar el context sin necesidad de hacer nada mas:
    const mensaje = useContext(MensajeContext);
    return <p>{mensaje}</p>;
    }

    export default App;


Formularios en React
####################

Combinando el uso de eventos y hooks se preparan los formularios 

.. code-block:: 
    :linenos:

    import {Fragment} from 'react';
    // importar el hook:
    import {useState} from 'react';
    import './App.css';

    function App() {
    // crear los hooks para el usuario y contraseña:
    const [usuario, setUsuario] = useState('');
    const [password, setPassword] = useState('');

    // cuando escribimos en el campo se irá cambiando su estado:
    const handleUsuario = (evento) =>{
        // se recupera el evento:
        setUsuario(evento.target.value);
        console.log(evento.target.value);
    }

    const handlePassword = (evento) =>{
        // se recupera el evento:
        setPassword(evento.target.value);
    }

    // Ejecutamos esta acción al hacer login:
    const login = (e) =>{
        // para prevenir que refresque por defecto la página:
        e.preventDefault();
        if(usuario === 'guillermo' && password === "1234"){
        alert("Sesión iniciada correctamente");
        }else{
        alert("Error al iniciar sesión");
        }
    }

    return (
        <>
        <form onSubmit={login}>
            <input type="text" placeholder="Usuario" onChange={handleUsuario} />
            <input type="password" placeholder="Contraseña" onChange={handlePassword} />
            <input type="submit" value="Iniciar sesión" />
        </form>
        </>
    );
    }

    export default App;


Rutas con React Router 
######################

Para las rutas se utiliza un modulo llamado React Router 

Instalación 
***********

Instalar el módulo en el proyecto: ``npm install react-router-dom --save``

Crear archivo de rutas 
**********************

1. Dentro de la carpeta **src** crear archivo **Router.js**:

.. code-block::  
    :linenos:

    // importar funciones del modulo react router:
    import {BrowserRouter, Route, Routes} from 'react-router-dom';
    // importar fragment también:
    import {Fragment} from 'react';

    // importar los componentes de vista:
    import Inicio from './Inicio';
    import Prueba from './Prueba';
    import Error from './Error';
    import Parametros from './Parametros';

    function Router(){
        // retornar la estructura de rutas:
        return(
            <Fragment>  
                <BrowserRouter>
                    <Routes>
                        {/* Ruta raiz (necesita el atributo exact): */}
                        <Route exact path="/" element={<Inicio />} />
                        <Route path="/prueba" element={<Prueba />} />
                        {/* Ruta con parametros: */}
                        <Route path="/parametros/:nombre" element={<Parametros />} />
                        {/* Ruta para urls no establecidas (error 404): */}
                        <Route path="*" element={<Error />} />
                    </Routes>
                </BrowserRouter>
            </Fragment>
        )
    }

    export default Router;

2. Cargar el enrutador en **App.js**:

.. code-block::  
    :linenos:

    import {Fragment} from 'react';
    import './App.css';
    // importar router:
    import Router from './Router';

    function App() {
    // cargar directamente el router en el return:
    return(
        <Fragment>
        <Router />
        </Fragment>
    )

    }

    export default App;
    
Recibir parámetros de una ruta 
******************************

Recibir parametros en el controlador **Parametros.js**:

.. code-block::  
    :linenos:

    // importar useParams de React Router:
    import { useParams } from 'react-router-dom';

    function Parametros(){
        // cargar un parametro mediante desestructuración:
        const {nombre} = useParams();

        return(
            <div>
                <h1>Te llamas: {nombre}</h1>
            </div>
        )
    }

    export default Parametros;

Crear Navbar con NavLink 
************************

Con la función **NavLink** se crea la barra de navegación de nuestra aplicación, editamos **Router.js**:

.. code-block::  
    :linenos:

    // importar función navlink:
    import {BrowserRouter, Route, Routes, NavLink} from 'react-router-dom';
    // importar fragment también:
    import {Fragment} from 'react';

    // importar los componentes de vista:
    import Inicio from './Inicio';
    import Prueba from './Prueba';
    import Error from './Error';
    import Parametros from './Parametros';

    function Router(){
        // retornar la estructura de rutas:
        return(
            <Fragment>  
                <BrowserRouter>
                    {/* cargamos el nav aquí: */}
                    <nav>
                        <NavLink to="/">Inicio</NavLink>
                        <NavLink to="/prueba" activeClassName="activa">Prueba</NavLink>
                        <NavLink to="/parametros/Guillermo" activeClassName="activa">Parametros</NavLink>
                    </nav>
                    <Routes>
                        <Route exact path="/" element={<Inicio />} />
                        <Route path="/prueba" element={<Prueba />} />
                        <Route path="/parametros/:nombre" element={<Parametros />} />
                        <Route path="*" element={<Error />} />
                    </Routes>
                </BrowserRouter>
            </Fragment>
        )
    }

    export default Router;

.. attention::
    El atributo **activeClassName** define el nombre de la clase que se activa cuando esta la ruta activa. 
    Solo hay que crear dicha clase en nuestro css y react router la reconocerá.

Proyecto API Rest 
#################

Paso 1: Preparar entorno 
************************

1. Tener instalado NodeJS desde su página oficial: https://nodejs.org/es/
2. Instalar React con npx desde la carpeta del proyecto: ``npx create-react-app task-list``
3. Acceder a la carpeta del proyecto e instalar axios que facilita las operaciones REST: ``npm install axios --save``
4. Ejecutar proyecto: ``npm start``
5. Se abre el navegador con la ruta: ``http://localhost:3000``
6. Crear una carpeta llamada **requests** donde guardaremos cada archivo para consumir APIs.


Paso 2: Diseñar tabla
*********************

Editamos el componente **App.js**:

.. code-block::  
    :linenos:

    import './App.css';

    function App() {
    return (
        <div className="App">
        <table border="1">
            <tr>
                <th>ID</th>
                <th>Título</th>
                <th>Descripción</th>
                <th>Fecha de creación</th>
                <th>Completa</th>
            </tr>
        </table>
        </div>
    );
    }

    export default App;


Paso 3: Preparar servicio para listar elementos 
***********************************************

1. Crear en la carpeta **requests** el archivo **taskRequest.js**:

.. code-block:: 
    :linenos:

    // importar axios:
    import axios from 'axios';

    // configurar axios para aceptar petición via JWT:
    const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYzMDc5OTI1MTU5OTE5NTE4M2NjYjM3OCIsImVtYWlsIjoicHl0b25pY3VzQGdtYWlsLmNvbSIsImlhdCI6MTY2MTQ0MjM3MiwiZXhwIjoxNjYxNDg1NTcyfQ.QaQ4BzKbGqWyXZv6Ltvp7mecm_2OsEk4-FUKnTuXOho";
    const config = {
        headers: {
            Authorization: token
        }  
    }

    // preparar url base:
    const url_base = "http://localhost:3977/api";

    // función para recuperar todas las tareas:
    async function getTasks(status){ // recibe por parametros el status del hook
        // se hace una petición con axios al endpoint y se guarda el resultado:
        await axios.get(`${url_base}/task`, config) // recibe la configuración
        .then(response => {
            status(response.data);
            console.log(response.data);
        }).catch(error =>{
            // avisar de cualquier error por consola:
            console.log(error);
        });
    }

    export{
        getTasks
    }

Paso 4: Cargar listado en la tabla
**********************************

.. code-block:: 
    :linenos:

    // importar hooks:
    import {useEffect, useState} from 'react';
    import './App.css';
    // importar el servicio:
    import {getTasks} from './requests/taskRequest';

    function App() {
    // crear un hook para cargar la información: 
    const [tasks, setTasks] = useState(null);

    // crear otro hook para llamar al servicio:
    useEffect(()=>{
        getTasks(setTasks)
    },[]);

    return (
        <div className="App">
        <table border="1">
            <tr>
                <th>ID</th>
                <th>Título</th>
                <th>Descripción</th>
                <th>Fecha de creación</th>
                <th>Completa</th>
            </tr>
            {/* Recorrer elementos y añadirlos a cada campo */}
            { tasks ? (
                tasks.map(task =>{
                return(
                    <tr key={task._id}>
                    <td>{task._id}</td>
                    <td>{task.title}</td>
                    <td>{task.description}</td>
                    <td>{task.create_at}</td>
                    <td>{task.complete ? ('Si'): ('No')}</td>
                    </tr>
                )
                })
            ): ('No existen tareas')}
        </table>
        </div>
    );
    }

    export default App;

Ahora se deben listar las tareas.

Paso 5: cargar registros con POST 
*********************************

Ahora se edita **taskRequest.js** para registrar tareas:

.. code-block::  
    :linenos:

    import axios from 'axios';

    const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYzMDc5OTI1MTU5OTE5NTE4M2NjYjM3OCIsImVtYWlsIjoicHl0b25pY3VzQGdtYWlsLmNvbSIsImlhdCI6MTY2MTQ0MjM3MiwiZXhwIjoxNjYxNDg1NTcyfQ.QaQ4BzKbGqWyXZv6Ltvp7mecm_2OsEk4-FUKnTuXOho";
    const config = {
        headers: {
            Authorization: token
        }  
    }

    const url_base = "http://localhost:3977/api";

    async function getTasks(status){ 
        await axios.get(`${url_base}/task`, config) 
        .then(response => {
            status(response.data);
            console.log(response.data);
        }).catch(error =>{
            console.log(error);
        });
    }

    // crear función para enviar datos a la API:
    async function postTask(status, titulo, descripcion){
        // se le pasan los campos uno a uno y luego la configuración con el token:
        await axios.post(`${url_base}/task`, {
            title: titulo,
            description: descripcion
        }, config)
        .then(response =>{
            console.log(status)
            // si todo va bien se modifica el estado del listado para añadir el resultado que será la nueva tarea:
            status(tasks => [...tasks, response.data.task]);
        }).catch(error =>{
            console.log(error);
        });
    }

    export{
        getTasks,
        postTask
    }

Paso 6: Crear formulario para añadir tareas 
*******************************************

Volver a **App.js** y crear un formulario para registrar tareas:

.. code-block::  
    :linenos:

    import {useEffect, useState} from 'react';
    import './App.css';
    import {getTasks, postTask} from './requests/taskRequest';

    function App() {
    const [tasks, setTasks] = useState(null);
    // crear hooks para campos del form:
    const [titulo, setTitulo] = useState(null);
    const [descripcion, setDescripcion] = useState(null);

    // crear los handles para cada campo del form:
    const handleTitulo = (e) =>{
        setTitulo(e.target.value);
    }

    const handleDescripcion = (e) => {
        setDescripcion(e.target.value);
    }

    // crear función que va a guardar la tarea:
    const sendTask = (e) => {
        e.preventDefault();
        // se manda el estado del hook y los campos a guardar:
        postTask(setTasks, titulo, descripcion)
    }

    useEffect(()=>{
        getTasks(setTasks)
    },[

    ]);

    return (
        <div className="App">
        <table border="1">
            <tr>
                <th>ID</th>
                <th>Título</th>
                <th>Descripción</th>
                <th>Fecha de creación</th>
                <th>Completa</th>
            </tr>
            { tasks ? (
                tasks.map(task =>{
                return(
                    <tr key={task._id}>
                    <td>{task._id}</td>
                    <td>{task.title}</td>
                    <td>{task.description}</td>
                    <td>{task.create_at}</td>
                    <td>{task.complete ? ('Si'): ('No')}</td>
                    </tr>
                )
                })
            ): ('No existen tareas')}
        </table>
        <hr/>
        {/* Añadir un formulario para crear nuevas tareas: */}
        <form onSubmit={sendTask}>
            <label for="titulo">Título: </label>
            <input type="text" onChange={handleTitulo} />
            <label for="descripcion">Descripción: </label>
            <input type="text" onChange={handleDescripcion} />
            <input type="submit" value="Guardar tarea" />
        </form>
        </div>
    );
    }

    export default App;

Paso 7: Editar documentos (tareas ok)
*************************************

Se edita el nuevo servicio para hacer update en **taskRequest.js**:

.. code-block::  
    :linenos:

    import axios from 'axios';

    const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYzMDc5OTI1MTU5OTE5NTE4M2NjYjM3OCIsImVtYWlsIjoicHl0b25pY3VzQGdtYWlsLmNvbSIsImlhdCI6MTY2MTQ0MjM3MiwiZXhwIjoxNjYxNDg1NTcyfQ.QaQ4BzKbGqWyXZv6Ltvp7mecm_2OsEk4-FUKnTuXOho";
    const config = {
        headers: {
            Authorization: token
        }  
    }

    const url_base = "http://localhost:3977/api";

    async function getTasks(status){ 
        await axios.get(`${url_base}/task`, config) 
        .then(response => {
            status(response.data);
            console.log(response.data);
        }).catch(error =>{
            console.log(error);
        });
    }

    async function postTask(status, titulo, descripcion){
        await axios.post(`${url_base}/task`, {
            title: titulo,
            description: descripcion
        }, config)
        .then(response =>{
            console.log(status)
            status(tasks => [...tasks, response.data.task]);
        }).catch(error =>{
            console.log(error);
        });
    }

    // crear función para editar tarea y ponerla a ok:
    async function setOK(tasks, setTasks, id){ // recibe estado del listado y el id
        await axios.put(`${url_base}/task/${id}`, {
            complete: true
        }, config)
        .then(response =>{
            // recorrer las tareas en busca de la que coincida con el id:
            tasks.map(task =>{
                if(task._id === id){
                    task.complete = true
                }
                // pide un return siempre despues de un map:
                return(null);
            });
            // actualizar lista de tareas:
            setTasks(tasks => [...tasks]);
        }).catch(error =>{
            console.log(error);
        })
    }

    export{
        getTasks,
        postTask,
        setOK
    }

Paso 8: Botón para editar documentos 
************************************

Añadir el botón y la función para actualizar tarea en **App.js**:

.. code-block:: 
    :linenos:

    import {useEffect, useState} from 'react';
    import './App.css';
    import {getTasks, postTask, setOK} from './requests/taskRequest';

    function App() {
    const [tasks, setTasks] = useState(null);
    const [titulo, setTitulo] = useState(null);
    const [descripcion, setDescripcion] = useState(null);

    const handleTitulo = (e) =>{
        setTitulo(e.target.value);
    }

    const handleDescripcion = (e) => {
        setDescripcion(e.target.value);
    }

    const sendTask = (e) => {
        e.preventDefault();
        postTask(setTasks, titulo, descripcion)
    }

    // función para actualizar tarea, recuerda usar eventos con retorno:
    const updateOK = (id) =>{ // sino se hace así te coge todos los id
        return(e) => {
        setOK(tasks, setTasks, id);
        }
    }

    useEffect(()=>{
        getTasks(setTasks)
    },[

    ]);

    return (
        <div className="App">
        <table border="1">
            <tr>
                <th>ID</th>
                <th>Título</th>
                <th>Descripción</th>
                <th>Fecha de creación</th>
                <th>Completa</th>
                <th colspan="2"></th>
            </tr>
            { tasks ? (
                tasks.map(task =>{
                return(
                    <tr key={task._id}>
                    <td>{task._id}</td>
                    <td>{task.title}</td>
                    <td>{task.description}</td>
                    <td>{task.create_at}</td>
                    <td>{task.complete ? ('Si'): ('No')}</td>
                    {/* Añadir botón para terminar tareas a ok: */}
                    <td><button onClick={updateOK(task._id)}>finalizar</button></td>
                    </tr>
                )
                })
            ): ('No existen tareas')}
        </table>
        <hr/>
        <form onSubmit={sendTask}>
            <label for="titulo">Título: </label>
            <input type="text" onChange={handleTitulo} />
            <label for="descripcion">Descripción: </label>
            <input type="text" onChange={handleDescripcion} />
            <input type="submit" value="Guardar tarea" />
        </form>
        </div>
    );
    }

    export default App;

Paso 9: Crear servicio para eliminar tareas 
*******************************************

Editar el servicio **taskRequest.js**:

.. code-block:: 
    :linenos:

    import axios from 'axios';

    const token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYzMDc5OTI1MTU5OTE5NTE4M2NjYjM3OCIsImVtYWlsIjoicHl0b25pY3VzQGdtYWlsLmNvbSIsImlhdCI6MTY2MTQ0MjM3MiwiZXhwIjoxNjYxNDg1NTcyfQ.QaQ4BzKbGqWyXZv6Ltvp7mecm_2OsEk4-FUKnTuXOho";
    const config = {
        headers: {
            Authorization: token
        }  
    }

    const url_base = "http://localhost:3977/api";

    async function getTasks(status){ 
        await axios.get(`${url_base}/task`, config) 
        .then(response => {
            status(response.data);
            console.log(response.data);
        }).catch(error =>{
            console.log(error);
        });
    }

    async function postTask(status, titulo, descripcion){
        await axios.post(`${url_base}/task`, {
            title: titulo,
            description: descripcion
        }, config)
        .then(response =>{
            console.log(status)
            status(tasks => [...tasks, response.data.task]);
        }).catch(error =>{
            console.log(error);
        });
    }

    async function setOK(tasks, setTasks, id){ 
        await axios.put(`${url_base}/task/${id}`, {
            complete: true
        }, config)
        .then(response =>{
            tasks.map(task =>{
                if(task._id === id){
                    task.complete = true
                }
                return(null);
            });
            setTasks(tasks => [...tasks]);
        }).catch(error =>{
            console.log(error);
        })
    }

    // eliminar tarea:
    async function deleteTask(tasks, setTasks, id){
        await axios.delete(`${url_base}/task/${id}`, config)
        .then(response => {
        // eliminar tarea de la colección:
        tasks.pop(id);
        // cargar en el
        setTasks(tasks => [...tasks]);
        }).catch(error =>{  
            console.log(error);
        })
    }

    export{
        getTasks,
        postTask,
        setOK,
        deleteTask
    }

Paso 10: Crear botón y función para eliminar tareas 
***************************************************

Ir a **App.js** y añadir el siguiente código:

.. code-block:: 
    :linenos:

    import {useEffect, useState} from 'react';
    import './App.css';
    import {getTasks, postTask, setOK, deleteTask} from './requests/taskRequest';

    function App() {
    const [tasks, setTasks] = useState(null);
    const [titulo, setTitulo] = useState(null);
    const [descripcion, setDescripcion] = useState(null);

    const handleTitulo = (e) =>{
        setTitulo(e.target.value);
    }

    const handleDescripcion = (e) => {
        setDescripcion(e.target.value);
    }

    const sendTask = (e) => {
        e.preventDefault();
        postTask(setTasks, titulo, descripcion)
    }

    const updateOK = (id) =>{
        return(e) => {
        const id = e.target.value;
        setOK(tasks, setTasks, id);
        }
    }

    // funcion para eliminar tarea:
    const removeTask = (id) => {
        return(e) => {
        const id = e.target.value;
        deleteTask(tasks, setTasks, id);
        }
    }

    useEffect(()=>{
        getTasks(setTasks)
    },[

    ]);

    return (
        <div className="App">
        <table border="1">
            <tr>
                <th>ID</th>
                <th>Título</th>
                <th>Descripción</th>
                <th>Fecha de creación</th>
                <th>Completa</th>
            </tr>
            { tasks ? (
                tasks.map(task =>{
                return(
                    <tr key={task._id}>
                    <td>{task._id}</td>
                    <td>{task.title}</td>
                    <td>{task.description}</td>
                    <td>{task.create_at}</td>
                    <td>{task.complete ? ('Si'): ('No')}</td>
                    <td>
                        <button value={task._id} onClick={updateOK()}>finalizar</button>
                        {/* Añadir botón para eliminar tareas: */}
                        <button value={task._id} onClick={removeTask()}>eliminar</button>
                    </td>
                    </tr>
                )
                })
            ): ('No existen tareas')}
        </table>
        <hr/>
        <form onSubmit={sendTask}>
            <label for="titulo">Título: </label>
            <input type="text" onChange={handleTitulo} />
            <label for="descripcion">Descripción: </label>
            <input type="text" onChange={handleDescripcion} />
            <input type="submit" value="Guardar tarea" />
        </form>
        </div>
    );
    }

    export default App;

Preparar sistema de login vía JWT
#################################

Paso 1: Preparar proyecto  
*************************

- Instalar react router: ``npm install react-router-dom --save``
- Instalar React JWT: ``npm install react-jwt --save``
- Dentro de **src** crear directorio **helpers**.
- Ahora dentro de **helpers** crear archivo **checkToken.js**:


Paso 2: Mover datos a un nuevo componente 
*****************************************

- Crear una carpeta llamada **pages** y dentro un archivo **TaskPage.js** y mover contenido de **App.js**:

.. code-block:: 
    :linenos:

    import {useEffect, useState} from 'react';
    import {getTasks, postTask, setOK, deleteTask} from '../requests/taskRequest';


    function TaskPage(){
        const [tasks, setTasks] = useState(null);
        const [titulo, setTitulo] = useState(null);
        const [descripcion, setDescripcion] = useState(null);
    
        const handleTitulo = (e) =>{
        setTitulo(e.target.value);
        }
    
        const handleDescripcion = (e) => {
        setDescripcion(e.target.value);
        }
    
        const sendTask = (e) => {
        e.preventDefault();
        postTask(setTasks, titulo, descripcion)
        }
    
        const updateOK = (id) =>{
        return(e) => {
            const id = e.target.value;
            setOK(tasks, setTasks, id);
        }
        }
    
        // funcion para eliminar tarea:
        const removeTask = (id) => {
        return(e) => {
            const id = e.target.value;
            deleteTask(tasks, setTasks, id);
        }
        }
    
        useEffect(()=>{
        getTasks(setTasks)
        },[
    
        ]);
    
        return (
        <div className="App">
            <table border="1">
                <tr>
                <th>ID</th>
                <th>Título</th>
                <th>Descripción</th>
                <th>Fecha de creación</th>
                <th>Completa</th>
                </tr>
                { tasks ? (
                tasks.map(task =>{
                    return(
                    <tr key={task._id}>
                        <td>{task._id}</td>
                        <td>{task.title}</td>
                        <td>{task.description}</td>
                        <td>{task.create_at}</td>
                        <td>{task.complete ? ('Si'): ('No')}</td>
                        <td>
                        <button value={task._id} onClick={updateOK()}>finalizar</button>
                        {/* Añadir botón para eliminar tareas: */}
                        <button value={task._id} onClick={removeTask()}>eliminar</button>
                        </td>
                    </tr>
                    )
                })
                ): ('No existen tareas')}
            </table>
            <hr/>
            <form onSubmit={sendTask}>
            <label for="titulo">Título: </label>
            <input type="text" onChange={handleTitulo} />
            <label for="descripcion">Descripción: </label>
            <input type="text" onChange={handleDescripcion} />
            <input type="submit" value="Guardar tarea" />
            </form>
        </div>
        );
    }

    export default TaskPage;

Paso 3: Crear nuevo servicio para usuarios
******************************************

- En la carpeta **requests** creamos el servicio **userRequest.js**:

.. code-block::  
    :linenos:

    import axios from 'axios';

    const url_base = "http://localhost:3977/api";

    async function loginRequest(email, password){
        await axios.post(`${url_base}/login`, {
            email: email,
            password: password
        })
        .then(response =>{
            localStorage.setItem('token', response.data.token);
            window.location.href = 'http://localhost:3000';
        }).catch(error =>{
            console.log(error);
        });
    }

    export{
        loginRequest
    } 

Paso 4: Crear componente para página 
************************************

- Crear componente **LoginPage.js** en la carpeta **pages**:

.. code-block::  
    :linenos:

    import {useState} from 'react';
    // importar servicio:
    import {loginRequest} from '../requests/userRequest';

    function LoginPage(){

        const [email, setEmail] = useState('');
        const [password, setPassword] = useState('');

        const emailHandle = (e) => {
            setEmail(e.target.value);
        }

        const passwordHandle = (e) => {
            setPassword(e.target.value);
        }

        const loginHandle = (e)=> {
            e.preventDefault();
            loginRequest(email, password);
        }

        return(
            <div>
                <h1>Pagina de login </h1>
                <form onSubmit={loginHandle}>
                    <label>Email: </label>
                    <input type="text" onChange={emailHandle} />
                    <label>Password: </label>
                    <input type="password" onChange={passwordHandle} />
                    <input type="submit" value="Iniciar sesión" />
                </form>
            </div>
        )
    }

    export default LoginPage;

Paso 5: Crear archivo de rutas y validador de rutas 
***************************************************

Añadir a la carpeta **src** el archivo **Router.js**:

.. code-block:: 
    :linenos:

    import {BrowserRouter, Route, Routes, Navigate} from "react-router-dom";
 
    // importar fragment también:
    import {Fragment} from 'react';

    // importar nuestro comprobador de token:
    import {useJwt} from "react-jwt";

    import TaskPage from './pages/TaskPage';
    import LoginPage from './pages/LoginPage';


    function Router() {
        // recuperar token:
        const localToken = localStorage.getItem("token");
        // comprobar si ha caducado:
        const {isExpired} = useJwt(localToken);

        const redirect = <Navigate replace to='/login' /> 
    
        return(
            <Fragment>
                <BrowserRouter>
                    <Routes>
                        {/* Ahora se cambia el estado del componente raiz por RouteGuard: */}
                        <Route exact path="/" element={
                            isExpired ? redirect : <TaskPage />} />
                        <Route path="/login" element={<LoginPage />} />
                    </Routes>
                </BrowserRouter>
            </Fragment>
        );
    }

    export default Router;

Paso 6: Modificar archivo App.js
********************************

- Ahora hay que añadir el enrutador a **App.js**:

.. code-block:: 
    :linenos:

    import './App.css';
    // importar rutas:
    import Router from './Router';

    function App() {
        return(
            <div>
                <h1>Task Maker</h1>
                <Router />
            </div>
        )
    }

    export default App;
    

Paso 7: Recuperar el token correctamente para tareas 
****************************************************

- Hay que modificar el servicio **taskRequest.js**:

.. code-block:: 
    :linenos:

    import axios from 'axios';

    const config = {
        headers: {
            Authorization: localStorage.getItem("token") // pasar el token guardado a la autorización
        }  
    }

    console.log(config);

    const url_base = "http://localhost:3977/api";

    async function getTasks(status){ 
        await axios.get(`${url_base}/task`, config) 
        .then(response => {
            status(response.data);
            console.log(response.data);
        }).catch(error =>{
            console.log(error);
        });
    }

    async function postTask(status, titulo, descripcion){
        await axios.post(`${url_base}/task`, {
            title: titulo,
            description: descripcion
        }, config)
        .then(response =>{
            console.log(status)
            status(tasks => [...tasks, response.data.task]);
        }).catch(error =>{
            console.log(error);
        });
    }

    async function setOK(tasks, setTasks, id){ 
        await axios.put(`${url_base}/task/${id}`, {
            complete: true
        }, config)
        .then(response =>{
            tasks.map(task =>{
                if(task._id === id){
                    task.complete = true
                }
                return(null);
            });
            setTasks(tasks => [...tasks]);
        }).catch(error =>{
            console.log(error);
        })
    }

    // eliminar tarea:
    async function deleteTask(tasks, setTasks, id){
        await axios.delete(`${url_base}/task/${id}`, config)
        .then(response => {
        // eliminar tarea de la colección:
        tasks.pop(id);
        // cargar en el
        setTasks(tasks => [...tasks]);
        }).catch(error =>{  
            console.log(error);
        })
    }

    export{
        getTasks,
        postTask,
        setOK,
        deleteTask
    }

