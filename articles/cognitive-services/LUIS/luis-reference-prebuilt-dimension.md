---
title: Referencia de entidades precompiladas de dimensión de LUIS en Azure | Microsoft Docs
titleSuffix: Azure
description: Este artículo contiene información sobre la entidad precompilada de dimensión en Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cgronlun
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 11/26/2018
ms.author: diberry
ms.openlocfilehash: 138cf1d2fbc050797c133afaffdb2a9820e2717f
ms.sourcegitcommit: 922f7a8b75e9e15a17e904cc941bdfb0f32dc153
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52332925"
---
# <a name="dimension-entity"></a>Entidad de dimensión
La entidad de dimensión precompilada detecta varios tipos de dimensiones, con independencia de la referencia cultural de la aplicación LUIS. Dado que esta entidad ya está entrenada, no se necesita agregar expresiones de ejemplo que contengan dimensiones en las intenciones de la aplicación. La entidad de dimensión se admite en [muchas referencias culturales](luis-reference-prebuilt-entities.md). 

## <a name="types-of-dimension"></a>Tipos de dimensión

La dimensión se administra desde el repositorio de GitHub [Recognizers-Text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-NumbersWithUnit.yaml).


## <a name="resolution-for-dimension-entity"></a>Resolución de la entidad de dimensión
En el siguiente ejemplo, se muestra la resolución de la entidad **builtin.ordinal**.

```JSON
{
  "query": "it takes more than 10 1/2 miles of cable and wire to hook it all up , and 23 computers.",
  "topScoringIntent": {
    "intent": "None",
    "score": 0.762141049
  },
  "intents": [
    {
      "intent": "None",
      "score": 0.762141049
    }
  ],
  "entities": [
    {
      "entity": "10 1/2 miles",
      "type": "builtin.dimension",
      "startIndex": 19,
      "endIndex": 30,
      "resolution": {
        "unit": "Mile",
        "value": "10.5"
      }
    }
  ]
}
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de las entidades de [correo electrónico](luis-reference-prebuilt-email.md), [número](luis-reference-prebuilt-number.md) y [ordinal](luis-reference-prebuilt-ordinal.md). 