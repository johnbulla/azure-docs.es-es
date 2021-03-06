---
title: Configuración de dispositivos híbridos unidos a Azure Active Directory | Microsoft Docs
description: Aprenda a configurar dispositivos híbridos unidos a Azure Active Directory.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.component: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2018
ms.author: markvi
ms.reviewer: sandeo
ms.openlocfilehash: ebf5a23743d1fdd9553b391bb0518c2887ddb096
ms.sourcegitcommit: ada7419db9d03de550fbadf2f2bb2670c95cdb21
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/02/2018
ms.locfileid: "50959994"
---
# <a name="how-to-plan-your-hybrid-azure-active-directory-join-implementation"></a>Planeamiento de la implementación de unión a Azure Active Directory híbrido

De forma similar a un usuario, un dispositivo se está convirtiendo en otra identidad que debe proteger y usar también para proteger los recursos en cualquier momento y lugar. Puede lograr este objetivo incluyendo las identidades de los dispositivos en Azure AD mediante uno de los métodos siguientes:

- Unión a Azure AD
- Unión a Azure AD híbrido
- Registro de Azure AD

Al traer sus dispositivos a Azure AD, está maximizando la productividad de los usuarios mediante un inicio de sesión único (SSO) en los recursos de nube y del entorno local. Al mismo tiempo, puede proteger el acceso a los recursos de nube y de entorno local con [acceso condicional](../active-directory-conditional-access-azure-portal.md).

Si tiene un entorno local de Active Directory y quiere unir sus dispositivos unidos a un dominio a Azure AD, puede hacerlo configurando dispositivos híbridos unidos a Azure AD. En este artículo se proporcionan los pasos relacionados con la implementación de una unión a Azure AD híbrido en su entorno. 


## <a name="prerequisites"></a>Requisitos previos

En este artículo se da por hecho que está familiarizado con la [introducción a la administración de dispositivos en Azure Active Directory](../device-management-introduction.md).


## <a name="plan-your-implementation"></a>Planeamiento de la implementación

Para planear la implementación de Azure AD híbrido, debe familiarizarse con:

|   |   |
|---|---|
|![Comprobar][1]|Revisión de los dispositivos compatibles|
|![Comprobar][1]|Revisión de los aspectos que debe conocer|
|![Comprobar][1]|Revisión del control de la unión de dispositivos a Azure AD híbrido|
|![Comprobar][1]|Selección del escenario|


 


## <a name="review-supported-devices"></a>Revisión de los dispositivos compatibles 

La unión a Azure AD híbrido admite una amplia variedad de dispositivos Windows. Dado que la configuración para los dispositivos que ejecutan versiones anteriores de Windows requiere pasos adicionales o diferentes, los dispositivos compatibles se agrupan en dos categorías:

**Dispositivos Windows actuales**

- Windows 10
    
- Windows Server 2016


Para dispositivos que ejecutan el sistema operativo de escritorio de Windows, la versión admitida es la Actualización de aniversario de Windows 10 (versión 1607), o una versión posterior. Como procedimiento recomendado, actualice a la versión más reciente de Windows 10.



 **Dispositivos Windows de nivel inferior**

- Windows 8.1
 
- Windows 7

- Windows Server 2012 R2
 
- Windows Server 2012 
 
- Windows Server 2008 R2 


Como primer paso del planeamiento, debe revisar el entorno y determinar si necesita admitir dispositivos Windows de nivel inferior.



## <a name="review-things-you-should-know"></a>Revisión de los aspectos que debe conocer

No se puede usar una unión a Azure AD híbrido si el entorno consta de un solo bosque que sincronizó datos de identidad con más de un inquilino de Azure AD.

Si está confiando en la Herramienta de preparación del sistema (Sysprep), asegúrese de crear imágenes desde una instalación de Windows que no se haya configurado para la unión a Azure AD híbrido.

Si está confiando en una instantánea de máquina virtual (VM) para crear otras máquinas virtuales, asegúrese de usar una instantánea de VM que no se haya configurado para la unión a Azure AD híbrido.

La unión de dispositivos de nivel inferior a Azure AD híbrido:

- **Es** compatible en entornos no federados a través del [inicio de sesión único de conexión directa de Azure Active Directory](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso-quick-start). 

- **No es** compatible cuando se usa la autenticación de paso a través de Azure AD sin inicio de sesión único de conexión directa.

- **No es** compatible cuando se usa con credenciales móviles o perfil de usuario móvil o cuando se usa la infraestructura de escritorio virtual (VDI).


No se admite el registro de Windows Server que ejecuta el rol de controlador de dominio (DC).

Si su organización requiere acceso a Internet a través de un servidor proxy saliente autenticado, tiene que asegurarse de que los equipos de Windows 10 pueden autenticarse correctamente en el proxy de salida. Debido a que los equipos de Windows 10 ejecutan el registro de dispositivos utilizando el contexto del equipo, es necesario configurar la autenticación de proxy de salida utilizando el contexto del equipo.


La unión a Azure AD híbrido es un proceso para registrar automáticamente los dispositivos unidos al dominio en el entorno local con Azure AD. Hay casos en los que es mejor que no todos los dispositivos se registren automáticamente. Si esto es así, consulte [Control de la unión de los dispositivos híbridos a Azure AD](hybrid-azuread-join-control.md).


## <a name="review-how-to-control-the-hybrid-azure-ad-join-of-your-devices"></a>Revisión del control de la unión de dispositivos a Azure AD híbrido

La unión a Azure AD híbrido es un proceso para registrar automáticamente los dispositivos unidos al dominio en el entorno local con Azure AD. Hay casos en los que es mejor que no todos los dispositivos se registren automáticamente. Esto es así, por ejemplo, durante el lanzamiento inicial para comprobar que todo funciona según lo previsto.

Para más información, consulte [Control de la unión de los dispositivos híbridos a Azure AD](hybrid-azuread-join-control.md).

## <a name="select-your-scenario"></a>Selección del escenario

Puede configurar la unión a Azure AD híbrido para los escenarios siguientes:

- Dominios administrados
- Dominios federados  



Si el entorno tiene dominios administrados, a unión a Azure AD híbrido admite:

- Autenticación de paso a través (PTA) con inicio de sesión único (SSO) de conexión directa 

- Sincronización de hash de contraseña (PHS) con inicio de sesión único (SSO) de conexión directa 

Desde la versión 1.1.819.0, Azure AD Connect proporciona un asistente para configurar la unión a Azure AD híbrido. El asistente permite simplificar considerablemente el proceso de configuración. Para más información, consulte:

- [Configuración de dispositivos híbridos unidos a Azure Active Directory para dominios federados](hybrid-azuread-join-federated-domains.md)


- [Configuración de dispositivos híbridos unidos a Azure Active Directory para dominios administrados](hybrid-azuread-join-managed-domains.md)


 Si no le es posible instalar la versión requerida de Azure AD Connect, consulte la información sobre [cómo configurar manualmente el registro de dispositivos](../device-management-hybrid-azuread-joined-devices-setup.md). 






## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Configuración de dispositivos híbridos unidos a Azure Active Directory para dominios federados](hybrid-azuread-join-federated-domains.md)
> [Configuración de dispositivos híbridos unidos a Azure Active Directory para dominios administrados](hybrid-azuread-join-managed-domains.md)




<!--Image references-->
[1]: ./media/hybrid-azuread-join-plan/12.png
