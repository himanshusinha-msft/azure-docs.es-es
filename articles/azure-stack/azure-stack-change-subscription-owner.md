---
title: Actualización del propietario de la suscripción de usuario de Azure Stack | Microsoft Docs
description: Cambie el propietario de la facturación para las suscripciones de usuario de Azure Stack.
services: azure-stack
documentationcenter: ''
author: sethmanheim
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: get-started-article
ms.date: 02/21/2019
ms.author: sethm
ms.reviewer: shnatara
ms.lastreviewed: 10/19/2018
ms.openlocfilehash: de5c20cf2113bcd6ce902a05d4613376145a4da3
ms.sourcegitcommit: a4efc1d7fc4793bbff43b30ebb4275cd5c8fec77
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/21/2019
ms.locfileid: "56649414"
---
# <a name="change-the-owner-for-an-azure-stack-user-subscription"></a>Cambio del propietario de una suscripción de usuario de Azure Stack

Los operadores de Azure Stack pueden usar PowerShell para cambiar el propietario de la facturación de una suscripción de usuario. Por ejemplo, una razón para cambiar el propietario es reemplazar un usuario que deja la organización.

Hay dos tipos de *propietarios* que se asignan a una suscripción:

- **Propietario de la facturación**: de forma predeterminada, es la cuenta de usuario que obtiene la suscripción de una oferta y, a continuación, posee la relación de facturación para esa suscripción. Esta cuenta también es la del administrador de la suscripción. Solo una cuenta de usuario puede tener esta designación en una suscripción. Un propietario de facturación a menudo es el responsable de una organización o equipo.

  Puede usar el cmdlet de PowerShell [Set-AzsUserSubscription](/powershell/module/azs.subscriptions.admin/set-azsusersubscription) para cambiar el propietario de la facturación.  

- **Propietarios agregados con roles RBAC**: se puede conceder el rol de **propietario** a otros usuarios con el sistema [Control de acceso basado en rol](azure-stack-manage-permissions.md) (RBAC). Se puede agregar cualquier número de cuentas de usuario adicionales como propietarios para complementar al propietario de la facturación. Los propietarios adicionales también son administradores de la suscripción y tienen todos los privilegios para ella, excepto los permisos para eliminar al propietario de la facturación.

  Puede usar PowerShell para administrar los propietarios adicionales. Para obtener más información, consulte [este artículo](/azure/role-based-access-control/role-assignments-powershell).

## <a name="change-the-billing-owner"></a>Cambio del propietario de la facturación

Ejecute el script siguiente para cambiar el propietario de la facturación de una suscripción de usuario. El equipo que se usa para ejecutar el script debe conectarse a Azure Stack y ejecutar el módulo de Azure Stack PowerShell 1.3.0 o posterior. Para más información, consulte [Instalación de Azure Stack PowerShell](azure-stack-powershell-install.md).

>[!NOTE]
>En una instancia de Azure Stack multiinquilino, el nuevo propietario debe estar en el mismo directorio que el actual. Para poder proporcionar la propiedad de la suscripción a un usuario que se encuentre en otro directorio, primero debe [invitar a ese usuario como invitado en su directorio](../active-directory/b2b/add-users-administrator.md).

Reemplace los valores siguientes en el script antes de que se ejecute:

- **$ArmEndpoint**: punto de conexión de Resource Manager para su entorno.
- **$TenantId**: El identificador de inquilino.
- **$SubscriptionId**: El identificador de suscripción.
- **$OwnerUpn**: una cuenta como **user@example.com** para agregar como el nuevo propietario de la facturación.

```powershell
# Set up Azure Stack admin environment
Add-AzureRmEnvironment -ARMEndpoint $ArmEndpoint -Name AzureStack-admin
Add-AzureRmAccount -Environment AzureStack-admin -TenantId $TenantId

# Select admin subscription
$providerSubscriptionId = (Get-AzureRmSubscription -SubscriptionName "Default Provider Subscription").Id
Write-Output "Setting context to the Default Provider Subscription: $providerSubscriptionId"
Set-AzureRmContext -Subscription $providerSubscriptionId

# Change user subscription owner
$subscription = Get-AzsUserSubscription -SubscriptionId $SubscriptionId
$Subscription.Owner = $OwnerUpn
Set-AzsUserSubscription -InputObject $subscription
```

## <a name="next-steps"></a>Pasos siguientes

- [Administración del control de acceso basado en rol](azure-stack-manage-permissions.md)
