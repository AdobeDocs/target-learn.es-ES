---
title: Descargar y actualizar la aplicación de ejemplo de We.Travel
description: 'La aplicación de ejemplo We.Travel está preimplementada con el SDK v4 de Adobe Mobile Services. Solo tiene que actualizarlo para que apunte a su propia organización Experience Cloud y cuentas de solución.   '
role: Desarrollador
level: Intermedio
topic: Móvil, personalización
feature: Implementar Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# Descargar y actualizar la aplicación de ejemplo de We.Travel

La aplicación de ejemplo We.Travel está preimplementada con el SDK v4 de Adobe Mobile Services. Solo tiene que actualizarlo para que apunte a su propia organización Experience Cloud y cuentas de solución.

## Objetivos de aprendizaje

Al final de esta lección, podrá:

* Descargue y abra la aplicación de ejemplo We.Travel en Android Studio.
* Verificación y actualización de la configuración del SDK de Mobile Services para [!DNL Target]

## Descargue la aplicación We.Travel .

* Descargue [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Descomprima el archivo zip
* Abra la aplicación en Android Studio como un proyecto existente (omita los errores sobre &quot;Asignación raíz de VCS no válida&quot;).
* Ejecute la aplicación en un emulador para confirmar que la aplicación se compila y que puede ver la pantalla principal
* Examine la aplicación y verifique que puede completar el proceso de reserva (seleccione cualquier opción de pago y pulse &quot;Continuar&quot; para omitir la pantalla de facturación).

   ![Abra la pantalla ](assets/wetravel_homeScreen.png)![appConfirmation .](assets/wetravel_confirmationScreen.png)

## Verificación y actualización de la configuración del SDK de Mobile Services para [!DNL Target]

El SDK de Adobe Mobile Services se ha preinstalado en la aplicación We.Travel [de acuerdo con la documentación](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html). Ahora actualizará la instalación para que apunte a su propia cuenta [!DNL Target].

En primer lugar, cree una nueva aplicación en la interfaz de usuario de Mobile Services:

1. Inicie sesión en la interfaz [Adobe Mobile Services](https://mobilemarketing.adobe.com).
1. Vaya a [!UICONTROL Administrar aplicaciones] y, a continuación, haga clic en **[!UICONTROL Agregar]** para agregar una nueva aplicación para utilizarla con este tutorial (**[!UICONTROL Administrar aplicaciones]** > **[!UICONTROL Agregar]**).
1. Elija un grupo de informes de Analytics con datos que no sean de producción, asígnele un nombre, seleccione el tipo **[!UICONTROL Standard]** y haga clic en **[!UICONTROL Guardar]**.
1. Una vez añadida la aplicación, añada el código de cliente [!DNL Target] en la siguiente pantalla de la sección [!UICONTROL Opciones de SDK Target] (puede encontrar el código de cliente en la interfaz [!DNL Target] en **[!UICONTROL Configuración]** > **[!UICONTROL Implementación]** > **[!UICONTROL Editar configuración]**, junto a Descargar &lt;a 10/ > ).`at.js`
1. La configuración [!UICONTROL Tiempo de espera de solicitud] determina cuánto tiempo espera la aplicación la respuesta del servidor [!DNL Target] antes de ejecutar las instrucciones de tiempo de espera. Deje la configuración predeterminada.
1. Habilite el [!UICONTROL Servicio de ID de visitante] y asegúrese de que la [!UICONTROL Organización] esté seleccionada en la lista desplegable.
1. Guarde los cambios haciendo clic en **[!UICONTROL Guardar]** en la parte superior derecha de la ventana (no en la sección [!UICONTROL Vínculos universales], [!UICONTROL Vínculos de la aplicación] o [!UICONTROL Servicios push]).
1. Desplácese a la sección Descargas del SDK de la aplicación que aparece en la parte inferior de la página y descargue el archivo de configuración:

   ![Descargar el archivo de configuración](assets/config_file.jpg)

1. Reemplace el archivo `ADBMobileConfig.json` en la carpeta de recursos de su proyecto de Android Studio (app > src > main > assets).

1. A continuación, abra el archivo `ADBMobileConfig.json` y asegúrese de que contiene los cambios esperados, como el código de cliente [!DNL Target] y los detalles de Analytics:
   ![Descargar el archivo de configuración](assets/client_code.jpg)

Si no ve la configuración, confirme que ha hecho clic en el botón **[!UICONTROL Save]** correcto de la interfaz [!UICONTROL Mobile Services] y copiado el archivo en la ubicación correcta.

¡Felicidades! Ha actualizado el SDK con sus [!DNL Target] detalles de cuenta. Realizaremos una validación adicional de la configuración después de añadir [!DNL Target] solicitudes en la siguiente lección.

**[SIGUIENTE : &quot;Añadir solicitudes de Target&quot; >](add-requests.md)**
