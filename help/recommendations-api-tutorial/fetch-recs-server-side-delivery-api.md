---
title: Cómo recuperar Recommendations con la API de envío
description: Esta parte del tutorial guía a los desarrolladores por los pasos necesarios para recuperar contenido de Recommendations mediante la API de envío de Adobe Target.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 553d1208-647f-479d-acc7-d7760469d642
source-git-commit: cee2618bb92284da1f82d108a0aff0d39340a15b
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 1%

---

# Recuperación [!DNL Recommendations] con la API de envío

Adobe Target y Adobe Target [!DNL Recommendations] Las API se pueden utilizar para enviar respuestas a páginas web, pero también se pueden utilizar en experiencias que no estén basadas en HTML, como aplicaciones, pantallas, consolas, correos electrónicos, kioscos y otros dispositivos de visualización. En otras palabras, cuando [!DNL Target] no se pueden usar las bibliotecas ni JavaScript, la variable **[!DNL Target]API de envío** todavía nos permite acceder a toda la gama de [!DNL Target] para ofrecer experiencias personalizadas.

>[!NOTE]
>
> Cuando solicite contenido que contenga recomendaciones reales (productos o artículos recomendados), use la variable [!DNL Target] API de envío.

Para recuperar las recomendaciones, envíe una llamada de POST de la API de envío de Adobe Target con la información contextual adecuada, que puede incluir un ID de usuario (para su uso con recomendaciones específicas del perfil, como los artículos vistos recientemente por el usuario), el nombre de mbox pertinente, parámetros de mbox, parámetros de perfil u otros atributos. La respuesta incluirá entity.ids recomendado (y puede incluir otros datos de entidad) en formato JSON o HTML, que luego se pueden mostrar en el dispositivo.

La variable [API de envío](https://developer.adobe.com/target/implement/delivery-api/){target=&quot;_blank&quot;} para Adobe Target expone todas las funciones existentes que un estándar [!DNL Target] proporciona la solicitud.

>[!NOTE]
>La API de envío:
>* Permite recuperar experiencias u ofertas para una ubicación y una audiencia de forma RESTful.
>* No requiere autenticación.
>* Solo POST.
>* No procesa cookies ni redirige llamadas.
>* No requiere ni reconoce &quot;funciones de usuario&quot;. Simplemente busca contenido o informes de eventos a [!DNL Target] servidores Edge.


Para utilizar la API de envío para enviar [!DNL Target] las experiencias (incluidas las recomendaciones) siguen estos pasos:

1. Cree un [!DNL Target] actividad (A/B, XT, AP o [!DNL Recommendations]) mediante el Compositor basado en formularios (no el Compositor de experiencias visuales).
2. Utilice la API de envío para obtener una respuesta a las solicitudes generadas por la variable [!DNL Target] actividad que acaba de crear.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Crear una recomendación con el Compositor de experiencias basadas en formularios

Para crear recomendaciones que se puedan usar con la API de envío, use la variable [Compositor basado en formularios](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en).

1. En primer lugar, cree y guarde un diseño basado en JSON para utilizarlo en su recomendación. Para obtener JSON de muestra, además de información general sobre cómo se pueden devolver las respuestas JSON al configurar una actividad basada en formularios, consulte la documentación de [Creación de diseños de recomendación](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html?lang=en). En este ejemplo, el diseño tiene el nombre *JSON simple.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. En [!DNL Target], vaya a **[!UICONTROL Actividades] > [!UICONTROL Crear actividad] > [!UICONTROL Recommendations]** y, a continuación, seleccione **[!UICONTROL Formulario]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. Seleccione una propiedad y haga clic en **[!UICONTROL Siguiente]**.
4. Defina la ubicación en la que desea que los usuarios reciban la respuesta de la recomendación. El ejemplo siguiente utiliza una ubicación denominada *api_charter*. Seleccione su diseño basado en JSON, creado anteriormente, con nombre *JSON simple.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Guarde y active la recomendación. Generará resultados. [Una vez que los resultados estén listos](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html?lang=en), puede utilizar la API de envío para recuperarlas.

## Usar la API de envío

La sintaxis de la variable [API de envío](https://developer.adobe.com/target/implement/delivery-api/#tag/Delivery-API){target=&quot;_blank&quot;} es:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Tenga en cuenta que se requiere el código de cliente. Como recordatorio, es posible que el código de cliente se encuentre en Adobe Target navegando hasta **[!UICONTROL Recommendations] > [!UICONTROL Configuración]**. Tenga en cuenta que **[!UICONTROL Código de cliente]** en la variable **[!UICONTROL Token de la API de recomendación]** para obtener más información.
   ![client-code.png](assets/client-code.png)
1. Una vez que tenga el código de cliente, construya la llamada a la API de envío. El ejemplo siguiente comienza con el **[!UICONTROL Llamada de API de envío de mboxes por lotes web]** en el [Recopilación de Postman de API de envío](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection), haciendo las modificaciones pertinentes. Por ejemplo:
   * el **explorador** y **address** los objetos se quitaron de la variable **Cuerpo**, ya que no son necesarios para casos de uso que no sean de HTML
   * *api_charter* aparece como el nombre de la ubicación en este ejemplo
   * se especifica entity.id , ya que esta recomendación se basa en Similitud de contenido, que requiere que se pase una clave de artículo actual a [!DNL Target].
      ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)
Recuerde configurar los parámetros de consulta correctamente. Por ejemplo, asegúrese de especificar 
`{{CLIENT_CODE}}` según sea necesario. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Envíe la solicitud. Esto se ejecuta en el *api_charter* ubicación, que tiene una recomendación activa ejecutándose en ella, definida con su diseño JSON que mostrará una lista de entidades recomendadas.
1. Reciba una respuesta basada en el diseño JSON.
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
La respuesta incluye el ID de clave, así como los ID de entidad de las entidades recomendadas.

Uso de la API de envío con [!DNL Recommendations] de este modo, puede realizar pasos adicionales antes de mostrar las recomendaciones al visitante en el dispositivo que no sea de HTML. Por ejemplo, puede tomar la respuesta de la API de envío para realizar una búsqueda adicional en tiempo real de los detalles de atributos de entidad (inventario, precio, clasificación, etc.) desde otro sistema (como un CMS, un PIM o una plataforma de comercio electrónico) antes de mostrar los resultados finales.

Con el método descrito en este tutorial, puede obtener cualquier aplicación para aprovechar la respuesta de [!DNL Target] para proporcionar recomendaciones personalizadas.

## Ejemplos de implementaciones

En los siguientes recursos se proporcionan ejemplos de varias implementaciones no centradas en el HTML. Tenga en cuenta que cada implementación será única, debido al sistema y a los dispositivos involucrados.

| Recurso | Detalles |
| --- | --- |
| [Adobe Target en todas partes: implementación del lado del servidor o en IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab que proporciona experiencia práctica para una aplicación React que aprovecha las API del lado del servidor de Adobe Target. |
| [Adobe Target en una aplicación móvil sin el SDK de Adobe](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Esta guía le muestra cómo configurar Adobe Target en su aplicación móvil sin instalar el SDK de Adobe. Esta solución utiliza la vista web del SDK de Tealium y el módulo Comandos remotos para enviar y recibir solicitudes a la API de visitante de Adobe (Experience Cloud) y a la API de Adobe Target. |
| [Cómo funciona Adobe Target en las aplicaciones móviles](https://experienceleague.adobe.com/docs/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html?lang=en) | Cómo [!DNL Target] funciona con el SDK de Mobile |
| [Configuración de la variable [!DNL Target] extensión en Experience Platform Launch e implementación [!DNL Target] API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Pasos para configurar la variable [!DNL Target] en el Experience Platform Launch, agregando la variable [!DNL Target] Extensión a la aplicación e implementación [!DNL Target] API para solicitar actividades, ofertas de recuperación previa e introducir modo de vista previa visual. |
| [Cliente de nodo de Adobe Target](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | De código abierto [!DNL Target] SDK v1.0 de Node.js |
| [Información general del servidor](https://experienceleague.adobe.com/docs/target/using/implement-target/server-side/api-and-sdk-overview.html?lang=en) | Información sobre las API de envío del servidor de Adobe Target, las API de envío por lotes del servidor, el SDK de Node.js y Adobe Target [!DNL Recommendations] API. |
| [Adobe Campaign Content Recommendations en correo electrónico](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog que describe cómo aprovechar las recomendaciones de contenido en correos electrónicos a través de Adobe Target y Adobe I/O Runtime en Adobe Campaign. |

## Administración [!DNL Recommendations] Configuración con API

La mayoría de las veces, las recomendaciones se configuran en la interfaz de usuario de Adobe Target y luego se utilizan o se accede a ellas a través del [!DNL Target] por motivos como los mencionados en las secciones anteriores. Esta coordinación de la interfaz de usuario y la API es común. Sin embargo, a veces los usuarios pueden querer realizar todas las acciones a través de API, tanto de la configuración como del uso de los resultados. Aunque es mucho menos común, los usuarios pueden configurar, ejecutar, *y* aproveche los resultados de las recomendaciones completamente utilizando las API.

Aprendimos en un [sección anterior](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=&quot;_blank&quot;} cómo administrar entidades de Adobe Target Recommendations y entregarlas en el servidor. Del mismo modo, Adobe I/O le permite administrar los criterios, las promociones, las colecciones y las plantillas de diseño sin tener que iniciar sesión en Adobe Target. Una lista completa de todos [!DNL Recommendations] Se pueden encontrar las API [here](https://developers.adobetarget.com/api/recommendations/), pero aquí tiene un resumen de referencia.

| Recurso | Detalles |
| --- | --- |
| [Colecciones](https://developers.adobetarget.com/api/recommendations/#tag/Collections) | Enumerar, crear, obtener, editar y eliminar colecciones. |
| [Criterios](https://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Enumerar y obtener criterios. |
| [Diseños](https://developers.adobetarget.com/api/recommendations/#tag/Designs) | Enumerar, crear, obtener, editar, eliminar y validar diseños. |
| [Entidades](https://developers.adobetarget.com/api/recommendations/#tag/Entities) | Guarde, elimine y obtenga entidades. |
| [Promociones](https://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Enumerar, crear, obtener, editar y eliminar promociones. |
| [Criterios de categoría](https://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Enumerar, crear, obtener, editar y eliminar criterios de categoría. |
| [Criterios personalizados](https://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Enumerar, crear, obtener, editar y eliminar criterios personalizados. |
| [Criterios de artículo](https://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Enumerar, crear, obtener, editar y eliminar criterios de elementos. |
| [Criterios de popularidad](https://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Enumerar, crear, obtener, editar y eliminar criterios de popularidad. |
| [Criterios de atributo de perfil](https://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Enumerar, crear, obtener, editar y eliminar criterios de atributos de perfil. |
| [Criterios recientes](https://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Enumerar, crear, obtener, editar y eliminar criterios recientes. |
| [Criterios de secuencia](https://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Enumerar, crear, obtener, editar y eliminar criterios de secuencia. |

## Documentación de referencia

* [Documentación de la API de administración de Adobe Target](https://developer.adobe.com/target/administer/admin-api/){target=&quot;_blank&quot;}
* [API de envío de Adobe Target](https://developer.adobe.com/target/implement/delivery-api/){target=&quot;_blank&quot;}
* [Integración de  [!DNL Recommendations]  con el correo electrónico](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Resumen y revisión

¡Felicidades! Al finalizar este tutorial, ha aprendido a:
* [Administrar el catálogo mediante la API de Recommendations](https://developer.adobe.com/target/before-administer/recs-api/manage-catalog/){target=&quot;_blank&quot;}
* [Administrar criterios personalizados mediante la API de Recommendations](https://developer.adobe.com/target/before-administer/recs-api/manage-custom-criteria/){target=&quot;_blank&quot;}
* [Uso de la API de envío con Recommendations](https://developer.adobe.com/target/before-administer/recs-api/fetch-recs-server-side-delivery-api/){target=&quot;_blank&quot;}
