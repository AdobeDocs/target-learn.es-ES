---
title: Añadir parámetros a las solicitudes
description: En esta lección, agregaremos métricas del ciclo vital de Adobe y parámetros personalizados a las solicitudes de Target agregadas en la lección anterior. Estas métricas y parámetros se utilizarán para crear audiencias personalizadas más adelante en el tutorial.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 0250e55f-a233-4060-84e1-86d1f88a6106
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 0%

---

# Añadir parámetros a las solicitudes

En esta lección agregaremos métricas del ciclo vital y parámetros personalizados de Adobe a las [!DNL Target] solicitudes agregadas en la lección anterior. Estas métricas y parámetros se utilizarán para crear audiencias personalizadas más adelante en el tutorial.

## Objetivos de aprendizaje

Al final de esta lección, podrá hacer lo siguiente:

* Añadir las métricas del ciclo vital de Adobe móvil
* Adición de parámetros a una solicitud de recuperación previa
* Añadir parámetros a una ubicación activa
* Validar los parámetros de ambas solicitudes

## Añadir los parámetros del ciclo vital

Habilitemos [las métricas del ciclo vital de Adobe Mobile](https://experienceleague.adobe.com/docs/mobile-services/android/metrics.html?lang=en). Esto añadirá parámetros a las solicitudes de ubicación que contengan información completa sobre el dispositivo del usuario y la participación con la aplicación. Generaremos audiencias en la siguiente lección utilizando los datos que proporciona la solicitud del ciclo vital.

Para habilitar las métricas del ciclo vital, vuelva a abrir el controlador HomeActivity y agregue `Config.collectLifecycleData(this);` a la función onResume():

![Solicitud de ciclo vital](assets/lifecycle_code.jpg)

### Validación de los parámetros del ciclo vital para la solicitud de recuperación previa

Ejecute el emulador y utilice Logcat para validar los parámetros del ciclo vital. Filtre por &quot;recuperación previa&quot; para encontrar la respuesta de recuperación previa y busque los nuevos parámetros:
![Validación del ciclo vital](assets/lifecycle_validation.jpg)

Aunque solo hemos agregado `Config.collectLifecycleData()` al controlador de HomeActivity, también debería ver las métricas del ciclo vital enviadas con la solicitud de Target en la pantalla de agradecimiento.

## Añadir el parámetro at_property a la solicitud de recuperación previa

Las propiedades de Adobe Target se definen en la interfaz [!DNL Target] y se utilizan para establecer límites para personalizar aplicaciones y sitios web. El parámetro at_property identifica la propiedad específica a la que se accede y mantiene a sus ofertas y actividades. Agregaremos una propiedad a las solicitudes de recuperación previa y de ubicación activa.

>[!NOTE]
>
>Puede que vea o no las opciones de Propiedades en la interfaz [!DNL Target], según la licencia. Si no tiene estas opciones o si no utiliza Propiedades en su empresa, vaya a la siguiente sección de esta lección.

Puede recuperar su valor at_property en la interfaz [!DNL Target] en [!UICONTROL Setup] > [!UICONTROL Properties].  Pase el ratón sobre la propiedad, seleccione el icono de fragmento de código y copie el valor `at_property`:

![Copiar at_property](assets/at_property_interface.jpg)

Añádalo como parámetro para cada ubicación en la solicitud de recuperación previa de esta manera:
![Agregar parámetro at_property](assets/params_at_property.jpg)
Este es el código actualizado para la función `targetPrefetchContent()` (asegúrese de actualizar el texto del marcador de posición _[!UICONTROL your at_property value goes here]_):

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

En futuros proyectos, es posible que desee implementar parámetros adicionales. El método `createTargetPrefetchObject()` permite tres tipos de parámetros: `locationParams`, `orderParams` y `productParams`. Consulte la documentación de [más detalles sobre cómo agregar estos parámetros a la solicitud de recuperación previa](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=en).

Tenga en cuenta también que se pueden agregar diferentes parámetros de ubicación a cada ubicación en la solicitud de recuperación previa. Por ejemplo, puede crear otro mapa llamado param2, ponerle un nuevo parámetro y, a continuación, establecer param2 en una ubicación y param1 en la otra ubicación. A continuación se muestra un ejemplo:

```java
prefetchList.add(Target.createTargetPrefetchObject(location1_name, params1);
prefetchList.add(Target.createTargetPrefetchObject(location2_name, params2);
```

## Validar el parámetro at_property en la solicitud de recuperación previa

Ahora ejecute el emulador y utilice Logcat para comprobar que at_property se muestra en la solicitud de recuperación previa y la respuesta de ambas ubicaciones:
![Validar el parámetro at_property](assets/parameters_at_property_validation.jpg)

## Añadir parámetros personalizados a la solicitud de ubicación activa

La solicitud de ubicación activa (wetravel_context_dest) se añadió en la lección anterior para que pudiéramos mostrar una promoción relevante en la pantalla de confirmación final del proceso de reserva. Nos gustaría personalizar la promoción según el destino del usuario y, para ello, la añadiremos como parámetro a la solicitud. También agregaremos un parámetro para el origen trop y el valor at_property.

Agregue los siguientes parámetros a la función targetLoadRequest() en el controlador thankYouActivity:
![Agregar parámetros a la solicitud de ubicación de Live](assets/parameters_live_location.jpg)
Este es el código actualizado para la función targetLoadRequest() (asegúrese de actualizar el texto del marcador de posición &quot;agregue su valor at_property aquí&quot;):

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

### Validación de los parámetros personalizados en la solicitud de ubicación activa

Ejecute el emulador y abra Logcat. Filtre por uno de los parámetros para comprobar que la solicitud contiene los parámetros necesarios:
![Validar los parámetros personalizados en la solicitud de ubicación de Live](assets/parameters_live_location_validation.jpg)

>[!NOTE]
>
>Parámetros y solicitudes de confirmación de pedido: aunque no se usan en este proyecto de demostración, los detalles de pedido generalmente se capturan en una implementación real, de modo que [!DNL Target] puede usar detalles de pedido como métricas/dimensiones. Consulte la documentación para obtener instrucciones sobre cómo [implementar la solicitud de confirmación de pedido y los parámetros](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-target-methods.html?lang=en).

>[!NOTE]
>
>Analytics for Target (A4T): Adobe Analytics se puede configurar como fuente de informes para [!DNL Target]. Esto permite ver en Adobe Analytics todas las métricas y dimensiones recopiladas por Target SDK. Consulte la [Información general de A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=en) para obtener más información.

¡Buen trabajo! Ahora que los parámetros están configurados, estamos listos para usarlos para crear audiencias y ofertas en Adobe Target.

**[SIGUIENTE: &quot;Crear audiencias y ofertas&quot; >](create-audiences-and-offers.md)**
