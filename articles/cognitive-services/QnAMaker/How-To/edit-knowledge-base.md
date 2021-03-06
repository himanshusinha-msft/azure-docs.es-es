---
title: 'Edición de una base de conocimiento: QnA Maker'
titleSuffix: Azure Cognitive Services
description: QnA Maker le permite administrar el contenido de la base de conocimiento, proporcionando una experiencia de edición sencilla.
services: cognitive-services
author: tulasim88
manager: nitinme
ms.service: cognitive-services
ms.subservice: qna-maker
ms.topic: article
ms.date: 03/04/2019
ms.author: tulasim
ms.custom: seodec18
ms.openlocfilehash: ade6737d2df37d35eefd0be77895a54e1cea433d
ms.sourcegitcommit: 3f4ffc7477cff56a078c9640043836768f212a06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/04/2019
ms.locfileid: "57314881"
---
# <a name="edit-a-knowledge-base-in-qna-maker"></a>Edición de una base de conocimiento en QnA Maker

QnA Maker le permite administrar el contenido de la base de conocimiento, proporcionando una experiencia de edición sencilla.

## <a name="edit-your-knowledge-base-content"></a>Edición del contenido de una base de conocimiento

1.  Seleccione **Mis bases de conocimiento** en la barra de navegación superior. 

    Puede observar que todos los servicios creados o compartidos con usted aparecen ordenados de forma descendente en función de la fecha de la **última modificación**.

    ![Mis bases de conocimiento](../media/qnamaker-how-to-edit-kb/my-kbs.png)

1. Seleccione una base de conocimiento determinada para editarla.
 
1. Seleccione **Configuración**. Aquí puede editar el campo obligatorio Nombre de servicio.
  
    |Objetivo|.|
    |--|--|
    |Agregar dirección URL|Puede agregar nuevas direcciones URL para agregar nuevo contenido de preguntas frecuentes a la base de conocimiento si hace clic en **Manage knowledge base -> + Add URL** (Administrar base de conocimiento > Agregar dirección URL).|
    |Eliminar dirección URL|Puede eliminar las direcciones URL existentes si selecciona el icono de eliminación (la papelera).|
    |Actualizar el contenido de la dirección URL|Si quiere que la base de conocimiento rastree el contenido más reciente de las direcciones URL existentes, active la casilla **Refresh** (Actualizar). Con esta acción se actualiza la base de conocimiento con el contenido de la dirección URL más reciente.|
    |Agregar archivo|Puede agregar un documento de archivo admitido como parte de una base de conocimiento; para ello, seleccione **Manage knowledge base** (Administrar base de conocimiento) y, luego, seleccione **+ Add File** (+ Agregar archivo).|
    |Importar|También puede importar cualquier base de conocimiento existente si selecciona el botón **Import Knowledge Base** (Importar base de conocimiento). |
    |Actualizar|La actualización de la base de conocimiento depende del **plan de tarifa de administración** que se va a usar al crear el servicio de QnA Maker asociado con su base de conocimiento. También puede actualizar el nivel de administración de Azure Portal, si es necesario.

1. Una vez realizados los cambios en la base de conocimiento, haga clic en **Save and train** (Guardar y entrenar) en la esquina superior derecha de la página para almacenar los cambios.    

    ![Guardar y entrenar](../media/qnamaker-how-to-edit-kb/save-and-train.png)

    >[!CAUTION]
    >Si abandona la página antes de seleccionar **Save and train** (Guardar y entrenar), todos los cambios se perderán.

## <a name="add-a-qna-pair"></a>Adición de un par de QnA

Seleccione **Adición de un par de QnA** para agregar una fila nueva a la tabla de la base de conocimiento.

![Adición de un par de QnA](../media/qnamaker-how-to-edit-kb/add-qnapair.png)

## <a name="delete-a-qna-pair"></a>Eliminación de un par de QnA

Para eliminar un QnA, haga clic en el icono **eliminar** en el extremo derecho de la fila QnA. Esta es una operación permanente. No se puede deshacer. Considere la posibilidad de exportar la base de conocimiento desde la página **Publish** (Publicar) antes de eliminar los pares. 

![Eliminación de un par de QnA](../media/qnamaker-how-to-edit-kb/delete-qnapair.png)

## <a name="add-alternate-questions"></a>Agregar preguntas alternativas

Agregue preguntas alternativas a un par de QnA existente para mejorar la probabilidad de encontrar una coincidencia para una consulta de usuario.

![Agregar preguntas alternativas](../media/qnamaker-how-to-edit-kb/add-alternate-question.png)

## <a name="add-metadata"></a>Agregar metadatos


Agregue los pares de metadatos seleccionando el icono de metadatos. Un par de metadatos consta de una clave y un valor.

![Agregar metadatos](../media/qnamaker-how-to-edit-kb/add-metadata.png)

> [!TIP]
> Asegúrese de hacer clic periódicamente en Guardar y entrenar en la base de conocimiento después de realizar las ediciones, a fin de evitar perder los cambios.

## <a name="manage-large-knowledge-bases"></a>Administración de bases de conocimiento grandes

* **Grupos de origen de datos**: Los pares de QnA se agrupan según el origen de datos del que se han extraído. Puede expandir o contraer el origen de datos.

    ![Uso de la barra de origen de datos de QnA Maker para contraer y expandir preguntas y respuestas acerca del origen de datos](../media/qnamaker-how-to-edit-kb/data-source-grouping.png)

* **Buscar en Knowledge Base**: Puede buscar en la base de conocimiento si escribe en el cuadro de texto en la parte superior de la tabla de Knowledge Base. Haga clic en Entrar para buscar en el contenido de la pregunta, la respuesta o los metadatos. Haga clic en el icono X para quitar el filtro de búsqueda.

    ![Use el cuadro de búsqueda de QnA Maker situado encima de las preguntas y respuestas para reducir la vista a solo elementos que coincidan con el filtro](../media/qnamaker-how-to-edit-kb/search-paginate-group.png)

* **Paginación**: Muévase rápidamente a través de los orígenes de datos para administrar bases de conocimiento de gran tamaño.

    ![Uso de las características de paginación de QnA Maker situadas encima de las preguntas y respuestas para desplazarse por las páginas de preguntas y respuestas](../media/qnamaker-how-to-edit-kb/pagination.png)

## <a name="delete-knowledge-bases"></a>Eliminación de bases de conocimiento

La eliminación de una base de conocimiento (KB) es una operación permanente. No se puede deshacer. Antes de eliminar una base de conocimiento, debe exportarla desde la página **Configuración** del portal de QnA Maker. 

Si comparte la KB con [colaboradores](collaborate-knowledge-base.md) y, a continuación, la elimina, todos perderán el acceso a la KB. 

## <a name="delete-azure-resources"></a>Eliminación de recursos de Azure 

Si elimina cualquiera de los recursos de Azure usados para las bases de conocimiento de QnA Maker, estas dejarán de funcionar. Antes de eliminar todos los recursos, asegúrese de exportar las bases de conocimiento desde la página **Settings** (Configuración). 

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Colaborar en una base de conocimiento](./collaborate-knowledge-base.md)
