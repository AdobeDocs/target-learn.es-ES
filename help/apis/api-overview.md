---
title: Información general de la API de Adobe Target
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations incluye un conjunto dedicado de API que le permiten administrar su catálogo de productos y/o contenido recomendables; administrar los algoritmos y campañas de las recomendaciones; y envíe recomendaciones en objetos JSON, HTML o XML para que se muestren en web, móviles, de correo electrónico, IOT y otros canales.
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: b66dbae616c9559f5d1b7bbedf2d9b383840973b
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 2%

---


# Información general de la API de Adobe Target

Las API de Adobe Target pueden agruparse según el tipo.

| Tipo de API | Lo que le permite hacer | Vínculo de descarga |
| --- | --- | --- |
| Administración | Cree, modifique y elimine actividades, audiencias, ofertas y otros objetos (incluidas [!DNL Recommendations] entidades, criterios, diseños, etc.). Las [!DNL Recommendations] API son un tipo de API de administración). | <UL><li>[API de administración de Destinatario Colección Postman](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman Collection](https://developers.adobetarget.com/api/recommendations/#section/Postman)</li></ul> |
| Entrega | Recupere contenido optimizado y personalizado de [!DNL Target] para envío a un usuario final. | [API de Destinatario Envío Colección Postman](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection) |
| Creación de informes | Exportar resultados de actividad y otros resultados de sistema de informes. | Las API de Sistema de informes se incluyen en la colección [de Postman de la API de administración de](https://developers.adobetarget.com/api/#admin-postman-collection)Destinatario. |
| Perfil | Recuperar y modificar perfiles de usuario almacenados en Adobe Target. | [API de Destinatario Perfil Colección Postman](https://developers.adobetarget.com/api/#profiles) |

Tenga en cuenta la distinción entre las API de **administración** (incluidas [!DNL Recommendations] las API), que le permiten configurar varios aspectos de Adobe Target, en comparación con las API **de** envío, que le permiten recuperar contenido. Las API de administración requieren autenticación, mientras que las API de envío no.

Para utilizar las API de administración de Adobe Target, primero debe configurar la autenticación mediante E/S de Adobe.

[Siguiente &quot;Configurar autenticación&quot; >](configure-io-target-integration.md)
