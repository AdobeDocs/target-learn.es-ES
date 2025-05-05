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
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Implemente [!UICONTROL Data Providers] para integrar datos de terceros en Adobe Target

Detalles de implementación y ejemplos de cómo usar la función [!UICONTROL Data Providers] de Adobe Target para recuperar datos de proveedores de datos de terceros y pasarlos en la solicitud de Target.

>[!NOTE]
>
>[!UICONTROL Data Providers] requiere `at.js` 1.3 o superior

## Implementar los componentes básicos de los proveedores de datos

>[!VIDEO](https://video.tv.adobe.com/v/34016/?quality=12&captions=spa)

Una breve descripción general de los componentes básicos de `dataProvider` y cómo obtener el código en el orden correcto.\
Puede encontrar un ejemplo práctico con el código utilizado en el vídeo aquí:
[https://target.enablementadobe.com/data-providers/simple.html](https://target.enablementadobe.com/data-providers/simple.html)

## Integración con una API de terceros

>[!VIDEO](https://video.tv.adobe.com/v/33687?captions=spa)

Un ejemplo más realista, al integrar una API meteorológica.\
Puede encontrar un ejemplo práctico con el código utilizado en el vídeo aquí:
[https://target.enablementadobe.com/data-providers/3rdparty.html](https://target.enablementadobe.com/data-providers/3rdparty.html)

## Integración con varios proveedores

>[!VIDEO](https://video.tv.adobe.com/v/36783?captions=spa)

Cómo incorporar datos de varios proveedores a su solicitud global de [!DNL Target].\
Puede encontrar un ejemplo práctico con el código utilizado en el vídeo aquí:
[https://target.enablementadobe.com/data-providers/combined.html](https://target.enablementadobe.com/data-providers/combined.html)

## Minimizar el impacto en la carga de página

>[!VIDEO](https://video.tv.adobe.com/v/36784?captions=spa)

Minimice el impacto en el tiempo de carga de la página almacenando datos en un objeto de almacenamiento de sesión. Como alternativa, puede pasar los valores como parámetros de perfil utilizando el prefijo `profile.` y simplemente pasarlos en la primera [!DNL Target] solicitud de la sesión. Sin embargo, se limitaría a pasar cincuenta parámetros de perfil por solicitud.

Aquí puede encontrar un ejemplo práctico con el código utilizado en el vídeo: [https://target.enablementadobe.com/data-providers/reducedCalls.html](https://target.enablementadobe.com/data-providers/reducedCalls.html)

## Materiales de apoyo

* [Usar proveedores de datos con Adobe Target](use-data-providers-to-integrate-third-party-data.md)
