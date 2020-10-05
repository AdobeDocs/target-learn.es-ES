---
title: Adobe Target con Adobe Mobile Services SDK v4 para Android
description: Adobe Target con el SDK v4 de Adobe Mobile Services para Android es el punto de partida perfecto para los desarrolladores de Android que ya están utilizando el SDK v4 de Adobe Mobile Services y desean inicio personalizar las experiencias de la aplicación con Adobe Target.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: d6cedd55dcc9c08d2d2ca5709e15fe5ea9fab8b8
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 2%

---


# Adobe Target con Adobe Mobile Services SDK v4 para Android: Descripción general

_Adobe Target con el SDK v4 de Adobe Mobile Services para Android_ es el punto de partida perfecto para los desarrolladores de Android que ya utilizan el SDK v4 de Adobe Mobile Services y desean inicio personalizar las experiencias de la aplicación con Adobe Target.

Se proporciona una aplicación de demostración de Android para completar las clases. Después de completar este tutorial, debe estar preparado para implementar inicios [!DNL Target] en su propia aplicación de Android.

Tras completar este tutorial, podrá:

* Validación de la configuración del SDK [de](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html) Adobe Mobile Services
* Implementar los siguientes tipos de [!DNL Target] solicitudes:
   * Recuperación previa del [!DNL Target] contenido
   * Lleve por lotes varias [!DNL Target] ubicaciones (mboxes) en una sola solicitud
   * Bloqueo de solicitudes (se ejecuta antes de que se muestre la aplicación)
   * Solicitudes no bloqueadas (se ejecuta en segundo plano)
   * Tiempo real (sin almacenamiento en caché)
   * Recuperación de eliminación de caché
* Añadir parámetros a solicitudes de personalización mejorada
* Crear audiencias y ofertas
* Personalización de diseños
* Despliegue nuevas funciones con el indicador de funciones

## Requisitos previos  

En estas lecciones se supone que:

* Tener un ID de Adobe y acceso de nivel de aprobador a la interfaz de Adobe Target (consulte los pasos de verificación a continuación)
* Conozca el código de cliente de Adobe Target para poder realizar solicitudes a su propia cuenta. El código de cliente se muestra en la interfaz de Adobe Target en la pantalla Ajustes > Implementación > Editar la configuración de at.js
* Tener acceso a la interfaz de usuario de [Mobile Services y familiarizarse con ella](https://mobilemarketing.adobe.com)
* Tenga un IDE para el desarrollo de aplicaciones móviles Android. Este tutorial incluye [Android Studio](https://developer.android.com/studio/install) en varios pasos y capturas de pantalla

Si no tiene el acceso necesario a las soluciones de Experience Cloud, póngase en contacto con el administrador de Experience Cloud.

Además, se supone que está familiarizado con el desarrollo de Android en Java. No es necesario que sea un experto en Java para completar las lecciones, pero obtendrá más de ellas si puede leer y entender el código cómodamente.

### Verificar el acceso a Adobe Target

Esta lección requiere acceso a Adobe Target. Antes de seguir los pasos siguientes, asegúrese de tener acceso a Adobe Target haciendo lo siguiente:

1. Inicie sesión en el [Adobe Experience Cloud](https://experience.adobe.com/)
1. From the Experience Cloud home screen, click [!DNL Target]:
   ![Pantalla principal del Experience Cloud](assets/aec_homeScreen_clickTarget.png)
1. Debe llegar a la lista Actividades en Adobe Target, como se muestra a continuación, y debe ver que el usuario tiene acceso a nivel Aprobador. Si no puede acceder [!DNL Target] o no puede comprobar el acceso a nivel de aprobador, póngase en contacto con uno de los administradores Experience Cloud de su compañía, solicite este acceso y reanude este tutorial una vez que se haya concedido:

   ![IU de Adobe](assets/targetUI_approver.png)

## Acerca de las lecciones

En estas lecciones, implementará Adobe Target en una aplicación de viajes de demostración llamada &quot;We.Travel&quot; con su propia cuenta de Adobe Target. Al final del tutorial, estará enviando mensajes personalizados al usuario en función de su uso de la aplicación. Las experiencias de personalización final tendrán este aspecto:

![Final de la aplicación We.Travel](assets/overview_final_result.jpg)

Después de recorrer la implementación dentro de la aplicación We.Travel, podrá realizar inicios usando [!DNL Target] su propia aplicación móvil.

Empecemos!

**[SIGUIENTE: &quot;Descargar y actualizar la aplicación de ejemplo&quot; >](download-and-update-the-sample-app.md)**
