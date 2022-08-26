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

    // se exporta el modelo añadiendo el nombre de la colección de MongoDB y el Schema:
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


Securizar una API Restful
#########################

Paso 1: Instalación de dependencias 
***********************************

- Se instalará `moment` para controlar las fechas: ``npm install moment --save``
- Se instalará `jsonwebtoken` para trabajar con JWT: ``npm install jsonwebtoken --save``
- Se instalará `bcryptjs` para encriptación de contraseñas: ``npm install bcryptjs -- save``

Paso 2: Modelo de usuarios
**************************

- en la carpeta **models** se crea el archivo **userModel.js**:

.. code-block:: javascript
    :linenos:

    const mongoose = require('mongoose');
    const Schema = mongoose.Schema;

    const UserSchema = Schema({
        name: {
            type: String,
            require: false
        },
        lastname: {
            type: String,
            require: false 
        },
        email: {
            type: String,
            require: true,
            unique: true,
        },
        password: {
            type: String,
            require: true 
        },
        avatar: {
            type: String,
            require: false
        }
    });

    module.exports = mongoose.model('users', UserSchema);


Paso 3: Controlador para usuarios 
*********************************

En la carpeta **controllers** crear el archivo **userController.js**:

.. code-block:: javascript 
    :linenos:

    // importar el encriptador de contraseñas: 
    const bcryptjs = require('bcryptjs');
    const User = require('../models/userModel');

    // Registro de usuarios:
    async function register(req, res){
        const params = req.body;
        const user = new User(params);

        try{
            // comprobar que los campos email y password:
            if(!params.email) throw{msg: "Email es un campo obligatorio"};
            if(!params.password) throw{msg: "Contraseña es un campo obligatorio"};

            // revisar si el email esta en uso:
            const emailExists = await User.findOne({email: params.email});
            if(emailExists) throw {msg: "Email ya se encuentra en uso"};

            // configurar el salt de bcrypt: 
            const salt = bcryptjs.genSaltSync(10);
            // encriptar la contraseña:
            user.password = await bcryptjs.hash(params.password, salt);
            
            user.save();
            res.status(200).send(user);
            
        }catch(error){
            res.status(500).send(error);
        }
    }

    module.exports = {
        register,
    }

Paso 4: Endpoint de usuarios 
****************************

En la carpeta **routes** crear el archivo **userRoutes.js**:

.. code-block:: javascript 
    :linenos:

    const express = require("express");
    const userController = require('../controllers/userController');

    const api = express.Router();

    api.post("/register", userController.register);


    module.exports = api;

Paso 5: Añadir endpoint de rutas a usuarios 
*******************************************

Editar app.js para añadir las rutas de usuarios:

.. code-block:: javascript 
    :linenos:

    const express = require("express");
    const app = express();

    app.use(express.json());
    app.use(express.urlencoded({extended: true})); 

    const hello_routes = require("./routes/hello");
    const task_routes = require('./routes/taskRoutes');
    const user_routes = require('./routes/userRoutes');

    app.use("/api", hello_routes);
    app.use('/api', task_routes);
    app.use('/api', user_routes);

    module.exports = app;


Paso 6: Crear el servicio JWT para login por token 
**************************************************

En la raiz del proyecto crear la carpeta **services** y dentro el archivo **jwtService.js**:

.. code-block:: javascript 
    :linenos:

    // importar jwt:
    const jwt = require("jsonwebtoken");

    // crear la clave secreta (escribe algo aleatorio):
    const SECRET_KEY = "2ha9df238dhha87d8vaq";

    // crear token:
    function createToken(user, expiresIn){
        // recuperamos el id y el email del objeto user:
        const {id, email} = user;
        // y lo añadimos al payload:
        const payload = {id, email}

        // utilizamos el payload para retornar el token tras iniciar sesión:
        return jwt.sign(payload, SECRET_KEY, {expiresIn: expiresIn});
    }

    // crear uan función para decodificar el token:
    function decodeToken(token){
        return jwt.decode(token, SECRET_KEY);
    }

    // exportar las dos funciones para crear y decodificar token:
    module.exports = {
        createToken,
        decodeToken
    }

Paso 7: Crear controlador para hacer login con JWT
**************************************************

Editar el archivo **userController.js**:

.. code-block:: javascript 
    :linenos:

    const bcryptjs = require('bcryptjs');
    const User = require('../models/userModel');
    // importar el servicio jwt:
    const jwt = require('../services/jwtService');

    async function register(req, res){
        const params = req.body;
        const user = new User(params);

        try{
            if(!params.email) throw{msg: "Email es un campo obligatorio"};
            if(!params.password) throw{msg: "Contraseña es un campo obligatorio"};

            const emailExists = await User.findOne({email: params.email});
            if(emailExists) throw {msg: "Email ya se encuentra en uso"};

            const salt = bcryptjs.genSaltSync(10);
            user.password = await bcryptjs.hash(params.password, salt);
            
            user.save();
            res.status(200).send(user);

        }catch(error){
            res.status(500).send(error);
        }
    }

    // crear función para hacer login:
    async function login(req, res){
        // recuperar el email y password del body:
        const {email, password} = req.body;

        try {
            // buscamos si existe el usuario por su email:
            const user = await User.findOne({email: email});
            // si el usuario no existe se lanza un mensaje de error:
            if(!user) throw {msg: "el email no existe"};

            // comprobar la contraseña recibida con la contraseña encriptada:
            const passwordCorrect = await bcryptjs.compare(password, user.password);
            // si la contraseña no es correcta avisar:
            if(!passwordCorrect) throw {msg: "la contraseña no es correcta"};

            // creamos el token que lleva el usuario la fecha de expiración del token (12 horas):
            token =  jwt.createToken(user, "12h");

            // se responde con  el token: 
            res.status(200).send({token: token});


        }catch(error){
            req.status(500).send(error);
        }

    }

    module.exports = {
        register,
        login // no olvides exportar el login
    }

Paso 8: Crear endpoint para hacer login con JWT
***********************************************

Editar el archivo **userController.js**:

.. code-block:: javascript 
    :linenos:

    const express = require("express");
    const userController = require('../controllers/userController');

    const api = express.Router();

    api.post("/register", userController.register);
    // el login jwt va con post:
    api.post("/login", userController.login);

    module.exports = api;

.. attention:: 
    Al hacer login en la aplicación nos devolverá un token, si copiamos ese token y lo ponemos en la página **jwt.io** podemos desencriptar el id y usuario. 
    Por ello no es nada recomendable poner datos sensibles en un token.


Paso 9: Crear middleware de autenticación 
*****************************************

Para proteger los endpoints, creamos un middleware que verifique si hemos hecho login:

- Crear una carpeta en la raiz llamada **middlewares** y dentro el archivo **authMiddleware.js**:

.. code-block:: javascript 
    :linenos:

    // importamos moment para las fechas:
    const moment = require('moment');
    // importamos el servicio que hemos creado con jwt:
    const jwt = require('../services/jwtService');

    // copiamos la clave secreta de jwtService.js:
    const SECRET_KEY = "2ha9df238dhha87d8vaq";

    // crear una función (next es una función que continuará el proceso si todo va bien):
    function ensureAuth(req, res, next){
        // si no recibimos el token por el apartado autorización del header:
        if(!req.headers.authorization){
            // damos error de autorización:
            return res.status(403).send({msg: "Faltan las credenciales de autenticación"});
        }

        // si tenemos la cabecera con el token lo guardamos:
        const token = req.headers.authorization.replace(/['"]+/g, ""); // reemplazar las comillas simples por nada

        try {
            // decodificamos el token:
            const payload = jwt.decodeToken(token, SECRET_KEY);

            // si el token ha caducado respondemos con error:
            if(payload.exp <= moment().unix()){
                return res.status(400).send({msg: "el token ha expirado"});
            }

            // si todo va bien le pasamos el payload al usuario y avanzamos a la función ext:
            req.user = payload;
            next();
        }catch(error){
            return res.status(404).send({msg: "Token inválido"});
        }
    }

    // exportar la función:
    module.exports = {
        ensureAuth
    }


Paso 10: Proteger los endpoints con el middleware 
*************************************************

Vamos al archivo **taskRoutes.js** y añadimos el middleware a las rutas:

.. code-block:: javascript 
    :linenos:

    const express = require('express');
    const api = express.Router();
    // importar el middleware de autenticación:
    const authMiddleware = require('../middlewares/authMiddleware');

    const taskController = require("../controllers/taskController");

    // añadimos el middleware a cada ruta:
    api.post("/task", [authMiddleware.ensureAuth], taskController.createTask);
    api.get("/task", [authMiddleware.ensureAuth], taskController.getTasks);
    api.get("/task/:id", [authMiddleware.ensureAuth], taskController.getTask);
    api.put("/task/:id", [authMiddleware.ensureAuth], taskController.updateTask);
    api.delete("/task/:id", [authMiddleware.ensureAuth], taskController.deleteTask);

    module.exports = api;

Paso 11: Habilitar CORS 
***********************
Para poder utilizar nuestra API desde otro lugar o aplicación (React, Angular o Vue) es necesario 
habilitar CORS, editamos **app.js**:

.. code-block:: javascript 
    :linenos: 
 
    const express = require("express");
    const app = express();
    // importar cors:
    const cors = require('cors');

    app.use(express.json());
    app.use(express.urlencoded({extended: true})); 
    // habilitar todas las peticiones cors:
    app.use(cors());

    const hello_routes = require("./routes/hello");
    const task_routes = require('./routes/taskRoutes');
    const user_routes = require('./routes/userRoutes');

    app.use("/api", hello_routes);
    app.use('/api', task_routes);
    app.use('/api', user_routes);

    module.exports = app;

Paso 12: probar los endpoints 
*****************************

1. En postman, vamos a cualquiera de los endpoints e intentamos hacer una petición.
2. Si nos avisa de que falta el token todo va bien, lo añadimos desde la pestaña **Authorization** elegimos la opción **API Key** y escribimos los valores:
    - Key: Authorization 
    - Value: **el token que nos facilitó el sistema**
    - Add to: Header 
3. Si todo va bien nos dejará hacer la petición.

..attention::
    Falta definir de quien es cada tarea, hay que crear una relación entre task y user mediante id de user para consultar dichas tareas.


Trabajar con ficheros en API Restful
####################################

Paso 1: Instalar dependencias 
*****************************

- Instalar **multyparty**: ``npm install connect-multiparty --save``

Paso 2: Subir imagenes y actualizarlas
**************************************

Para subir imágenes editamos un controlador como **userController.js**:

.. code-block:: javascript 
    :linenos:

    const bcryptjs = require('bcryptjs');
    const User = require('../models/userModel');
    const jwt = require('../services/jwtService');

    async function register(req, res){
        const params = req.body;
        const user = new User(params);

        try{
            if(!params.email) throw{msg: "Email es un campo obligatorio"};
            if(!params.password) throw{msg: "Contraseña es un campo obligatorio"};

            const emailExists = await User.findOne({email: params.email});
            if(emailExists) throw {msg: "Email ya se encuentra en uso"};

            const salt = bcryptjs.genSaltSync(10);
            user.password = await bcryptjs.hash(params.password, salt);
            
            user.save();
            res.status(200).send(user);

        }catch(error){
            res.status(500).send(error);
        }
    }

    async function login(req, res){
        const {email, password} = req.body;

        try {
            const user = await User.findOne({email: email});
            if(!user) throw {msg: "el email no existe"};

            const passwordCorrect = await bcryptjs.compare(password, user.password);
            if(!passwordCorrect) throw {msg: "la contraseña no es correcta"};

            token =  jwt.createToken(user, "12h");

            res.status(200).send({token: jwt.createToken(user, "12h")});


        }catch(error){
            req.status(500).send(error);
        }

    }

    function protected(req, res){
        res.status(200).send({msg: "endpoint protegido"});   
    }

    // se crea una función para subir avatar:
    function uploadAvatar(req, res){

        // recuperar todos los parámetros (no el body ni files):
        const params = req.params;
        // se recupera el  usuario:
        User.findById({ _id: params.id}, (err, userData) => {
            // si da error lanzamos un 500:
            if(err){
                res.status(500).send({msg: "Error del servidor"});
            }else{
                // si no tiene datos o no encuentra el usuario lanzamos 404:
                if(!userData){
                    res.status(404).send({msg: "El usuario no existe"});
                }else{
                    // recuperamos el usuario:
                    let user = userData;

                    // si tenemos datos seguimos adelante:
                    if(req.files){
                        // obtener el path del fichero:
                        const filePath = req.files.avatar.path;
                        // separar el id del archivo de la ruta upload:
                        const fileSplit = filePath.split("\\");
                        // sacamos el id unico del archivo para usarlo como nombre:
                        let filename = fileSplit[2];

                        // filtar el tipo de fichero a subir:
                        let fileExt = filename.split("."); // separar la extensión
                        if(fileExt[1] !== "jpg" && fileExt[1] !== "png"){
                            // se da un error 400 con las extensiones no permitidas:
                            res.status(400).send({msg: "La extensión no es correcta, solo JPG o PNG"});
                        }else{
                            // le pasamos al objeto user el nombre del archivo:
                            user.avatar = filename;

                            // actualizar el nombre del archivo en la base de datos:
                            User.findByIdAndUpdate({_id: params.id}, user, (err, userResult) => {
                                // si hay errores un 500:
                                if(err){
                                    res.status(500).send({msg: "Error en servidor"});
                                }else{
                                    // verificar si no existe le usuario:
                                    if(!userResult){
                                        res.status(404).send({msg: "No se encontró el usuario"});
                                    }else{
                                        res.status(200).send({msg: "Se ha subido el avatar"});
                                    }
                                }
                            });
                        }

                    }
                }
            }
        });

    }

    module.exports = {
        register,
        login, 
        protected,
        uploadAvatar // se exporta
    }

Paso 3: Crear ruta para subir imagenes 
**************************************

Editar el archivo **userRoutes.js**:

.. code-block:: javascript 
    :linenos:

    const express = require("express");
    // importar multiparty:
    const multiparty = require("connect-multiparty");
    const userController = require('../controllers/userController');
    const authMiddleware = require('../middlewares/authMiddleware');
    // crear middleware con multipary:
    const uploadAvatarMiddleware = multiparty({uploadDir: './uploads/avatars'});

    const api = express.Router();

    api.post("/register", userController.register);
    api.post("/login", userController.login);
    api.get("/protected", [authMiddleware.ensureAuth], userController.protected);
    // añadimos la ruta que se utilizará para subir el avatar (sin token de momento):
    api.put('/upload-avatar/:id', [uploadAvatarMiddleware], userController.uploadAvatar);

    module.exports = api;

A continuación hay que crear la carpeta **uploads** y dentro de esta la carpeta **avatars**.

Para subir un archivo, en **Postman** presionar la pestaña body, elegimos la opción form-data y añadimos un campo **avatar** cambiamos text por file y subimos un archivo. 

Paso 4: preparar función para recuperar avatar 
**********************************************

Editar nuevamente el controlador **userController.js**: 

.. code-block:: javascript 
    :linenos:

    const bcryptjs = require('bcryptjs');
    // importar la api interna filesystem:
    const fs = require('fs');
    // importar la api interna path:
    const path = require('path');
    const User = require('../models/userModel');
    const jwt = require('../services/jwtService');

    async function register(req, res){
        const params = req.body;
        const user = new User(params);

        try{
            if(!params.email) throw{msg: "Email es un campo obligatorio"};
            if(!params.password) throw{msg: "Contraseña es un campo obligatorio"};

            const emailExists = await User.findOne({email: params.email});
            if(emailExists) throw {msg: "Email ya se encuentra en uso"};

            const salt = bcryptjs.genSaltSync(10);
            user.password = await bcryptjs.hash(params.password, salt);
            
            user.save();
            res.status(200).send(user);

        }catch(error){
            res.status(500).send(error);
        }
    }

    async function login(req, res){
        const {email, password} = req.body;

        try {
            const user = await User.findOne({email: email});
            if(!user) throw {msg: "el email no existe"};

            const passwordCorrect = await bcryptjs.compare(password, user.password);
            if(!passwordCorrect) throw {msg: "la contraseña no es correcta"};

            token =  jwt.createToken(user, "12h");

            res.status(200).send({token: jwt.createToken(user, "12h")});


        }catch(error){
            req.status(500).send(error);
        }

    }

    function protected(req, res){
        res.status(200).send({msg: "endpoint protegido"});   
    }

    function uploadAvatar(req, res){

        const params = req.params;
        User.findById({ _id: params.id}, (err, userData) => {
            if(err){
                res.status(500).send({msg: "Error del servidor"});
            }else{
                if(!userData){
                    res.status(404).send({msg: "El usuario no existe"});
                }else{
                    let user = userData;

                    if(req.files){
                        const filePath = req.files.avatar.path;
                        const fileSplit = filePath.split("\\");
                        let filename = fileSplit[2];

                        let fileExt = filename.split("."); 
                        if(fileExt[1] !== "jpg" && fileExt[1] !== "png"){
                            res.status(400).send({msg: "La extensión no es correcta, solo JPG o PNG"});
                        }else{
                            user.avatar = filename;

                            User.findByIdAndUpdate({_id: params.id}, user, (err, userResult) => {
                                if(err){
                                    res.status(500).send({msg: "Error en servidor"});
                                }else{
                                    if(!userResult){
                                        res.status(404).send({msg: "No se encontró el usuario"});
                                    }else{
                                        res.status(200).send({msg: "Se ha subido el avatar"});
                                    }
                                }
                            });
                        }

                    }
                }
            }
        });
    }

    // crear función para leer archivo:
    function getAvatar(req, res){
        // recuperar el nombre del avatar:
        const avatarName = req.params.avatarName;
        // se prepara la ruta del archivo:
        const filePath = `./uploads/avatars/${avatarName}`;

        // comprobar que existe el fichero:
        fs.stat(filePath, (err, stat)=>{
            // si no existe 404:
            if(err){
                res.status(404).send({msg: "el avatar no existe"});
            }else{
                // si existe lo recuperamos:
                res.sendFile(path.resolve(filePath));
            }
        });
    }

    module.exports = {
        register,
        login, 
        protected,
        uploadAvatar,
        getAvatar // exportar controlador
    }

Paso 5: Ruta para recuperar avatar 
**********************************

Se crea una ruta en el archivo **userRoutes.js**:

.. code-block:: javascript 
    :linenos:

    const express = require("express");
    const multiparty = require("connect-multiparty");
    const userController = require('../controllers/userController');
    const authMiddleware = require('../middlewares/authMiddleware');
    const uploadAvatarMiddleware = multiparty({uploadDir: './uploads/avatars'});

    const api = express.Router();

    api.post("/register", userController.register);
    api.post("/login", userController.login);
    api.get("/protected", [authMiddleware.ensureAuth], userController.protected);
    api.put('/upload-avatar/:id', [uploadAvatarMiddleware], userController.uploadAvatar);
    // recuperar avatar:
    api.get("/avatar/:avatarName", userController.getAvatar);

    module.exports = api;
    