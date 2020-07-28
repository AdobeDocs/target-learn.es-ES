---
title: Descargar y actualizar la aplicación de muestra We.Travel
seo-title: Descargue la aplicación de ejemplo y compruebe el SDK de los servicios móviles
description: 'La aplicación de ejemplo We.Travel está preimplementada con el SDK v4 de Adobe Mobile Services. Solo tiene que actualizarlo para que apunte a su propia organización Experience Cloud y a las cuentas de la solución.   '
seo-description: La aplicación de ejemplo We.Travel está preimplementada con el SDK v4 de Adobe Mobile Services. Solo tiene que actualizarlo para que apunte a su propia organización Experience Cloud y a las cuentas de la solución.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---


# Descargar y actualizar la aplicación de muestra We.Travel

La aplicación de ejemplo We.Travel está preimplementada con el SDK v4 de Adobe Mobile Services. Solo tiene que actualizarla para que apunte a su propia organización Experience Cloud y a las cuentas de la solución.

## Objetivos de aprendizaje

Al final de esta lección, podrá:

* Descargar y abrir la aplicación de muestra We.Travel en Android Studio
* Verificación y actualización de la configuración del SDK de Mobile Services para [!DNL Target]

## Descargar la aplicación We.Travel

* Descargue [sample-app-android-SDKv4-Base-Version.zip](assets/sample-app-android-SDKv4-Base-Version.zip)
* Descomprima el archivo zip
* Abra la aplicación en Android Studio como un proyecto existente (omita los errores sobre la &quot;Asignación raíz VCS no válida&quot;)
* Ejecute la aplicación en un emulador para confirmar que la aplicación se crea y podrá ver la pantalla de inicio
* Examine la aplicación y verifique que puede completar el proceso de reservación (seleccione cualquier opción de pago y pulse &quot;Continuar&quot; para omitir la pantalla de facturación).

   ![Abra la pantalla](assets/wetravel_homeScreen.png)![appConfirmation](assets/wetravel_confirmationScreen.png)

## Verificación y actualización de la configuración del SDK de Mobile Services para [!DNL Target]

El SDK de Adobe Mobile Services se ha preinstalado en la aplicación We.Travel [según la documentación](https://docs.adobe.com/content/help/en/mobile-services/android/getting-started-android/requirements.html). Ahora actualizará la instalación para que apunte a su propia [!DNL Target] cuenta.

En primer lugar, cree una nueva aplicación en la interfaz de usuario de Mobile Services:

1. Log in to the [Adobe Mobile Services interface](https://mobilemarketing.adobe.com).
1. Vaya a [!UICONTROL Administrar aplicaciones]y, a continuación, haga clic en **[!UICONTROL Añadir]** para agregar una nueva aplicación para utilizarla con este tutorial (**[!UICONTROL Administrar aplicaciones]** > **[!UICONTROL Añadir]**).
1. Elija un grupo de informes de Analytics con datos que no sean de producción, asigne un nombre a la aplicación, seleccione el tipo **[!UICONTROL Estándar]** y haga clic en **[!UICONTROL Guardar]**.
1. Una vez agregada la aplicación, agregue su código [!DNL Target] de cliente en la siguiente pantalla de la sección Opciones [!UICONTROL de Destinatario del] SDK (puede encontrar el código de cliente en la [!DNL Target] interfaz en **[!UICONTROL Configuración]** > **[!UICONTROL Implementación]** > **[!UICONTROL Editar configuración]**`at.js` , junto al botón Descargar).
1. El ajuste Tiempo de espera [!UICONTROL de] solicitud determina cuánto tiempo espera la aplicación la respuesta del [!DNL Target] servidor antes de ejecutar las instrucciones de tiempo de espera. Deje la configuración predeterminada.
1. Habilite el servicio [!UICONTROL de ID de] Visitante y asegúrese de que su [!UICONTROL organización] está seleccionada en la lista desplegable.
1. Guarde los cambios haciendo clic en **[!UICONTROL Guardar]** en la parte superior derecha de la ventana (no en la sección Vínculos universales, Vínculos [!UICONTROL de] aplicación o Servicios [!UICONTROL push] ).
1. Vaya a la sección Descargas del SDK de la aplicación en la parte inferior de la página y descargue el archivo de configuración:

   ![Descargar el archivo de configuración](assets/config_file.jpg)

1. Reemplace el `ADBMobileConfig.json` archivo en la carpeta de recursos del proyecto de Android Studio (aplicación > src > main > assets).

1. Ahora abra el `ADBMobileConfig.json` archivo y asegúrese de que contiene los cambios esperados, como el código [!DNL Target] del cliente y los detalles de Analytics:
   ![Descargar el archivo de configuración](assets/client_code.jpg)

Si no ve la configuración, confirme que ha hecho clic en el botón derecho **[!UICONTROL Guardar]** en la interfaz de [!UICONTROL Mobile Services] y que ha copiado el archivo en la ubicación correcta.

¡Felicitaciones! Ha actualizado el SDK con los detalles de su [!DNL Target] cuenta. Realizaremos una validación adicional de la configuración después de agregar [!DNL Target] solicitudes en la siguiente lección.

**[SIGUIENTE: &quot;Añadir solicitudes de Destinatario&quot; >](add-requests.md)**
