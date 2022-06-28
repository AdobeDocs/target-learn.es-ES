---
title: ¿Qué es la API de Adobe Recommendations?
description: Este tutorial explica a los desarrolladores la práctica práctica práctica de usar las API de Adobe Target Recommendations para configurar y administrar catálogos de Recommendations y criterios personalizados, así como el uso de la API de envío para recuperar contenido de Recommendations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 10f80056-fb71-4362-86bc-d161f596cb91
source-git-commit: cee2618bb92284da1f82d108a0aff0d39340a15b
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 3%

---

# Información general de la API de Adobe Recommendations

API relevantes para [!DNL Recommendations] include [API de administración](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) que le permiten:

* Administrar el catálogo de productos o contenido recomendables
* Administre su [!DNL Recommendations] algoritmos y actividades

Al usar la variable [!DNL Target] [API de envío](https://experienceleague.adobe.com/docs/target/using/apis/api-overview.html?lang=en) con Recommendations, también puede:

* Recupere recomendaciones en objetos JSON, HTML o XML para que se puedan mostrar en web, móviles, correo electrónico, Internet de las cosas (IOT) y otros canales.

## Descripción del tutorial

Este tutorial guía a los desarrolladores por la práctica práctica práctica que utiliza el [!DNL Recommendations] API para configurar y administrar [!DNL Recommendations] catálogos y criterios personalizados, así como el uso de la API de envío para recuperar contenido de Recommendations. Al final de este tutorial, podrá:

* Configuración y administración de entidades mediante la API de Recommendations
* Configuración y administración de criterios personalizados mediante la API de Recommendations
* Obtenga información sobre cómo utilizar Recommendations con la API de envío para utilizar resultados de recomendaciones en dispositivos que no sean HTML

## Audiencia

Este tutorial está diseñado para desarrolladores que utilicen las API de Target o las API de Recommendations.

## Requisitos previos

El uso de las API de administración de Target requiere [Configuración de autenticación de Adobe](https://developer.adobe.com/target/before-administer/configure-authentication/){target=&quot;_blank&quot;}. Asegúrese de tener esto configurado antes de comenzar este tutorial.

## Recursos

Tenga en cuenta los siguientes recursos, que son necesarios para comprender este tutorial y seguirlo correctamente:

| Recurso | Detalles |
| --- | --- |
| Postman | Obtenga la variable [aplicación Postman](https://www.postman.com/downloads/) para su sistema operativo. Postman básico es gratuito con la creación de cuentas. Aunque no es necesario para utilizar las API de Adobe Target en general, Postman facilita los flujos de trabajo de las API y Adobe Target proporciona varias colecciones de Postman para ayudar a ejecutar sus API y aprender a funcionar. El resto de este tutorial asume el conocimiento práctico de Postman. Para obtener ayuda, consulte la [Documentación de Postman](https://learning.getpostman.com/). |
| Referencias | Durante el resto de este tutorial se asume la familiaridad con los siguientes recursos:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentación del Adobe I/O de Target](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentación de la API de Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

[Siguiente: &quot;Gestionar su catálogo de Recommendations&quot; >](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=&quot;_blank&quot;}
