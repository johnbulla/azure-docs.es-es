---
title: 'Inicio rápido: SDK de Bing Video Search, Node'
titleSuffix: Azure Cognitive Services
description: Configuración de la aplicación de consola del SDK de Bing Video Search.
services: cognitive-services
author: mikedodaro
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: quickstart
ms.date: 02/12/2018
ms.author: rosh
ms.openlocfilehash: 985ddcff35a16c747fff34ed487c72744e1ee466
ms.sourcegitcommit: a08d1236f737915817815da299984461cc2ab07e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2018
ms.locfileid: "52313459"
---
# <a name="quickstart-bing-video-search-sdk-with-node"></a>Inicio rápido: SDK de Bing Video Search con Node

El SDK de Bing Video Search contiene la funcionalidad de la API REST para consultas de vídeo y análisis de resultados. 

El [código fuente de los ejemplos del SDK de Bing Video Search para Node](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/videoSearch.js) está disponible en Git Hub.

## <a name="application-dependencies"></a>Dependencias de aplicaciones
Obtenga una [clave de acceso de Cognitive Services](https://azure.microsoft.com/try/cognitive-services/) en **Buscar**.  Consulte también [Precios de Cognitive Services - Bing Search API](https://azure.microsoft.com/pricing/details/cognitive-services/search-api/).

Para configurar una aplicación de consola mediante el SDK de Bing Video Search:
* Ejecute `npm install ms-rest-azure` en el entorno de desarrollo.
* Ejecute `npm install azure-cognitiveservices-videosearch` en el entorno de desarrollo.

## <a name="video-search-client"></a>Cliente de Video Search
Obtenga una [clave de acceso de Cognitive Services](https://azure.microsoft.com/try/cognitive-services/) en *Buscar*. Creación de una instancia de `CognitiveServicesCredentials`:
```
const CognitiveServicesCredentials = require('ms-rest-azure').CognitiveServicesCredentials;
let credentials = new CognitiveServicesCredentials('YOUR-ACCESS-KEY');
```
Después, cree una instancia del cliente:
```
const VideoSearchAPIClient = require('azure-cognitiveservices-videosearch');
let client = new VideoSearchAPIClient(credentials);
```
Busque los resultados.
```
client.videosOperations.search('Interstellar Trailer').then((result) => {
    console.log(result.value);
}).catch((err) => {
    throw err;
});

```

<!-- Remove until the response can be replace with a sanitized version.
The code prints `result.value` items to the console without parsing any text. The results will be:
- _type: 'VideoObjectElementType'

![Video results](media/video-search-sdk-node-results.png)
-->

## <a name="next-steps"></a>Pasos siguientes

[Ejemplos del SDK de Cognitive Services para Node.js](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)
