---
title: 'Tutorial: Integración de Azure Active Directory con IBM Kenexa Survey Enterprise | Microsoft Docs'
description: Aprenda a configurar el inicio de sesión único entre Azure Active Directory e IBM Kenexa Survey Enterprise.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.collection: M365-identity-device-management
ms.openlocfilehash: f67b24ca0008a03474b54a1bf226261c3f395fec
ms.sourcegitcommit: 301128ea7d883d432720c64238b0d28ebe9aed59
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2019
ms.locfileid: "56183231"
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a>Tutorial: Integración de Azure Active Directory con IBM Kenexa Survey Enterprise

En este tutorial, aprenderá a integrar IBM Kenexa Survey Enterprise con Azure Active Directory (Azure AD).

La integración de IBM Kenexa Survey Enterprise con Azure AD proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a IBM Kenexa Survey Enterprise.
- Puede permitir que los usuarios inicien sesión automáticamente en IBM Kenexa Survey Enterprise mediante el inicio de sesión único (SSO) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: Azure Portal.

Si quiere obtener más información sobre la integración de aplicaciones de software como servicio (SaaS) con Azure AD, vea [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Requisitos previos

Para configurar la integración de Azure AD con IBM Kenexa Survey Enterprise, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para el inicio de sesión único en IBM Kenexa Survey Enterprise

> [!NOTE]
> No se recomienda usar un entorno de producción para probar los pasos de este tutorial.

Para probar los pasos de este tutorial, siga estas recomendaciones:

- No use el entorno de producción, salvo que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede [obtener una versión de prueba durante un mes](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Descripción del escenario
En este tutorial, puede probar el inicio de sesión único (SSO) de Azure AD en un entorno de prueba. El escenario descrito en el tutorial consta de dos bloques de creación principales:

* Adición de IBM Kenexa Survey Enterprise desde la galería
* Configuración y prueba del inicio de sesión único de Azure AD

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a>Agregar IBM Kenexa Survey Enterprise desde la galería
Para configurar la integración de IBM Kenexa Survey Enterprise en Azure AD, agregue IBM Kenexa Survey Enterprise desde la galería a la lista de aplicaciones SaaS administradas.

Para agregar IBM Kenexa Survey Enterprise desde la galería, siga estos pasos:

1. En el panel izquierdo de [Azure Portal](https://portal.azure.com), haga clic en el botón **Azure Active Directory**. 

    ![Botón Azure Active Directory][1]

1. Vaya a **Aplicaciones empresariales** y seleccione **Todas las aplicaciones**.

    ![Hoja Aplicaciones empresariales][2]
    
1. Para agregar una aplicación, haga clic en el botón **Nueva aplicación**.

    ![Botón Nueva aplicación][3]

1. En el cuadro de búsqueda, escriba **IBM Kenexa Survey Enterprise**.

    ![Creación de un usuario de prueba de Azure AD](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

1. En la lista de resultados, seleccione **IBM Kenexa Survey Enterprise** y haga clic en el botón **Agregar** para agregar la aplicación.

    ![IBM Kenexa Survey Enterprise en la lista de resultados](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Configuración y prueba del inicio de sesión único en Azure AD
En esta sección, configurará y probará el inicio de sesión único de Azure AD con IBM Kenexa Survey Enterprise con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe identificar el usuario homólogo de IBM Kenexa Survey Enterprise en Azure AD. Es decir, Azure AD debe establecer una relación de vínculo entre un usuario de Azure AD y un usuario relacionado de IBM Kenexa Survey Enterprise.

Para establecer la relación de vínculo, asigne el valor de **nombre de usuario** de IBM Kenexa Survey Enterprise como valor de **nombre de usuario** de Azure AD.

Para configurar y probar el inicio de sesión único de Azure AD con IBM Kenexa Survey Enterprise, complete los bloques de creación de las dos secciones siguientes.

### <a name="configure-azure-ad-sso"></a>Configuración del inicio de sesión único de Azure AD

En esta sección, habilitará el inicio de sesión único de Azure AD en Azure Portal y configurará el inicio de sesión único en la aplicación IBM Kenexa Survey Enterprise siguiendo estos pasos:

1. En Azure Portal, en la página de integración de la aplicación **IBM Kenexa Survey Enterprise**, haga clic en **Inicio de sesión único**.

    ![Vínculo de inicio de sesión único de IBM Kenexa Survey Enterprise][4]

1. En el cuadro de diálogo **Inicio de sesión único**, en el cuadro **Modo**, seleccione **Inicio de sesión basado en SAML** para habilitar el inicio de sesión único.
 
    ![Cuadro de diálogo Inicio de sesión único](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

1. En la sección **Dominio y direcciones URL de IBM Kenexa Survey Enterprise**, siga estos pasos:

    ![Información de dominio y direcciones URL de IBM Kenexa Survey Enterprise](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

     a. En el cuadro de texto **Identificador**, escriba una dirección URL con el siguiente patrón: `https://surveys.kenexa.com/<companycode>`

    b. En el cuadro de texto **URL de respuesta**, escriba una dirección URL con el siguiente patrón: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`

    > [!NOTE] 
    > Los valores anteriores no son reales. Actualícelos con el identificador y la URL de respuesta reales. Para obtener los valores reales, póngase en contacto con el [equipo de soporte técnico de IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).

1. En **Certificado de firma de SAML**, haga clic en **Certificado (Base64)** y, luego, guarde el archivo de certificado en el equipo.

    ![Vínculo de descarga del certificado (Base64)](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    La aplicación IBM Kenexa Survey Enterprise espera recibir las aserciones del Lenguaje de marcado de aserción de seguridad (SAML) en un formato específico, que requiere que se agreguen asignaciones de atributos personalizados a la configuración de los atributos de token de SAML. El valor de la notificación de identificador de usuario en la respuesta debe coincidir con el Id. de inicio de sesión único configurado en el sistema Kenexa. Para asignar el identificador de usuario adecuado en su organización como Protocolo de datagramas de Internet (IDP) de inicio de sesión único, trabaje con el [equipo de soporte técnico de IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw). 

    De forma predeterminada, Azure AD establece el identificador de usuario como el valor de nombre principal de usuario (UPN). Puede cambiar este valor en la pestaña **Atributo**, como se muestra en la captura de pantalla siguiente. La integración solo funciona después de haber completado correctamente la asignación.
    
    ![El cuadro de diálogo Atributos de usuario](./media/kenexasurvey-tutorial/tutorial_attribute.png) 

1. Haga clic en **Save**(Guardar).

    ![Botón Guardar de Configurar inicio de sesión único](./media/kenexasurvey-tutorial/tutorial_general_400.png)

1. Para abrir la ventana **Configurar inicio de sesión**, en la sección **Configuración de IBM Kenexa Survey Enterprise**, haga clic en **Configurar IBM Kenexa Survey Enterprise**. 
 
    ![El vínculo Configurar IBM Kenexa Survey Enterprise](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

1. Copie los valores de **Sign-Out URL** (Dirección URL de cierre de sesión), **SAML Entity ID** (Identificador de entidad de SAML) y **SAML single sign-on Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) de la sección **Referencia rápida**.

1. En la ventana **Configurar inicio de sesión**, bajo **Referencia rápida**, copie los valores de **Sign-Out URL**, **SAML Entity ID** y **SAML single sign-on Service URL**.

1. Para configurar el inicio de sesión único en **IBM Kenexa Survey Enterprise**, envíe los valores descargados de **Certificado (Base64)**, **Sign-Out URL** (Dirección URL de cierre de sesión), **SAMLSAML Entity ID** (Identificador de entidad de SAML) y **SAML single sign-on Service URL** (Dirección URL del servicio de inicio de sesión único de SAML) al [equipo de soporte técnico de IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).

> [!TIP]
> Puede consultar una versión resumida de estas instrucciones en [Azure Portal](https://portal.azure.com) mientras configura la aplicación. Después de agregar la aplicación desde la sección **Active Directory** > **Aplicaciones empresariales**, simplemente haga clic en la pestaña **Inicio de sesión único** y obtenga acceso a la documentación insertada a través de la sección **Configuración** de la parte final. Para obtener más información sobre la característica de documentación insertada, vea la [documentación insertada de Azure AD](https://go.microsoft.com/fwlink/?linkid=845985).
> 

### <a name="create-an-azure-ad-test-user"></a>Creación de un usuario de prueba de Azure AD
En esta sección, creará el usuario de prueba Britta Simon en Azure Portal siguiendo estos pasos:

![Creación de un usuario de prueba de Azure AD][100]

1. En el panel izquierdo de Azure Portal, haga clic en el botón **Azure Active Directory**.

    ![Botón Azure Active Directory](./media/kenexasurvey-tutorial/create_aaduser_01.png) 

1. Para mostrar la lista de usuarios, vaya a **Usuarios y grupos** y, luego, haga clic en **Todos los usuarios**.
    
    ![Vínculos "Usuarios y grupos" y "Todos los usuarios"](./media/kenexasurvey-tutorial/create_aaduser_02.png) 

1. En la parte superior del cuadro de diálogo **Todos los usuarios**, haga clic en **Agregar** para abrir el cuadro de diálogo **Agregar**.
 
    ![Botón Agregar](./media/kenexasurvey-tutorial/create_aaduser_03.png) 

1. En el cuadro de diálogo **Usuario** , realice los pasos siguientes:
 
    ![Cuadro de diálogo Usuario](./media/kenexasurvey-tutorial/create_aaduser_04.png) 

     a. En el cuadro **Nombre**, escriba **BrittaSimon**.

    b. En el cuadro de texto **Nombre de usuario**, escriba la dirección de correo electrónico del usuario Britta Simon.

    c. Active la casilla **Mostrar contraseña** y, después, anote el valor que se muestra en el cuadro **Contraseña**.

    d. Haga clic en **Create**(Crear).
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a>Creación de un usuario de prueba de IBM Kenexa Survey Enterprise

En esta sección, creará un usuario llamado Britta Simon en IBM Kenexa Survey Enterprise. 

Para crear usuarios en el sistema IBM Kenexa Survey Enterprise y asignarles el identificador de SSO, puede trabajar con el [equipo de soporte técnico de IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw). Este valor de identificador de SSO también debe asignarse al valor user identifier (identificador de usuario) de Azure AD. Puede cambiar esta configuración predeterminada en la pestaña **Atributo**.

### <a name="assign-the-azure-ad-test-user"></a>Asignación del usuario de prueba de Azure AD

En esta sección, concederá acceso al usuario Britta Simon a IBM Kenexa Survey Enterprise para que use el inicio de sesión único de Azure.

![Asignación de rol de usuario][200] 

Para asignar al usuario Britta Simon a IBM Kenexa Survey Enterprise, siga estos pasos:

1. En Azure Portal, abra la vista **Aplicaciones**, vaya a la vista **Directorio**, seleccione **Aplicaciones empresariales** y después haga clic en **Todas las aplicaciones**.

    ![Vínculos "Aplicaciones empresariales" y "Todas las aplicaciones"][201] 

1. En la lista **Aplicaciones**, seleccione **IBM Kenexa Survey Enterprise**.

    ![Vínculo IBM Kenexa Survey Enterprise en la lista Aplicaciones](./media/kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

1. En el panel izquierdo, haga clic en **Usuarios y grupos**.

    ![Vínculo "Usuarios y grupos"][202] 

1. Haga clic en el botón **Agregar** y, después, en el panel **Agregar asignación**, seleccione **Usuarios y grupos**.

    ![Panel Agregar asignación][203]

1. En el cuadro de diálogo **Usuarios y grupos**, en la lista **Usuarios** seleccione **Britta Simon**.

1. En el cuadro de diálogo **Usuarios y grupos**, haga clic en el botón **Seleccionar**.

1. En el cuadro de diálogo **Agregar asignación**, haga clic en el botón **Asignar**.
    
### <a name="test-single-sign-on"></a>Prueba de inicio de sesión único

En esta sección, probará la configuración de inicio de sesión único de Azure AD mediante el panel de acceso.

Al hacer clic en el icono de **IBM Kenexa Survey Enterprise** en el panel de acceso, debería iniciar sesión automáticamente en su aplicación IBM Kenexa Survey Enterprise.

## <a name="additional-resources"></a>Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/kenexasurvey-tutorial/tutorial_general_203.png

 
