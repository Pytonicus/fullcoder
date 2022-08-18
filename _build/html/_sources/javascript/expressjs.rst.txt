Framework: ExpressJS  
====================

.. image:: /logos/logo-express.png
    :scale: 50%
    :alt: Logo Angular
    :align: center

.. |date| date::
.. |time| date:: %H:%M

Documentación básica de NodeJS 

.. contents:: Índice
  
Configuraciones
###############  

* Crear una carpeta para el proyecto y dentro ejecutar ``npm init``
* RECOMENDADO Instalar nodemon: ``npm install nodemon`` y agregar al **package.json**
* Instalar ExpressJS: ``npm install express --save``

Archivo Inicial
***************

* Se crea un archivo **index.js** o simil:

.. code-block:: javascript
    :linenos:

    // importamos la librería express:
    const express = require('express');

    // instanciamos express:
    const app = express();
    // definimos el puerto:
    const port = 3000;

    // se preparan los datos hardcodeados:
    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ]

    // Creamos una ruta raiz:
    app.get('/', (req, res)=>{
        // se define la cabezera y el cuerpo:
        res.status(200).send(consolas); // no hay que parsear a json.
    });

    // creamos el servidor:
    app.listen(port, ()=>{
        console.log(`Servidor ejecutandose en http://localhost:${port}`);
    });

Habilitar CORS
##############

Por defecto el proyecto tiene las CORS restringidas, de modo que si vamos a conectarnos desde 
una aplicación externa se bloqueará.

* Para trabajar con cors se instala ``npm install cors --save``

CORS Publicas
*************
Habilitar cors para hacer publica la API: 

.. code-block:: javascript 
    :linenos:

    const express = require('express');

    const app = express();
    const port = 3500;
    // importamos la librería cors:
    const cors = require('cors');

    // decimos a express que defina los cors (por defecto ahora es pública):
    app.use(cors());


Rutas Express
#############

Peticiones Get
**************

Ejemplo de Get con parámetros:

.. code-block:: javascript
    :linenos:

    const express = require('express');

    const app = express();
    const port = 3000;

    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ]

    app.get('/', (req, res)=>{
        res.status(200).send(consolas); 
    });

    // petición get de una ruta con un parámetro:
    app.get('/consola/:modelo', (req, res)=>{
        // recorremos las consolas y recuperamos la consola con el modelo buscado:
        let consola = consolas.find(elem => {
            return elem.modelo === req.params.modelo;
        });
        // si no encuentra nada:
        if(consola === undefined){
            return res.status(404).json({
                message: 'No se encontró ninguna consola'
            })
        }
        res.status(200).send(consola);
    });

    app.listen(port, ()=>{
        console.log(`Servidor ejecutandose en http://localhost:${port}`);
    });

Peticiones POST 
***************

Ejemplo de inserciones post:

.. code-block:: javascript 
    :linenos:

    const express = require('express');

    const express = require('express');

    const app = express();
    const port = 3000;

    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ];

    // ejecutamos el siguiente middleware para parsear código json de todo el body que entra por POST:
    app.use(express.json());
    app.use(express.urlencoded({extended: true}));

    app.get('/', (req, res)=>{
        res.status(200).send(consolas); 
    });

    app.get('/consola/:modelo', (req, res)=>{
        let consola = consolas.find(elem => {
            return elem.modelo === req.params.modelo;
        });

        if(consola === undefined){
            return res.status(404).json({
                message: 'Consola creada correctamente'
            })
        }
        res.status(200).send(consola);
    });

    // petición post:
    app.post('/consola/crear/', (req, res)=>{
        // añadir el nuevo valor al array:
        consolas.push(req.body);
        // devolvemos una respuesta:
        res.status(201).json({
            mensaje: 'Se ha registrado la consola'
        });
    });

    app.listen(port, ()=>{
        console.log(`Servidor ejecutandose en http://localhost:${port}`);
    });

Peticiones PUT  
**************

Ejemplo de actualizaciones put:

.. code-block:: javascript 
    :linenos:

    const express = require('express');

    const app = express();
    const port = 3000;

    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ];

    app.use(express.json());
    app.use(express.urlencoded({extended: true}));

    app.get('/', (req, res)=>{
        res.status(200).send(consolas); 
    });

    app.get('/consola/:modelo', (req, res)=>{
        let consola = consolas.find(elem => {
            return elem.modelo === req.params.modelo;
        });

        if(consola === undefined){
            return res.status(404).json({
                message: 'Consola creada correctamente'
            })
        }
        res.status(200).send(consola);
    });

    app.post('/consola/crear/', (req, res)=>{
        consolas.push(req.body);
        res.status(201).json({
            mensaje: 'Se ha registrado la consola'
        });
    });

    // crear un put que recibirá un parámetro para buscar el registro a actualizar:
    app.put('/consola/actualizar/:modelo', (req, res)=>{
        // localizar la posición en el array:
        let i = consolas.findIndex(elem => {
            return elem.modelo === req.params.modelo;
        });
        console.log();
        // si existe coincidencia se procede a crear:
        if(i > 0){
            consolas[i] = req.body;
            res.status(201).json({
                message: 'Consola actualizada con éxito'
            });
        }
    });

    app.listen(port, ()=>{
        console.log(`Servidor ejecutandose en http://localhost:${port}`);
    });


Peticiones DELETE   
*****************

Ejemplo de actualizaciones put:

.. code-block:: javascript 
    :linenos:

    const express = require('express');

    const app = express();
    const port = 3000;

    let consolas = [
        {marca: 'Sony', modelo: 'PlayStation', lanzamiento: 1994},
        {marca: 'Sega', modelo: 'MegaDrive ', lanzamiento: 1991},
        {marca: 'Nintendo', modelo: 'Gameboy', lanzamiento: 1989},
        {marca: 'Microsoft', modelo: 'XBOX', lanzamiento: 2001},
    ];

    app.use(express.json());
    app.use(express.urlencoded({extended: true}));

    app.get('/', (req, res)=>{
        res.status(200).send(consolas); 
    });

    app.get('/consola/:modelo', (req, res)=>{
        let consola = consolas.find(elem => {
            return elem.modelo === req.params.modelo;
        });

        if(consola === undefined){
            return res.status(404).json({
                message: 'Consola creada correctamente'
            })
        }
        res.status(200).send(consola);
    });

    app.post('/consola/crear/', (req, res)=>{
        consolas.push(req.body);
        res.status(201).json({
            mensaje: 'Se ha registrado la consola'
        });
    });

    app.put('/consola/actualizar/:modelo', (req, res)=>{
        let i = consolas.findIndex(elem => {
            return elem.modelo === req.params.modelo;
        });
        console.log();
        if(i > 0){
            consolas[i] = req.body;
            res.status(201).json({
                message: 'Consola actualizada con éxito'
            });
        }
    });

    // el delete recibirá también un parámetro para localizar un elemento:
    app.delete('/consola/eliminar/:modelo', (req, res)=>{
        let i = consolas.findIndex(elem => {
            return elem.modelo === req.params.modelo;
        });
        console.log();
        if(i > 0){
            // ejecutar método para borrar y mensaje:
            consolas.splice(i, 1);
            res.status(200).json({
                message: 'Consola eliminada con éxito'
            });
        }
    });

    app.listen(port, ()=>{
        console.log(`Servidor ejecutandose en http://localhost:${port}`);
    });


Proyecto API rest Estructurado 
##############################

Paso 1 - Iniciar proyecto
*************************

- Crear una carpeta para el proyecto.
- Crear un repositorio en github, gitlab o simil.
- ejecutar ``npm init`` para iniciar el proyecto.
- instalar express: ``npm install express --save``

Paso 2 - Preparar estructura 
****************************

- crear archivos **index.js** y **app.js**
- crear carpetas **controllers**, **routes** y **models**

Paso 3 - Archivo de entrada (index.js)
**************************************

.. code-block:: javascript 
    :linenos:

    // importa la constante app con express:
    const app = require('./app');
    const port = 3000;

    app.listen(port, () => {
        console.log(`Servidor funcionando en: http://localhost:${port}`);
    });

Paso 4 - Archivo que ejecuta dependencias (app.js)
**************************************************

.. code-block:: javascript 
    :linenos:

    // importar e inicializar express:
    const express = require("express");
    const app = express();

    // Cargar rutas de cada archivo enrutador:
    const pruebaRoutes = require("./routes/pruebaRoutes");

    // ruta base:
    app.use("/api", pruebaRoutes);

    // exportar app para index.js:
    module.exports = app;


Paso 5 - Crear controlador
**************************

En la carpeta controllers se crea el controlador **pruebaController**:

.. code-block:: javascript 
    :linenos:

    // se crea la función del controlador que recibe el request y la response:
    function getPrueba(req, res){
        res.status(200).send({msg: "controller de prueba"});
    }

    module.exports = {
        getPrueba
    }; 

Paso 6 - Crear archivo de rutas 
*******************************

En la carpeta routes se crea el archivo **pruebaRoutes**:

.. code-block:: javascript 
    :linenos:

    // se importa y carga el enrutador de express:
    const express = require('express');
    const api = express.Router();

    // se importan los controladores para cada ruta:
    const pruebaController = require("../controllers/pruebaController");

    // se le pasa el controlador a la ruta:
    api.get("/prueba", pruebaController.getPrueba);

    // se exporta el archivo de rutas:
    module.exports = api;


Ejecutar el servidor y acceder a la ruta: http://localhost:3000/api/prueba

Paso 7 - Conectar a la base de datos MongoDB
********************************************

Lo primero será instalar en el proyecto mongoose: ``npm install mongoose --save``

Ahora vamos al archivo **index.js** y editamos:

.. code-block:: javascript 
    :linenos:

    // se importa el paquete mongoose:
    const mongoose = require("mongoose");
    const app = require('./app');
    const port = 3000;

    // conectar a mongo introduciendo ruta y nombre de la base de datos tras la barra:
    mongoose.connect("mongodb://localhost:27017/tasker", {
        // se añade una configuración recomendada
        useNewUrlParser: true, 
        useUnifiedTopology: true,
        // si existe algún tipo de mensaje de error añadir esta opción: useFindAndModify: false
    }, (err, res)=>{
            try{
                if(err){
                    throw err;
                }else{
                    console.log("Se ha establecido la conexión a la base de datos");
                }
            }catch(error){
                console.error(error);
            }
        });


    app.listen(port, () => {
        console.log(`Servidor funcionando en: http://localhost:${port}`);
    });

Paso 8 - Configurar entorno para trabajar con JSON
**************************************************

Nos vamos a **app.json** y se añade lo siguiente:

.. code-block:: javascript 
    :linenos:

    const express = require("express");
    const app = express();

    // para trabajar con json se carga el modulo json de express:
    app.use(express.json());
    app.use(express.urlencoded({extended: true})); // también es necesaria la codificación

    const hello_routes = require("./routes/hello");
    const task_routes = require('./routes/taskRoutes'); 

    app.use("/api", hello_routes);
    app.use('/api', task_routes);  

    module.exports = app;


Paso 9 - Crear modelo de datos con MongoDB 
******************************************

En la carpeta models se crea un archivo llamado **taskModel.js**:

.. code-block:: javascript 
    :linenos:

    // se importa mongoose para mongodb y se inicializa el modulo schema para hacer un modelo:
    const mongoose = require('mongoose');
    const Schema = mongoose.Schema;

    // se crea un schema del modelo:
    const TaskSchema = Schema({
        title: {
            type: String,
            require: true
        },
        description: {
            type: String,
            require: true
        },
        complete: {
            type: Boolean,
            require: true,
            default: false
        },
        create_at: {
            type: Date,
            require: true,
            default: Date.now
        }
    });

    // se exporta el modelo:
    module.exports = mongoose.model("Task", TaskSchema);

Paso 10 - Crear controlador para gestionar peticiones 
*****************************************************

en la carpeta controllers se crea un nuevo controlador llamado **taskController.js**:

.. code-block:: javascript 
    :linenos:

    const Task = require('../models/taskModel');

    // la funcion será asíncrona para que espere a terminar de guardar antes de proceder:
    async function createTask(req, res){
        // se crea una instancia del modelo:
        const task = new Task();
        // recuperar los parámetros del body:
        const params = req.body;

        // recuperar los datos del body y añadirlos al modelo:
        task.title = params.title;
        task.description = params.description;

        // guardar datos:
        try{
            // guardar resultados en la base de datos:
            const taskStore = await task.save(); // el proceso será lineal hasta llegar al await (evita ejecutar todo a la vez)

            // revisar si no se ha guardado la tarea:
            if(!taskStore){
                res.status(400).send({msg: "No se ha guardado la tarea"});
            }else{
                res.status(200).send({task: taskStore});
            }
        }catch (error){
            // devolver error 500 si sale mal:
            res.status(500).send(error);
        }
    }

    // función para listar tareas:
    async function getTasks(req, res){
        try{
            // recuperar tareas de base de datos:
            const tasks = await Task.find().sort({create_at: -1}); // opcional: ordenar resultados con sort por un parámetro seleccionado.
            // Agregar condición dentro de find: const tasks = await Task.find({completed: false}).sort({create_at: -1}); 

            // comprobar si hay tareas:
            if(!tasks){
                res.status(400).send({msg: "Error al obtener las tareas"});
            }else {
                res.status(200).send(tasks);
            }
        }catch(error){
            res.status(500).send(error);
        }
    }

    // recuperar un solo resultado:
    async function getTask(req, res){
        // recuperar el id:
        const taskId = req.params.id;

        try{
            // se hace un findById con el id recibido por request:
            const task = await Task.findById(taskId);

            if(!task){
                res.status(400).send({msg: "No existe la tarea"});
            }else{
                res.status(200).send(task);
            }
        }catch(error){
            res.status(500).send(error);
        }
    }

    // crear la función asincrona para actualizar tareas:
    async function updateTask(req, res){
        // recuperar el id:
        const taskId = req.params.id;
        // recuperar parametros a actualizar:
        const params = req.body;

        try{
            // realizar consulta para recuperar la tarea y le pasamos los datos a actualizar:
            const task = await Task.findByIdAndUpdate(taskId, params); // OJO: ahora usamos findByIdAndUpdate()


            if(!task){
                res.status(400).send({msg: "No existe la tarea"});
            }else{
                res.status(200).send(task);
            }
        }catch(error){
            res.status(500).send(error);
        }
    }

    // función para eliminar datos:
    async function deleteTask(req, res){
        // recuperar el id:
        const taskId = req.params.id;

        try{
            // realizar delete:
            const task = await Task.findByIdAndDelete(taskId); 

            if(!task){
                res.status(400).send({msg: "No existe la tarea"});
            }else{
                res.status(200).send({msg: "Se ha eliminado la tarea correctamente"});
            }
        }catch(error){
            res.status(500).send(error);
        }
    }

    module.exports = {
        createTask,
        getTasks,
        getTask,
        updateTask,
        deleteTask
    }

Paso 11: crear rutas para peticiones  
************************************

Nos vamos a la carpeta routes y se crea el archivo **taskRoutes.js**:

.. code-block:: javascript
    :linenos:

    const express = require('express');
    const api = express.Router();

    const taskController = require("../controllers/taskController");

    api.post("/task", taskController.createTask);
    api.get("/task", taskController.getTasks);
    api.get("/task/:id", taskController.getTask);
    api.put("/task/:id", taskController.updateTask);
    api.delete("/task/:id", taskController.deleteTask);

    module.exports = api;


Paso 12: Añadir el archivo de rutas a app.json
**********************************************

.. code-block:: javascript 
    :linenos:

    const express = require("express");
    const app = express();

    app.use(express.json());
    app.use(express.urlencoded({extended: true})); 

    const hello_routes = require("./routes/hello");
    const task_routes = require('./routes/taskRoutes'); // tras crear ruta se añade aquí

    app.use("/api", hello_routes);
    app.use('/api', task_routes);  // tras crear ruta se añade aquí

    module.exports = app;


