---
title: 'Tutorial: Integración de Azure Active Directory con Workplace by Facebook | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Workplace by Facebook.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 30f2ee64-95d3-44ef-b832-8a0a27e2967c
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2018
ms.author: jeedes
ms.openlocfilehash: 2e072a27087f90bddd3f7c416904758e40c2f6b9
ms.sourcegitcommit: c61c98a7a79d7bb9d301c654d0f01ac6f9bb9ce5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52425197"
---
# <a name="tutorial-azure-active-directory-integration-with-workplace-by-facebook"></a>Tutorial: integración de Azure Active Directory con Workplace by Facebook

En este tutorial obtendrá información sobre cómo integrar Workplace by Facebook con Azure Active Directory (Azure AD).

Integrar Workplace by Facebook con Azure AD le proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a Workplace by Facebook
- Puede permitir que los usuarios inicien sesión automáticamente en Workplace by Facebook (inicio de sesión único) con sus cuentas de Azure AD
- Puede administrar sus cuentas en una ubicación central: el nuevo Azure Portal.

Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con Workplace by Facebook, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único de Workplace by Facebook

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).

> [!NOTE]
> Facebook tiene dos productos: Workplace Standard (gratis) and Workplace Premium (de pago). Todo inquilino de Workplace Premium puede configurar la integración de SCIM y SSO sin otras implicaciones de coste ni requerimiento de licencias. SSO y SCIM no están disponibles en las instancias de Workplace Standard.

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. El escenario descrito en este tutorial consta de dos bloques de creación principales:

1. Incorporación de Workplace by Facebook desde la galería
1. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-workplace-by-facebook-from-the-gallery"></a>Incorporación de Workplace by Facebook desde la galería
Para configurar la integración de Workplace by Facebook en Azure AD, deberá agregar Workplace by Facebook desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar Workplace by Facebook desde la galería, siga estos pasos:**

1. En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![APLICACIONES][2]
    
1. Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.

    ![APLICACIONES][3]

1. En el cuadro de búsqueda, escriba **Workplace by Facebook**.

    ![Creación de un usuario de prueba de Azure AD](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_search.png)

1. En el panel de resultados, seleccione **Workplace by Facebook** y haga clic en el botón **Agregar** para agregar la aplicación.

    ![Creación de un usuario de prueba de Azure AD](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configuración y comprobación del inicio de sesión único de Azure AD
En esta sección podrá configurar y probar el inicio de sesión único de Azure AD con Workplace by Facebook con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Workplace by Facebook para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Workplace by Facebook.

Esta relación de vínculo se establece mediante la asignación del valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en Workplace by Facebook.

Para configurar y probar el inicio de sesión único de Azure AD con Workplace by Facebook, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-sign-on)** : para permitir a los usuarios usar esta característica.
1. **[Configurar la frecuencia de reautenticación](#configuring-reauthentication-frequency)**: para configurar Workplace para que solicite una comprobación SAML.
1. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)** : para probar el inicio de sesión único de Azure AD con Britta Simon.
1. **[Creación de un usuario de prueba de Workplace by Facebook](#creating-a-workplace-by-facebook-test-user)**: para tener un homólogo de Britta Simon en Workplace by Facebook que esté vinculado a la representación del usuario en Azure AD.
1. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)** : para permitir que Britta Simon use el inicio de sesión único de Azure AD.
1. **[Testing Single Sign-On](#testing-single-sign-on)** : para comprobar si funciona la configuración.

### <a name="configuring-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Workplace by Facebook.

**Para configurar el inicio de sesión único de Azure AD con Workplace by Facebook, siga estos pasos:**

1. En la página de integración de la aplicación **Workplace by Facebook** de Azure Portal, haga clic en **Inicio de sesión único**.

    ![Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Configurar inicio de sesión único](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_samlbase.png)

1. En la sección **Dominio y direcciones URL de Workplace by Facebook**, siga estos pasos:

    ![Configurar inicio de sesión único](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_url.png)

     a. En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: `https://<instancename>.facebook.com`.

    b. En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://www.facebook.com/company/<instanceID>`

    > [!NOTE] 
    > Estos valores no son reales. Debe actualizarlos con la dirección URL y el identificador reales de inicio de sesión. Consulte la página de autenticación del panel de la empresa Workplace para obtener los valores correctos de la comunidad Workplace. 

1. En la sección **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.

    ![Configurar inicio de sesión único](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_certificate.png) 

1. Haga clic en el botón **Guardar** .

    ![Configurar inicio de sesión único](./media/workplacebyfacebook-tutorial/tutorial_general_400.png)

1. En la sección **Configuración de Workplace by Facebook**, haga clic en **Configurar Workplace by Facebook** para abrir la ventana **Configurar inicio de sesión**. Copie la **URL del servicio de inicio de sesión único de SAML, el identificador de entidad de SAML y la dirección URL de cierre de sesión** de la sección **Referencia rápida**.

    ![Configurar inicio de sesión único](./media/workplacebyfacebook-tutorial/config.png) 

1. En otra ventana del explorador web, inicie sesión en el sitio de empresa de Workplace by Facebook como administrador.
  
   > [!NOTE] 
   > Como parte del proceso de autenticación SAML, es posible que Workplace use cadenas de consulta de hasta 2,5 kilobytes de tamaño para pasar parámetros a Azure AD.

1. En el **panel de administración**, vaya a la pestaña **Seguridad** y, a continuación, a **Autenticación**.

1. En **Autenticación SAML**, seleccione **Solo SSO** en la lista desplegable.

1. Escriba los valores copiados de la sección **Configuración de Workplace by Facebook** de Azure Portal en los campos correspondientes:

    *   En el cuadro de texto **Dirección URL de SAML**, pegue el valor de **Dirección URL del servicio de inicio de sesión único** que ha copiado de Azure Portal.
    *   En el cuadro de texto **SAML Issuer URL** (Dirección URL del emisor SAML), pegue el valor de **SAML Entity ID** (Identificador de entidad SAML) que ha copiado de Azure Portal.
    *   En el cuadro de texto **Logout URL SAML** (Dirección URL de cierre de sesión de SAML), pegue el valor de **Dirección URL de cierre de sesión** que ha copiado de Azure Portal.
    *   Abra el **certificado codificado en Base 64** descargado de Azure Portal en el Bloc de notas, copie su contenido en el Portapapeles y luego péguelo en el cuadro de texto **Certificado SAML**.

1. Es posible que sea necesario escribir la dirección URL del público, la dirección URL del destinatario y la dirección URL de ACS (Servicio de consumidor de aserciones) que aparecen en la sección **Configuración de SAML**.

1. Desplácese hasta la parte inferior de la sección y haga clic en el botón **Probar SSO**. Como resultado aparece una ventana emergente en la que se muestra la página de inicio de sesión de Azure AD. Escriba las credenciales de la forma habitual para autenticarse. 

    **Solución de problemas:** Asegúrese de que la dirección de correo electrónico que se devuelve desde Azure AD es la misma que la cuenta de Workplace con la que ha iniciado sesión.

1. Una vez que la prueba se ha realizado correctamente, desplácese hasta la parte inferior de la página y haga clic en el botón **Guardar**.

1. Ahora se presentará a todos los usuarios de Workplace la página de inicio de sesión de Azure AD para la autenticación.

1. **Redirigir el cierre de sesión de SAML (opcional)** - 

    Puede optar por configurar una dirección URL de cierre de sesión de SAML que puede usarse para apuntar a la página de cierre de sesión de Azure AD. Si esta opción está habilitada y configurada, ya no se dirige al usuario a la página de cierre de sesión de Workplace, sino que se le redirige a la dirección URL agregada en la opción Redirigir el cierre de sesión de SAML.

### <a name="configuring-reauthentication-frequency"></a>Configuración de la frecuencia de reautenticación

Puede configurar Workplace para que solicite una comprobación SAML cada día, cada tres días, cada semana, cada dos semanas, cada mes o nunca.

> [!NOTE] 
>El valor mínimo para la comprobación SAML en aplicaciones móviles se establece en una semana.

También puede forzar el restablecimiento de SAML para todos los usuarios mediante el botón: Require SAML authentication for all users now (Requerir autenticación de SAML para todos los usuarios ahora).


### <a name="creating-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

![Creación de un usuario de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo de **Azure Portal**, haga clic en el icono de **Azure Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/workplacebyfacebook-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y haga clic en **Todos los usuarios**.
    
    ![Creación de un usuario de prueba de Azure AD](./media/workplacebyfacebook-tutorial/create_aaduser_02.png) 

1. Para abrir el cuadro de diálogo **Usuario**, haga clic en **Agregar** en la parte superior del cuadro de diálogo.
 
    ![Creación de un usuario de prueba de Azure AD](./media/workplacebyfacebook-tutorial/create_aaduser_03.png) 

1. En la página de diálogo **Usuario**, realice los siguientes pasos:
 
    ![Creación de un usuario de prueba de Azure AD](./media/workplacebyfacebook-tutorial/create_aaduser_04.png) 

     a. En el cuadro de texto **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la **dirección de correo electrónico** de Britta Simon.

    c. Seleccione **Mostrar contraseña** y anote el valor del cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).
 
### <a name="creating-a-workplace-by-facebook-test-user"></a>Creación de un usuario de prueba de Workplace by Facebook

En esta sección se crea un usuario llamado Britta Simon en Workplace by Facebook. Workplace by Facebook admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada.

El usuario no tiene que hacer nada en esta sección. Si no existe un usuario en Workplace by Facebook, se crea uno cuando intenta obtener acceso a Workplace by Facebook.

>[!Note]
>Si necesita crear un usuario de forma manual, póngase en contacto con el [equipo de soporte de cliente de Workplace by Facebook](https://workplace.fb.com/faq/)

### <a name="assigning-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, habilitará a Britta Simon para usar el inicio de sesión único de Azure al concederle acceso a Workplace by Facebook.

![Asignar usuario][200] 

**Para asignar a Britta Simon a Workplace by Facebook, siga estos pasos:**

1. En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione **Workplace by Facebook**.

    ![Configurar inicio de sesión único](./media/workplacebyfacebook-tutorial/tutorial_workplacebyfacebook_app.png) 

1. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Asignar usuario][202] 

1. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Asignar usuario][203]

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

1. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

1. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="testing-single-sign-on"></a>Prueba del inicio de sesión único 

Si desea probar la configuración de inicio de sesión único, abra el Panel de acceso.
Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](../user-help/active-directory-saas-access-panel-introduction.md).


## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)
* [Configuración del aprovisionamiento de usuarios](workplacebyfacebook-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/workplacebyfacebook-tutorial/tutorial_general_01.png
[2]: ./media/workplacebyfacebook-tutorial/tutorial_general_02.png
[3]: ./media/workplacebyfacebook-tutorial/tutorial_general_03.png
[4]: ./media/workplacebyfacebook-tutorial/tutorial_general_04.png

[100]: ./media/workplacebyfacebook-tutorial/tutorial_general_100.png

[200]: ./media/workplacebyfacebook-tutorial/tutorial_general_200.png
[201]: ./media/workplacebyfacebook-tutorial/tutorial_general_201.png
[202]: ./media/workplacebyfacebook-tutorial/tutorial_general_202.png
[203]: ./media/workplacebyfacebook-tutorial/tutorial_general_203.png
