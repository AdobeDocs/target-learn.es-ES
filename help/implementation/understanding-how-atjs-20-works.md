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
TQID: https://experienceleague.adobe.com/yi78hasak-rtlhpCG4-UnewWXAwMfPZJSpw9sFzRenU
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 396
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
