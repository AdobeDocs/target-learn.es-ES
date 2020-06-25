---
title: Comprender cómo funciona el Adobe Target at.js 2.0
seo-title: Comprender cómo funciona el Adobe Target at.js 2.0
description: at.js 2.0 mejora la compatibilidad del Adobe Target con aplicaciones de una sola página (SPA) y se integra con otras soluciones de Experience Cloud. Este vídeo y los diagramas que lo acompañan explican cómo todo se une.
audience: developer
difficulty: 3
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: 37443ae4c1cdda387c8db0053201d520fa1ec224
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 20%

---


# Comprender cómo funciona el Adobe Target at.js 2.0

`at.js` 2.0 mejora la compatibilidad del Adobe Target con aplicaciones de una sola página (SPA) y se integra con otras soluciones de Experience Cloud. Este vídeo y los diagramas que lo acompañan explican cómo todo se une.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagramas de arquitectura

![Comportamiento de at.js 2.0 al cargar la página](assets/pageload.png)

1. La llamada devuelve un ID de Experience Cloud (ECID). Si el usuario está autenticado, otra llamada sincroniza el ID de cliente.

1. `at.js` la biblioteca se carga sincrónicamente y oculta el cuerpo del documento (`at.js` también se puede cargar asincrónicamente con un fragmento de ocultación previa opcional implementado en la página).

1. La solicitud de carga de página se realiza incluyendo todos los parámetros configurados, ECID, SDID e ID de cliente.

1. Profile scripts execute and feed into the [!UICONTROL Profile Store]. The Store requests qualified audiences from the [!UICONTROL Audience Library] (e.g. audiences shared from [!DNL Analytics], Audience Manager, etc). [!UICONTROL Los atributos] del cliente se envían al almacén [!UICONTROL de] Perfiles en un proceso por lotes.
1. Based on URL, request parameters, and profile data, [!DNL Target] decides which Activities and Experiences to return to the visitor for the current page and future views

1. Contenido de destino devuelto a la página, incluyendo opcionalmente valores de perfil para una personalización adicional.

   El contenido dirigido se muestra en la página actual lo más rápido posible y sin parpadeo del contenido predeterminado.

   El contenido de destino para futuras vistas de una aplicación de una sola página se almacena en caché en el navegador, por lo que se puede aplicar instantáneamente sin necesidad de realizar una llamada al servidor adicional cuando se activan las vistas. (Consulte el siguiente diagrama para ver el `triggerView()` comportamiento).

1. [!DNL Analytics] datos enviados desde la página a los servidores de recopilación [!UICONTROL de] datos
1. [!DNL Target]Se comparan los datos de con los datos de mediante el SDID y se procesan en el almacén de informes de Analytics. [!DNL Analytics] [!DNL Analytics] los datos se pueden ver en los informes [!DNL Analytics] y [!DNL Target] a través de A4T.

![Comportamiento de at.js 2.0 cuando se utiliza la función desencadenadorView()](assets/triggerview.png)

1. `adobe.target.triggerView()` se llama en la aplicación de una sola página
1. El contenido dirigido para la vista se lee desde la caché

1. El contenido dirigido se muestra lo más rápido posible y sin parpadeo del contenido predeterminado

1. La solicitud de notificación se envía al Almacenamiento de perfiles de [!DNL Target] para contar al visitante en la actividad e incrementar las métricas
1. [!DNL Analytics] los datos se envían desde el SPA a los servidores de recopilación [!UICONTROL de] datos

1. [!DNL Target] los datos se envían desde el [!DNL Target] servidor a los servidores de recopilación [!UICONTROL de] datos. Se comparan los datos de [!DNL Target] con los datos de [!DNL Analytics] mediante el SDID y se procesan en el almacén de informes de [!DNL Analytics]. [!DNL Analytics] los datos se pueden ver en los informes [!DNL Analytics] y [!DNL Target] a través de A4T.

## Recursos adicionales

* [Implementar at.js 2.0 en una aplicación de una sola página](implement-atjs-20-in-a-single-page-application.md)
* [Usar el Compositor de experiencias visuales de Adobe Target para aplicaciones de una sola página (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Cómo funciona la documentación de at.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/at-js/how-atjs-works.html)