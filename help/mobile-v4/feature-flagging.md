---
title: Indicador de características
description: Adobe Target se puede utilizar para experimentar con funciones de experiencia de usuario como color, copia, botones, texto e imágenes, y proporcionar esas funciones a audiencias específicas.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 034d13f2-63b1-44b0-b3dc-867efe37672f
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 1%

---

# Indicador de características

Los propietarios de productos de aplicaciones móviles necesitan la flexibilidad para implementar nuevas funciones en su aplicación sin tener que invertir en varias versiones de aplicaciones. También es posible que deseen desplegar las funciones gradualmente a un porcentaje de la base de usuarios para comprobar la eficacia. Adobe Target se puede utilizar para experimentar con funciones de experiencia de usuario como color, copia, botones, texto e imágenes, y proporcionar esas funciones a audiencias específicas.

En esta lección, crearemos una oferta de &quot;indicador de características&quot; que se puede usar como déclencheur para habilitar funciones específicas de la aplicación.

## Objetivos de aprendizaje

Al final de esta lección, podrá:

* Añadir una nueva ubicación a la solicitud de recuperación previa por lotes
* Cree una actividad [!DNL Target] con una oferta que se utilizará como indicador de característica
* Cargar y validar la oferta del indicador de características en la aplicación

## Agregar una nueva ubicación a la solicitud de recuperación previa a la actividad principal

En la aplicación de demostración de nuestras lecciones anteriores, agregaremos una nueva ubicación denominada &quot;wetravel_feature_flag_recs&quot; a la solicitud de recuperación previa en la actividad principal y la cargaremos en la pantalla con un nuevo método Java.

>[!NOTE]
>
>Una de las ventajas de utilizar una solicitud de recuperación previa es que añadir una nueva solicitud no añade ninguna sobrecarga de red adicional ni causa trabajo de carga adicional, ya que la solicitud está empaquetada dentro de la solicitud de recuperación previa

En primer lugar, compruebe que la constante wetravel_feature_flag_recs se agrega en el archivo Constant.java:

![Agregar constante de indicador de función](assets/feature_flag_constant.jpg)

Este es el código:

```java
public static final String wetravel_feature_flag_recs = "wetravel_feature_flag_recs";
```

Ahora, agregue la ubicación a la solicitud de recuperación previa y cargue una nueva función llamada `processFeatureFlags()`:

![Código de marca de características](assets/feature_flag_code.jpg)

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

### Validación de la solicitud de marca de características

Una vez agregado el código, ejecute el emulador en la actividad principal y vea Logcat para obtener la respuesta actualizada:

![Validar la ubicación del indicador de características](assets/feature_flag_code_logcat.jpg)

## Creación de una oferta JSON con marca de característica

Ahora crearemos una oferta JSON sencilla que actuará como indicador o déclencheur para una audiencia específica: la audiencia que recibiría el despliegue de funciones en su aplicación. En la interfaz [!DNL Target], cree una oferta nueva:

![Creación de una oferta JSON con marca de característica](assets/feature_flag_json_offer.jpg)

Denomínela &quot;Indicador de características v1&quot; con el valor {&quot;enable&quot;:1}

![feature_flag_v1 Oferta JSON](assets/feature_flag_json_name.jpg)

## Crear una actividad

Ahora vamos a crear una actividad de prueba A/B con esa oferta. Para ver los pasos detallados sobre la creación de una actividad, consulte la lección anterior. La actividad solo necesitará una audiencia para este ejemplo. En un escenario en directo, es posible que desee crear audiencias personalizadas específicas para lanzamientos de funciones específicas y luego configurar la actividad para que use esas audiencias. En este ejemplo, asignaremos el tráfico 50/50 (50 % a los visitantes que verán las actualizaciones de funciones y 50 % a los visitantes que verán una experiencia estándar). Esta es la configuración de la actividad:

1. Asigne a la actividad el nombre &quot;Indicador de características&quot;.
1. Seleccione la ubicación &quot;wetravel_feature_flag_recs&quot;
1. Cambiar el contenido a la oferta JSON &quot;Indicador de características v1&quot;

   ![Configuración de actividad de marca de características](assets/feature_flag_activity.jpg)

1. Haga clic en **[!UICONTROL Agregar experiencia]** para agregar la experiencia B.
1. Deje la ubicación &quot;wetravel_feature_flag_recs&quot;
1. Deje **[!UICONTROL Contenido predeterminado]** para el contenido
1. Haga clic en **[!UICONTROL Siguiente]** para avanzar a la pantalla [!UICONTROL Segmentación]

   ![Configuración de actividad de marca de características](assets/feature_flag_activity_2.jpg)

1. En la pantalla [!UICONTROL Segmentación], verifique que el método [!UICONTROL Asignación de tráfico] esté establecido en la configuración predeterminada (Manual) y que cada experiencia tenga la asignación predeterminada del 50%. Seleccione **[!UICONTROL Siguiente]** para avanzar a **[!UICONTROL Objetivos y configuración]**.

   ![Configuración de actividad de marca de características](assets/feature_flag_activity_3.jpg)

1. Establezca el **[!UICONTROL Objetivo principal]** en **[!UICONTROL Conversión]**.
1. Establezca la acción en **[!UICONTROL Visualizó un mbox]**. Utilizaremos la ubicación &quot;wetravel_context_dest&quot; (ya que esta ubicación está en la pantalla Confirmación, podemos utilizarla para ver si la nueva función genera más conversiones).
1. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   ![Configuración de actividad de marca de características](assets/feature_flag_activity_4.jpg)

Activar la actividad.

## Validar la actividad del indicador de características

Ahora utilice el emulador para ver la solicitud. Dado que establecemos el objetivo en el 50 % de los usuarios, hay un 50 % que verá que la respuesta del indicador de características contiene el valor `{enable:1}`.

![Validación de marca de características](assets/feature_flag_validation.jpg)

Si no ve el valor `{enable:1}` , significa que no fue el objetivo de la experiencia. Como prueba temporal, para forzar la presentación de la oferta, puede:

1. Desactive la actividad.
1. Cambie la asignación de tráfico al 100 % en la nueva experiencia de funciones.
1. Guarde y reactive.
1. Borre los datos del emulador y reinicie la aplicación.
1. La oferta ahora debe devolver el valor `{enable:1}`.

En un escenario en directo, la respuesta `{enable:1}` se puede usar para habilitar más lógica personalizada en la aplicación para mostrar el conjunto de funciones específico que desea que muestre a la audiencia de destino.

## Conclusión. 

¡Buen trabajo! Ahora tiene las habilidades necesarias para implementar funciones para audiencias de usuario específicas.
