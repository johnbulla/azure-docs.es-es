---
title: Aplicación de Node.Js y Angular con la API de MongoB (parte 5)
titleSuffix: Azure Cosmos DB
description: Parte 5 de la serie de tutoriales en la que se explica cómo crear una aplicación de MongoDB con Angular y Node en Azure Cosmos DB utilizando las mismas API que para MongoDB
author: johnpapa
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 12/06/2018
ms.author: jopapa
ms.custom: seodec18
ms.openlocfilehash: bda500c07e2ecccc317b5b669a947a415aaf147f
ms.sourcegitcommit: 78ec955e8cdbfa01b0fa9bdd99659b3f64932bba
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/10/2018
ms.locfileid: "53134138"
---
# <a name="create-a-mongodb-app-with-angular-and-azure-cosmos-db---part-5-connect-to-azure-cosmos-db"></a>Creación de una aplicación de MongoDB con Angular y Azure Cosmos DB (parte 5): Conexión a Azure Cosmos DB 

En este tutorial de varias partes, se muestra cómo crear una aplicación Node.js con Express y Angular y conectarla a la cuenta de la [API de MongoDB para Azure Cosmos DB](mongodb-introduction.md).

La parte 5 del tutorial se basa en la [parte 4](tutorial-develop-mongodb-nodejs-part4.md) y aborda las tareas siguientes:

> [!div class="checklist"]
> * Uso de Mongoose para conectarse a Azure Cosmos DB
> * Obtención de la información de la cadena de conexión de Cosmos DB
> * Creación del modelo de Hero
> * Creación del servicio Hero para obtener datos de héroes
> * Ejecución de la aplicación de forma local

## <a name="video-walkthrough"></a>Tutorial en vídeo

Puede ver el siguiente vídeo para aprender rápidamente los pasos descritos en este documento: 

> [!VIDEO https://www.youtube.com/embed/sI5hw6KPPXI]


## <a name="prerequisites"></a>Requisitos previos

Antes de iniciar esta parte del tutorial, asegúrese de que ha completado los pasos descritos en la [parte 4](tutorial-develop-mongodb-nodejs-part4.md).

> [!TIP]
> Este tutorial le guía por los pasos necesarios para crear la aplicación paso a paso. Si desea descargar el proyecto finalizado, puede obtener la aplicación completa en el [repositorio de angular-cosmosdb](https://github.com/Azure-Samples/angular-cosmosdb) en GitHub.

## <a name="use-mongoose-to-connect-to-azure-cosmos-db"></a>Uso de Mongoose para conectarse a Azure Cosmos DB

1. Instale el módulo mongoose npm, que es una API que se usa para comunicarse con MongoDB.

    ```bash
    npm i mongoose --save
    ```

2. Ahora, cree un archivo en la carpeta **server** llamada **mongo.js**. Agregará los detalles de conexión de su cuenta de Cosmos DB a este archivo.

3. Copie el código siguiente en **mongo.js**. Este código:

    * Requiere Mongoose.

    * Invalida la promesa de Mongo para utilizar la promesa básica que se integra en ES6/ES2015 y versiones posteriores.

    * Llama a un archivo env que le permite configurar ciertos elementos en función de si se encuentra en fase de ensayo, producción o desarrollo. En la siguiente sección, va a crear ese archivo.

    * Incluye la cadena de conexión de MongoDB, que se establecerá en el archivo env.

    * Crea una función de conexión que llama a Mongoose.

    ```javascript
    const mongoose = require('mongoose');
    /**
     * Set to Node.js native promises
     * Per https://mongoosejs.com/docs/promises.html
     */
    mongoose.Promise = global.Promise;

    const env = require('./env/environment');

    // eslint-disable-next-line max-len
    const mongoUri = `mongodb://${env.accountName}:${env.key}@${env.accountName}.documents.azure.com:${env.port}/${env.databaseName}?ssl=true`;

    function connect() {
     mongoose.set('debug', true);
     return mongoose.connect(mongoUri, { useMongoClient: true });
    }

    module.exports = {
      connect,
      mongoose
    };
    ```
    
4. En el panel del Explorador, cree una carpeta en **server** denominada **environment** y, en la carpeta **environment**, cree un archivo nuevo denominado **environment.js** .

5. Desde el archivo mongo.js, sabemos que debemos incluir los valores de `dbName`, `key` y `cosmosPort`, por lo que debe copiar el código siguiente en **environment.js**.

    ```javascript
    // TODO: replace if yours are different
    module.exports = {
      accountName: 'your-cosmosdb-account-name-goes-here',
      databaseName: 'admin', 
      key: 'your-key-goes-here',
      port: 10255
    };
    ```

## <a name="get-the-connection-string-information"></a>Obtención de la información de la cadena de conexión

1. En **environment.js**, cambie el valor de `port` a 10255. (Puede encontrar el puerto de Cosmos DB en Azure Portal)

    ```javascript
    const port = 10255;
    ```

2. En **environment.js**, cambie el valor de `accountName` por el nombre de la cuenta de Azure Cosmos DB creada en el [paso 4](tutorial-develop-mongodb-nodejs-part4.md). 

3. Recupere la clave principal de la cuenta de Azure Cosmos DB mediante el siguiente comando de la CLI en la ventana del terminal: 

    ```azure-cli-interactive
    az cosmosdb list-keys --name <cosmosdb-name> -g myResourceGroup
    ```    
    
    * `<cosmosdb-name>` es el nombre de la cuenta de Azure Cosmos DB que creó en el [paso 4](tutorial-develop-mongodb-nodejs-part4.md).

4. Copie la clave principal en el archivo environment.js como valor de `key`.

    La aplicación tiene ahora toda la información que necesita para conectarse a Azure Cosmos DB. Esta información también se puede recuperar en el portal. Para más información, consulte [Obtención de la cadena de conexión de MongoDB para personalizar](connect-mongodb-account.md#GetCustomConnection). El nombre de usuario en el portal equivale al nombre de base de datos (dbName) en environments.js. 

## <a name="create-a-hero-model"></a>Creación de un modelo de Hero

1. En el panel de Explorer, cree el archivo **hero.model.js** en la carpeta **server**.

2. Copie el código siguiente en **hero.model.js**. Este código proporciona la funcionalidad siguiente:

   * Requiere Mongoose.
   * Crea un nuevo esquema con un identificador, un nombre y un mensaje.
   * Crea un modelo con el esquema.
   * Exporta el modelo. 
   * Asigne a la colección el nombre Heroes (en lugar de Heros, que sería el nombre predeterminado de la colección según las reglas de nomenclatura de plurales de Mongoose).

   ```javascript
   const mongoose = require('mongoose');

   const Schema = mongoose.Schema;

   const heroSchema = new Schema(
     {
       id: { type: Number, required: true, unique: true },
       name: String,
       saying: String
     },
     {
       collection: 'Heroes'
     }
   );

   const Hero = mongoose.model('Hero', heroSchema);

   module.exports = Hero;
   ```

## <a name="create-a-hero-service"></a>Creación de un servicio Hero

1. En el panel de Explorer, cree el archivo **hero.service.js** en la carpeta **server**.

2. Copie el código siguiente en **hero.service.js**. Este código:

   * Obtiene el modelo recién creado
   * Se conecta a la base de datos
   * Crea una variable docquery que utiliza el método hero.find para definir una consulta que devuelve todos los héroes.
   * Ejecuta una consulta con el archivo docquery.exec y una promesa para obtener una lista de todos los héroes, en la que el estado de respuesta es 200. 
   * Si el estado es 500, devuelve el mensaje de error
   * Dado que usamos módulos, obtiene los héroes. 

   ```javascript
   const Hero = require('./hero.model');

   require('./mongo').connect();

   function getHeroes() {
     const docquery = Hero.find({});
     docquery
       .exec()
       .then(heroes => {
         res.status(200).json(heroes);
       })
       .catch(error => {
         res.status(500).send(error);
         return;
       });
   }

   module.exports = {
     getHeroes
   };
   ```

## <a name="add-the-hero-service-to-routesjs"></a>Incorporación del servicio Hero a routes.js

1. En Visual Studio Code, en **routes.js**, marque como comentario la función `res.send` que envía los datos de ejemplo de Hero y agregue una línea para llamar a la función `heroService.getHeroes` en su lugar.

    ```javascript
    router.get('/heroes', (req, res) => {
      heroService.getHeroes(req, res);
    //  res.send(200, [
    //      {"id": 10, "name": "Starlord", "saying": "oh yeah"}
    //  ])
    });
    ```

2. En **routes.js**, requiera el servicio Hero:

    ```javascript
    const heroService = require('./hero.service'); 
    ```

3. En **hero.service.js**, actualice la función getHeroes para tomar los parámetros `req` y `res`, tal y como se indica a continuación:

    ```javascript
    function getHeroes(req, res) {
    ```

    Dediquemos un minuto a revisar y recorrer la cadena de llamadas aquí. En primer lugar, empezamos con `index.js`, que configura el servidor de nodo; observe que está configurando y definiendo las rutas. El archivo routes.js se comunica entonces con el servicio Hero y le indica que obtenga las funciones como getHeroes y pase la solicitud y la respuesta. Aquí, hero.service.js va a tomar el modelo y a conectarse a Mongo, y, a continuación, ejecutará getHeroes cuando lo llamemos, y devolverá 200 como respuesta. A continuación, se propaga a través de la cadena. 

## <a name="run-the-app"></a>Ejecución de la aplicación

1. Ahora vamos a ejecutar la aplicación de nuevo. En Visual Studio Code, guarde los cambios, haga clic en el botón **Depurar** ![Icono Depurar en Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part5/debug-button.png) en el lado izquierdo y haga clic en el botón **Iniciar depuración** ![Icono Depurar en Visual Studio Code](./media/tutorial-develop-mongodb-nodejs-part5/start-debugging-button.png).

3. Ahora, vamos a cambiar al explorador, abrir las herramientas de desarrollador y la pestaña Red y, a continuación, iremos a http://localhost:3000 y ahí está nuestra aplicación.

    ![La nueva cuenta de Azure Cosmos DB en Azure Portal](./media/tutorial-develop-mongodb-nodejs-part5/azure-cosmos-db-heroes-app.png)

   Aún no hay ningún héroe almacenado en la aplicación, pero en el paso siguiente del tutorial se agregarán las funciones put, push y delete, para que podamos agregar, actualizar y eliminar héroes desde la interfaz de usuario con conexiones de Mongoose a nuestra base de datos de Azure Cosmos DB. 

## <a name="next-steps"></a>Pasos siguientes

En esta parte del tutorial, ha hecho las siguientes tareas:

> [!div class="checklist"]
> * Se usaron las API de Mongoose para conectar su aplicación Heroes a Azure Cosmos DB 
> * Agregó la funcionalidad getHeroes a la aplicación

Puede continuar con la siguiente parte del tutorial para agregar las funciones Post, Put y Delete a la aplicación.

> [!div class="nextstepaction"]
> [Incorporación de las funciones Post, Put y Delete a la aplicación](tutorial-develop-mongodb-nodejs-part6.md)
