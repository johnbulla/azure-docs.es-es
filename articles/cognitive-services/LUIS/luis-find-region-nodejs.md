---
title: Búsqueda de la región de punto de conexión con Node.js en LUIS
titleSuffix: Azure Cognitive Services
description: Busque mediante programación la región de publicación con la clave de punto de conexión y el id. de la aplicación para LUIS.
services: cognitive-services
author: diberry
manager: cgronlun
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: 193872d03dde1d5c620acca1b7aba99b60db238d
ms.sourcegitcommit: 4ecc62198f299fc215c49e38bca81f7eb62cdef3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "47034083"
---
# <a name="find-endpoint-region-with-nodejs"></a>Búsqueda de la región de punto de conexión con Node.js
Si tiene los identificadores de aplicación y suscripción de LUIS, puede buscar la región que se va a usar para las consultas de punto de conexión.

> [!NOTE] 
> La solución completa de Node.js está disponible en el repositorio [**LUIS-Samples** de GitHub](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/find-region/nodejs/).

## <a name="luis-endpoint-query-strategy"></a>Estrategia de consulta de punto de conexión de LUIS
Cada consulta de punto de conexión de LUIS requiere lo siguiente:

* Una clave de punto de conexión
* Un id. de la aplicación
* Una región

Si la consulta de punto de conexión de LUIS usa la clave de punto de conexión y el id. de la aplicación correctos pero la región incorrecta, el código de respuesta es 401. La solicitud 401 no se cuenta para la cuota de suscripción. Convierta esta solicitud en una estrategia para sondear todas las regiones para buscar la región correcta. La región correcta es la única solicitud que devuelve un código de estado 2xx. 

|Response code|Parámetros|
|--|--|
|2xx|clave de punto de conexión correcta<br>Id. de la aplicación correcto<br>Región de host correcta|
|401|clave de punto de conexión correcta<br>Id. de la aplicación correcto<br>Región de host _incorrecta_|

## <a name="nodejs-code-to-find-region"></a>Código de clase de Node.js para buscar la región
La aplicación de consola toma el id. de la aplicación de LUIS y la clave de punto de conexión y devuelve todas las regiones asociadas con ella. En la actualidad, una clave de punto de conexión se crea por región, por lo que solo se debe devolver una región.

Incluya las dependencias de NPM:

[!code-javascript[Add the dependencies](~/samples-luis/documentation-samples/find-region/nodejs/index.js?range=5-6 "Add the dependencies")]

Agregue las constantes. Reemplace los valores de variable para de `subscriptionKey` y `appId` por valores propios.  

[!code-javascript[Add constants](~/samples-luis/documentation-samples/find-region/nodejs/index.js?range=8-25 "Add constants")]

Agregue la función `searchRegions` para buscar la región. Todas las regiones incorrectas devuelven 401, que se captura y se omite.

[!code-javascript[Find region](~/samples-luis/documentation-samples/find-region/nodejs/index.js?range=27-37 "Find region")]

Llame a la función `searchRegions` y devuelva una única región:

[!code-javascript[Call the function](~/samples-luis/documentation-samples/find-region/nodejs/index.js?range=39-43 "Call the function")]

Cuando se ejecuta la aplicación, en el terminal se muestra la región para el id. de la aplicación.

![Captura de pantalla de la aplicación de consola en la que se muestra la región de LUIS](./media/find-region-nodejs/console.png)


## <a name="next-steps"></a>Pasos siguientes

Más información sobre las [regiones](luis-reference-regions.md) de LUIS.
