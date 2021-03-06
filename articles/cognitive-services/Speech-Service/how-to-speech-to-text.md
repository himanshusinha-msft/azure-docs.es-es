---
title: Uso de Conversión de voz en texto | Microsoft Docs
description: Obtenga información sobre cómo usar Conversión de voz en texto en el servicio Voz.
titleSuffix: Microsoft Cognitive Services
services: cognitive-services
author: v-jerkin
manager: noellelacharite
ms.service: cognitive-services
ms.component: speech-service
ms.topic: article
ms.date: 07/16/2018
ms.author: v-jerkin
ms.openlocfilehash: 26cecedfc3ad2d472b9686e25054fe08253cee77
ms.sourcegitcommit: 0b05bdeb22a06c91823bd1933ac65b2e0c2d6553
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39068529"
---
# <a name="use-speech-to-text-in-the-speech-service"></a>Uso de "Conversión de voz en texto" en el servicio Voz

Puede usar **Conversión de voz en texto** en las aplicaciones de dos maneras diferentes.

| Método | DESCRIPCIÓN |
|-|-|
| [SDK](speech-sdk.md) | El método más sencillo para los desarrolladores de C, C++, C# y Java |
| [REST](rest-apis.md) | Reconocer expresiones cortas mediante una solicitud POST de HTTP | 

## <a name="using-the-sdk"></a>Uso del SDK

El [SDK de Voz](speech-sdk.md) proporciona la manera más sencilla de usar **Conversión de voz en texto** en la aplicación con una funcionalidad completa.

1. Cree un generador de voz y proporcione una clave de suscripción al servicio Voz y una [región](regions.md) o un token de autorización. En este momento, también puede configurar opciones, como el idioma de reconocimiento o un punto de conexión personalizado para modelos de reconocimiento de voz propios.

2. Obtenga un reconocedor del generador. Existen tres tipos diferentes de reconocedores. Cada tipo de reconocedor puede usar el micrófono predeterminado del dispositivo, una secuencia de audio o audio de un archivo.

    Reconocedor | Función
    -|-
    Reconocedor de voz|Proporciona la transcripción textual de la voz.
    Reconocedor de intenciones|Deriva la intención del hablante a través de [LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/) después del reconocimiento\*.
    Reconocedor de traducción|Traduce el texto transcrito a otro idioma (vea [Traducción de voz](how-to-translate-speech.md)).

    \* *Para el reconocimiento de la intención, debe usar una clave de suscripción de LUIS independiente al crear un generador de voz para el reconocimiento de la intención.*
    
4. Si quiere, asocie los eventos para la operación asincrónica. Después, el reconocedor llama a los controladores de eventos cuando tiene resultados provisionales y finales. En caso contrario, la aplicación recibirá un resultado de transcripción final.

5. Inicie el reconocimiento.
   Para el reconocimiento de una toma, como el reconocimiento de comandos o consultas, utilice `RecognizeAsync()`, que devuelve la primera expresión que se está reconociendo.
   Para el reconocimiento a largo plazo, como la transcripción, utilice `StartContinuousRecognitionAsync()` y asocie los eventos de resultados de reconocimiento asincrónica.

### <a name="sdk-samples"></a>Ejemplos del SDK

Para obtener el conjunto más reciente de ejemplos, consulte el [repositorio de GitHub de ejemplos del SDK de Voz de Cognitive Services](https://aka.ms/csspeech/samples).

## <a name="using-the-rest-api"></a>Uso de la API de REST

La API REST es la manera más sencilla de reconocer la voz si no se usa un idioma admitido por el SDK. Se realiza una solicitud POST de HTTP al punto de conexión de servicio, y se pasa la expresión completa en el cuerpo de la solicitud. Se recibe una respuesta que contiene el texto reconocido.

> [!NOTE]
> Cuando se usa la API REST, las expresiones se limitan a 15 segundos o menos.

Para obtener más información sobre la API REST de **Conversión de voz en texto**, vea [API REST](rest-apis.md#speech-to-text). Para verla en acción, descargue los [ejemplos de API REST](https://github.com/Azure-Samples/SpeechToText-REST) desde GitHub.

## <a name="next-steps"></a>Pasos siguientes

- [Obtenga su suscripción de prueba a Voz](https://azure.microsoft.com/try/cognitive-services/)
- [How to recognize speech in C++](quickstart-cpp-windows.md) (Reconocimiento de voz en C++)
- [How to recognize speech in C#](quickstart-csharp-dotnet-windows.md) (Reconocimiento de voz en C#)
- [How to recognize speech in Java](quickstart-java-android.md) (Reconocimiento de voz en Java)
