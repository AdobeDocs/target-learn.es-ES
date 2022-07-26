---
title: Implementación de proveedores de datos para integrar datos de terceros
description: Este tutorial proporciona detalles de implementación y ejemplos de cómo utilizar la función Proveedores de datos de Adobe Target para recuperar datos de proveedores de datos de terceros y pasarlos en la solicitud de Target.
role: Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: fcf6d1a8-e2a7-41ce-9c1c-02985b7afb5a
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Implemente [!UICONTROL Proveedores de datos] para integrar datos de terceros en Adobe Target

Detalles de implementación y ejemplos de cómo utilizar la función [!UICONTROL Data Providers] de Adobe Target para recuperar datos de proveedores de datos de terceros y pasarlos en la solicitud de Target.

>[!NOTE]
>
>[!UICONTROL Proveedores ] de datos requiere  `at.js` 1.3 o superior

## Implementación de los componentes básicos de los proveedores de datos

>[!VIDEO](https://video.tv.adobe.com/v/22348/?quality=12)

Una visión general rápida de los componentes básicos de un `dataProvider` y cómo obtener el código en el orden correcto.\
Aquí puede encontrar un ejemplo práctico con el código utilizado en el vídeo:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integración con una API de terceros

>[!VIDEO](https://video.tv.adobe.com/v/22345/)

Un ejemplo más realista, la integración de una API meteorológica.\
Aquí puede encontrar un ejemplo práctico con el código utilizado en el vídeo:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integración con varios proveedores

>[!VIDEO](https://video.tv.adobe.com/v/22346/)

Cómo incorporar datos de varios proveedores a su solicitud global [!DNL Target].\
Aquí puede encontrar un ejemplo práctico con el código utilizado en el vídeo:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimizar el impacto en la carga de la página

>[!VIDEO](https://video.tv.adobe.com/v/22347/)

Minimice el impacto en el tiempo de carga de la página almacenando datos en un objeto de almacenamiento de sesión. Como alternativa, puede pasar los valores como parámetros de perfil utilizando el prefijo `profile.` y pasarlos en la primera solicitud [!DNL Target] de la sesión. Sin embargo, se limitaría a pasar cincuenta parámetros de perfil por solicitud.

Aquí puede encontrar un ejemplo práctico con el código utilizado en el vídeo: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiales de apoyo

* [Uso de proveedores de datos con Adobe Target](use-data-providers-to-integrate-third-party-data.md)

* [Documentación de proveedores de datos](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en#data-providers)
