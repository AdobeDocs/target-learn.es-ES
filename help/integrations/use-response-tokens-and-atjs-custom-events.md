---
title: Usar tokens de respuesta y Eventos personalizados de at.js con Adobe Target
seo-title: Usar tokens de respuesta y Eventos personalizados de at.js con Adobe Target
description: Los tokens de respuesta y los Eventos personalizados de at.js le permiten compartir información de perfil de Destinatario a sistemas de terceros. Cualquier objeto del perfil de visitante de Destinatario, incluidos los atributos de perfil personalizados, la información geográfica, los detalles de actividad y los perfiles integrados, se puede agregar a la respuesta de Destinatario, donde puede utilizar JavaScript personalizado para integrarlo con un tercero.
audience: developer
difficulty: 5
author: Daniel Wright
doc-type: implement
activity-type: technical-video
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 2%

---


# Usar tokens de respuesta y Eventos personalizados de at.js con Adobe Target

Los tokens de respuesta y `at.js` los Eventos personalizados le permiten compartir información de perfiles de [!DNL Target] sistemas de terceros. Cualquier objeto del perfil de [!DNL Target] [!DNL Target] visitante, incluidos los atributos de perfil personalizados, la información geográfica, los detalles de actividad y los perfiles integrados, se pueden agregar a la respuesta, donde puede utilizar JavaScript personalizado para integrarlo con un tercero.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Cómo usar tokens de respuesta y Eventos personalizados de at.js

1. Determinar de qué datos necesita [!DNL Target]
1. Active los tokens de respuesta para los datos que necesita activando el botón de alternancia en la pantalla Configuración->Tokens de respuesta
1. Determinar qué detector de evento necesita utilizar
1. Escriba el JavaScript necesario para escuchar el evento de Adobe Target, leer los tokens de respuesta y hacer lo que necesite para la integración
1. Implemente el código JavaScript del detector de evento mediante una acción de código personalizado en Iniciar después de la acción &quot;Cargar Destinatario&quot; o agréguelo a la sección Pie de página de biblioteca de at.js en la pantalla Configuración->Implementación y guarde un nuevo archivo at.js
1. Control de calidad y publicación de la integración

## Recursos adicionales

* [Usar el Experience Cloud Debugger con Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentación del token de respuesta](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [Documentación de Evento personalizado de At.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [Uso de Proveedores de datos en Adobe Target](use-data-providers-to-integrate-third-party-data.md)