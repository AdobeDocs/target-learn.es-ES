---
title: Personalizar diseños
description: En esta lección final, creamos dos actividades de personalización en Target para nuestras audiencias. Obtenga información sobre cómo cargar y mostrar las actividades en la aplicación y validar que el contenido se muestra en el momento adecuado en las ubicaciones adecuadas.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
author: Daniel Wright
exl-id: a9f033d9-9f72-4154-88f5-d36423a404d0
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 1%

---

# Personalizar diseños

Ahora es el momento de juntar todo y crear las experiencias personalizadas. Una _Actividad_ es el mecanismo de [!DNL Target] que vincula las ubicaciones, audiencias y ofertas juntas, de modo que cuando se realice la solicitud desde la aplicación, [!DNL Target] responda con el contenido personalizado. Generaremos dos actividades de personalización en [!DNL Target] y validaremos que el contenido personalizado se muestra al usuario correcto en el momento y en la ubicación correctos.

## Objetivos de aprendizaje

Al final de esta lección, podrá hacer lo siguiente:

* Crear actividades en Adobe Target
* Valide las actividades en la aplicación de ejemplo.

## Crear actividades en Adobe Target

Obtenga información sobre cómo crear actividades de Participación de usuarios y Ofertas contextuales.

### Primera actividad: &quot;Participación de usuarios&quot;

Este es un resumen de la actividad que vamos a crear:

| Audiencia | Ubicaciones | Ofertas |
|---|---|---|
| Nuevos usuarios de aplicaciones móviles | wetravel_engage_home, wetravel_engage_search | Inicio: Interactuar con nuevos usuarios, Buscar: Interactuar con nuevos usuarios |
| Devolución de usuarios de aplicaciones móviles | wetravel_engage_home, wetravel_engage_search | Inicio: Usuarios que regresan, default_content |

En la interfaz [!DNL Target], haga lo siguiente:

1. Seleccione **[!UICONTROL Activities]** > **[!UICONTROL Create Activity]** > **[!UICONTROL Experience Targeting]**.

   ![Crear actividad](assets/activity_create_1.jpg)

1. Haga clic en **[!UICONTROL Mobile App]**.
1. Seleccione **[!UICONTROL Form composer]**.
1. Seleccione el espacio de trabajo (el mismo que utilizó en lecciones anteriores).
1. Seleccione su propiedad (la misma propiedad que utilizó en lecciones anteriores).
1. Haga clic en **[!UICONTROL Next]**.

   ![Crear actividad](assets/activity_create_2.jpg)

1. Cambie el título de la actividad a **[!UICONTROL Engage Users]**.
1. Seleccione **[!UICONTROL ellipsis]** > **[!UICONTROL Change Audience]**.
   ![Nuevos usuarios de aplicaciones móviles cambiaron la audiencia](assets/activity_create_3.jpg)
1. Establezca la audiencia en **[!UICONTROL New Mobile App Users]**.
1. Haga clic en **[!UICONTROL Done]**.
   ![Nueva audiencia de usuarios de aplicaciones móviles](assets/activity_create_4.jpg)

1. Cambiar la ubicación a _wetravel_engage_home_.
1. Seleccione la flecha desplegable junto a Contenido predeterminado y seleccione **[!UICONTROL Change HTML Offer]**.

   ![Nueva audiencia de usuarios de aplicaciones móviles](assets/activity_create_5.jpg)

1. Seleccione la oferta **[!UICONTROL Home: Engage New Users]**.
1. Seleccione **[!UICONTROL Done]**.

   ![Nueva audiencia de usuarios de aplicaciones móviles](assets/activity_create_6.jpg)

1. Seleccione **[!UICONTROL Add Location]**.
   ![Nueva audiencia de usuarios de aplicaciones móviles](assets/activity_create_7.jpg)

1. Seleccione la ubicación _wetravel_engage_search_.
1. Cambie la oferta de HTML.

   ![Nueva audiencia de usuarios de aplicaciones móviles](assets/activity_create_8.jpg)

1. Seleccione la oferta **[!UICONTROL Search: Engage New Users]**.
1. Haga clic en **[!UICONTROL Done]**.

   ![Nueva audiencia de usuarios de aplicaciones móviles](assets/activity_create_9.jpg)

Acaba de conectar una audiencia a ubicaciones y ofertas para crear la experiencia personalizada para los nuevos usuarios de aplicaciones móviles. La experiencia debería tener un aspecto similar al siguiente:

![Experiencia A Final](assets/activity_engage_users_a_final.jpg)

Ahora cree una experiencia para los usuarios de aplicaciones móviles que regresan:

1. Seleccione **[!UICONTROL Add Experience Targeting]** a la izquierda.
1. Seleccione la audiencia **[!UICONTROL Returning Mobile App Users]**.
1. Seleccione **[!UICONTROL Done]**.
   ![Audiencia de usuarios de aplicaciones móviles que regresa](assets/activity_create_11.jpg)

Ahora utilice el mismo proceso que utilizamos anteriormente para configurar la nueva experiencia. La configuración de la experiencia Devolución de usuarios de aplicaciones móviles debería ser similar a la siguiente:

![Devolución de usuarios de aplicaciones móviles final](assets/activity_engage_users_b_final.jpg)

Vamos a pasar a la siguiente pantalla de la configuración:

1. Haga clic en **[!UICONTROL Next]** para avanzar a la pantalla **[!UICONTROL Targeting]**.
1. Utilice la configuración predeterminada para Segmentación. Si tiene experiencias para audiencias que se superpusieron (por ejemplo, _Usuarios de Nueva York_ y _Usuarios por primera vez_), puede organizar el orden de prioridad en esta pantalla.
1. Haga clic en **[!UICONTROL Next]** para avanzar a **[!UICONTROL Goals & Settings]**.

   ![Actividad de participación de usuarios - Segmentación predeterminada](assets/activity_engage_users_targeting.jpg)

Ahora vamos a completar la configuración de la actividad:

1. Establezca **[!UICONTROL Primary Goal]** en **[!UICONTROL Conversion]**.
1. Establezca la acción en **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (como esta ubicación está en la pantalla de confirmación, podemos utilizarla para medir las conversiones).

   ![Actividad de participación de usuarios - Objetivos](assets/activity_create_12.jpg)

1. Mantenga el resto de configuraciones en la pantalla con los valores predeterminados.
1. Haga clic **[!UICONTROL Save & Close]** para guardar la actividad.
1. Activar **[!UICONTROL Activity]** en la siguiente pantalla.

![Audiencia de experiencia B](assets/activity_create_13.jpg)

Nuestra primera actividad ya está activa y lista para probar.

### Segunda actividad: &quot;Ofertas contextuales&quot;

Este es un resumen de la segunda actividad que crearemos:

| Audiencia | Ubicación | Ofertas |
| --- | --- | --- |
| Destino: San Diego | wetravel_context_dest | Promoción para San Diego |
| Destino: Los Ángeles | wetravel_context_dest | Promoción para Los Ángeles |

Repita el mismo proceso que se ha descrito anteriormente para la siguiente actividad: &quot;Ofertas contextuales&quot;. A continuación, se muestra la configuración final para ambas experiencias:

#### San Diego

![Ofertas contextuales - Experiencia A](assets/activity_contextual_a_final.jpg)

#### Los Ángeles

![Ofertas contextuales - Experiencia B](assets/activity_contextual_b_final.jpg)

En el paso Objetivos y configuración, cambiaremos la meta principal a la ubicación en la pantalla de confirmación de la reserva:

1. En **[!UICONTROL Reporting Settings]**, establezca **[!UICONTROL Primary Goal]** en **[!UICONTROL Conversion]**.
1. Establezca la acción en **[!UICONTROL Viewed an mbox]** > _wetravel_context_dest_ (en esta actividad, esta métrica carece básicamente de sentido, ya que también es la misma ubicación que ofrece la experiencia).
1. Haga clic en **[!UICONTROL Save & Close]**.

![Ofertas contextuales - Experiencia](assets/activity_create_14.jpg)

Active la actividad en la pantalla siguiente.

Ahora, la segunda actividad está activa y lista para probarse.

## Validar la oferta de inicio

Ejecute el emulador y observe si se muestra la primera oferta en la parte inferior de la pantalla principal. Si eres un usuario que regresa con 5 o más inicios de aplicación, verás la oferta _bienvenido de nuevo_. Si es un usuario nuevo (menos de 5 inicios de aplicación), debería ver el mensaje _nuevo usuario_:

![Validar oferta de inicio](assets/layout_home_validate.jpg)

Si no se muestra la nueva oferta de usuario, intente borrar los datos del emulador. Esto restablecerá los inicios de la aplicación a 1 la próxima vez que la inicie. Esto se hace en **[!UICONTROL Tools]** > **[!UICONTROL AVD Manager]**. Es posible que también tenga que reiniciar Android Studio si Logcat no funciona correctamente:

![Emulador de borrado](assets/layout_home_validate_avd_wipe.jpg)

También puede validar la respuesta en Logcat filtrando por _wetravel_engage_home_:

![Validar oferta de inicio - Logcat](assets/layout_home_validate_logcat.jpg)

## Validación de la oferta de búsqueda

Seleccione **[!UICONTROL San Jose]** como su **[!UICONTROL Departure]** y **[!UICONTROL San Diego]** como su **[!UICONTROL Destination]** y haga clic en **[!UICONTROL Find Bus]** para buscar los buses disponibles.

En la pantalla de resultados, debería ver el mensaje _usar filtros_. Si es un usuario que regresa con 5 o más inicios de aplicación, no aparecerá ningún mensaje aquí, ya que el contenido predeterminado está configurado para esta ubicación (que está en blanco):

![Validar oferta de búsqueda](assets/layout_search_validate.jpg)

## Validación de las ofertas contextuales en la pantalla de agradecimiento

Ahora continúe con el proceso de reserva:

* Seleccione un bus en la pantalla de resultados.
* Seleccione un asiento en la pantalla de pago y envío.
* Seleccione **[!UICONTROL Credit Card]** en la pantalla de pago (deje la información de pago en blanco: no se realizará ninguna reserva real).

Como San Diego fue seleccionado como destino, debería ver el banner de la oferta _DJ SAM_ en la pantalla de confirmación:

![Validar oferta de contexto - San Diego](assets/layout_context_san_diego.jpg)

Ahora selecciona **[!UICONTROL Done]** y prueba otra reserva con Los Ángeles como destino. La pantalla de confirmación debería mostrar el banner de _Universal Studios_:

![Validar oferta contextual - Los Ángeles](assets/layout_context_los_angeles.jpg)

## Conclusión

¡Felicidades! Con esto concluye la parte principal del tutorial de Adobe Target SDK 4.x para Android. Ahora tiene las habilidades para implementar la personalización en aplicaciones de Android. Puede consultar esta documentación y la aplicación de demostración como referencia para sus futuros proyectos.

Siguiente: El indicador de funciones es otra función que se puede implementar con Adobe Target en Android. Para obtener más información sobre el marcado de características, consulte la siguiente lección.

**[SIGUIENTE: Marca de característica >](feature-flagging.md)**
