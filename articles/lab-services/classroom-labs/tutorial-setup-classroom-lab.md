---
title: Configuración de un laboratorio con Azure Lab Services | Microsoft Docs
description: En este tutorial, va a configurar un laboratorio para usarlo en una clase.
services: devtest-lab, lab-services, virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 02/07/2019
ms.author: spelluru
ms.openlocfilehash: 4abec80df4aeeb4c20d56b43ba122ee7266905a6
ms.sourcegitcommit: a4efc1d7fc4793bbff43b30ebb4275cd5c8fec77
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/21/2019
ms.locfileid: "56649601"
---
# <a name="tutorial-set-up-a-classroom-lab"></a>Tutorial: Configuración de un laboratorio educativo 
En este tutorial, se va a configurar un laboratorio de clase con las máquinas virtuales que van a utilizar los estudiantes de la clase.  

En este tutorial realizará lo siguiente:

> [!div class="checklist"]
> * Creación de un laboratorio educativo
> * Incorporación de usuarios al laboratorio
> * Envío del vínculo de registro a los estudiantes

## <a name="prerequisites"></a>Requisitos previos
Para configurar un laboratorio educativo en una cuenta de laboratorio, debe ser miembro de alguno de estos roles en la cuenta de laboratorio: Propietario, Creador de laboratorio o Colaborador. La cuenta que usó para crear una cuenta de laboratorio se agrega automáticamente al rol de propietario.

El propietario de un laboratorio puede agregar a otros usuarios al rol **Creador de laboratorio**. Por ejemplo, un propietario de laboratorio agrega profesores al rol Creador de laboratorio. A continuación, los profesores pueden crear laboratorios con máquinas virtuales para sus clases. Los estudiantes pueden usar el vínculo de registro que reciban de los profesores para registrar el laboratorio. Una vez registrados, pueden usar las máquinas virtuales de los laboratorios para hacer las tareas de clase y de casa. Para obtener instrucciones detalladas sobre cómo agregar usuarios al rol Creador de laboratorio, consulte [Incorporación de un usuario al rol Creador de laboratorio](tutorial-setup-lab-account.md#add-a-user-to-the-lab-creator-role).


## <a name="create-a-classroom-lab"></a>Creación de un laboratorio educativo

1. Vaya al [sitio web de Azure Lab Services](https://labs.azure.com). 
2. Seleccione **Iniciar sesión** y escriba las credenciales. Azure Lab Services es compatible con cuentas profesionales y cuentas Microsoft. 
3. En la ventana **Nuevo laboratorio**, lleve a cabo las siguientes acciones: 
    1. Especifique un **nombre** para el laboratorio. 
    2. Especifique el máximo **número de máquinas virtuales** del laboratorio. Puede aumentar o reducir el número de máquinas virtuales después de crear el laboratorio o en un laboratorio existente. Para más información, consulte [Actualización del número de máquinas virtuales en un laboratorio](how-to-configure-student-usage.md#update-number-of-virtual-machines-in-lab).
    6. Seleccione **Guardar**.

        ![Creación de un laboratorio educativo](../media/tutorial-setup-classroom-lab/new-lab-window.png)
4. En la página **Seleccionar especificaciones de máquina virtual**, realice los pasos siguientes:
    1. Seleccione un **tamaño** para las máquinas virtuales (VM) creadas en el laboratorio. 
    3. Seleccione la **imagen de máquina virtual** que se usará para crear máquinas virtuales en el laboratorio. 
    4. Seleccione **Next** (Siguiente).

        ![Especificaciones de máquina virtual](../media/tutorial-setup-classroom-lab/select-vm-specifications.png)    
5. En la página **Establecer credenciales**, especifique las credenciales predeterminadas de todas las máquinas virtuales del laboratorio. 
    1. Especifique el **nombre del usuario** para todas las máquinas virtuales del laboratorio.
    2. Especifique la **contraseña** del usuario. 

        > [!IMPORTANT]
        > Tome nota de ambos. No se volverán a mostrar.
    3. Seleccione **Crear**. 

        ![Establecer credenciales](../media/tutorial-setup-classroom-lab/set-credentials.png)
6. En la página **Configurar plantilla**, puede ver el estado del proceso de creación del laboratorio. La creación de la plantilla en el laboratorio tarda un máximo de 20 minutos. 

    ![Configurar plantilla](../media/tutorial-setup-classroom-lab/configure-template.png)
7. Una vez completada la configuración de la plantilla, verá la siguiente página: 

    ![Página Configurar plantilla una vez terminada](../media/tutorial-setup-classroom-lab/configure-template-after-complete.png)
8. En la página **Configurar plantilla**, siga estos pasos: Estos pasos son **opcionales** para el tutorial.
    2. Seleccione **Conectar** para conectarse a la plantilla de máquina virtual. 
    3. Instale y configure el software en la plantilla de máquina virtual.     
    5. Escriba una **descripción** para la plantilla.
9. Seleccione **Siguiente** en la página de plantilla. 
10. En la página **Publicar la plantilla**, realice las acciones siguientes. 
    1. Para publicar inmediatamente la plantilla, seleccione **Publicar**.  

        > [!WARNING]
        > Una vez que publique, no se puede cancelar la publicación. 
    2. Para publicar más adelante, seleccione **Guardar para más adelante**. Puede publicar la plantilla de máquina virtual una vez finalizado el asistente. Para más información sobre cómo configurar y publicar una vez finalizado el asistente, consulte la sección [Publicación de la plantilla](how-to-create-manage-template.md#publish-the-template-vm) del artículo [Administración de laboratorios educativos](how-to-manage-classroom-labs.md).

        ![Publicar plantilla](../media/tutorial-setup-classroom-lab/publish-template.png)
11. Puede ver el **progreso de la publicación** de la plantilla. Este proceso puede tardar hasta una hora. 

    ![Publicar plantilla: progreso](../media/tutorial-setup-classroom-lab/publish-template-progress.png)
12. Podrá ver la página siguiente cuando la plantilla se haya publicado correctamente. Seleccione **Listo**.

    ![Publicar plantilla: correctamente](../media/tutorial-setup-classroom-lab/publish-success.png)
1. Verá el **panel** del laboratorio. 
    
    ![Panel del laboratorio de clase](../media/tutorial-setup-classroom-lab/classroom-lab-home-page.png)
4. Cambie a la página **Máquinas virtuales**, para lo que debe seleccionar Máquinas virtuales en el menú izquierdo o icono de las máquinas virtuales. Confirme que ve las máquinas virtuales que están en el estado **Sin asignar**. Estas máquinas virtuales no están asignadas a los alumnos todavía. Deberían estar en estado **Detenida**. En esta pagina, puede iniciar una máquina virtual de un alumno, conectarse a la máquina virtual, detener la máquina virtual y eliminar la máquina virtual. Puede iniciarlas en esta página o dejar que los alumnos inicien las máquinas virtuales. 

    ![Máquinas virtuales en estado detenido](../media/tutorial-setup-classroom-lab/virtual-machines-stopped.png)

## <a name="add-users-to-the-lab"></a>Incorporación de usuarios al laboratorio

1. En el menú izquierdo, seleccione **Users** (Usuarios). De forma predeterminada, está habilitada la opción **Restrict access** (Restringir acceso). Cuando esta opción está activada, los usuarios no se pueden registrar en el laboratorio aunque tengan el vínculo de registro si no aparecen en la lista de usuarios. Solo los usuarios de la lista pueden registrarse en el laboratorio mediante el vínculo de registro enviado. En este procedimiento, agregará usuarios a la lista. Como alternativa, puede desactivar **Restrict access** (Restringir acceso), que permite que los usuarios se registren en el laboratorio, siempre y cuando tengan el vínculo de registro. 
2. Seleccione **Add users** (Agregar usuarios) en la barra de herramientas. 

    ![Botón Agregar usuarios](../media/how-to-configure-student-usage/add-users-button.png)
1. En la página **Add users** (Agregar usuarios), escriba las direcciones de correo electrónico de los usuarios en líneas independientes, o bien en una sola línea separadas por punto y coma. 

    ![Incorporación de direcciones de correo electrónico de usuarios](../media/how-to-configure-student-usage/add-users-email-addresses.png)
4. Seleccione **Guardar**. Verá las direcciones de correo electrónico de los usuarios y sus estados (registrados o no) en la lista. 

    ![Lista de usuarios](../media/how-to-configure-student-usage/users-list-new.png)


## <a name="send-registration-link-to-students"></a>Envío del vínculo de registro a los estudiantes

1. Cambie a la vista **Users** (Usuarios) si aún no está en la página. 
2. Seleccione el icono **Get registration link** (Obtener vínculo de registro) en la barra de herramientas.
1. En el cuadro de diálogo **Registro de usuario**, seleccione el botón **Copiar**. El vínculo se copia en el Portapapeles.

    ![Vínculo de registro](../media/tutorial-setup-classroom-lab/registration-link.png)
1. En el cuadro de diálogo **Registro de usuario**, seleccione **Cerrar**. 
2. Comparta el vínculo de registro con un alumno para que este se pueda registrar para la clase.

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha creado un laboratorio de clase y ha configurado el laboratorio. Para saber cómo el estudiante puede acceder a una máquina virtual en el laboratorio con el enlace de registro, avance al siguiente tutorial:

> [!div class="nextstepaction"]
> [Conexión a una máquina virtual en el laboratorio de clase](tutorial-connect-virtual-machine-classroom-lab.md)

