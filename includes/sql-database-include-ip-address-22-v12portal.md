---
title: Reglas de firewall de nivel de servidor
description: Reglas de firewall de nivel de servidor
keywords: conexión sql, cadena de conexión
services: sql-database
author: dalechen
manager: craigg
ms.service: sql-database
ms.custom: develop apps
ms.topic: include
ms.date: 07/13/2018
ms.author: ninarn
ms.openlocfilehash: 07bbba28b7e1b048ef3a4e1afa4db255967dc093
ms.sourcegitcommit: 7827d434ae8e904af9b573fb7c4f4799137f9d9b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39117280"
---
1. Inicie sesión en el [Azure Portal](https://portal.azure.com/).

2. En la lista de la izquierda, seleccione **Todos los servicios**.

3. Desplácese y seleccione **Servidores SQL Server**.

    ![Encontrar el servidor de Azure SQL Database en el portal][b21-FindServerInPortal]
5. En el cuadro de texto de filtro, empiece a escribir el nombre del servidor. Aparecerá su fila.

6. Seleccione la fila para el servidor. Aparecerá una hoja para el servidor.

7. En la hoja del servidor, seleccione **Configuración**.

8. Seleccione **Firewall**.

    ![Selección de Configuración > Firewall][b31-SettingsFirewallNavig]
9. Seleccione **Agregar IP de cliente**. Escriba un nombre para la regla nueva en el primer cuadro de texto.

10. Escriba los valores de dirección IP inferior y superior para el intervalo que quiere habilitar.

    * Puede resultar útil que el valor inferior termine en **.0** y el valor alto en **.255**.

11. Seleccione **Guardar**.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
