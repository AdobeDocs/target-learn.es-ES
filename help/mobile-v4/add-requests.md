---
title: Añadir solicitudes de Adobe Target
description: El SDK de Adobe Mobile Services (v4) proporciona métodos y funcionalidades de Adobe Target que le permiten personalizar su aplicación con diferentes experiencias para distintos usuarios.
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
exl-id: 88a5be3f-d61f-43e7-997a-574ef56122ed
source-git-commit: 342e02562b5296871638c1120114214df6115809
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---

# Añadir solicitudes de Adobe Target

El SDK de Adobe Mobile Services (v4) proporciona métodos y funcionalidades de Adobe Target que le permiten personalizar su aplicación con diferentes experiencias para distintos usuarios. Normalmente, se realizan una o más solicitudes desde la aplicación a Adobe Target para recuperar el contenido personalizado y medir el impacto de ese contenido.

En esta lección, debe preparar la aplicación We.Travel para la personalización mediante la implementación de [!DNL Target] solicitudes.

## Requisitos previos  

Asegúrese de [descargar y actualizar la aplicación de ejemplo](download-and-update-the-sample-app.md).

## Objetivos de aprendizaje

Al final de esta lección, podrá hacer lo siguiente:

* Almacenar en caché varias ofertas [!DNL Target] (es decir, contenido personalizado) mediante una solicitud de recuperación previa por lotes
* Cargar ubicaciones de [!DNL Target] previamente recuperadas
* Cargar una ubicación [!DNL Target] en tiempo real (sin recuperación previa)
* Borrar ubicaciones de recuperación previa de la caché
* Validar solicitudes de recuperación previa y en tiempo real

## Terminología  

A continuación se muestra parte de la terminología clave de Target que utilizaremos en el resto de este tutorial.

* **Solicitud:** una solicitud de red a los servidores de Adobe Target
* **Oferta:** un fragmento de código u otro contenido basado en texto, definido en la interfaz de usuario de [!DNL Target] (o con API), que se entrega en la respuesta. Normalmente es JSON cuando [!DNL Target] se usa en aplicaciones móviles nativas.
* **Ubicación:** un nombre definido por el usuario dado a una solicitud, usado en la interfaz [!DNL Target] para asociar ofertas con solicitudes específicas
* **Solicitud por lotes:** una sola solicitud que incluye varias ubicaciones
* **Solicitud de recuperación previa:** una sola solicitud que recupera ofertas y las almacena en la memoria caché para su uso futuro en la aplicación
* **Solicitud de recuperación previa por lotes:** una sola solicitud que recupera previamente ofertas para varias ubicaciones
* **Audiencia:** un grupo de visitantes definido en la interfaz de [!DNL Target] o compartido con [!DNL Target] desde otras aplicaciones de Adobe (por ejemplo, &quot;visitantes de iPhone X&quot;, &quot;visitantes en California&quot;, &quot;Primera aplicación abierta&quot;)
* **Actividad:** una construcción [!DNL Target], definida en la interfaz de usuario [!DNL Target] (o con API) que vincula ubicaciones, ofertas y audiencias para crear una experiencia personalizada

## Añadir una solicitud de recuperación previa por lotes

La primera solicitud que implementaremos en We.Travel es una solicitud de recuperación previa por lotes con dos ubicaciones de [!DNL Target] en la pantalla de inicio. En una lección posterior, configuraremos ofertas para estas ubicaciones que muestran mensajes para ayudar a guiar a los nuevos usuarios a través del proceso de reserva.

Una solicitud de recuperación previa recupera el contenido de [!DNL Target] lo menos posible almacenando en caché la respuesta (oferta) del servidor de Adobe Target. Una solicitud de recuperación previa por lotes recupera y almacena en caché varias ofertas, cada una de ellas asociada a una ubicación diferente. Todas las ubicaciones de recuperación previa se almacenan en la caché del dispositivo para su uso futuro en la sesión del usuario. Al recuperar previamente varias ubicaciones en la pantalla de inicio, podemos recuperar ofertas para utilizarlas más adelante a medida que el visitante navega por la aplicación. Consulte la [documentación de recuperación previa](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html?lang=es) para obtener más información sobre los métodos de recuperación previa.

### Añadir la solicitud de recuperación previa del lote

Actualicemos el controlador de la actividad en el hogar (el código fuente de la pantalla de inicio), que se encuentra en aplicación > principal > java > com.wetravel > Controlador. Agregaremos los dos bloques de código que se muestran en rojo:

Empezaremos con el controlador de HomeActivity (el código fuente de la pantalla de inicio), que se encuentra en aplicación > principal > java > com.wetravel > Controlador.

Agregaremos los dos bloques de código que se muestran en rojo:

![Código de recuperación previa de HomeActivity](assets/homeactivity.jpg)

Desplácese hacia abajo hasta el final del código de HomeActivity y agregue el código proporcionado a continuación después de la función `setHeader()` y *reemplazando* la función `onResume()` actual:

```java
@Override
protected void onResume() {
    super.onResume();
    targetPrefetchContent();
}

public void targetPrefetchContent() {
    List<TargetPrefetchObject> prefetchList = new ArrayList<>();
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_home, null));
    prefetchList.add(Target.createTargetPrefetchObject(Constant.wetravel_engage_search, null));
    Target.TargetCallback<Boolean> prefetchStatusCallback = new Target.TargetCallback<Boolean>() {
        @Override
        public void call(final Boolean status) {
            HomeActivity.this.runOnUiThread(new Runnable() {
                @Override
                public void run() {
                    String cachingStatus = status ? "YES" : "NO";
                    System.out.println("Received Response from prefetch : " + cachingStatus);
                    setUp();

                }
            });
        }};
    Target.prefetchContent(prefetchList, null, prefetchStatusCallback);
}
```

Es probable que el IDE le advierta que no tiene las clases [!DNL Target] importadas en el archivo. Asegúrese de importar las clases [!DNL Target] en la parte superior del controlador HomeActivity, tal y como se muestra en rojo a continuación:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Importar las clases de destino](assets/import.jpg)

Probablemente también verá errores para &quot;no se puede encontrar la variable de símbolo wetravel_engage_home&quot; y &quot;no se puede encontrar la variable de símbolo wetravel_engage_search&quot;. Añádalos al archivo `Constant.java` (en app > src > main > java > com > wetravel > Utils):

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Agregar los nombres de ubicación al archivo Constant.java](assets/constants.jpg)

### Explicación del código de solicitud de recuperación previa de lotes

| Código | Descripción |
|--- |--- |
| `targetPrefetchContent()` | Una función definida por el usuario (que no forma parte del SDK) que utiliza métodos de [!DNL Target] para recuperar y almacenar en caché dos ubicaciones de [!DNL Target]. |
| `prefetchContent()` | El método SDK [!DNL Target] que envía la solicitud de recuperación previa |
| `Constant.wetravel_engage_home` | Se obtuvo previamente el nombre de la ubicación [!DNL Target], que mostrará el contenido de su oferta en la pantalla de inicio |
| `Constant.wetravel_engage_search` | Se obtuvo previamente el nombre de ubicación [!DNL Target], que mostrará el contenido de su oferta en la pantalla Resultados de la búsqueda. Dado que esta es una segunda ubicación en la recuperación previa, esta solicitud de recuperación previa se denomina &quot;solicitud de lote de recuperación previa&quot;. |
| setUp() | Función definida por el usuario que representa la pantalla de inicio de la aplicación después de recuperar previamente las ofertas de [!DNL Target] |

### Acerca de asincrónico frente a sincrónico

Con el código que acabamos de implementar, la solicitud de recuperación previa se realiza como una llamada sincrónica de bloqueo justo antes de que se procese la pantalla de inicio. Cuando pegamos el nuevo código en el controlador HomeActivity, movimos la ejecución de la función `setUp()` desde la función `onResume()` hasta después de la solicitud de Target. Esto puede resultar beneficioso en situaciones en las que desea personalizar el contenido cuando la aplicación se abre por primera vez, ya que garantiza que el contenido personalizado de los servidores de Target se ha devuelto (o se ha agotado el tiempo de espera) antes de que se procese la primera pantalla. Para permitir que las solicitudes se carguen asincrónicamente (en segundo plano), simplemente llame a `setUp()` dentro de la función `onCreate()`.

### Validar la solicitud de recuperación previa del lote

Vuelva a compilar la aplicación y abra el emulador de Android. (Las siguientes capturas de pantalla utilizan el Pixel 2 en Android Q versión 9+, nivel de API 29). La respuesta de recuperación previa debe ser &quot;respuesta de recuperación previa recibida&quot;:

Cuando se muestra la pantalla Inicio, se debe cargar la solicitud de recuperación previa. Con Logcat, filtre [!DNL "Target"] para ver la solicitud y la respuesta:

![Validar las solicitudes en la pantalla de inicio](assets/prefetch_validation.jpg)

Si no ve una respuesta correcta, compruebe la configuración del archivo `ADBMobileConfig.json` y la sintaxis de código del archivo HomeActivity.

Dos ubicaciones ahora se almacenan en caché en el dispositivo. Los nombres de las ubicaciones se cargarán de forma diferida en breve en la interfaz [!DNL Target], donde se pueden seleccionar en varios menús desplegables cuando los utilice en una actividad.

### Agregar solicitudes de carga para cada ubicación en caché

Ahora que las ubicaciones están previamente recuperadas y sus respuestas almacenadas en caché en el dispositivo, vamos a agregar el método `Target.loadRequest()` que recupera el contenido de la oferta de la caché para que pueda utilizarlo para actualizar su aplicación. Se agregará un nuevo método personalizado denominado `engageMessage()` que se ejecutará con la solicitud de recuperación previa. `engageMessage()` llamará a `Target.loadRequest()`. `engageMessage()` se ejecuta antes que `setUp()` para garantizar que se llama a la solicitud de carga antes de que se configure la pantalla.

En primer lugar, agregue la llamada y el método `engageMessage()` para la ubicación wetravel_engage_home en HomeActivity:

![Agregar solicitud de primera carga](assets/wetravel_engage_home_loadRequest.jpg)

Este es el código actualizado:

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
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_home, "", null, null, null,
            new Target.TargetCallback<String>(){
                @Override
                public void call(final String s) {
                    runOnUiThread(new Runnable() {
                        @Override
                        public void run() {
                            System.out.println("Engage Message : " + s);
                            if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                        }
                    });
                }
            });
    }
```

Ahora agregue la llamada y el método `engageMessage()` para la ubicación wetravel_engage_search en SearchBusActivity. Observe que la llamada a `engageMessage()` está establecida en el método `onResume()` antes de la llamada a `setUpSearch()`, de modo que se ejecuta antes de que se configure la pantalla:

![Agregar segunda solicitud de carga](assets/wetravel_engage_search_loadRequest.jpg)

Este es el código actualizado:

```java
    @Override
    public void onResume() {
        super.onResume();
        engageMessage();
        setUpSearch();
    }
    public void engageMessage() {
        Target.loadRequest(Constant.wetravel_engage_search, "", null, null, null,
                new Target.TargetCallback<String>(){
                    @Override
                    public void call(final String s) {
                        runOnUiThread(new Runnable() {
                            @Override
                            public void run() {
                                System.out.println("Engage Message : " + s);
                                if(s != null && !s.isEmpty()) Utility.showToast(getApplicationContext(), s);
                            }
                        });
                    }
                });
    }
```

Dado que acaba de agregar métodos de Target a SearchBusActivity, asegúrese de importar las clases [!DNL Target]:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## Añadir una solicitud en tiempo real

La próxima solicitud que añadiremos a la aplicación será una solicitud en tiempo real en la pantalla de agradecimiento. Con &quot;tiempo real&quot; queremos decir que tanto la solicitud como la respuesta se aplicarán inmediatamente (no se almacenarán en caché más adelante). En una lección posterior, se creará una experiencia con esta solicitud, que está personalizada para el destino de viaje del usuario.

Así que vamos a añadir una solicitud en tiempo real en la pantalla de agradecimiento. En el archivo Actividad de agradecimiento, realizaremos los cambios que se muestran en rojo:
![Agregar una ubicación en tiempo real en la pantalla de agradecimiento](assets/thankyou.jpg)

Desplácese hasta el final del archivo de actividad de agradecimiento. Comente las tres líneas de la función `getRecommandations()` y agregue la invocación de la función `targetLoadRequest()`:

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

Agregue esta línea de código a la función `getRecommandations()`:

```java
targetLoadRequest(recommandation.recommandations);
```

Ahora, necesitamos definir la función `targetLoadRequest()`:
![Agregar una ubicación en tiempo real en la pantalla de agradecimiento](assets/thankyou2.jpg)

Agregue este bloque de código después de la función `filterRecommendationBasedOnOffer()`:

```java
public void targetLoadRequest(final ArrayList<Recommandation> recommandations) {
    Target.loadRequest(Constant.wetravel_context_dest, "", null, null, null, new Target.TargetCallback<String>() {
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
}
```

Dado que acaba de agregar métodos de Target a la actividad de agradecimiento, asegúrese de importar las clases de Target:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### Explicación del código targetLoadRequest()

| Código | Descripción |
|--- |--- |
| `targetLoadRequest()` | Una función definida por el usuario (que no forma parte del SDK) que activa `Target.loadRequest()`, la cual carga y muestra la ubicación wetravel_context_dest |
| `Target.loadRequest()` | El método SDK que realiza la solicitud al servidor de Target |
| Constant.wetravel_context_dest | El nombre de ubicación asignado a la solicitud que usaremos más adelante cuando generemos la actividad en la interfaz [!DNL Target] |
| `filterRecommendationBasedOnOffer()` | Una función definida por el usuario en la aplicación que toma la oferta de la ubicación de la respuesta de Target y decide cómo debe cambiar la aplicación en función del contenido de la oferta |
| `recommandations.addAll()` | Función definida por el usuario en la aplicación que se solía ejecutar de forma predeterminada cuando se cargaba la pantalla de agradecimiento, pero que ahora se ejecuta después de que `filterRecommendationBasedOnOffer()` haya recibido y analizado la respuesta de Target |

Esta fue una actualización más sofisticada que hicimos a la aplicación luego con la solicitud que agregamos a la pantalla de inicio, así que vamos a tomarnos un momento para revisar lo que hicimos:

1. Interrumpimos el comportamiento anterior de la aplicación de mostrar tres promociones predeterminadas, comentando las líneas de código
1. Le dijimos a la aplicación que ejecutara una nueva función, a la que llamamos arbitrariamente targetLoadRequest
1. Definimos la función `targetLoadRequest` para realizar una solicitud a Target mediante el método Target.loadRequest y ejecutar inmediatamente la función `filterRecommendationBasedOnOffer()` cuando se reciba la respuesta de oferta [!DNL Target]
1. La función `filterRecommendationBasedOnOffer()` interpreta la respuesta y decide qué promociones se deben aplicar a la pantalla

Este es un patrón de uso muy común cuando se usa [!DNL Target] en aplicaciones móviles.  Es muy potente, ya que puede personalizar casi cualquier aspecto de su aplicación móvil. También requiere coordinación entre el código de la aplicación y las ofertas que definiremos más adelante en la interfaz [!DNL Target]. Debido a esta coordinación, algunos casos de uso de personalización pueden requerir que actualice la aplicación en la tienda de aplicaciones para iniciar la actividad.

### Validación de la solicitud en tiempo real

Abra el emulador de Android y siga todos los pasos para reservar un viaje: Inicio > Resultados de la búsqueda del autobús > Selección de puestos, Opciones de pago (cualquier opción de pago con datos en blanco funcionará).

En la última pantalla de agradecimiento, observe cómo responde Logcat. La respuesta debe decir &quot;Se devolvió el contenido predeterminado para &quot;wetravel_context_dest&quot;:

![Agregar una ubicación en tiempo real en la pantalla de agradecimiento](assets/thankyou_validation.jpg)

## Borrando ubicaciones recuperadas previamente de la caché

Puede haber situaciones en las que sea necesario borrar ubicaciones de recuperación previa durante una sesión. Por ejemplo, cuando se produce una reserva, tiene sentido borrar las ubicaciones en caché, ya que el usuario ahora está &quot;comprometido&quot; y comprende el proceso de reserva. Si reservan otro viaje durante su sesión, no necesitarán las ubicaciones originales en la pantalla de inicio y en la pantalla de resultados de búsqueda para guiar su reserva. Tendría más sentido borrar las ubicaciones de la caché y recuperar previamente nuevas ofertas para una segunda reserva con descuento u otro escenario relevante. Se puede añadir lógica a la pantalla de inicio y a la pantalla de resultados de búsqueda para recuperar previamente nuevas ubicaciones si se ha realizado una reserva durante la sesión.

Para este ejemplo, solo borraremos las ubicaciones previamente recuperadas de la sesión cuando se realice una reserva. Esto se hace llamando a la función `Target.clearPrefetchCache()`. Establezca la función dentro de la función `targetLoadRequest()` como se muestra a continuación:

```java
Target.clearPrefetchCache()
```

![Borrar ubicaciones de recuperación previa de la caché](assets/clearPrefetch.jpg)

¡Felicidades! La aplicación ahora tiene el marco para la personalización. En la siguiente lección, vamos a mejorar nuestras capacidades de personalización añadiendo parámetros a estas ubicaciones.

**[SIGUIENTE: &quot;Agregar parámetros&quot; >](add-parameters.md)**
