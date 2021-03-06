---
title: archivo de inclusión
description: archivo de inclusión
services: virtual-machines-windows, virtual-machines-linux
author: dlepow
ms.service: multiple
ms.topic: include
ms.date: 10/09/2018
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: 6c7a9857f6d6d57dc9e314bcb1ef848a326b7ed2
ms.sourcegitcommit: 07a09da0a6cda6bec823259561c601335041e2b9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2018
ms.locfileid: "49437150"
---
## <a name="terminology"></a>Terminología

Una imagen de Marketplace de Azure tiene los atributos siguientes:

* **Publicador**: organización que ha creado la imagen. Ejemplos: Canonical, MicrosoftWindowsServer
* **Oferta**: nombre de un grupo de imágenes relacionadas creado por un publicador. Ejemplos: Ubuntu Server, WindowsServer
* **SKU**: instancia de una oferta, por ejemplo, una versión principal de una distribución. Ejemplos: 16.04-LTS, 2016-Datacenter
* **Versión**: número de versión de una SKU de imagen. 

Para identificar una imagen de Marketplace cuando se implementa una máquina virtual mediante programación, brinde estos valores de manera individual como parámetros. Algunas herramientas aceptan una imagen *URN* que combina estos valores separados por el carácter de dos puntos (:): *Publicador*:*Oferta*:*Sku*:*Versión*. En un URN, puede reemplazar el número de versión por "latest", que selecciona la versión más reciente de la imagen. 

Si el publicador de la imagen proporciona términos adicionales de licencia y compra, debe aceptar esos términos y habilitar la implementación mediante programación. También debe suministrar los parámetros de *plan de compra* al implementar una máquina virtual mediante programación. Consulte la sección [Implementación de una imagen con términos de Marketplace](#deploy-an-image-with-marketplace-terms).