---
title: Verificación de los paquetes del fabricante de equipos originales (OEM) en la validación como servicio de Azure Stack | Microsoft Docs
description: Aprenda a verificar los paquetes del fabricante de equipos originales (OEM) con la validación como servicio.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 02/19/2019
ms.author: mabrigg
ms.reviewer: johnhas
ms.lastreviewed: 02/19/2019
ROBOTS: NOINDEX
ms.openlocfilehash: f9ed10c84be86304722020606873b0c7866df1e8
ms.sourcegitcommit: a8948ddcbaaa22bccbb6f187b20720eba7a17edc
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/21/2019
ms.locfileid: "56594056"
---
# <a name="validate-oem-packages"></a>Validación de paquetes de OEM

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

Puede probar un nuevo paquete de OEM cuando se ha producido un cambio en el firmware o en los controladores para una validación de solución completa. Cuando el paquete ha superado la prueba, Microsoft lo firma. La prueba debe contener el paquete de extensión de OEM actualizado con los controladores y el firmware que han superado las pruebas del logotipo de Windows Server y las pruebas PCS.

[!INCLUDE [azure-stack-vaas-workflow-validation-completion](includes/azure-stack-vaas-workflow-validation-completion.md)]

> [!IMPORTANT]
> Antes de cargar o enviar paquetes, consulte [Create an OEM package](azure-stack-vaas-create-oem-package.md) (Creación de un paquete de OEM) para el formato y el contenido de paquete esperados.

## <a name="managing-packages-for-validation"></a>Administración de paquetes para la validación

Al usar el flujo de trabajo **Validación del paquete** para validar un paquete, deberá proporcionar una dirección URL a **Azure Storage Blob**. Este blob es el paquete de OEM firmado de prueba que se instalará como parte del proceso de actualización. Cree el blob mediante la cuenta de almacenamiento de Azure que creó durante la instalación (consulte [Configuración de los recursos de Validación como servicio](azure-stack-vaas-set-up-resources.md)).

### <a name="prerequisite-provision-a-storage-container"></a>Requisito previo: aprovisionar un contenedor de almacenamiento

Cree un contenedor en la cuenta de almacenamiento para los blobs de paquetes. Este contenedor puede utilizarse para todas las ejecuciones de Package Validation (Validación del paquete).

1. En [Azure Portal](https://portal.azure.com), vaya a la cuenta de almacenamiento que creó en [Configuración de los recursos de Validación como servicio](azure-stack-vaas-set-up-resources.md).
2. En la hoja izquierda de **Blob Service**, seleccione **Containers**.
3. Seleccione **+ Contenedor** en la barra de menús y proporcione un nombre al contenedor, por ejemplo, `vaaspackages`.

### <a name="upload-package-to-storage-account"></a>Carga de un paquete en una cuenta de almacenamiento

1. Prepare el paquete que desea validar. Si tiene varios archivos, comprímalos en un archivo `.zip`.
2. En [Azure Portal](https://portal.azure.com), seleccione el contenedor del paquete y cargue el paquete; para ello, seleccione **Cargar** en la barra de menús.
3. Seleccione el archivo `.zip` del paquete que se va a cargar. Mantenga los valores predeterminados para **Tipo de blob** (es decir, **Blob en bloques**) y **Tamaño de bloque**.

> [!NOTE]
> Asegúrese de que el contenido del archivo `.zip` se coloca en la raíz del archivo `.zip`. El paquete no debe tener subcarpetas.

### <a name="generate-package-blob-url-for-vaas"></a>Generación de la dirección URL del blob del paquete para VaaS

Al crear un flujo de trabajo de **Package Validation** (Validación del paquete) en el portal de VaaS, deberá proporcionar una dirección URL a la instancia de Azure Storage Blob que contiene el paquete.

#### <a name="option-1-generating-a-blob-sas-url"></a>Opción 1: Generar una dirección URL de SAS de blob

Use esta opción si no desea habilitar el acceso de lectura público a su contenedor de almacenamiento o blobs.

1. En el [Azure Portal](https://portal.azure.com/), vaya a la cuenta de almacenamiento y, después, al archivo .zip que contiene el paquete.

2. Seleccione **Generar SAS** en el menú contextual.

3. Seleccione **Lectura** en **Permisos**.

4. En **Hora de inicio** especifique la hora actual y en **Hora de finalización** una hora que sea al menos 48 horas posterior a la de inicio **.** Si va a ejecutar otras pruebas con el mismo paquete, considere la posibilidad de aumentar el valor de **Hora de finalización** para que abarque todo el tiempo que duren las pruebas. Las pruebas programadas mediante VaaS después del valor de **Hora de finalización** producirán un error y tendrá que generarse una nueva SAS.

5. Seleccione **Generate blob SAS token and URL** (Generar URL y token de SAS del blob).

Use la **dirección URL de SAS del blob** al proporcionar las direcciones URL del blob de paquete para el portal.

#### <a name="option-2-grant-public-read-access"></a>Opción 2: Conceder el acceso de lectura público

> [!CAUTION]
> Esta opción abre los blobs para el acceso anónimo de solo lectura.

1. Conceda **acceso de lectura público solo para blobs** al contenedor del paquete; para ello, siga las instrucciones de la sección [Concesión de permisos a usuarios anónimos a contenedores y blobs](https://docs.microsoft.com/azure/storage/storage-manage-access-to-resources#grant-anonymous-users-permissions-to-containers-and-blobs).

> [!NOTE]
> Si va a proporcionar una dirección URL del paquete a una *prueba interactiva* (por ejemplo, la comprobación de la actualización mensual de AzureStack o la comprobación del paquete de extensión de OEM), debe conceder **acceso de lectura público completo** para seguir con las pruebas.

2. En el contenedor del paquete, seleccione el blob del paquete para abrir el panel de propiedades.

3. Copie la **dirección URL**. Use este valor al proporcionar las direcciones URL del blob de paquete para el portal.

## <a name="apply-monthly-update"></a>Aplicación de actualización mensual

[!INCLUDE [azure-stack-vaas-workflow-section_update-azs](includes/azure-stack-vaas-workflow-section_update-azs.md)]

## <a name="create-a-package-validation-workflow"></a>Creación de un flujo de trabajo Package Validation (Validación del paquete)

1. Inicie sesión en el [portal de VaaS](https://azurestackvalidation.com).

2. [!INCLUDE [azure-stack-vaas-workflow-step_select-solution](includes/azure-stack-vaas-workflow-step_select-solution.md)]

3. Seleccione **Iniciar** en el icono **Package Validation** (Validación del paquete).

    ![Icono de flujo de trabajo Package Validation (Validación del paquete)](media/tile_validation-package.png)

4. [!INCLUDE [azure-stack-vaas-workflow-step_naming](includes/azure-stack-vaas-workflow-step_naming.md)]

5. Escriba la dirección URL del blob de Azure Storage para el paquete de OEM firmado de prueba que requiera una firma de Microsoft. Para instrucciones, consulte [Generación de la dirección URL del blob del paquete para VaaS](#generate-package-blob-url-for-vaas).

6. [!INCLUDE [azure-stack-vaas-workflow-step_upload-stampinfo](includes/azure-stack-vaas-workflow-step_upload-stampinfo.md)]

7. [!INCLUDE [azure-stack-vaas-workflow-step_test-params](includes/azure-stack-vaas-workflow-step_test-params.md)]

    > [!NOTE]
    > No se pueden modificar los parámetros de entorno después de crear un flujo de trabajo.

8. [!INCLUDE [azure-stack-vaas-workflow-step_tags](includes/azure-stack-vaas-workflow-step_tags.md)]

9. [!INCLUDE [azure-stack-vaas-workflow-step_submit](includes/azure-stack-vaas-workflow-step_submit.md)]
    Se le redirigirá a la página de resumen de las pruebas.

## <a name="required-tests"></a>Pruebas necesarias

Las pruebas siguientes son necesarias para la validación del paquete de OEM:

- Comprobación del paquete de extensión de OEM
- Cloud Simulation Engine

## <a name="run-package-validation-tests"></a>Ejecución de pruebas de Package Validation

1. En la página **Package Validation tests summary** (Resumen de las pruebas de validación del paquete), se ejecutará un subconjunto de las pruebas enumeradas apropiadas para su escenario.

    En los flujos de trabajo de validación, para **programar** una prueba se usan los parámetros comunes de nivel de flujo de trabajo que especificó durante la creación del flujo de trabajo (consulte [Parámetros comunes del flujo de trabajo en la validación de Azure Stack como servicio](azure-stack-vaas-parameters.md)). Si alguno de los valores de parámetro de prueba deja de ser válido, debe volver a suministrarlo como se indica en [Modify workflow parameters](azure-stack-vaas-monitor-test.md#change-workflow-parameters) (Modificación de los parámetros de flujo de trabajo).

    > [!NOTE]
    > La programación a través de una prueba de validación a través de una instancia existente creará una nueva instancia en el lugar de la anterior en el portal. Los registros de la instancia anterior se conservarán, pero no se podrá acceder a ellos desde el portal.  
    Una vez finalizada una prueba correctamente, la acción **Schedule** (Programar) pasará a estar deshabilitada.

2. Seleccione el agente que ejecutará la prueba. Para más información acerca de cómo agregar agentes de ejecución de prueba, consulte [Implementación del agente local](azure-stack-vaas-local-agent.md).

3. Para completar la comprobación del paquete de extensión de OEM, seleccione **Schedule** (Programar) desde el menú contextual para abrir un símbolo del sistema y programar la instancia de prueba.

4. Revise los parámetros de prueba y, luego, seleccione **Submit** (Enviar) para programar la ejecución de la comprobación del paquete de extensión de OEM.

5. Revise el resultado de la comprobación del paquete de extensión de OEM. Una vez que la prueba se haya realizado correctamente, programe el motor de simulación en la nube para ejecutarse.

Cuando todas las pruebas finalicen correctamente, envíe el nombre de la solución de VaaS y la validación del paquete a [vaashelp@microsoft.com](mailto:vaashelp@microsoft.com) para solicitar la firma del paquete.

## <a name="next-steps"></a>Pasos siguientes

- [Supervisión y administración de pruebas en el portal de VaaS](azure-stack-vaas-monitor-test.md)