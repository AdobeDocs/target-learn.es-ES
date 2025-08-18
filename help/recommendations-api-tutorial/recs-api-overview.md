---
title: ¿Qué es la API de Adobe Recommendations?
description: Este tutorial guía a los desarrolladores a través de la práctica práctica para utilizar las API de Recommendations de Adobe Target para configurar y administrar los catálogos de Recommendations y los criterios personalizados, así como para utilizar la API de envío para recuperar contenido de Recommendations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: 542ff406fc24df54a2f1b007422492341ea46507
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 2%

---

# Información general de API de Adobe Recommendations

Las API relevantes para [!DNL Recommendations] incluyen [API de administrador](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=es) que le permiten lo siguiente:

* Administre su catálogo de productos o contenido recomendables
* Administrar los algoritmos y las actividades de [!DNL Recommendations]

Con la [!DNL Target] [API de envío](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=es) con Recommendations, también puede:

* Recupere recomendaciones en objetos JSON, HTML o XML para que se puedan mostrar en la web, dispositivos móviles, correo electrónico, Internet de las cosas (IOT) y otros canales.

## Descripción del tutorial

Este tutorial guía a los desarrolladores a través de la práctica práctica para usar las API [!DNL Recommendations] con el fin de configurar y administrar [!DNL Recommendations] catálogos y criterios personalizados, así como el uso de la API de envío para recuperar contenido de Recommendations. Al final de este tutorial, debería saber cómo:

* Configuración y administración de entidades mediante la API de Recommendations
* Configuración y administración de criterios personalizados con la API de Recommendations
* Obtenga información sobre cómo utilizar Recommendations con la API de envío para utilizar los resultados de Recommendations en dispositivos que no son de HTML

## Audiencia

Este tutorial está diseñado para desarrolladores que utilicen las API de Target o las API de Recommendations por primera vez.

## Requisitos previos

El uso de las API de administración de Target requiere [configuración de autenticación de Adobe](https://experienceleague.adobe.com/docs/target-dev/developer/api/configure-authentication.html?lang=es){target="_blank"}. Asegúrese de tener esto configurado antes de comenzar este tutorial.

## Recursos

Tenga en cuenta los siguientes recursos, que son necesarios para comprender este tutorial y seguirlo correctamente:

| Recurso | Detalles |
| --- | --- |
| Postman | Obtén la [aplicación de Postman](https://www.postman.com/downloads/) para tu sistema operativo. Postman basic es gratuito con la creación de cuentas. Aunque no es necesario para utilizar las API de Adobe Target en general, Postman facilita los flujos de trabajo de las API y Adobe Target proporciona varias colecciones de Postman para ayudarle a ejecutar sus API y aprender cómo funcionan. El resto de este tutorial supone conocimientos prácticos de Postman. Para obtener ayuda, consulte la [documentación de Postman](https://learning.getpostman.com/). |
| Referencias | En el resto de este tutorial se da por hecho que está familiarizado con los siguientes recursos:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentación de Target Adobe I/O](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentación de la API de Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Siguiente: &quot;Administrar el catálogo de Recommendations&quot; >](https://experienceleague.adobe.com/docs/target-dev/developer/api/recommendations-api/manage-catalog.html?lang=es){target="_blank"}
