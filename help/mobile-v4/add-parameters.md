---
title: Añadir parámetros a las solicitudes
description: En esta lección, agregaremos métricas del ciclo vital de Adobe y parámetros personalizados a las solicitudes de Destinatario agregadas en la lección anterior. Estas métricas y parámetros se utilizarán para crear audiencias personalizadas más adelante en el tutorial.
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# Añadir parámetros a las solicitudes

En esta lección, agregaremos métricas del ciclo vital de Adobe y parámetros personalizados a las [!DNL Target] solicitudes agregadas en la lección anterior. Estas métricas y parámetros se utilizarán para crear audiencias personalizadas más adelante en el tutorial.

## Objetivos de aprendizaje

Al final de esta lección, podrá:

* Añadir las métricas del ciclo vital de Adobe Mobile
* Añadir parámetros a una solicitud de recuperación previa
* Añadir parámetros a una ubicación activa
* Validar los parámetros de ambas solicitudes

## Añadir los parámetros del ciclo vital

Habilitemos las métricas [del ciclo vital móvil de](https://docs.adobe.com/content/help/en/mobile-services/android/metrics.html)Adobe. Esto agregará parámetros a las solicitudes de ubicación que contengan información completa sobre el dispositivo del usuario y la participación en la aplicación. Generaremos audiencias en la siguiente lección utilizando los datos que proporciona la solicitud del ciclo vital.

Para habilitar las métricas del ciclo vital, abra de nuevo el controlador HomeActivity y agregue `Config.collectLifecycleData(this);` a la función onResume():

![Solicitud de ciclo de vida](assets/lifecycle_code.jpg)

### Validar los parámetros del ciclo vital para la solicitud de recuperación previa

Ejecute el emulador y utilice Logcat para validar los parámetros del ciclo vital. Filtre &quot;prefetch&quot; para buscar la respuesta de recuperación previa y buscar los nuevos parámetros:
![Validación del ciclo de vida](assets/lifecycle_validation.jpg)

Aunque solo hemos agregado `Config.collectLifecycleData()` al controlador HomeActivity, también debería ver las métricas del ciclo vital enviadas con la solicitud de Destinatario en la pantalla de agradecimiento.

## Añadir el parámetro at_property en la solicitud de recuperación previa

Las propiedades de Adobe Target se definen en la [!DNL Target] interfaz y se utilizan para definir límites para personalizar aplicaciones y sitios web. El parámetro at_property identifica la propiedad específica en la que se accede a sus ofertas y actividades y se mantienen. Añadiremos una propiedad a las solicitudes de recuperación previa y de ubicación activa.

>[!NOTE] Puede que vea o no las opciones de Propiedades en la [!DNL Target] interfaz, según su licencia. Si no tiene estas opciones, o si no utiliza Propiedades en la compañía, vaya a la siguiente sección de esta lección.

Puede recuperar el valor de at_property en la [!DNL Target] interfaz en [!UICONTROL Configuración] > [!UICONTROL Propiedades].  Pase el ratón sobre la propiedad, seleccione el icono de fragmento de código y copie el `at_property` valor:

![Copiar at_property](assets/at_property_interface.jpg)

Añada como parámetro para cada ubicación en la solicitud de recuperación previa de este modo:
![Añadir parámetro](assets/params_at_property.jpg)at_propertyEste es el código actualizado de la `targetPrefetchContent()` función (asegúrese de actualizar el _[!UICONTROL valor de at_property aquí]_texto de marcador de posición):

```java
public void targetPrefetchContent() {
        List<TargetPrefetchObject> prefetchList = new ArrayList<>();

        Map<String, Object> params1;
        params1 = new HashMap<String, Object>();
        params1.put("at_property", "your at_property value goes here");

        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
        prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
        Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
            @Override
            public void call(final Boolean status) {
                HomeActivity.this.runOnUiThread(new Runnable() {
                    @Override
                    public void run() {
                        String cachingStatus = status ? "YES" : "NO";
                        System.out.println("Received Response from prefetch : " + cachingStatus);
                        engageMessage();
                        setUp();

                    }
                });
            }};
        Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
    }
```

### Nota sobre los parámetros

Para futuros proyectos, es posible que desee implementar parámetros adicionales. El `createTargetPrefetchObject()` método permite tres tipos de parámetros: `locationParams`, `orderParams`, y `productParams`. Consulte la documentación para obtener [más detalles sobre cómo agregar estos parámetros a la solicitud](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html)de recuperación previa.

Además, tenga en cuenta que se pueden agregar diferentes parámetros de ubicación a cada ubicación en la solicitud de recuperación previa. Por ejemplo, puede crear otro mapa llamado param2, colocar un nuevo parámetro en él y luego configurar param2 en una ubicación y param1 con la otra ubicación. A continuación se muestra un ejemplo:

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## Validar el parámetro at_property en la solicitud de recuperación previa

A continuación, ejecute el emulador y utilice Logcat para comprobar que at_property se muestra en la solicitud de recuperación previa y en la respuesta para ambas ubicaciones:
![Validar el parámetro at_property](assets/parameters_at_property_validation.jpg)

## Añadir parámetros personalizados a la solicitud de ubicación activa

La solicitud de ubicación activa (wetravel_context_dest) se agregó en la lección anterior para que pudiéramos mostrar una promoción relevante en la pantalla de confirmación final del proceso de reservación. Nos gustaría personalizar la promoción en función del destino del usuario y para ello agregaremos eso como parámetro a la solicitud. También agregaremos un parámetro para el origen trop y el valor at_property.

Añada los siguientes parámetros a la función targetLoadRequest() en el controlador de actividades de agradecimiento:
![Añadir parámetros a la solicitud](assets/parameters_live_location.jpg)de ubicación activaEste es el código actualizado de la función targetLoadRequest() (asegúrese de actualizar el texto del marcador de posición &quot;agregar el valor de at_property aquí&quot;):

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Map<String, Object> locationParams = new HashMap<>();
    locationParams.put("at_property","add your at_property value here");
    locationParams.put("locationSrc", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.departure,"")));
    locationParams.put("locationDest", (""+Utility.getInSharedPreference(ThankYouActivity.this,Constant.destination,"")));

    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, locationParams, new Target.TargetCallback<String>() {
        @Override
        public void call(final String response) {
        try {
            runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    AppDialogs.dialogLoaderHide();
                    filterRecommendationBasedOnOffer(recommandations, response);
                    recommandationbAdapter.notifyDataSetChanged();
                }
            });
        } catch (Exception e) {
            e.printStackTrace();
        }
        }
    });
    Target.clearPrefetchCache();
}
```

### Validar los parámetros personalizados en la solicitud de ubicación activa

Ejecute el emulador y abra Logcat. Filtre uno de los parámetros para comprobar que la solicitud contiene los parámetros necesarios:
![Validar los parámetros personalizados en la solicitud de ubicación activa](assets/parameters_live_location_validation.jpg)

>[!NOTE] Solicitudes y parámetros de confirmación de pedido: Aunque no se utiliza en este proyecto de demostración, los detalles de los pedidos generalmente se capturan en una implementación real, por lo que [!DNL Target] pueden utilizar los detalles de los pedidos como métricas y dimensiones. Consulte la documentación para obtener instrucciones sobre cómo [implementar la solicitud de confirmación de pedido y los parámetros](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-target-methods.html).

>[!NOTE] Analytics para Destinatario (A4T): Adobe Analytics se puede configurar como fuente de sistema de informes para [!DNL Target]. Esto permite que todas las métricas y dimensiones recopiladas por el SDK de Destinatario se vean en Adobe Analytics. Consulte la Descripción general [de](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html) A4T para obtener más información.

¡Buen trabajo! Ahora que los parámetros están establecidos, estamos listos para usar esos parámetros para crear audiencias y ofertas en Adobe Target.

**[SIGUIENTE: &quot;Crear Audiencias y Ofertas&quot; >](create-audiences-and-offers.md)**
