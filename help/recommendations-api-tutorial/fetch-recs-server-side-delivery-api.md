---
title: Recuperación de Recommendations con la API de Envío
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations incluye un conjunto dedicado de API que le permiten administrar su catálogo de productos y/o contenido recomendables; administrar los algoritmos y campañas de las recomendaciones; y envíe recomendaciones en objetos JSON, HTML o XML para que se muestren en web, móviles, de correo electrónico, IOT y otros canales.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: c221f434ce9daec03dbb4d897343775b40b14462
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 0%

---


# Obteniendo [!DNL Recommendations] con la API de Envío

Las API [!DNL Recommendations] de Adobe Target y Adobe Target se pueden utilizar para ofrecer respuestas a páginas web, pero también se pueden utilizar en experiencias no basadas en HTML, como aplicaciones, pantallas, consolas, correos electrónicos, kioscos y otros dispositivos de visualización. En otras palabras, cuando [!DNL Target] bibliotecas y JavaScript no se pueden usar, la **[!DNL Target]API de Envío** aún nos permite acceder a toda la gama de funcionalidades [!DNL Target] para ofrecer experiencias personalizadas.

>[!NOTE]
>
> Cuando solicite contenido que contenga recomendaciones reales (productos o artículos recomendados), utilice la API de Envío [!DNL Target].

Para recuperar recomendaciones, envíe una llamada de POST de la API de Adobe Target Envío con la información contextual adecuada, que puede incluir un ID de usuario (para su uso con recomendaciones específicas de perfil como los artículos vistos recientemente por el usuario), el nombre del mbox relevante, los parámetros de mbox, los parámetros de perfil u otros atributos. La respuesta incluirá entity.ids recomendado (y puede incluir otros datos de entidad) en formato JSON o HTML, que se pueden mostrar en el dispositivo.

La [API de Envío](https://developers.adobetarget.com/api/delivery-api/) para Adobe Target expone todas las funciones existentes que proporciona una solicitud estándar [!DNL Target].

>[!NOTE]
>La API de Envío:
>* Permite recuperar experiencias o ofertas para una ubicación y una audiencia de una manera RESTful.
>* No requiere autenticación.
>* Solo POST.
>* No procesa las cookies ni las llamadas de redirección.
>* No requiere ni reconoce &quot;funciones de usuario&quot;. Simplemente captura contenido o informa eventos a [!DNL Target] servidores Edge.


Para utilizar la API de Envío para ofrecer [!DNL Target] experiencias, incluidas las recomendaciones, siga estos pasos:

1. Cree una actividad [!DNL Target] (A/B, XT, AP o [!DNL Recommendations]) mediante el Compositor basado en formularios (no el Compositor de experiencias visuales).
2. Utilice la API de Envío para obtener una respuesta a las solicitudes generadas por la actividad [!DNL Target] que acaba de crear.

<!-- Q: Why are BOTH steps necessary for this? If you have a Form-based recommendation defined for an mbox, what's the point/benefit of ALSO having the Delivery API step in to retrieve results? Why can't you just have the Form-based Rec deliver the results in the destination device...?? A: See use case below... it's when you want to "intercept" the pending results in order to do more stuff prior to displaying the results. Things like real-time comparisons to inventory levels. -->

## Creación de una recomendación mediante el Compositor de experiencias basadas en formularios

Para crear recomendaciones que se puedan utilizar con la API de Envío, utilice el [Compositor basado en formularios](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html).

1. En primer lugar, cree y guarde un diseño basado en JSON para utilizarlo en la recomendación. Para obtener JSON de muestra, además de información general sobre cómo se pueden devolver las respuestas JSON al configurar una actividad basada en formularios, consulte la documentación sobre [Creación de diseños de recomendación](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-design/create-design.html). En este ejemplo, el diseño se denomina *JSON simple.*

   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

2. En [!DNL Target], vaya a **[!UICONTROL Actividades] > [!UICONTROL Crear Actividad] > [!UICONTROL Recommendations]** y, a continuación, seleccione **[!UICONTROL Formulario]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

3. Seleccione una propiedad y haga clic en **[!UICONTROL Siguiente]**.
4. Defina la ubicación en la que desea que los usuarios reciban la respuesta de la recomendación. El ejemplo siguiente utiliza una ubicación denominada *api_charter*. Seleccione el diseño basado en JSON, creado anteriormente con el nombre *JSON simple.*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
5. Guarde y active la recomendación. Generará resultados. [Una vez que los resultados estén listos](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html), puede utilizar la API de Envío para recuperarlos.

## Uso de la API de Envío

La sintaxis de la [API de Envío](https://developers.adobetarget.com/api/delivery-api/#tag/Delivery-API) es:

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. Tenga en cuenta que se requiere el código de cliente. Como recordatorio, el código de cliente se puede encontrar en Adobe Target navegando a **[!UICONTROL Recommendations] > [!UICONTROL Configuración]**. Observe el valor **[!UICONTROL Client Code]** en la sección **[!UICONTROL Token de API de recomendación]**.
   ![client-code.png](assets/client-code.png)
1. Una vez que tenga el código de cliente, cree la llamada de API de Envío. El ejemplo siguiente comienza con la **[!UICONTROL Llamada de API de Envío de mboxes Web en lote]** proporcionada en la [colección de Postman de API de Envío](https://developers.adobetarget.com/api/delivery-api/#section/Getting-Started/Postman-Collection), con las modificaciones pertinentes. Por ejemplo:
   * los objetos **browser** y **address** se eliminaron del **Body**, ya que no son necesarios en casos de uso que no sean HTML
   * *api_* charteris aparece como el nombre de la ubicación en este ejemplo
   * se especifica entity.id, ya que esta recomendación se basa en la Similitud de contenido, que requiere que se pase una clave de elemento actual a [!DNL Target].
      ![server-side-Envío-API-call.](assets/server-side-delivery-api-call2.png)
pngRecuerde configurar correctamente los parámetros de consulta. Por ejemplo, asegúrese de especificar 
`{{CLIENT_CODE}}` según sea necesario. <!--Q: In the updated call syntax, entity.id is listed as a profileParameter instead of an mboxParameter as in older versions. --> <!--Q: Old image ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) Old accompanying text: "Note this recommendation is based on Content Similar products based on the entity.id sent via mboxParameters." -->
      ![client-code3](assets/client-code3.png)
1. Envíe la solicitud. Esto se ejecuta en la ubicación *api_charter*, que tiene una recomendación activa ejecutándose en ella, definida con el diseño JSON que generará una lista de las entidades recomendadas.
1. Reciba una respuesta basada en el diseño JSON.
   ![server-side-create-recs-json-response2.](assets/server-side-create-recs-json-response2.png)
pngLa respuesta incluye el ID de clave, así como los ID de entidad de las entidades recomendadas.

El uso de la API de Envío con [!DNL Recommendations] permite realizar pasos adicionales antes de mostrar las recomendaciones al visitante en el dispositivo que no es HTML. Por ejemplo, puede tomar la respuesta de la API de Envío para realizar una búsqueda adicional en tiempo real de los detalles de atributos de entidad (inventario, precio, clasificación, etc.) desde otro sistema (como una plataforma CMS, PIM o de comercio electrónico), antes de mostrar los resultados finales.

Con el método descrito en este tutorial, puede obtener cualquier aplicación para aprovechar la respuesta de [!DNL Target] para proporcionar recomendaciones personalizadas.

## Ejemplos de implementaciones

Los siguientes recursos proporcionan ejemplos de varias implementaciones no centradas en HTML. Tenga en cuenta que cada implementación será única, debido al sistema y los dispositivos involucrados.

| Recurso | Detalles |
| --- | --- |
| [Consumo de API de RESTful en AEM](https://helpx.adobe.com/experience-manager/using/restful-services.html) | Cómo crear e implementar un paquete OSGi de Adobe Experience Manager que consume datos de un servicio web RESTful de terceros. |
| [Adobe Target en todas partes: implemente el servidor o en la IoT](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit 2019 Lab que ofrece una experiencia práctica para una aplicación React que aprovecha las API del servidor de Adobe Target. |
| [Adobe Target en una aplicación móvil sin el SDK de Adobe](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | Esta guía le muestra cómo configurar Adobe Target en su aplicación móvil sin instalar el SDK de Adobe. Esta solución utiliza la vista web del SDK de Tealium y el módulo Comandos remotos para enviar y recibir solicitudes a la API de Adobe Visitante (Experience Cloud) y a la API de Adobe Target. |
| [Funcionamiento de Adobe Target en aplicaciones móviles](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html) | Cómo [!DNL Target] funciona con el SDK de Mobile |
| [Configuración  [!DNL Target] extension in Experience Platform Launch and Implementing [!DNL Target] de las API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target) | Pasos para configurar la extensión [!DNL Target] en Experience Platform Launch, agregar la extensión [!DNL Target] a la aplicación e implementar las API [!DNL Target] para solicitar actividades, recuperar ofertas y entrar al modo de previsualización visual. |
| [Adobe Target Node Client](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | SDK de Node.js v1.0 de origen abierto [!DNL Target] |
| [Información general del servidor](https://docs.adobe.com/content/help/en/target/using/implement-target/server-side/api-and-sdk-overview.html) | Información sobre las API de Adobe Target Server Side envío, las API de Envío por lotes del servidor, el SDK de Node.js y las API de Adobe Target [!DNL Recommendations]. |
| [Adobe Campaign Content Recommendations en correo electrónico](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | Blog que describe cómo aprovechar las recomendaciones de contenido en el correo electrónico a través de Adobe Target y Adobe I/O Runtime en Adobe Campaign. |

## Administración de la configuración [!DNL Recommendations] con API

La mayoría de las veces, las recomendaciones se configuran en la interfaz de usuario de Adobe Target y luego se utilizan o se accede a ellas a través de las API [!DNL Target], por motivos como los mencionados en las secciones anteriores. Esta coordinación UI-API es común. Sin embargo, a veces es posible que los usuarios deseen realizar todas las acciones a través de las API, tanto la configuración como el uso de los resultados. Aunque es mucho menos común, los usuarios pueden configurar, ejecutar, *y* aprovechar por completo los resultados de las recomendaciones usando las API.

Hemos aprendido en una [sección anterior](manage-catalog.md) cómo administrar las entidades de Adobe Target Recommendations y proporcionarlas en el servidor. Del mismo modo, Adobe I/O le permite administrar criterios, promociones, colecciones y plantillas de diseño sin tener que iniciar sesión en Adobe Target. Se puede encontrar una lista completa de todas las [!DNL Recommendations] API [aquí](http://developers.adobetarget.com/api/recommendations/), pero aquí hay un resumen para consulta.

| Recurso | Detalles |
| --- | --- |
| [Colecciones](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | Lista, creación, obtención, edición y eliminación de colecciones. |
| [Criterios](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | Lista y obtención de criterios. |
| [Diseños](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | Lista, creación, obtención, edición, eliminación y validación de diseños. |
| [Entidades](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | Guarde, elimine y obtenga entidades. |
| [Promociones](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | Lista, creación, obtención, edición y eliminación de promociones. |
| [Criterios de categoría](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | Lista, creación, obtención, edición y eliminación de criterios de categoría. |
| [Criterios personalizados](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | Lista, creación, obtención, edición y eliminación de criterios personalizados. |
| [Criterios de elemento](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | Lista, creación, obtención, edición y eliminación de criterios de elementos. |
| [Criterios de popularidad](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | Lista, creación, obtención, edición y eliminación de criterios de popularidad. |
| [Criterios de atributo de perfil](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | Lista, creación, obtención, edición y eliminación de criterios de atributos de perfil. |
| [Criterios recientes](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | Lista, creación, obtención, edición y eliminación de criterios recientes. |
| [Criterios de secuencia](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | Lista, creación, obtención, edición y eliminación de criterios de secuencia. |

## Documentación de referencia

* [Documentación de la API de Adobe Target](https://developers.adobetarget.com/api/#getting-started)
* [Adobe Target Envío API](https://developers.adobetarget.com/api/delivery-api/)
* [ [!DNL Recommendations] Integración con correo electrónico](https://docs.adobe.com/content/help/en/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## Resumen y revisión

¡Felicitaciones! Al finalizar este tutorial, ha aprendido a:
* [Administrar el catálogo mediante la API de Recommendations](manage-catalog.md)
* [Administrar criterios personalizados mediante la API de Recommendations](manage-custom-criteria.md)
* [Uso de la API de Envío con Recommendations](fetch-recs-server-side-delivery-api.md)
