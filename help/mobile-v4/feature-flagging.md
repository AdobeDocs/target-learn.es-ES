---
title: Indicador de funcionalidad
description: Adobe Target se puede utilizar para experimentar con funciones de experiencia de usuario como color, copiar, botones, texto e imágenes, y proporcionar esas funciones a audiencias específicas.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 034d13f2-63b1-44b0-b3dc-867efe37672f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---

# Indicador de funcionalidad

Los propietarios de productos de aplicaciones móviles necesitan la flexibilidad para implementar nuevas funciones en sus aplicaciones sin tener que invertir en varias versiones de aplicaciones. También es posible que deseen implementar las funciones gradualmente hasta un porcentaje de la base de usuarios para probar la eficacia. Adobe Target se puede utilizar para experimentar con funciones de experiencia de usuario como color, copiar, botones, texto e imágenes, y proporcionar esas funciones a audiencias específicas.

En esta lección, vamos a crear una oferta de &quot;indicador de funcionalidad&quot; que puede utilizarse como déclencheur para habilitar funciones específicas de la aplicación.

## Objetivos de aprendizaje

Al final de esta lección, podrá hacer lo siguiente:

* Añadir una nueva ubicación a la solicitud de recuperación previa de lotes
* Crear una actividad [!DNL Target] con una oferta que se utilizará como indicador de funcionalidad
* Cargue y valide la oferta de indicador de funcionalidad en la aplicación

## Añadir una nueva ubicación a la solicitud de recuperación previa en la actividad de inicio

En la aplicación de demostración de nuestras lecciones anteriores, añadiremos una nueva ubicación llamada &quot;wetravel_feature_flag_recs&quot; a la solicitud de recuperación previa en la actividad de inicio y la cargaremos en la pantalla con un nuevo método de Java.

>[!NOTE]
>
>Una de las ventajas de utilizar una solicitud de recuperación previa es que añadir una nueva solicitud no añade ninguna sobrecarga de red adicional ni provoca trabajo de carga adicional, ya que la solicitud se empaqueta dentro de la solicitud de recuperación previa

En primer lugar, compruebe que la constante wetravel_feature_flag_recs se agrega en el archivo Constant.java:

![Agregar constante de indicador de funcionalidad](assets/feature_flag_constant.jpg)

Este es el código:

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

Ahora agregue la ubicación a la solicitud de recuperación previa y cargue una nueva función llamada `processFeatureFlags()`:

![Código de marca de característica](assets/feature_flag_code.jpg)

Este es el código actualizado completo:

```java
public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();

    Map<String, Object> params1;
    params1 = new HashMap<String, Object>();
    params1.put("at_property", "7962ac68-17db-1579-408f-9556feccb477");

    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, params1));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_feature_flag_recs, params1));

    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    engageMessage();
                    processFeatureFlags();
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}

public void processFeatureFlags() {
    Target.loadRequest(Constant.wetravel_feature_flag_recs, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Feature Flags : " + s);
                            if(s != null && !s.isEmpty()) {
                                //enable or disable features
                            }
                        }
                    });
                }
            });
}
```

### Validación de la solicitud de indicador de funcionalidad

Una vez agregado el código, ejecute el emulador en la actividad de inicio y observe cómo aparece la respuesta actualizada en Logcat:

![Validar ubicación del indicador de funcionalidad](assets/feature_flag_code_logcat.jpg)

## Crear una oferta JSON de indicador de funcionalidad

Ahora crearemos una oferta JSON simple que actuará como un indicador o déclencheur para una audiencia específica: la audiencia que recibiría el despliegue de la función en su aplicación. En la interfaz [!DNL Target], cree una nueva oferta:

![Crear oferta JSON de marcador de característica](assets/feature_flag_json_offer.jpg)

Asignemos un nombre &quot;Marca de característica v1&quot; con el valor {&quot;enable&quot;:1}

![oferta JSON feature_flag_v1](assets/feature_flag_json_name.jpg)

## Crear una actividad

Ahora vamos a crear una actividad Prueba A/B con esa oferta. Para ver los pasos detallados sobre la creación de una actividad, consulte la lección anterior. La actividad solo necesita una audiencia para este ejemplo. En un escenario en directo, es posible que desee crear audiencias personalizadas específicas para despliegues de funciones específicas y, a continuación, configurar la actividad para utilizar esas audiencias. En este ejemplo, asignaremos el tráfico 50/50 (50 % a los visitantes que verán las actualizaciones de funciones y el 50 % a los visitantes que verán una experiencia estándar). Esta es la configuración de la actividad:

1. Asigne un nombre a la actividad &quot;Marca de característica&quot;
1. Seleccione la ubicación &quot;wetravel_feature_flag_recs&quot;
1. Cambiar el contenido a la oferta JSON &quot;Marca de característica v1&quot;

   ![Configuración de actividad de marcador de característica](assets/feature_flag_activity.jpg)

1. Haga clic **[!UICONTROL Add Experience]** para agregar la experiencia B.
1. Deje la ubicación &quot;wetravel_feature_flag_recs&quot;
1. Dejar **[!UICONTROL Default Content]** para el contenido
1. Haga clic en **[!UICONTROL Next]** para avanzar a la pantalla [!UICONTROL Targeting]

   ![Configuración de actividad de marcador de característica](assets/feature_flag_activity_2.jpg)

1. En la pantalla [!UICONTROL Targeting], compruebe que el método [!UICONTROL Traffic Allocation] está establecido en la configuración predeterminada (Manual) y que cada experiencia tiene la asignación predeterminada del 50 %. Seleccione **[!UICONTROL Next]** para avanzar a **[!UICONTROL Goals & Settings]**.

   ![Configuración de actividad de marcador de característica](assets/feature_flag_activity_3.jpg)

1. Establezca **[!UICONTROL Primary Goal]** en **[!UICONTROL Conversion]**.
1. Establezca la acción en **[!UICONTROL Viewed an Mbox]**. Usaremos la ubicación &quot;wetravel_context_dest&quot; (ya que esta ubicación está en la pantalla de confirmación, podemos usarla para ver si la nueva función conduce a más conversiones).
1. Haga clic en **[!UICONTROL Save & Close]**.

   ![Configuración de actividad de marcador de característica](assets/feature_flag_activity_4.jpg)

Activar la actividad.

## Validación de la actividad de indicador de funcionalidad

Ahora utilice el emulador para inspeccionar la solicitud. Como establecemos la segmentación en el 50 % de los usuarios, hay un 50 % en el que verá que la respuesta de indicador de funcionalidad contiene el valor `{enable:1}`.

![Validación de marca de característica](assets/feature_flag_validation.jpg)

Si no ve el valor `{enable:1}`, significa que no fue el destinatario de la experiencia. Como prueba temporal, para forzar que se muestre la oferta, puede:

1. Desactive la actividad.
1. Cambie la asignación de tráfico al 100 % en la nueva experiencia de funciones.
1. Guarde y vuelva a activar.
1. Borre los datos del emulador y reinicie la aplicación.
1. La oferta debería devolver ahora el valor `{enable:1}`.

En un escenario activo, la respuesta `{enable:1}` se puede usar para habilitar una lógica más personalizada en la aplicación y mostrar el conjunto de características específico que desea para la audiencia de destino.

## Conclusión

¡Buen trabajo! Ahora dispone de las habilidades necesarias para desplegar funciones para audiencias de usuario específicas.
