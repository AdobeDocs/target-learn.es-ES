---
title: Personalización de diseños
seo-title: Personalización de diseños
description: 'En esta última lección, construiremos dos actividades de personalización en Destinatario para nuestras Audiencias. Cargaremos y mostraremos las actividades en la aplicación y validaremos que el contenido se muestra en el momento adecuado en las ubicaciones correctas.  '
seo-description: En esta última lección, construiremos dos actividades de personalización en Destinatario para nuestras Audiencias. Cargaremos y mostraremos las actividades en la aplicación y validaremos que el contenido se muestra en el momento adecuado en las ubicaciones correctas.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 1%

---


# Personalización de diseños

Ahora es el momento de unir todo y crear las experiencias personalizadas. Una _Actividad_ es el mecanismo [!DNL Target] que vincula las ubicaciones, audiencias y ofertas juntas, de modo que cuando la solicitud se realiza desde la aplicación, [!DNL Target] responde con el contenido personalizado. Generaremos dos actividades de personalización en [!DNL Target] y validaremos que el contenido personalizado se muestra al usuario correcto en el momento y en la ubicación correctos.

## Objetivos de aprendizaje

Al final de esta lección, podrá:

* Generar Actividades en Adobe Target
* Validar las Actividades en la aplicación de muestra

## Crear Actividades en Adobe Target

Obtenga información sobre cómo crear actividades de participación de usuarios y Ofertas contextuales.

### Primera Actividad: &quot;Participación de usuarios&quot;

A continuación se presenta un resumen de la actividad que construiremos:

| Audiencia | Ubicaciones | Ofertas |
|---|---|---|
| Nuevos usuarios de aplicaciones móviles | wetravel_engagement_home, wetravel_engagement_search | Inicio: Participación de nuevos usuarios, buscar: Participación de nuevos usuarios |
| Devolución de usuarios de aplicaciones móviles | wetravel_engagement_home, wetravel_engagement_search | Inicio: Usuarios que regresan, default_content |

En la interfaz [!DNL Target] haga lo siguiente:

1. Seleccione **[!UICONTROL Actividades]** > **[!UICONTROL Crear Actividad]** > **[!UICONTROL Segmentación de experiencias]**.

   ![Crear Actividad](assets/activity_create_1.jpg)

1. Haga clic en **[!UICONTROL Aplicación móvil]**.
1. Seleccione el **[!UICONTROL Compositor de formularios]**.
1. Seleccione el espacio de trabajo (el mismo espacio de trabajo que utilizó en las lecciones anteriores).
1. Seleccione la propiedad (la misma propiedad que utilizó en las lecciones anteriores).
1. Haga clic en **[!UICONTROL Siguiente]**.

   ![Crear Actividad](assets/activity_create_2.jpg)

1. Cambie el título de la actividad a **[!UICONTROL Participación de usuarios]**.
1. Seleccione la **[!UICONTROL elipsis]** > **[!UICONTROL Cambiar Audiencia]**.
   ![Nuevos usuarios de aplicaciones móviles cambiar Audiencia](assets/activity_create_3.jpg)
1. Establezca la audiencia en **[!UICONTROL Nuevos usuarios de aplicaciones móviles]**.
1. Haga clic en **[!UICONTROL Finalizado]**.
   ![Nueva Audiencia de usuarios de aplicaciones móviles](assets/activity_create_4.jpg)

1. Cambie la ubicación a _wetravel_engagement_home_.
1. Seleccione la flecha desplegable junto a Contenido predeterminado y seleccione **[!UICONTROL Cambiar Oferta HTML]**.

   ![Nueva Audiencia de usuarios de aplicaciones móviles](assets/activity_create_5.jpg)

1. Seleccione el **[!UICONTROL Inicio: Participación en la oferta Nuevos usuarios]**.
1. Seleccione **[!UICONTROL Listo]**.

   ![Nueva Audiencia de usuarios de aplicaciones móviles](assets/activity_create_6.jpg)

1. Seleccione **[!UICONTROL Añadir ubicación]**.
   ![Nueva Audiencia de usuarios de aplicaciones móviles](assets/activity_create_7.jpg)

1. Seleccione la ubicación _wetravel_engagement_search_.
1. Cambie la oferta HTML.

   ![Nueva Audiencia de usuarios de aplicaciones móviles](assets/activity_create_8.jpg)

1. Seleccione la **[!UICONTROL búsqueda: Participación en la oferta Nuevos usuarios]**.
1. Haga clic en **[!UICONTROL Finalizado]**.

   ![Nueva Audiencia de usuarios de aplicaciones móviles](assets/activity_create_9.jpg)

Acaba de conectar una audiencia a ubicaciones y ofertas, creando la experiencia personalizada para los nuevos usuarios de aplicaciones móviles. Ahora la experiencia debería tener este aspecto:

![Experiencia A Final](assets/activity_engage_users_a_final.jpg)

Ahora cree una experiencia para los usuarios de aplicaciones móviles que regresan:

1. Seleccione **[!UICONTROL Añadir Segmentación de experiencias]** a la izquierda.
1. Seleccione la Audiencia **[!UICONTROL Devolución de usuarios de aplicaciones móviles]**.
1. Seleccione **[!UICONTROL Listo]**.
   ![Devolución de la Audiencia de usuarios de aplicaciones móviles](assets/activity_create_11.jpg)

Ahora utilice el mismo proceso que hemos utilizado anteriormente para configurar la nueva experiencia. La configuración de la experiencia de usuarios que vuelven de la aplicación móvil debería tener este aspecto:

![Devolución final de usuarios de aplicaciones móviles](assets/activity_engage_users_b_final.jpg)

Continuemos con la siguiente pantalla de la configuración:

1. Haga clic en **[!UICONTROL Siguiente]** para avanzar a la pantalla **[!UICONTROL Objetivo]**.
1. Utilice la configuración predeterminada para la segmentación. Si tenía experiencias para audiencias que se solapaban (p. ej. _Usuarios de Nueva York_ y _Nuevos usuarios_) puede organizar el orden de prioridad en esta pantalla.
1. Haga clic en **[!UICONTROL Siguiente]** para avanzar a **[!UICONTROL Objetivos y configuración]**.

   ![Actividad de participación de usuarios: establecimiento de objetivos predeterminado](assets/activity_engage_users_targeting.jpg)

Ahora completemos la configuración de la actividad:

1. Establezca el **[!UICONTROL Objetivo principal]** en **[!UICONTROL Conversión]**.
1. Establezca la acción en **[!UICONTROL Visualizó un mbox]** > _wetravel_context_dest_ (como esta ubicación está en la pantalla de confirmación, podemos utilizarla para medir las conversiones).

   ![Actividad de participación de usuarios: objetivos](assets/activity_create_12.jpg)

1. Mantenga el resto de la configuración en pantalla a los valores predeterminados.
1. Haga clic en **[!UICONTROL Guardar y cerrar]** para guardar la Actividad.
1. Active la **[!UICONTROL Actividad]** en la siguiente pantalla.

![Audiencia de la experiencia B](assets/activity_create_13.jpg)

Nuestra primera actividad está ahora lista para probar!

### Segunda Actividad: &quot;Ofertas contextuales&quot;

A continuación se presenta un resumen de la segunda actividad que construiremos:

| Audiencia | Ubicación | Ofertas |
| --- | --- | --- |
| Destino: San Diego | wetravel_context_dest | Promoción para San Diego |
| Destino: Los Ángeles | wetravel_context_dest | Promoción para Los Ángeles |

Repita el mismo proceso que el anterior para la siguiente Actividad: &quot;Ofertas contextuales&quot;. La configuración final de ambas experiencias se muestra a continuación:

#### San Diego

![Ofertas contextuales - Experiencia A](assets/activity_contextual_a_final.jpg)

#### Los Ángeles

![Ofertas contextuales - Experiencia B](assets/activity_contextual_b_final.jpg)

En el paso Objetivos y configuración, cambiaremos el objetivo principal a la ubicación en la pantalla de confirmación de reservación:

1. En **[!UICONTROL Configuración de Sistema de informes]**, establezca el **[!UICONTROL Objetivo principal]** en **[!UICONTROL Conversión]**.
1. Establezca la acción en **[!UICONTROL Visualizó un mbox]** > _wetravel_context_dest_ (en esta actividad, esta métrica no tiene sentido, ya que también es la misma ubicación que ofrece la experiencia).
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

![Ofertas contextuales: experiencia](assets/activity_create_14.jpg)

Active la Actividad en la siguiente pantalla.

¡Ahora nuestra segunda actividad está lista para probarse!

## Validar la Oferta principal

Ejecute el emulador y observe la primera oferta que aparece en la parte inferior de la pantalla de inicio. Si es un usuario que regresa con 5 o más inicios de la aplicación, verá la oferta _bienvenido de nuevo_. Si es un usuario nuevo (menos de 5 inicios de aplicación), debería ver el mensaje _nuevo usuario_:

![Validar Oferta principal](assets/layout_home_validate.jpg)

Si la nueva oferta de usuario no se muestra, intente borrar los datos del emulador. Esto restablecerá los inicios de la aplicación a 1 la próxima vez que se inicie. Esto se realiza en **[!UICONTROL Herramientas]** > **[!UICONTROL Administrador de AVD]**. También es posible que tenga que reiniciar Android Studio si Logcat no funciona correctamente:

![Emulador de borrado](assets/layout_home_validate_avd_wipe.jpg)

También puede validar la respuesta en Logcat filtrando para _wetravel_engagement_home_:

![Validar Oferta principal - Logcat](assets/layout_home_validate_logcat.jpg)

## Validar la Oferta de búsqueda

Seleccione **[!UICONTROL San José]** como su **[!UICONTROL Salida]** y **[!UICONTROL San Diego]** como su **[!UICONTROL Destino]** y haga clic en **[!UICONTROL Buscar bus]** para buscar buses disponibles.

En la pantalla de resultados, debería ver el mensaje _use filtros_. Si es un usuario que regresa con 5 o más inicios de la aplicación, no aparecerá ningún mensaje aquí, ya que el contenido predeterminado se establece para esta ubicación (que está en blanco):

![Validar Oferta de búsqueda](assets/layout_search_validate.jpg)

## Validar las Ofertas contextuales en la pantalla de agradecimiento

Ahora continúe con el proceso de reservación:

* Seleccione un bus en la pantalla de resultados.
* Seleccione un asiento en la pantalla de cierre de compra.
* Seleccione **[!UICONTROL Tarjeta de crédito]** en la pantalla de pago (deje la información de pago en blanco - no se realizará ninguna reservación real).

Como San Diego fue seleccionado como destino, debería ver la pancarta de oferta _DJ SAM_ en la pantalla de confirmación:

![Validar Oferta de contexto: San Diego](assets/layout_context_san_diego.jpg)

Ahora seleccione **[!UICONTROL Listo]** e intente otra reserva con Los Ángeles como destino. La pantalla de confirmación debe mostrar el letrero _Universal Studios_:

![Validar Oferta de contexto - Los Ángeles](assets/layout_context_los_angeles.jpg)

## Conclusión. 

¡Felicitaciones! Esto concluye la parte principal del tutorial de SDK 4.x de Adobe Target para Android. Ahora tiene las habilidades para implementar la personalización en las aplicaciones de Android. Puede consultar esta documentación y aplicación de demostración como referencia para sus futuros proyectos.

Siguiente: El marcado de funciones es otra función que se puede implementar con Adobe Target en Android. Para obtener más información sobre el marcado de funciones, consulte la siguiente lección.

**[SIGUIENTE: Marca de función >](feature-flagging.md)**
