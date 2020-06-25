---
title: Implementar proveedores de datos para integrar datos de terceros en Adobe Target
seo-title: Implementar proveedores de datos para integrar datos de terceros en Adobe Target
description: Detalles de implementación y ejemplos de cómo utilizar la función Proveedores de datos de Adobe Target para recuperar datos de proveedores de datos de terceros y pasarlos en la solicitud de Destinatario.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Implementar proveedores [!UICONTROL de datos] para integrar datos de terceros en Adobe Target

Implementation details and examples of how to use Adobe Target&#39;s [!UICONTROL Data Providers] feature to retrieve data from third-party data providers and pass it in the Target request.

>[!NOTE]
>
>[!UICONTROL Los proveedores] de datos requieren `at.js` 1.3 o superior

## Implementar los componentes básicos de los proveedores de datos

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Información general rápida sobre los componentes básicos de un `dataProvider` y cómo obtener el código en el orden correcto.\
Aquí puede encontrar un ejemplo práctico con el código utilizado en el vídeo:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integración con una API de terceros

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Un ejemplo más realista, la integración de una API meteorológica.\
Aquí puede encontrar un ejemplo práctico con el código utilizado en el vídeo:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integración con varios proveedores

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Cómo incorporar datos de varios proveedores a su [!DNL Target] solicitud global.\
Aquí puede encontrar un ejemplo práctico con el código utilizado en el vídeo:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimizar el impacto en la carga de la página

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Minimice el impacto en el tiempo de carga de la página almacenando datos en un objeto de almacenamiento de sesión. Como alternativa, puede pasar los valores como parámetros de perfil utilizando el `profile.` prefijo y pasarlos simplemente en la primera [!DNL Target] solicitud de la sesión. Sin embargo, estaría limitado a pasar cincuenta parámetros de perfil por solicitud.

Aquí puede encontrar un ejemplo práctico con el código utilizado en el vídeo: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiales de apoyo

* [Usar proveedores de datos con Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [Documentación de proveedores de datos](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)