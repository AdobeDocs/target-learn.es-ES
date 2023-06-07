---
title: ¿Cómo funciona at.js 2.0?
description: at.js 2.0 mejora la compatibilidad de Adobe Target SPA con aplicaciones de una sola página () e integra otras soluciones de Experience Cloud. Este vídeo y los diagramas adjuntos explican cómo se vincula todo.
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 7f037665-88a7-469c-8df5-c82cb0f65382
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 22%

---

# Funcionamiento de at.js 2.0 de Adobe Target

`at.js` 2.0 mejora la compatibilidad de Adobe Target SPA con aplicaciones de una sola página () e integra otras soluciones de Experience Cloud. Este vídeo y los diagramas adjuntos explican cómo se vincula todo.

>[!VIDEO](https://video.tv.adobe.com/v/26250?quality=12)

## Diagramas de arquitectura

![Comportamiento de at.js 2.0 al cargar la página](assets/pageload.png)

1. La llamada devuelve el ID del Experience Cloud (ECID). Si el usuario está autenticado, otra llamada sincroniza el ID de cliente.

1. `at.js` La biblioteca de se carga sincrónicamente y oculta el cuerpo del documento (`at.js` también se puede cargar de forma asíncrona con un fragmento de ocultamiento previo opcional implementado en la página).

1. Se realiza una solicitud de carga de página que incluye todos los parámetros configurados, ECID, SDID y el ID de cliente.

1. Los scripts de perfil se ejecutan y se alimentan de [!UICONTROL Almacenamiento de perfiles]. El Almacenamiento solicita audiencias de del [!UICONTROL Biblioteca de audiencias] (por ejemplo, audiencias compartidas de [!DNL Analytics], Audience Manager, etc). [!UICONTROL Atributos del cliente] se envían a [!UICONTROL Almacenamiento de perfiles] en un proceso por lotes.
1. En función de la dirección URL, los parámetros de solicitud y los datos de perfil, [!DNL Target] decide qué actividades y experiencias vuelven al visitante para la página actual y las vistas futuras

1. Contenido dirigido devuelto a la página, incluyendo, de manera opcional, los valores de perfil para una personalización adicional.

   El contenido dirigido se muestra en la página actual lo más rápido posible y sin parpadeo del contenido predeterminado.

   El contenido dirigido para futuras vistas de una aplicación de una sola página se almacena en caché en el explorador, por lo que se puede aplicar instantáneamente sin una llamada al servidor adicional cuando se activan las vistas. (Consulte el siguiente diagrama para `triggerView()` comportamiento).

1. [!DNL Analytics] datos enviados desde la página a [!UICONTROL Recopilación de datos] Servidores
1. [!DNL Target]Se comparan los datos de con los datos de mediante el SDID y se procesan en el almacén de informes de Analytics. [!DNL Analytics] [!DNL Analytics] por lo tanto, los datos de se pueden ver tanto en [!DNL Analytics] y [!DNL Target] mediante informes de A4T.

![Comportamiento de at.js 2.0 cuando se utiliza la función triggerView()](assets/triggerview.png)

1. `adobe.target.triggerView()` es invocado en la aplicación de una sola página
1. El contenido dirigido para la vista se lee desde la caché

1. El contenido dirigido se muestra lo más rápido posible y sin parpadeo del contenido predeterminado

1. La solicitud de notificación se envía al Almacenamiento de perfiles de [!DNL Target] para contar al visitante en la actividad e incrementar las métricas
1. [!DNL Analytics] SPA Los datos de se envían desde el a [!UICONTROL Recopilación de datos] Servidores

1. [!DNL Target] Los datos de se envían desde el [!DNL Target] back-end para [!UICONTROL Recopilación de datos] Servidores. Se comparan los datos de [!DNL Target] con los datos de [!DNL Analytics] mediante el SDID y se procesan en el almacén de informes de [!DNL Analytics]. [!DNL Analytics] por lo tanto, los datos de se pueden ver tanto en [!DNL Analytics] y [!DNL Target] mediante informes de A4T.

## Recursos adicionales

* [Implementar at.js 2.0 en una aplicación de una sola página](implement-atjs-20-in-a-single-page-application.md)
* [Uso del Compositor de experiencias visuales de Adobe Target SPA para aplicaciones de una sola página (VEC de)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
