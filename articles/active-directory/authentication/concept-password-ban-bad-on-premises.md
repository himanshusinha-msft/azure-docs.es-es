---
title: Versión preliminar de Protección con contraseña de Azure AD
description: Prohibir las contraseñas en Active Directory local mediante el uso de vista previa de protección de contraseña de Azure AD
services: active-directory
ms.service: active-directory
ms.subservice: authentication
ms.topic: conceptual
ms.date: 02/18/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: jsimmons
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2fdf308ff6178dcb51ec73e46d43b853f62e7777
ms.sourcegitcommit: 2d0fb4f3fc8086d61e2d8e506d5c2b930ba525a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/18/2019
ms.locfileid: "57840960"
---
# <a name="preview-enforce-azure-ad-password-protection-for-windows-server-active-directory"></a>Vista previa: Aplicación de Protección con contraseña de Azure AD para Windows Server Active Directory

|     |
| --- |
| Protección mediante contraseña de Azure Active Directory (Azure AD) y la lista de contraseñas prohibidas personalizados son características de versión preliminar pública de Azure AD. Para obtener información sobre las versiones preliminares, consulte [términos de uso complementarios para vistas previas de Microsoft Azure](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).|
|     |

Protección mediante contraseña de Azure AD es una nueva característica en versión preliminar pública que mejora las directivas de contraseña en una organización. Protección de contraseña de implementación local utiliza tanto el globales y personalizadas contraseñas prohibidas listas que se almacenan en Azure AD. Esto consigue el mismo comprobaciones locales como Azure AD para los cambios en la nube.

## <a name="design-principles"></a>Principios de diseño

Protección mediante contraseña de Azure AD está diseñado con estos principios en mente:

* Los controladores de dominio nunca tienen que comunicarse directamente con internet.
* No se abren nuevos puertos de red en los controladores de dominio.
* No se requiere ningún cambio de esquema de Active Directory. El software utiliza Active Directory de **contenedor** y **serviceConnectionPoint** los objetos de esquema.
* Active Directory bosque o dominio de nivel funcional mínimo (DFL/FFL) no se requiere.
* El software no crear ni exigen que las cuentas de los dominios de Active Directory que protección.
* Las contraseñas de usuario cifradas no permita que el controlador de dominio durante las operaciones de validación de contraseña o en cualquier otro momento.
* Se admite la implementación incremental. Pero solo se aplica la directiva de contraseñas está instalado el agente de controlador de dominio (DC agente).
* Se recomienda que instale al agente de controlador de dominio en todos los controladores de dominio para garantizar el cumplimiento de seguridad de protección de contraseña universal.

## <a name="architectural-diagram"></a>Diagrama de arquitectura

Es importante comprender el diseño subyacente y los conceptos de la función antes de implementar la protección de contraseña de Azure AD en un entorno de Active Directory local. El diagrama siguiente muestra cómo funcionan conjuntamente los componentes de la protección con contraseña:

![Funcionamiento conjunto de los componentes de Protección con contraseña de Azure AD](./media/concept-password-ban-bad-on-premises/azure-ad-password-protection.png)

* El servicio de proxy de Protección con contraseña de Azure AD se ejecuta en cualquier máquina unida a un dominio del bosque de Active Directory actual. Su objetivo principal es reenviar las solicitudes de descarga de directiva de contraseñas de los controladores de dominio a Azure AD. A continuación, devuelve las respuestas de Azure AD para el controlador de dominio.
* La DLL del agente de DC de filtro de contraseña recibe las solicitudes de validación de contraseña de usuario desde el sistema operativo. Lo reenvía al servicio del agente de controlador de dominio que se ejecuta localmente en el controlador de dominio.
* El servicio del agente de controlador de dominio de la protección con contraseña recibe las solicitudes de validación de contraseña de la DLL del agente de DC de filtro de contraseña. Se procesa mediante el uso de la directiva de contraseñas (disponibles localmente) actual y devuelve el resultado: *pasar* o *producirá un error en*.

## <a name="how-password-protection-works"></a>Cómo funciona la protección con contraseña

Cada instancia del servicio de Proxy de la protección de contraseña de Azure AD se anuncia a los controladores de dominio del bosque mediante la creación de un **serviceConnectionPoint** objeto en Active Directory.

Cada servicio del agente de controlador de dominio para la protección con contraseña también se crea un **serviceConnectionPoint** objeto en Active Directory. Este objeto se usa principalmente para los informes y diagnósticos.

El servicio del agente de controlador de dominio es responsable de iniciar la descarga de una directiva de contraseña de Azure AD. El primer paso consiste en localizar un servicio de Proxy de la protección de contraseña de Azure AD mediante la consulta del bosque para el proxy **serviceConnectionPoint** objetos. Cuando se encuentra un servicio de proxy disponible, el agente de controlador de dominio envía una solicitud de descarga de la directiva de contraseña para el servicio de proxy. El servicio de proxy a su vez envía la solicitud a Azure AD. El servicio de proxy, a continuación, devuelve la respuesta para el servicio del agente de controlador de dominio.

Una vez que el servicio del agente de controlador de dominio recibe una nueva directiva de contraseña de Azure AD, el servicio almacena la directiva en una carpeta dedicada en la raíz de su dominio *sysvol* uso compartido de carpetas. El servicio del agente de controlador de dominio también supervisa esta carpeta en caso de las directivas más recientes replican desde otros servicios de agente de controlador de dominio en el dominio.

El servicio del agente de controlador de dominio siempre solicita una nueva directiva al inicio del servicio. Una vez iniciado el servicio del agente de controlador de dominio, comprueba la antigüedad de la directiva actual disponible de forma local cada hora. Si la directiva es anterior a una hora, el agente de controlador de dominio solicita una nueva directiva de Azure AD, como se describió anteriormente. Si la directiva actual no es anterior a una hora, el agente de controlador de dominio sigue usando esa directiva.

Cada vez que se descarga una directiva de contraseña de protección de contraseña de Azure AD, esa directiva es específica de un inquilino. En otras palabras, las directivas de contraseñas son siempre una combinación de la lista global de contraseñas prohibidas de Microsoft y la lista de contraseñas prohibidas por inquilino personalizados.

El agente de controlador de dominio se comunica con el servicio de proxy a través de RPC a través de TCP. Escucha el servicio de proxy para estas llamadas en un puerto RPC dinámico o estático, según la configuración.

El agente de controlador de dominio nunca escucha en un puerto de red disponible.

El servicio de proxy nunca llama al servicio de agente de controlador de dominio.

El servicio de proxy es sin estado. Nunca almacena en caché las directivas o cualquier otro estado descargado de Azure.

El servicio del agente de controlador de dominio siempre usa la directiva de contraseña localmente disponible más reciente para evaluar una contraseña de usuario. Si no hay ninguna directiva de contraseña está disponible en el controlador de dominio local, se acepta automáticamente la contraseña. Cuando esto ocurre, se registra un mensaje de evento para advertir al administrador.

Protección mediante contraseña de Azure AD no es un motor de aplicación de directivas en tiempo real. Puede haber un retraso entre cuando se realiza un cambio de configuración de directiva de contraseña en Azure AD y al que cambiar alcanza y se aplican en todos los controladores de dominio.

## <a name="foresttenant-binding-for-password-protection"></a>Enlace del bosque o el inquilino para la protección con contraseña

Implementación de protección mediante contraseña de Azure AD en un bosque de Active Directory requiere el registro de dicho bosque con Azure AD. Cada servicio de proxy que se implementa también debe registrarse con Azure AD. Estos registros de bosque y el servidor proxy están asociados a un determinado inquilino de Azure AD, que se identifica implícitamente mediante las credenciales que se usan durante el registro.

El bosque de Active Directory y todos los servicios de proxy implementada dentro de un bosque deben registrarse con el mismo inquilino. No se admite para tener un bosque de Active Directory o cualquier servicio de proxy en ese bosque que se está registrando con Azure AD diferentes a los inquilinos. Los síntomas de esa implementación mal configurado incluyen la imposibilidad de descargar las directivas de contraseña.

## <a name="license-requirements"></a>Requisitos de licencia

Las ventajas de la lista de contraseñas prohibidas global se aplican a todos los usuarios de Azure AD.

La lista de contraseñas prohibidas personalizada requiere licencias de Azure AD Basic.

Protección con contraseña de Azure AD para Windows Server Active Directory requiere licencias premium de Azure AD.

Para obtener información adicional sobre licencias, consulte [precios de Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/).

## <a name="download"></a>Descargar

Los dos instaladores de agente necesario para la protección de contraseña de Azure AD están disponibles desde el [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=57071).

## <a name="next-steps"></a>Pasos siguientes
[Implementación de la protección de contraseñas de Azure AD](howto-password-ban-bad-on-premises-deploy.md)
