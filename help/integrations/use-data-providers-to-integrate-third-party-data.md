---
title: Cómo usar proveedores de datos para integrar datos de terceros
description: Este tutorial presenta a los usuarios los proveedores de datos. Aprenda a utilizar la capacidad de proveedores de datos para pasar fácilmente datos de terceros a Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 23%

---

# Utilice Data Providers para integrar datos de terceros en Adobe Target

[!UICONTROL Proveedores de datos es una funcionalidad que permite pasar fácilmente datos de terceros a Target.  ]  Un tercero podría ser un servicio de pronóstico del clima, un DMP o incluso su propio servicio web. Puede usar estos datos para crear audiencias, dirigir contenido y enriquecer el perfil del visitante.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Cómo utilizar los proveedores de datos

1. El experto en implementación agrega código antes de at.js (o en la sección Encabezado de biblioteca de at.js) que realiza la llamada de API a terceros, analiza la respuesta y especifica con pares de nombre/valor de la respuesta que se enviará a [!DNL Target].
1. at.js administra el parpadeo e incluye los pares nombre/valor como parámetros personalizados en la solicitud global de Target.
1. El especialista en marketing crea audiencias en la interfaz [!DNL Target] en función de estos parámetros personalizados.
1. El especialista en marketing utiliza estas audiencias para segmentar experiencias, actividades y métricas, así como para crear informes de audiencias.

>[!NOTE]
>
>[!UICONTROL Proveedores ] de datos requiere at.js 1.3 o superior

## Materiales de apoyo

* [Implementación de proveedores de datos en at.js y Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
* [Documentación de proveedores de datos](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=en#data-providers)
