---
title: Refuerce su seguridad con Azure Security Center | Microsoft Docs
description: Este artículo ayuda a reforzar la seguridad mediante la supervisión de los recursos en Azure Security Center.
services: security-center
documentationcenter: na
author: rkarlin
manager: mbaldwin
editor: ''
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/28/2018
ms.author: rkarlin
ms.openlocfilehash: 2827461ee78be8d8976ec23e59d489213eb94e31
ms.sourcegitcommit: a08d1236f737915817815da299984461cc2ab07e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/26/2018
ms.locfileid: "52316028"
---
# <a name="strengthen-your-security-posture-with-azure-security-center"></a>Refuerce su seguridad con Azure Security Center
Este artículo le ayuda a reforzar la seguridad. Use las funcionalidades de supervisión de Azure Security Center para asegurarse de que la seguridad de los recursos es tan estricta como sea posible y para supervisar que cumple con las directivas establecidas.

## <a name="how-do-you-strengthen-your-security-posture"></a>¿Cómo puede reforzar la seguridad?
Con frecuencia se piensa que supervisar es observar y esperar que se produzca un evento, para así poder reaccionar ante la situación. Reforzar la seguridad se refiere a contar con una estrategia proactiva que audita los recursos a fin de identificar los sistemas que no cumplen con los estándares o los procedimientos recomendados de la organización.

Después de habilitar las [directivas de seguridad](security-center-azure-policy.md) para los recursos de una suscripción, Security Center analizará la seguridad de los recursos para identificar vulnerabilidades potenciales. La información acerca de la configuración de la red está disponible de inmediato. Dependiendo del número de máquinas virtuales y de los equipos que tenga con el agente instalado, la recopilación de información sobre máquinas virtuales y la configuración del equipo, como el estado de actualización de seguridad y la configuración del sistema operativo, puede tardar una hora o más en estar disponible. Puede ver una lista completa de los problemas y formas de proteger su red y corregir riesgos en el icono de **recomendaciones**.

Puede ver el estado de seguridad de sus recursos, además de cualquier problema, en función del tipo de recurso:

- Para supervisar el estado de los recursos del equipo y las aplicaciones, y recibir recomendaciones para mejorar su seguridad, consulte [Protección de las aplicaciones y las máquinas en Azure Security Center](security-center-virtual-machine-protection.md).
- Para supervisar los recursos de red, como las máquinas virtuales, los grupos de seguridad de red y los puntos de conexión, y recibir recomendaciones para mejorar su seguridad, consulte [Protección de las redes en Azure Security Center](security-center-network-recommendations.md) para obtener más información. 
- Para supervisar los recursos de datos y almacenamiento, como los servidores de SQL y las cuentas de almacenamiento, y recibir recomendaciones para mejorar su seguridad, consulte [Protecting Azure SQL service and data in Azure Security Center](security-center-sql-service-recommendations.md) (Protección del servicio y los datos de SQL de Azure en Azure Security Center) para obtener más información. 
- Para supervisar los recursos de identidad y acceso, incluidos los permisos de cuenta y MFA, y recibir recomendaciones para mejorar su seguridad, consulte [Supervisión de la identidad y el acceso en Azure Security Center](security-center-identity-access.md) para obtener más información. 
- Para supervisar el acceso Just-in-Time a los recursos, consulte [Administrar el acceso a máquina virtual mediante Just-In-Time](security-center-just-in-time.md) para obtener más información. 


Para más información sobre cómo aplicar las recomendaciones, lea [Implementación de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md).



![Icono de estado de seguridad de los recursos](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)



## <a name="see-also"></a>Otras referencias
En este artículo, aprendió a usar las funcionalidades de supervisión en Azure Security Center. Para obtener más información sobre el Centro de seguridad de Azure, consulte los siguientes recursos:

* [Establecimiento de directivas de seguridad en Azure Security Center](security-center-azure-policy.md): obtenga información sobre cómo configurar los ajustes de seguridad en Azure Security Center.
* [Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.
* [Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.
* [Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md): encuentre las preguntas más frecuentes sobre el uso del servicio.
* [Blog de seguridad de Azure](https://blogs.msdn.com/b/azuresecurity/): encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.
