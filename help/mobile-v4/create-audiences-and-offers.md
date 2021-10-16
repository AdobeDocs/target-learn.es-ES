---
title: Crear audiencias y ofertas en Adobe Target
description: 'En esta lección, creamos audiencias y ofertas en Adobe Target para las tres ubicaciones que implementamos en las lecciones anteriores. Se utilizarán para mostrar experiencias personalizadas en la siguiente lección.   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 4b153e4f-a979-49a8-8c26-f7ac95162a2f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 1%

---

# Crear audiencias y ofertas en Adobe Target

En esta lección, entraremos en la interfaz [!DNL Target] y crearemos audiencias y ofertas para las tres ubicaciones que implementamos en las lecciones anteriores.

## Objetivos de aprendizaje

Al final de esta lección, podrá:

* Cree audiencias en Adobe Target
* Crear ofertas en Adobe Target

Más específicamente, en esta lección crearemos audiencias y ofertas necesarias para lograr los casos de uso de personalización definidos al principio del tutorial. Queremos usar las pantallas de inicio y búsqueda para ayudar a los usuarios de la aplicación a reservar sus viajes. Queremos usar la pantalla de agradecimiento para mostrar algunas promociones relevantes basadas en el destino del usuario. Esta es una tabla que representa lo que vamos a crear en esta lección para cada ubicación:

| Ubicación | Audiencia | Oferta |
| --- | --- | --- |
| wetravel_engagement_home | Nuevos usuarios de aplicaciones móviles | &quot;Seleccione su origen y destino para buscar rutas de bus disponibles&quot; |
| wetravel_engagement_search | Nuevos usuarios de aplicaciones móviles | &quot;Utilice filtros para reducir los resultados de búsqueda&quot; |
| wetravel_engagement_home | Devolución de usuarios de aplicaciones móviles | &quot;¡Bienvenido de nuevo! Utilice el código promocional BACK30 durante el cierre de compra para obtener un descuento del 10 %&quot;. |
| wetravel_engagement_search | Devolución de usuarios de aplicaciones móviles | contenido predeterminado |
| wetravel_context_dest | Destino: San Diego | &quot;DJ&quot; |
| wetravel_context_dest | Destino: Los Ángeles | &quot;Universal&quot; |

## Seleccionar el espacio de trabajo

Si su empresa utiliza Propiedades y Espacios de trabajo para establecer límites para personalizar aplicaciones y sitios web (y ha implementado el parámetro at_property en la última lección), primero debe asegurarse de que está en el espacio de trabajo correcto antes de continuar con esta lección. Si no utiliza Propiedades y espacios de trabajo, ignore este paso. Seleccione el espacio de trabajo que utilizó en la lección anterior para copiar el valor at_property :

![Ejemplo de Workspace](assets/workspace.jpg)

## Crear audiencias

Ahora vamos a crear las audiencias que vamos a usar para personalizar la aplicación.

### Crear una audiencia para nuevos usuarios

Las audiencias de Adobe Target se utilizan para identificar grupos específicos de visitantes. Las ofertas se pueden dirigir a esos grupos específicos. Para las dos primeras ubicaciones, utilizaremos una audiencia &quot;Nuevos usuarios&quot;:

1. Haga clic en **[!UICONTROL Audiencias]** en el panel de navegación superior.
1. Haga clic en el botón **[!UICONTROL Crear audiencia]**.
   ![Crear una audiencia de usuario nueva](assets/audience_new_mobile_app_users_1.jpg)

1. Escriba **[!UICONTROL Nuevos usuarios de aplicaciones móviles]** como nombre de audiencia.
1. Seleccione **[!UICONTROL Agregar regla]**.
1. Seleccione una regla **[!UICONTROL Personalizada]**.
   ![Crear una audiencia de usuario nueva](assets/audience_new_mobile_app_users_2.jpg)

1. Seleccione **[!UICONTROL a.Launches]**.
1. Seleccionar **[!UICONTROL es menor que]**.
1. Introduzca **5**.
1. Guarde la nueva audiencia.
   ![Crear una audiencia de usuario nueva](assets/audience_new_mobile_app_users_3.jpg)

### Crear una audiencia para usuarios que regresan

Siga los mismos pasos que se detallan arriba para crear una audiencia para los usuarios que regresan.

1. Asigne un nombre a la audiencia _Usuarios de aplicaciones móviles que regresan_.
1. Usar **[!UICONTROL a.Launches es bueno o igual a 5]** como regla personalizada.
1. Guarde la nueva audiencia.

   ![Crear una audiencia de usuario que regresa](assets/audience_returning_mobile_app_users.jpg)

>[!NOTE]
>
>Todas las métricas y dimensiones del ciclo vital recopiladas en el SDK móvil [!DNL Target] van precedidas de &quot;a&quot; (por ejemplo, a.Launches) y están disponibles en la opción &quot;Personalizado&quot; del menú desplegable y se pueden utilizar para crear audiencias.

### Crear una audiencia para los usuarios que reserven un viaje a San Diego

A continuación, crearemos algunas audiencias para algunos de los destinos ofrecidos por la aplicación We.Travel . En la última lección, pasamos el destino como parámetro de ubicación en la solicitud de ubicación wetravel_context_dest . Ese parámetro está disponible en la opción &quot;Personalizado&quot; del menú desplegable.

>[!NOTE]
>
>Si un parámetro que espera ver en la lista desplegable Personalizado no aparece en la interfaz [!DNL Target], verifique que se esté pasando en la solicitud. Si ha comprobado que está en la solicitud, pero no se ha cargado de forma diferida en la interfaz [!DNL Target], solo puede escribir el nombre del parámetro y pulsar Enter para continuar definiendo la audiencia

1. Asigne un nombre a la audiencia _Destination: San Diego_.
1. Utilice una regla personalizada con esta definición: _locationDest contiene San Diego_.
1. Guarde la nueva audiencia.

   ![Crear audiencia de &quot;San Diego&quot;](assets/audience_locationDest_san_diego.jpg)

### Crear una audiencia para los usuarios que reserven un viaje a Los Ángeles

1. Asigne un nombre a la audiencia _Destination: Los Ángeles_
1. Utilice una regla personalizada con esta definición: _locationDest contiene Los Ángeles_
1. Guarde la nueva audiencia.

![Crear audiencia de &quot;Los Ángeles&quot;](assets/audience_locationDest_los_angeles.jpg)

## Creación de ofertas

Ahora, vamos a crear ofertas para mostrar estos mensajes. Como recordatorio, las ofertas son fragmentos de código/contenido que se entregan en la respuesta [!DNL Target]. Normalmente se crean en la interfaz de usuario [!DNL Target], pero también se pueden crear mediante API o utilizando la integración de fragmentos de experiencias con Adobe Experience Manager. En las aplicaciones móviles, las ofertas JSON son comunes. En este tutorial, se utilizan ofertas de HTML, que se pueden utilizar para enviar contenido de texto sin formato (incluido JSON) a la aplicación.

### Creación de la oferta para nuevos usuarios

En primer lugar, vamos a crear ofertas para los mensajes a Nuevos usuarios:

1. Haga clic en **[!UICONTROL Ofertas]** en la barra de navegación superior.
1. Haga clic en **[!UICONTROL Crear]**.
1. Seleccione **[!UICONTROL Oferta de HTML]**.

   ![Crear oferta principal](assets/offer_home_1.jpg)

1. Asigne un nombre a la oferta _Home: Participación de nuevos usuarios_.
1. Introduzca _Seleccione Origen y Destino para buscar los buses disponibles_ como código.
1. Guarde la nueva oferta.

   ![Crear oferta de HTML principal](assets/offer_home_2.jpg)

### Creación de la oferta para usuarios que regresan

Ahora vamos a crear la oferta única para usuarios que regresan (la segunda oferta será contenido predeterminado, que se mostrará como nada):

1. Asigne un nombre a la oferta _Home: Devolver usuarios_.
1. Introduzca _Bienvenido de nuevo! Utilice el código promocional BACK30 durante el cierre de compra para obtener un descuento del 10 %._ como código de HTML.
1. Guarde la nueva oferta.

   ![Crear oferta de HTML principal](assets/offer_home_returning_users.jpg)

### Creación de la oferta de San Diego

Cuando se devuelve &quot;DJ&quot; a la actividad de agradecimiento, la lógica de la función filterRecommendationsBasedOnOffer() mostrará un banner para &quot;Rock Night with DJ SAM&quot;:

1. Asigne un nombre a la oferta _Promoción para San Diego_.
1. Introduzca _DJ_ como código de HTML.
1. Guarde la nueva oferta.

![Crear oferta &quot;San Diego&quot;](assets/offer_san_diego.jpg)

### Creación de una oferta para usuarios que vayan a Los Ángeles

Cuando se devuelve &quot;Universal&quot; a la actividad de agradecimiento, la lógica de la función filterRecommendationsBasedOnOffer() mostrará un banner para &quot;Universal Studios&quot;:

1. Asigne un nombre a la oferta _Promoción para Los Ángeles_.
1. Introduzca _Universal_ como código de HTML.
1. Guarde la nueva oferta.

![Crear oferta &quot;Los Ángeles&quot;](assets/offer_los_angeles.jpg)

## Conclusión. 

Ahora tenemos nuestras Audiencias y Ofertas. En la siguiente lección, crearemos actividades que vinculen las ubicaciones, audiencias y ofertas para crear experiencias personalizadas.

**[SIGUIENTE : &quot;Personalizar diseños&quot; >](personalize-layouts.md)**
