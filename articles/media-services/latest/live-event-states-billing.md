---
title: Estados y facturación de LiveEvent en Azure Media Services | Microsoft Docs
description: En este tema se proporciona información general sobre los estados y facturación de LiveEvent en Azure Media Services.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 11/16/2018
ms.author: juliako
ms.openlocfilehash: 1a49f62d7b5e21fe9d6483f71b729a9100aff1a3
ms.sourcegitcommit: 56d20d444e814800407a955d318a58917e87fe94
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/29/2018
ms.locfileid: "52585491"
---
# <a name="liveevent-states-and-billing"></a>Estados y facturación de LiveEvent

En Azure Media Services, un objeto LiveEvent comienza la facturación tan pronto como su estado realiza la transición a **En ejecución**. Para detener la facturación del objeto LiveEvent, debe pararlo.

Si **LiveEventEncodingType** en el objeto [LiveEvent](https://docs.microsoft.com/rest/api/media/liveevents) está establecido en Estándar (Básico), Media Services cerrará automáticamente cualquier objeto LiveEvent que tenga aún el estado **En ejecución** doce horas después de que se pierda la fuente de entrada y si no hay ningún objeto **LiveOutput** en ejecución. Sin embargo, se le facturará por el tiempo que el objeto LiveEvent haya estado en estado **En ejecución**.

## <a name="states"></a>States

LiveEvent puede estar en uno de los siguientes estados.

|Estado|DESCRIPCIÓN|
|---|---|
|**Stopped**| Este es el estado inicial del objeto LiveEvent después de su creación (a menos que haya establecido el inicio automático en true). No se produce ninguna facturación en este estado. En este estado, se pueden actualizar las propiedades del objeto LiveEvent pero no se permite el streaming.|
|**Starting** (iniciándose)| Se inicia LiveEvent y se asignan los recursos. No se produce ninguna facturación en este estado. Durante este estado no se permite realizar actualizaciones ni streaming. Si se produce un error, el objeto LiveEvent vuelve al estado Detenido.|
|**Ejecución**| Se han asignado los recursos de LiveEvent, se han generado las direcciones URL de ingesta y visualización previa y puede recibir transmisiones en vivo. En este momento, la facturación está activa. Debe llamar explícitamente a Stop en el recurso de LiveEvent para detener la facturación.|
|**Stopping** (Deteniéndose)| Se detiene LiveEvent y se desaprovisionan los recursos. No se produce facturación en este estado transitorio. Durante este estado no se permite realizar actualizaciones ni streaming.|
|**Eliminando**| El objeto LiveEvent se está eliminando. No se produce facturación en este estado transitorio. Durante este estado no se permite realizar actualizaciones ni streaming.|

## <a name="next-steps"></a>Pasos siguientes

- [Introducción al streaming en vivo](live-streaming-overview.md)
- [Tutorial de Live Streaming](stream-live-tutorial-with-api.md)
