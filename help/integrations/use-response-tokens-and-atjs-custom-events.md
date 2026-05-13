---
title: Uso de tokens de respuesta y eventos personalizados de at.js
description: Aprenda a utilizar los tokens de respuesta y los eventos personalizados de at.js para compartir información de perfil de Target con sistemas de terceros.
role: Developer
level: Experienced
topic: Personalization, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: d6ce5367-a453-4e6c-8545-9fa676977f04
TQID: https://experienceleague.adobe.com/gJfFi9mC3iKY8pEdvE1Tuk7Mk2rUOdTKtv67vXQwkO8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 230
ht-degree: 3%

---

# Use Tokens de respuesta y eventos personalizados de at.js con Adobe Target

Los tokens de respuesta y los eventos personalizados `at.js` le permiten compartir información de perfil de [!DNL Target] con sistemas de terceros. Cualquier objeto del perfil del visitante [!DNL Target], incluidos los atributos de perfil personalizados, la información geográfica, los detalles de actividad y los perfiles integrados, se puede agregar a la respuesta [!DNL Target], donde puede utilizar JavaScript personalizado para integrarlo con un tercero.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)

## Uso de tokens de respuesta y eventos personalizados de at.js

1. Determine qué datos necesita de [!DNL Target]
1. Active los tokens de respuesta para los datos que necesite haciendo clic en el botón de alternancia en la pantalla Configuración->Tokens de respuesta
1. Determine qué detector de eventos debe utilizar
1. Escriba el JavaScript necesario para detectar el evento de Adobe Target, lea los tokens de respuesta y haga lo que necesite para la integración
1. Implemente el detector de eventos JavaScript con una acción de código personalizado en Launch después de la acción &quot;Load Target&quot; o añádala a la sección Pie de página de la biblioteca de at.js en la pantalla Configuración->Implementación y guarde un nuevo archivo at.js
1. Control de calidad y publicación de la integración

## Recursos adicionales

* [Uso de Experience Cloud Debugger con Adobe Target](../troubleshooting/troubleshoot-with-the-experience-cloud-debugger.md)
* [Documentación del token de respuesta](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=en)
* [Uso de Proveedores de datos en Adobe Target](use-data-providers-to-integrate-third-party-data.md)
