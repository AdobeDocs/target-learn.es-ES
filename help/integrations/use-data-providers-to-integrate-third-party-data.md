---
title: Cómo utilizar proveedores de datos para integrar datos de terceros
description: Este tutorial presenta a los usuarios los proveedores de datos. Aprenda a utilizar la capacidad Proveedores de datos para pasar fácilmente datos de terceros a Adobe Target.
role: User, Developer
level: Experienced
topic: Personalization, Integrations
feature: Implementation, Integrations, APIs/SDKs
doc-type: feature video
kt: null
author: Daniel Wright
exl-id: 1892136e-14e3-4e52-8b1f-aee806d2f83a
TQID: https://experienceleague.adobe.com/XiUlJGHSFVxAMqdl6Y7hK9PoXOgiiUI43vrFeAj2Rpo
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 199
ht-degree: 16%

---

# Utilice proveedores de datos para integrar datos de terceros en Adobe Target

[!UICONTROL Proveedores de datos] es una funcionalidad que te permite pasar fácilmente datos de terceros a Target.  Un tercero podría ser un servicio de pronóstico del clima, un DMP o incluso su propio servicio web. Puede usar estos datos para crear audiencias, dirigir contenido y enriquecer el perfil del visitante.

>[!VIDEO](https://video.tv.adobe.com/v/22349/?quality=12)

## Cómo utilizar los proveedores de datos

1. El experto en implementación agrega código antes de at.js (o en la sección Encabezado de biblioteca de at.js) que realiza la llamada de API al tercero, analiza la respuesta y especifica con pares de nombre/valor de la respuesta que se enviará a [!DNL Target].
1. at.js administra el parpadeo e incluye los pares nombre/valor como parámetros personalizados en la solicitud global de Target.
1. El especialista en marketing crea audiencias en la interfaz [!DNL Target] en función de estos parámetros personalizados.
1. El especialista en marketing utiliza estas audiencias para segmentar experiencias, actividades y métricas, así como para informar a audiencias.

>[!NOTE]
>
>[!UICONTROL Proveedores de datos] requiere at.js 1.3 o superior

## Materiales de apoyo

* [Implementación de proveedores de datos en at.js y Adobe Target](implement-data-providers-to-integrate-third-party-data.md)
