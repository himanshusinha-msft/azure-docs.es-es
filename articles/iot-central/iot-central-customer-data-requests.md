---
title: Características de solicitud de datos del cliente de Azure IoT Central | Microsoft Docs
description: Características de solicitud de datos del cliente de Azure IoT Central
author: dominicbetts
ms.author: dobett
ms.date: 05/17/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: timlt
ms.openlocfilehash: 2952008ca788a620f2b558d5997aeebd59196b7a
ms.sourcegitcommit: 3f4ffc7477cff56a078c9640043836768f212a06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2019
ms.locfileid: "57314575"
---
# <a name="summary-of-customer-data-request-features"></a>Resumen de características de solicitud de datos del cliente

Azure IoT Central es una solución de software como servicio de Internet de las cosas (IoT) totalmente administrada que facilita la conexión, la supervisión y la administración de sus recursos de IoT a escala, la extracción de conclusiones detalladas de sus datos de IoT y la realización de acciones informadas.

[!INCLUDE [gdpr-intro-sentence](../../includes/gdpr-intro-sentence.md)]

## <a name="identifying-customer-data"></a>Identificación de los datos del cliente

Los id. de objeto de Azure Active Directory se utilizan para identificar usuarios y asignar roles. El portal Azure IoT Central muestra direcciones de correo electrónico de usuario para asignaciones de roles, pero solo se almacena el id. de objeto de Azure Active Directory; la dirección de correo electrónico se consulta de forma dinámica desde Azure Active Directory. Los administradores de Azure IoT Central pueden ver, exportar y eliminar usuarios de la aplicación en la sección de administración de usuarios de una aplicación de Azure IoT Central.

Desde la aplicación, se pueden configurar direcciones de correo electrónico para recibir alertas. En este caso, las direcciones de correo electrónico se almacenan en IoT Central y se deben administrar desde la página de administración de la cuenta de la aplicación.

En cuanto a los dispositivos, Microsoft no conserva ninguna información y no tiene acceso a datos que permitan la correlación entre el dispositivo y el usuario. Muchos de los dispositivos que se administran en Azure IoT Central no son dispositivos personales; por ejemplo, una máquina expendedora o una cafetera. Sin embargo, los clientes pueden considerar que algunos dispositivos se pueden identificar a nivel personal y, a su discreción, pueden mantener sus propios sistemas de seguimiento de activos o de inventario que vinculan dispositivos a personas. Azure IoT Central administra y almacena todos los datos asociados con dispositivos como si fueran datos personales.

Cuando se usan servicios para empresas de Microsoft, Microsoft genera cierta información, conocida como registros generados por el sistema. Estos registros constituyen acciones objetivas que se realizan en el servicio, diagnostican datos relacionados con dispositivos individuales y no están relacionados con la actividad del usuario. Los administradores de la aplicación no pueden acceder a los registros generados por el sistema de Azure IoT Central ni exportarlos.

## <a name="deleting-customer-data"></a>Eliminación de datos del cliente

La capacidad de eliminar datos del usuario solo se proporciona a través de la página de administración de IoT Central. Administradores de la aplicación pueden seleccionar el usuario que desea eliminar y seleccione **eliminar** en la esquina superior derecha de la aplicación para eliminar el registro. Los administradores de la aplicación también pueden quitar cuentas individuales que ya no están asociadas con la aplicación en cuestión.

Al eliminar un usuario, este deja de recibir alertas por correo electrónico. Sin embargo, su dirección de correo electrónico debe quitarse individualmente de cada alerta configurada.

Para obtener más información, consulte [Configure rules and actions for your device](tutorial-configure-rules.md) (Configuración de reglas y acciones para el dispositivo).

## <a name="exporting-customer-data"></a>Exportación de datos del cliente

La capacidad de exportar datos solo se proporciona a través de la página de administración de IoT Central. Un usuario de la aplicación puede seleccionar, copiar y pegar los datos del cliente, incluidos los roles asignados.

## <a name="links-to-additional-documentation"></a>Vínculos a documentación adicional

Para obtener más información acerca de la administración de cuentas, incluidas las definiciones de roles, consulte [How to administer your application](howto-administer.md) (Cómo administrar la aplicación).
