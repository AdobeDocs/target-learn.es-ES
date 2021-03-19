---
title: Cómo usar tokens de respuesta y eventos personalizados de at.js
description: Aprenda a utilizar tokens de respuesta y eventos personalizados de at.js para compartir información de perfil de Target con sistemas de terceros.
role: Desarrollador
level: Con experiencia
topic: Personalización, arquitectura, desarrollo
feature: Implementación
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 4%

---


# Use tokens de respuesta y eventos personalizados de at.js con Adobe Target

Los tokens de respuesta y los `at.js` eventos personalizados le permiten compartir información de perfil de [!DNL Target] a sistemas de terceros. Cualquier objeto del perfil del visitante [!DNL Target], incluidos los atributos de perfil personalizados, la información geográfica, los detalles de la actividad y los perfiles integrados, se puede añadir a la respuesta [!DNL Target], donde puede utilizar JavaScript personalizado para integrarlo con un tercero.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Cómo usar tokens de respuesta y eventos personalizados de at.js

1. Determine qué datos necesita de [!DNL Target]
1. Active los tokens de respuesta para los datos que necesite activando el botón de alternancia en la pantalla Configuración->Tokens de respuesta
1. Determine qué detector de eventos debe utilizar
1. Escriba el JavaScript necesario para detectar el evento de Adobe Target, lea los tokens de respuesta y haga lo que necesite para la integración
1. Implemente el JavaScript del detector de eventos con una acción de código personalizado en Launch después de la acción Load Target o agréguelo a la sección Library Footer de at.js en la pantalla Setup->Implementation y guarde un nuevo archivo at.js
1. Control de calidad y publicación de la integración

## Recursos adicionales

* [Uso del Experience Cloud Debugger con Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentación del token de respuesta](https://docs.adobe.com/help/en/target/using/administer/response-tokens.html)
* [Documentación de eventos personalizados de at.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/functions-overview/atjs-custom-events.html)
* [Uso de Proveedores de datos en Adobe Target](use-data-providers-to-integrate-third-party-data.md)