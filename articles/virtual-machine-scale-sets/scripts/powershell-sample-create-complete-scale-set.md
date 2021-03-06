---
title: 'Ejemplos de Azure PowerShell: Creación de un conjunto de escalado de máquinas virtuales completo | Microsoft Docs'
description: Ejemplos de Azure PowerShell
services: virtual-machine-scale-sets
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machine-scale-sets
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/29/2018
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 22de937c33edc7c8ec6944acf657937a1ce604f7
ms.sourcegitcommit: 943af92555ba640288464c11d84e01da948db5c0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2019
ms.locfileid: "55981901"
---
# <a name="create-a-complete-virtual-machine-scale-set-with-powershell"></a>Creación de un conjunto de escalado de máquinas virtuales completo con PowerShell

Este script crea un conjunto de escalado de máquinas virtuales que ejecutan Windows Server 2016. Se configuran y crean recursos individuales, en lugar de usar las [opciones integradas de creación de recursos disponibles aquí en New-AzVmss](powershell-sample-create-simple-scale-set.md). Después de ejecutar el script, puede acceder a las instancias de máquina virtual mediante RDP.


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [updated-for-az-vm.md](../../../includes/updated-for-az-vm.md)]

## <a name="sample-script"></a>Script de ejemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine-scale-sets/complete-scale-set/complete-scale-set.ps1 "Create a complete virtual machine scale set")]

## <a name="clean-up-deployment"></a>Limpieza de la implementación
Ejecute el siguiente comando para quitar el grupo de recursos, el conjunto de escalado y todos los recursos relacionados.

```powershell
Remove-AzResourceGroup -Name $resourceGroupName
```

## <a name="script-explanation"></a>Explicación del script
Este script usa los siguientes comandos para crear la implementación. Cada elemento de la tabla incluye vínculos a la documentación específica del comando.

| Get-Help | Notas |
|---|---|
| [New-AzResourceGroup](/powershell/module/az.resources/new-azresourcegroup) | Crea un grupo de recursos en el que se almacenan todos los recursos. |
| [New-AzVirtualNetworkSubnetConfig](/powershell/module/az.network/new-azvirtualnetworksubnetconfig) | Crea una configuración de subred. Esta configuración se utiliza con el proceso de creación de la red virtual. |
| [New-AzVirtualNetwork](/powershell/module/az.network/new-azvirtualnetwork) | Crea una red virtual. |
| [New-AzPublicIpAddress](/powershell/module/az.network/new-azpublicipaddress) | Crea una dirección IP pública. |
| [New-AzLoadBalancerFrontendIpConfig](/powershell/module/az.network/new-azloadbalancerfrontendipconfig) | Crea una configuración de dirección IP de Front-End para un equilibrador de carga. |
| [New-AzLoadBalancerBackendAddressPoolConfig](/powershell/module/az.network/new-azloadbalancerbackendaddresspoolconfig) | Crea una configuración de grupo de direcciones de back-end para un equilibrador de carga. |
| [New-AzLoadBalancerInboundNatRuleConfig](/powershell/module/az.network/new-azloadbalancerinboundnatruleconfig) | Crea una configuración de regla NAT entrante para un equilibrador de carga. |
| [New-AzLoadBalancer](/powershell/module/az.network/new-azloadbalancer) | Crea un equilibrador de carga. |
| [Add-AzLoadBalancerProbeConfig](/powershell/module/az.network/new-azloadbalancerprobeconfig) | Crea una configuración de sondeo para un equilibrador de carga. |
| [Add-AzLoadBalancerRuleConfig](/powershell/module/az.network/new-azloadbalancerruleconfig) | Crea una configuración de regla para un equilibrador de carga. |
| [Set-AzLoadBalancer](/powershell/module/az.Network/Set-azLoadBalancer) | Actualice el equilibrador de carga con la información que se proporciona. |
| [New-AzVmssIpConfig](/powershell/module/az.Compute/New-azVmssIpConfig) | Cree una configuración de IP para las instancias de máquina virtual del conjunto de escalado. Las instancias de máquina virtual están conectadas al grupo de back-end del equilibrador de carga, a un grupo de NAT y a una subred de la red virtual. |
| [New-AzVmssConfig](/powershell/module/az.Compute/New-azVmssConfig) | Crea una configuración del conjunto de escalado. Dicha configuración incluye información como el número de instancias de máquina virtual que se crean, la SKU de la máquina virtual (tamaño) y el modo de la directiva de actualización. La configuración se agrega a los cmdlets adicionales y se usa durante la creación del conjunto de escalado. |
| [Set-AzVmssStorageProfile](/powershell/module/az.Compute/Set-azVmssStorageProfile) | Defina la imagen que se va a utilizar para las instancias de máquina virtual y agréguela a la configuración del conjunto de escalado. |
| [Set-AzVmssOsProfile](/powershell/module/az.Compute/Set-azVmssStorageProfile) | Defina las credenciales del nombre de usuario y la contraseña de administración, así como el prefijo de asignación de nombres de máquina virtual. Agregue estos valores a la configuración del conjunto de escalado. |
| [Add-AzVmssNetworkInterfaceConfiguration](/powershell/module/az.Compute/Add-azVmssNetworkInterfaceConfiguration) | Agregue una interfaz de red virtual a las instancias de máquina virtual, en función de la configuración de la IP. Agregue estos valores a la configuración del conjunto de escalado. |
| [New-AzVmss](/powershell/module/az.Compute/New-azVmss) | Cree el conjunto de escalado en función de la información proporcionada en la configuración del conjunto de escalado. |
| [Remove-AzResourceGroup](/powershell/module/az.resources/remove-azresourcegroup) | Quita un grupo de recursos y todos los recursos incluidos en él. |

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).

Se pueden encontrar otros ejemplos de scripts de PowerShell de conjunto de escalado de máquinas virtuales en la [documentación del conjunto de escalado de máquinas virtuales de Azure](../powershell-samples.md).
