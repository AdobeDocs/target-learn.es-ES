---
title: ¿Cómo funciona at.js 2.0?
description: Descubra cómo at.js 2.0 mejora la compatibilidad de Adobe Target con las aplicaciones de una sola página (SPA) y se integra con otras soluciones de Experience Cloud.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: fcd2273ba373dc2b3bc59a77f1925cdb7b2ed3ee
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Descubra cómo funciona at.js 2.0 de Adobe Target

`at.js` 2.0 mejora la compatibilidad de Adobe Target con las aplicaciones de una sola página (SPA) e integra otras soluciones de Experience Cloud. Este vídeo y los diagramas adjuntos explican cómo se vincula todo.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagramas de arquitectura

![comportamiento de at.js 2.0 al cargar la página](assets/pageload.png)

1. La llamada devuelve el ID de Experience Cloud (ECID). Si el usuario está autenticado, otra llamada sincroniza el ID de cliente.

1. `at.js` biblioteca se carga sincrónicamente y oculta el cuerpo del documento (`at.js` también se puede cargar asincrónicamente con un fragmento de ocultamiento previo opcional implementado en la página).

1. Se realiza una solicitud de carga de página que incluye todos los parámetros configurados, ECID, SDID y el ID de cliente.

1. Los scripts de perfil se ejecutan y se alimentan en [!UICONTROL Profile Store]. El Almacenamiento solicita audiencias de [!UICONTROL Audience Library] que cumplan los requisitos (por ejemplo, audiencias compartidas de [!DNL Analytics], Audience Manager, etc.). [!UICONTROL Customer Attributes] se han enviado a [!UICONTROL Profile Store] en un proceso por lotes.
1. Según la dirección URL, los parámetros de solicitud y los datos de perfil, [!DNL Target] decide qué actividades y experiencias vuelven al visitante para la página actual y las vistas futuras

1. Contenido dirigido devuelto a la página, incluyendo, de manera opcional, los valores de perfil para una personalización adicional.

   El contenido dirigido se muestra en la página actual lo más rápido posible y sin parpadeo del contenido predeterminado.

   El contenido dirigido para vistas futuras de una aplicación de una sola página se almacena en caché en el explorador, por lo que se puede aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas. (Consulte el siguiente diagrama para ver el comportamiento de `triggerView()`).

1. [!DNL Analytics] datos enviados desde la página a los servidores [!UICONTROL Data Collection]
1. Se compararon los datos de [!DNL Target] con los datos de Analytics mediante el SDID y se procesaron en el almacén de informes de [!DNL Analytics]. Los datos de [!DNL Analytics] se pueden ver en [!DNL Analytics] y [!DNL Target] mediante los informes de A4T.

Comportamiento de ![at.js 2.0 cuando se usa la función triggerView()](assets/triggerview.png)

1. Se llama a `adobe.target.triggerView()` en la aplicación de una sola página
1. El contenido dirigido para la vista se lee desde la caché

1. El contenido dirigido se muestra lo más rápido posible y sin parpadeo del contenido predeterminado

1. La solicitud de notificación se envía a [!DNL Target] [!UICONTROL Profile Store] para contar al visitante en la actividad e incrementar las métricas
1. Los datos de [!DNL Analytics] se envían desde la SPA a los servidores de [!UICONTROL Data Collection]

1. Se han enviado los datos de [!DNL Target] desde el servidor de [!DNL Target] a los servidores de [!UICONTROL Data Collection]. Se compararon los datos de [!DNL Target] con los datos de [!DNL Analytics] mediante el SDID y se procesaron en el almacén de informes de [!DNL Analytics]. Los datos de [!DNL Analytics] se pueden ver en [!DNL Analytics] y [!DNL Target] mediante los informes de A4T.

## Recursos adicionales

* [Implementar at.js 2.0 en una aplicación de una sola página](implement-atjs-20-in-a-single-page-application.md)
* [Uso del Compositor de experiencias visuales de Adobe Target para aplicaciones de una sola página (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
