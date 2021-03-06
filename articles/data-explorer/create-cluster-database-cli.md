---
title: 'Inicio rápido: Creación de un clúster y una base de datos de Azure Data Explorer mediante la CLI'
description: Aprenda a crear un clúster y una base de datos de Azure Data Explorer mediante la CLI de Azure.
services: data-explorer
author: radennis
ms.author: radennis
ms.reviewer: orspod
ms.service: data-explorer
ms.topic: quickstart
ms.date: 2/4/2019
ms.openlocfilehash: 357f0efcf7300545d10113c92702d9fed4aad049
ms.sourcegitcommit: fdd6a2927976f99137bb0fcd571975ff42b2cac0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/27/2019
ms.locfileid: "56958029"
---
# <a name="create-an-azure-data-explorer-cluster-and-database-by-using-the-cli"></a>Creación de un clúster y una base de datos de Azure Data Explorer mediante la CLI

En este inicio rápido se describe cómo crear un clúster y una base de datos de Azure Data Explorer mediante la CLI de Azure.

## <a name="prerequisites"></a>Requisitos previos

Para completar esta guía de inicio rápido, necesita una suscripción de Azure. Si no tiene una, [cree una cuenta gratuita](https://azure.microsoft.com/free/) antes de empezar.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Si decide instalar y usar la CLI de Azure en un entorno local, en este inicio rápido se requiere la versión 2.0.4 o posterior de la CLI de Azure. Ejecute `az --version` para comprobar la versión. Si necesita instalarla o actualizarla, consulte [Instalación de la CLI de Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).

## <a name="configure-the-cli-parameters"></a>Configuración de los parámetros de la CLI

Los pasos siguientes no son necesarios si ejecuta comandos en Azure Cloud Shell. Si ejecuta la CLI localmente, realice los pasos siguientes para iniciar sesión en Azure y establecer su suscripción actual:

1. Ejecute el siguiente comandos para iniciar sesión en Azure:

    ```azurecli-interactive
    az login
    ```

2. Establezca la suscripción donde quiere que se cree el clúster. Reemplace `MyAzureSub` por el nombre de la suscripción de Azure que quiere usar:

    ```azurecli-interactive
    az account set --subscription MyAzureSub
    ```

## <a name="create-the-azure-data-explorer-cluster"></a>Creación del clúster de Azure Data Explorer

1. Cree el clúster mediante el siguiente comando:

    ```azurecli-interactive
    az kusto cluster create --name azureclitest --sku D11_v2 --resource-group testrg
    ```

   |**Configuración** | **Valor sugerido** | **Descripción del campo**|
   |---|---|---|
   | Nombre | *azureclitest* | Nombre que quiere para el clúster.|
   | sku | *D13_v2* | La SKU que se usará para el clúster. |
   | resource-group | *testrg* | Nombre del grupo de recursos en el que se creará el clúster. |

    Hay varios parámetros opcionales que puede usar, como la capacidad del clúster, etcétera.

2. Ejecute el siguiente comando para comprobar si el clúster se creó correctamente:

    ```azurecli-interactive
    az kusto cluster show --name azureclitest --resource-group testrg
    ```

Si el resultado contiene `provisioningState` con el valor `Succeeded`, significa que el clúster se ha creado correctamente.

## <a name="create-the-database-in-the-azure-data-explorer-cluster"></a>Creación de la base de datos en el clúster de Azure Data Explorer

1. Cree la base de datos con el siguiente comando:

    ```azurecli-interactive
    az kusto database create --cluster-name azureclitest --name clidatabase --resource-group testrg --soft-delete-period 3650:00:00:00 --hot-cache-period 3650:00:00:00
    ```

   |**Configuración** | **Valor sugerido** | **Descripción del campo**|
   |---|---|---|
   | cluster-name | *azureclitest* | Nombre del clúster donde se creará la base de datos.|
   | Nombre | *clidatabase* | Nombre de la base de datos.|
   | resource-group | *testrg* | Nombre del grupo de recursos en el que se creará el clúster. |
   | soft-delete-period | *3650:00:00:00* | Cantidad de tiempo que los datos estarán disponibles para consulta. |
   | hot-cache-period | *3650:00:00:00* | Cantidad de tiempo que los datos se conservarán en la caché. |

2. Ejecute el siguiente comando para ver la base de datos que ha creado:

    ```azurecli-interactive
    az kusto database show --name clidatabase --resource-group testrg --cluster-name azureclitest
    ```

Ahora cuenta con un clúster y una base de datos.

## <a name="clean-up-resources"></a>Limpieza de recursos

* Si tiene previsto seguir nuestros tutoriales y guías de inicio rápido, conserve los recursos que creó.
* Para limpiar los recursos, elimine el clúster. Cuando se elimina un clúster, también se eliminan todas las bases de datos en él. Use el siguiente comando para eliminar el clúster:

    ```azurecli-interactive
    az kusto cluster delete --name azureclitest --resource-group testrg
    ```

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Inicio rápido: Ingesta de datos mediante la biblioteca de Python de Azure Data Explorer](python-ingest-data.md)
