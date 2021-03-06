---
title: 'Tutorial: Integración de Azure Active Directory con Elium | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory y Elium.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: fae344b3-5bd9-40e2-9a1d-448dcd58155f
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/05/2018
ms.author: jeedes
ms.openlocfilehash: dfa90474632b2cf18055e0ba95994f120cb293ef
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39447791"
---
# <a name="tutorial-azure-active-directory-integration-with-elium"></a>Tutorial: Integración de Azure Active Directory con Elium

En este tutorial, aprenderá a integrar Elium con Azure Active Directory (Azure AD).

La integración de Elium con Azure AD le proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a Elium.
- Puede permitir que los usuarios inicien sesión automáticamente en Elium (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: Azure Portal.

Si desea saber más sobre la integración de aplicaciones SaaS con Azure AD, consulte [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con Elium, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en Elium

> [!NOTE]
> Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.

Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único de Azure AD en un entorno de prueba. El escenario descrito en este tutorial consta de dos bloques de creación principales:

1. Adición de Elium desde la galería
1. Configuración y comprobación del inicio de sesión único de Azure AD

## <a name="adding-elium-from-the-gallery"></a>Adición de Elium desde la galería
Para configurar la integración de Elium en Azure AD, deberá agregar Elium desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar Elium desde la galería, realice los pasos siguientes:**

1. En el panel de navegación izquierdo de **[Azure Portal](https://portal.azure.com)**, haga clic en el icono de **Azure Active Directory**. 

    ![Botón Azure Active Directory][1]

1. Vaya a **Aplicaciones empresariales**. A continuación, vaya a **Todas las aplicaciones**.

    ![Hoja Aplicaciones empresariales][2]
    
1. Para agregar una nueva aplicación, haga clic en el botón **Nueva aplicación** de la parte superior del cuadro de diálogo.

    ![Botón Nueva aplicación][3]

1. En el cuadro de búsqueda, escriba **Elium**, seleccione **Elium** en el panel de resultados y, luego, haga clic en el botón **Agregar** para agregar la aplicación.

    ![Elium en la lista de resultados](./media/elium-tutorial/tutorial_elium_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD

En esta sección, podrá configurar y probar el inicio de sesión único de Azure AD con Elium con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de Elium para un usuario de Azure AD. Es decir, es necesario establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de Elium.

Para configurar y probar el inicio de sesión único de Azure AD con Elium, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configure-azure-ad-single-sign-on)**: para que los usuarios puedan usar esta característica.
1. **[Creación de un usuario de prueba de Azure AD](#create-an-azure-ad-test-user)**, para probar el inicio de sesión único de Azure AD con Britta Simon.
1. **[Creación de un usuario de prueba de Elium](#create-an-elium-test-user)**: para tener un homólogo de Britta Simon en Elium que esté vinculado a la representación de ella en Azure AD.
1. **[Asignación del usuario de prueba de Azure AD](#assign-the-azure-ad-test-user)**, para permitir que Britta Simon use el inicio de sesión único de Azure AD.
1. **[Prueba del inicio de sesión único](#test-single-sign-on)**: para comprobar si la configuración funciona.

### <a name="configure-azure-ad-single-sign-on"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación Elium.

**Para configurar el inicio de sesión único de Azure AD con Elium, realice los pasos siguientes:**

1. En Azure Portal, en la página de integración de la aplicación **Elium**, haga clic en **Inicio de sesión único**.

    ![Vínculo Configurar inicio de sesión único][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en **Modo** seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/elium-tutorial/tutorial_elium_samlbase.png)

1. En la sección **Elium Domain and URLs** (Dominio y direcciones URL de Elium), realice los siguientes pasos si quiere configurar la aplicación en el modo iniciado por **IDP**:

    ![Información de dominio y direcciones URL de inicio de sesión único de Elium](./media/elium-tutorial/tutorial_elium_url.png)

    a. En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://<platform-domain>.elium.com/login/saml2/metadata`

    b. En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://<platform-domain>.elium.com/login/saml2/acs`.

1. Active **Mostrar configuración avanzada de URL** y siga estos pasos si desea configurar la aplicación en el modo iniciado por **SP**:

    ![Información de dominio y direcciones URL de inicio de sesión único de Elium](./media/elium-tutorial/tutorial_elium_url1.png)

    En el cuadro de texto **URL de inicio de sesión**, escriba una dirección URL con el siguiente patrón: ` https://<platform-domain>.elium.com/login/saml2/login`.
     
    > [!NOTE] 
    > Estos valores no son reales. Los obtendrá del **archivo de metadatos de SP** que se puede descargar en `https://<platform-domain>.elium.com/login/saml2/metadata`. Esto se explica más adelante en este tutorial.

1. La aplicación Elium espera las aserciones de SAML en un formato específico, lo que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos del token de SAML. Configure las siguientes notificaciones para esta aplicación. Puede administrar los valores de estos atributos en la sección "**Atributos de usuario**" de la página de integración de aplicaciones.

    ![Configurar inicio de sesión único](./media/elium-tutorial/tutorial_attribute.png)

1. En la sección **Atributos de usuario** del cuadro de diálogo **Inicio de sesión único**, configure el atributo del token de SAML como muestra la imagen anterior y realice los siguientes pasos:
           
    | Nombre del atributo | Valor de atributo |   
    | ---------------| ----------------|
    | email   |user.mail |
    | first_name| user.givenname |
    | last_name| user.surname|
    | job_title| user.jobtitle|
    | company| user.companyname|
    
    > [!NOTE]
    > Estas son las notificaciones predeterminadas. **Solo se requiere la notificación de correo electrónico**. Para el aprovisionamiento de JIT, también solo es obligatoria la notificación de correo electrónico. Otras notificaciones personalizadas pueden variar de una plataforma de cliente a otra.

    a. Haga clic en **Agregar atributo** para abrir el cuadro de diálogo **Agregar atributo**.

    ![Configurar inicio de sesión único](./media/elium-tutorial/tutorial_attribute_04.png)

    b. En el cuadro de texto **Nombre**, escriba el nombre que se muestra para la fila.

    ![Configurar inicio de sesión único](./media/elium-tutorial/tutorial_attribute_05.png)

    c. En la lista **Valor**, seleccione el atributo que se muestra para esa fila.

    d. Deje el espacio de nombres en blanco.
    
    e. Haga clic en **Aceptar**. 

1. En la sección **Certificado de firma de SAML**, haga clic en **XML de metadatos** y luego guarde el archivo de metadatos en el equipo.

    ![Vínculo de descarga del certificado](./media/elium-tutorial/tutorial_elium_certificate.png) 

1. Haga clic en el botón **Guardar** .

    ![Botón Configurar inicio de sesión único](./media/elium-tutorial/tutorial_general_400.png)
    
1. En otra ventana del explorador web, inicie sesión en su sitio de la compañía de Elium como administrador.

1. Haga clic en el **perfil de usuario** en la esquina superior derecha y, a continuación, seleccione **Administration** (Administración).

    ![Configurar inicio de sesión único](./media/elium-tutorial/user1.png)

1. Seleccione la pestaña **Seguridad**.

    ![Configurar inicio de sesión único](./media/elium-tutorial/user2.png)

1. Desplácese a la sección **Single sign-on (SSO)** (Inicio de sesión único [SSO]) y realice los pasos siguientes:

    ![Configurar inicio de sesión único](./media/elium-tutorial/user3.png)

    a. Copie el valor de **Verify that SAML2 authentication works for your account** (Verificar que la autenticación de SAML2 funciona para su cuenta) y péguelo en el cuadro de texto **Dirección URL de inicio de sesión** en la sección **Elium Domain and URLs** (Dominio y direcciones URL de Elium) en Azure Portal.

    > [!NOTE]
    > Después de configurar el inicio de sesión único, siempre puede acceder a la página de inicio de sesión remoto predeterminada en la siguiente dirección URL: `https://<platform_domain>/login/regular/login` 

    b. Active la casilla **Enable SAML2 federation** (Habilitar la federación de SAML2).

    c. Active la casilla **JIT Provisioning** (Aprovisionamiento de JIT).

    d. Abra el archivo de **metadatos de SP**; para ello, haga clic en el botón **Download** (Descargar).

    e. Busque **entityID** en el archivo de **metadatos de SP**, copie el valor de **entityID** y péguelo en el cuadro de texto **Identifier** (Identificador) de la sección **Elium Domain and URLs** (Dominio y direcciones URL de Elium) de Azure Portal. 

    ![Configurar inicio de sesión único](./media/elium-tutorial/user4.png)

    f. Busque **AssertionConsumerService** en el archivo de **metadatos de SP**, copie el valor de **Location** (Ubicación) y péguelo en el cuadro de texto **Dirección URL de respuesta** de la sección **Elium Domain and URLs** (Dominio y direcciones URL) de Azure Portal.

    ![Configurar inicio de sesión único](./media/elium-tutorial/user5.png)

    g. Abra el archivo de metadatos descargado de Azure Portal en el Bloc de notas, copie el contenido y péguelo en el cuadro de texto **IdP Metadata** (Metadatos del IdP).

    h. Haga clic en **Save**(Guardar).

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD

El objetivo de esta sección es crear un usuario de prueba en Azure Portal llamado "Britta Simon".

   ![Creación de un usuario de prueba de Azure AD][100]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.

    ![Botón Azure Active Directory](./media/elium-tutorial/create_aaduser_01.png)

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.

    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/elium-tutorial/create_aaduser_02.png)

1. En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.

    ![Botón Agregar](./media/elium-tutorial/create_aaduser_03.png)

1. En el cuadro de diálogo **Usuario** , realice los pasos siguientes:

    ![Cuadro de diálogo Usuario](./media/elium-tutorial/create_aaduser_04.png)

    a. En el cuadro **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.

    c. Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).
 
### <a name="create-an-elium-test-user"></a>Creación de un usuario de prueba de Elium

El objetivo de esta sección es crear un usuario de prueba llamado Britta Simon en Elium. Elium admite el aprovisionamiento Just-In-Time, que está habilitado de forma predeterminada. No hay ningún elemento de acción para usted en esta sección. Al intentar acceder a Elium, se crea un nuevo usuario, en caso de que no exista.
>[!Note]
>Si necesita crear manualmente un usuario, póngase en contacto con el [equipo de soporte técnico de Elium](mailto:support@elium.com).

### <a name="assign-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, permitirá que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a Elium.

![Asignación de rol de usuario][200] 

**Para asignar el usuario Britta Simon a Elium, realice los pasos siguientes:**

1. En Azure Portal, abra la vista de aplicaciones, navegue a la vista de directorio y vaya a **Aplicaciones empresariales**. Luego haga clic en **Todas las aplicaciones**.

    ![Asignar usuario][201] 

1. En la lista de aplicaciones, seleccione **Elium**.

    ![Vínculo a Elium en la lista de aplicaciones](./media/elium-tutorial/tutorial_elium_app.png)  

1. En el menú de la izquierda, haga clic en **Usuarios y grupos**.

    ![Vínculo "Usuarios y grupos"][202]

1. Haga clic en el botón **Agregar**. Después, seleccione **Usuarios y grupos** en el cuadro de diálogo **Agregar asignación**.

    ![Panel Agregar asignación][203]

1. En el cuadro de diálogo **Usuarios y grupos**, seleccione **Britta Simon** en la lista de usuarios.

1. Haga clic en el botón **Seleccionar** del cuadro de diálogo **Usuarios y grupos**.

1. Haga clic en el botón **Asignar** del cuadro de diálogo **Agregar asignación**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el Panel de acceso.

Al hacer clic en el icono de Elium en el panel de acceso, debería iniciar sesión automáticamente en su aplicación Elium.
Para más información sobre el Panel de acceso, consulte [Introducción al Panel de acceso](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/elium-tutorial/tutorial_general_01.png
[2]: ./media/elium-tutorial/tutorial_general_02.png
[3]: ./media/elium-tutorial/tutorial_general_03.png
[4]: ./media/elium-tutorial/tutorial_general_04.png

[100]: ./media/elium-tutorial/tutorial_general_100.png

[200]: ./media/elium-tutorial/tutorial_general_200.png
[201]: ./media/elium-tutorial/tutorial_general_201.png
[202]: ./media/elium-tutorial/tutorial_general_202.png
[203]: ./media/elium-tutorial/tutorial_general_203.png

