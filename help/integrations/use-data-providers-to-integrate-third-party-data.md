---
title: Utilizar proveedores de datos para integrar datos de terceros en Adobe Target
seo-title: Utilizar proveedores de datos para integrar datos de terceros en Adobe Target
description: Proveedores de datos es una funcionalidad que permite pasar fácilmente datos de terceros a Target.  Un tercero podría ser un servicio de pronóstico del clima, un DMP o incluso su propio servicio web. Puede usar estos datos para crear audiencias, dirigir contenido y enriquecer el perfil del visitante.
audience: marketer
difficulty: 5
author: Daniel Wright
doc-type: use
activity-type: feature-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 40%

---


# Utilizar proveedores de datos para integrar datos de terceros en Adobe Target

[!UICONTROL Proveedores de datos es una funcionalidad que permite pasar fácilmente datos de terceros a Target.  ]  Un tercero podría ser un servicio de pronóstico del clima, un DMP o incluso su propio servicio web. Puede usar estos datos para crear audiencias, dirigir contenido y enriquecer el perfil del visitante.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Cómo utilizar los proveedores de datos

1. El experto en implementación agrega código antes de at.js (o en la sección Encabezado de biblioteca de at.js) que realiza la llamada de API a terceros, analiza la respuesta y especifica con pares nombre/valor de la respuesta a la que se va a enviar [!DNL Target].
1. at.js administra el parpadeo e incluye los pares nombre/valor como parámetros personalizados en la solicitud de Destinatario global.
1. Marketer crea audiencias en la [!DNL Target] interfaz basándose en estos parámetros personalizados.
1. Marketer utiliza estas audiencias para destinatario de experiencias, actividades y métricas, así como para audiencias de sistemas de informes.

>[!NOTE]
>
>[!UICONTROL Los proveedores] de datos requieren at.js 1.3 o superior

## Materiales de apoyo

* [Implementar proveedores de datos en at.js y Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
* [Documentación de proveedores de datos](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/targetgobalsettings.html#data-providers)