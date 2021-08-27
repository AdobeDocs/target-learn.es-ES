---
title: Adobe Target con el SDK v4 de Adobe Mobile Services para Android
description: Adobe Target con el SDK v4 de Adobe Mobile Services para Android es el punto de partida perfecto para los desarrolladores de Android que ya utilizan el SDK v4 de Adobe Mobile Services y desean comenzar a personalizar las experiencias de la aplicación con Adobe Target.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile, Overview
doc-type: tutorial
kt: 3040
thumbnail: null
exl-id: 20f8ed4f-a86d-4c5e-9296-71a93724caa3
source-git-commit: ee58c7c85708722cf040cd9b039a2855dd390a16
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 3%

---

# Adobe Target con Adobe Mobile Services SDK v4 para Android: información general

_Adobe Target con el SDK v4 de Adobe Mobile Services para_ Android es el punto de partida perfecto para los desarrolladores de Android que ya utilizan el SDK v4 de Adobe Mobile Services y desean comenzar a personalizar las experiencias de la aplicación con Adobe Target.

Se proporciona una aplicación Android de ejemplo para completar las lecciones. Después de completar este tutorial, debe estar listo para empezar a implementar [!DNL Target] en su propia aplicación de Android.

Tras completar este tutorial, podrá:

* Validar la configuración del SDK [Adobe Mobile Services](https://experienceleague.adobe.com/docs/mobile-services/android/getting-started-android/requirements.html?lang=en)
* Implemente los siguientes tipos de solicitudes [!DNL Target]:
   * Recuperación previa de contenido [!DNL Target]
   * Lleve por lotes varias [!DNL Target] ubicaciones (mboxes) en una sola solicitud
   * Bloqueo de solicitudes (se ejecuta antes de la visualización de la aplicación)
   * Solicitudes no bloqueadas (se ejecuta en segundo plano)
   * Tiempo real (sin almacenamiento en caché)
   * Recuperación de eliminación de caché
* Añadir parámetros a solicitudes de personalización mejorada
* Crear audiencias y ofertas
* Personalización de diseños
* Despliegue nuevas funciones con el indicador de características

## Requisitos previos  

En estas lecciones, se da por hecho que:

* Tener un ID de Adobe y acceso a nivel de aprobador a la interfaz de Adobe Target (consulte los pasos de verificación a continuación)
* Conozca el código de cliente de Adobe Target para poder realizar solicitudes en su propia cuenta. El código de cliente se muestra en la interfaz de Adobe Target en la   Configuración > Implementación > Editar la pantalla de configuración de at.js
* Tener acceso a la [interfaz de usuario de Mobile Services](https://mobilemarketing.adobe.com/) y estar familiarizados con ella
* Tenga un IDE para el desarrollo de aplicaciones móviles de Android. Este tutorial incluye [Android Studio](https://developer.android.com/studio/install) en varios pasos y capturas de pantalla

Si no tiene el acceso necesario a las soluciones de Experience Cloud, póngase en contacto con el administrador Experience Cloud.

Además, se da por hecho que está familiarizado con el desarrollo de Android en Java. No necesita ser experto en Java para completar las lecciones, pero obtendrá más información si puede leer y comprender el código con comodidad.

### Comprobar acceso a Adobe Target

Esta lección requiere acceso a Adobe Target. Antes de continuar con los pasos siguientes, asegúrese de que tiene acceso a Adobe Target haciendo lo siguiente:

1. Inicie sesión en [Adobe Experience Cloud](https://experience.adobe.com/)
1. En la pantalla de inicio del Experience Cloud, haga clic en [!DNL Target]:
   ![Pantalla principal del Experience Cloud](assets/aec_homeScreen_clickTarget.png)
1. Debería llegar a la lista Actividades en Adobe Target, como se muestra a continuación, y debería ver que su usuario tiene acceso a nivel de Aprobador. Si no puede acceder a [!DNL Target] o no puede comprobar el acceso a nivel de aprobador, póngase en contacto con uno de los administradores Experience Cloud de su empresa, solicite este acceso y reanude este tutorial una vez concedido:

   ![IU de Adobe](assets/targetUI_approver.png)

## Acerca de las lecciones

En estas lecciones, implementará Adobe Target en una aplicación de viajes de demostración llamada &quot;We.Travel&quot; con su propia cuenta de Adobe Target. Al final del tutorial, estará enviando mensajes personalizados al usuario en función de su uso de la aplicación. Las experiencias de personalización finales tendrán este aspecto:

![Final de la aplicación We.Travel](assets/overview_final_result.jpg)

Después de avanzar por la implementación dentro de la aplicación We.Travel , podrá empezar a usar [!DNL Target] en su propia aplicación móvil.

Empecemos!

**[SIGUIENTE : &quot;Descargar y actualizar la aplicación de ejemplo&quot; >](download-and-update-the-sample-app.md)**
