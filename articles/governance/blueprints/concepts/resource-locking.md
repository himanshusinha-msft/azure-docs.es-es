---
title: Bloqueo de recursos
description: Obtenga más información sobre las opciones de bloqueo para proteger los recursos cuando asigne un plano técnico.
services: blueprints
author: DCtheGeek
ms.author: dacoulte
ms.date: 01/23/2019
ms.topic: conceptual
ms.service: blueprints
manager: carmonm
ms.custom: seodec18
ms.openlocfilehash: 799e496fd9dd8a405e5fc356e13cf6c05883e1ae
ms.sourcegitcommit: 5839af386c5a2ad46aaaeb90a13065ef94e61e74
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/19/2019
ms.locfileid: "57855419"
---
# <a name="understand-resource-locking-in-azure-blueprints"></a>Comprensión del bloqueo de recursos en planos técnicos de Azure Blueprint

La creación de entornos coherentes a escala solo es realmente valiosa si existe un mecanismo que mantenga la coherencia. En este artículo se explica cómo funciona el bloqueo de recursos en planos técnicos de Azure Blueprint. Para ver un ejemplo de bloqueo de recursos y las aplicaciones de _denegar asignaciones_, consulte el [protección de recursos nuevo](../tutorials/protect-new-resources.md) tutorial.

## <a name="locking-modes-and-states"></a>Estados y modos de bloqueos

El modo de bloqueo se aplica a la asignación de planos técnicos y tiene tres opciones: **No bloquear**, **Solo lectura** o **No eliminar**. El modo de bloqueo se configura durante la implementación del artefacto durante una asignación de plano técnico. Se puede establecer otro modo de bloqueo mediante la actualización de la asignación de plano técnico.
Sin embargo, los modos de bloqueo no se pueden cambiar fuera de los planos técnicos.

Los recursos creados por los artefactos en una asignación de plano técnico tienen cuatro estados: **Sin bloquear**, **Solo lectura**, **No se puede editar o eliminar** o **No se puede eliminar**. Cada tipo de artefacto pueden tener el estado **Sin bloquear**. La tabla siguiente puede usarse para determinar el estado de un recurso:

|Mode|Tipo de recurso de artefacto|Estado|DESCRIPCIÓN|
|-|-|-|-|
|No bloquear|*|Sin bloquear|Los recursos no están protegidos por planos técnicos. Este estado también se usa para los recursos que se agregan a un artefacto del grupo de recursos de **Solo lectura** o **No eliminar** a partir de fuera de una asignación de plano técnico.|
|Solo lectura|Grupos de recursos|No se puede editar o eliminar|El grupo de recursos es de solo lectura, y no se pueden modificar las etiquetas en el grupo de recursos. Los recursos **Sin bloquear** se pueden agregar, mover, cambiar o elimina de este grupo de recursos.|
|Solo lectura|Grupo que no son de recursos|Solo lectura|El recurso no se puede modificar de ninguna manera, no se puede cambiar ni eliminar.|
|No eliminar|*|No se puede eliminar|Los recursos se pueden modificar, pero no se pueden eliminar. Los recursos **Sin bloquear** se pueden agregar, mover, cambiar o elimina de este grupo de recursos.|

## <a name="overriding-locking-states"></a>Sustitución de los estados de bloqueo

Es típico que alguien con el[control de acceso basado en roles](../../../role-based-access-control/overview.md) (RBAC) adecuado en la suscripción, como el rol "Propietario", pueda modificar o eliminar cualquier recurso. Este acceso no es el caso cuando se aplican planos de bloqueo como parte de una asignación implementada. Si la asignación se estableció con la opción **Solo lectura** o **No eliminar**, ni siquiera el propietario de la suscripción puede realizar la acción bloqueada en el recurso protegido.

Esta medida de seguridad protege la coherencia del plano técnico definido y el entorno en el que se ha diseñado para crear a partir de una eliminación o modificación accidental o mediante programación.

## <a name="removing-locking-states"></a>Eliminación de los estados de bloqueo

Si es necesario modificar o eliminar un recurso protegido por una asignación, hay dos maneras de hacerlo.

- Actualizar la asignación de plano técnico a un modo de bloqueo de **No bloquear**
- Eliminar la asignación de plano técnico

Cuando se quita la asignación, se quitan los bloqueos creados por los planos técnicos. Sin embargo, el recurso se queda atrás y deberá eliminarse por medios normales.

## <a name="how-blueprint-locks-work"></a>Cómo funcionan los bloqueos de los planos técnicos

Una acción denegación [denegar asignaciones](../../../role-based-access-control/deny-assignments.md) de RBAC se aplica a los recursos de artefactos durante la asignación de un plano técnico si la asignación ha seleccionado la opción **Solo lectura** o **No eliminar**. La identidad administrada de la asignación del plano técnico agrega la acción de denegación, y solo la misma identidad administrada puede eliminar los recursos del artefacto. Esta medida de seguridad refuerza el mecanismo de bloqueo y evita que se quite el bloqueo del plano técnico fuera de Blueprint.

> [!IMPORTANT]
> Azure Resource Manager almacena en caché los detalles de asignación de roles durante un máximo de 30 minutos. Como resultado, la acción de denegación denegar asignaciones puede que no funcione completamente en los recursos de plano técnico. Durante este período de tiempo es posible eliminar un recurso diseñado para estar protegido por bloqueos de plano técnico.

## <a name="next-steps"></a>Pasos siguientes

- Siga el [proteger nuevos recursos](../tutorials/protect-new-resources.md) tutorial.
- Obtenga información sobre la [ciclo de vida del plano](lifecycle.md).
- Descubra cómo utilizar [parámetros estáticos y dinámicos](parameters.md).
- Aprenda a personalizar la [blueprint orden secuenciación](sequencing-order.md).
- Obtenga información sobre cómo [actualizar las asignaciones existentes](../how-to/update-existing-assignments.md).
- Solución de problemas durante la asignación de una instancia de blueprint con [solución de problemas generales](../troubleshoot/general.md).