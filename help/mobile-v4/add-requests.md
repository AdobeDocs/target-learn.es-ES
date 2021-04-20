---
title: Agregar solicitudes de Adobe Target
description: 'El SDK de Adobe Mobile Services (v4) proporciona métodos y funciones de Adobe Target que le permiten personalizar la aplicación con diferentes experiencias para distintos usuarios.   '
role: Developer
level: Intermediate
topic: Mobile, Personalization
feature: Implement Mobile
doc-type: tutorial
kt: 3040
thumbnail: null
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 0%

---


# Agregar solicitudes de Adobe Target

El SDK de Adobe Mobile Services (v4) proporciona métodos y funciones de Adobe Target que le permiten personalizar la aplicación con diferentes experiencias para distintos usuarios. Normalmente, se realizan una o más solicitudes desde la aplicación a Adobe Target para recuperar el contenido personalizado y medir el impacto de dicho contenido.

En esta lección, debe preparar la aplicación We.Travel para personalización mediante la implementación de solicitudes [!DNL Target].

## Requisitos previos  

Asegúrese de [descargar y actualizar la aplicación de ejemplo](download-and-update-the-sample-app.md).

## Objetivos de aprendizaje

Al final de esta lección, podrá:

* Almacene en caché varias [!DNL Target] ofertas (es decir, contenido personalizado) mediante una solicitud de recuperación previa por lotes
* Cargar ubicaciones de [!DNL Target] recuperación previa
* Cargar una ubicación [!DNL Target] en tiempo real (sin recuperación previa)
* Borrar ubicaciones previamente recuperadas de la caché
* Validación de solicitudes recuperadas previamente y en tiempo real

## Terminología  

A continuación se describen algunos de los términos clave de Target que utilizaremos en el resto de este tutorial.

* **Solicitud:**   una solicitud de red a los servidores de Adobe Target
* **Oferta:**  un fragmento de código u otro contenido basado en texto, definido en la interfaz de  [!DNL Target] usuario (o con API), que se entrega en la respuesta. Normalmente, JSON cuando [!DNL Target] se utiliza en aplicaciones móviles nativas.
* **Ubicación:**  un nombre definido por el usuario dado a una solicitud, utilizado en la  [!DNL Target] interfaz para asociar ofertas con solicitudes específicas.
* **Solicitud por lotes:**   una única solicitud que incluye varias ubicaciones
* **Solicitud de recuperación previa:**  una sola solicitud que recupera ofertas y las almacena en caché en la memoria para su uso futuro en la aplicación.
* **Solicitud de recuperación previa por lotes:**   una única solicitud que obtiene previamente ofertas para varias ubicaciones
* **Audiencia:**  grupo de visitantes definido en la  [!DNL Target] interfaz o compartido con  [!DNL Target] desde otras aplicaciones de Adobe (p. ej. &quot;Visitantes de iPhone X&quot;, &quot;Visitantes de California&quot;, &quot;Primera aplicación abierta&quot;)
* **Actividad:**  una  [!DNL Target] construcción definida en la interfaz de  [!DNL Target] usuario (o con API) que vincula ubicaciones, ofertas y audiencias para crear una experiencia personalizada.

## Añadir una solicitud de recuperación previa de lotes

La primera solicitud que implementaremos en We.Travel es una solicitud de recuperación previa por lotes con dos [!DNL Target] ubicaciones en la pantalla principal. En una lección posterior, configuraremos ofertas para estas ubicaciones que muestran mensajes para ayudar a guiar a los nuevos usuarios a través del proceso de reserva.

Una solicitud de recuperación previa obtiene contenido [!DNL Target] lo más mínimo posible almacenando en caché la respuesta del servidor de Adobe Target (oferta). Una solicitud de recuperación previa por lotes recupera y almacena en caché varias ofertas, cada una asociada a una ubicación diferente. Todas las ubicaciones recuperadas previamente se almacenan en caché en el dispositivo para su uso futuro en la sesión del usuario. Al recuperar previamente varias ubicaciones en la pantalla principal, podemos recuperar ofertas para usarlas más adelante, a medida que el visitante navega por la aplicación. Consulte la [documentación de recuperación previa](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html) para obtener más información sobre los métodos de recuperación previa.

### Añadir la solicitud de recuperación previa por lotes

Actualicemos el controlador HomeActivity (el código fuente de la pantalla principal), que se encuentra en app > main > java > com.wetravel > Controller. Añadiremos los dos bloques de código que se muestran en rojo:

Comenzaremos con el controlador HomeActivity (el código fuente de la pantalla principal), que se encuentra en app > main > java > com.wetravel > Controller.

Añadiremos los dos bloques de código que se muestran en rojo:

![Código de recuperación previa de HomeActivity](assets/homeactivity.jpg)

Desplácese hacia abajo hasta el final del código de HomeActivity y añada el código que se proporciona a continuación después de la función `setHeader()` y *reemplace* a la función `onResume()` actual:

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

Su IDE probablemente le avisará de que no tiene las clases [!DNL Target] importadas en el archivo. Asegúrese de importar las clases [!DNL Target] en la parte superior del controlador HomeActivity como se muestra en rojo a continuación:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Importar las clases de Target](assets/import.jpg)

Probablemente también verá errores para &quot;no se puede encontrar la variable de símbolo wetravel_engagement_home&quot; y &quot;no se puede encontrar la variable de símbolo wetravel_engagement_search&quot;. Añádalos al archivo `Constant.java` (en app > src > main > java > com > wetravel > Utils):

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Agregue los nombres de ubicación al archivo Constant.java](assets/constants.jpg)

### Explicación del código de solicitud de recuperación previa de lotes

| Código | Descripción |
|--- |--- |
| `targetPrefetchContent()` | Una función definida por el usuario (que no forma parte del SDK) que utiliza métodos [!DNL Target] para recuperar y almacenar en caché dos ubicaciones [!DNL Target]. |
| `prefetchContent()` | El método SDK [!DNL Target] que envía la solicitud de recuperación previa |
| `Constant.wetravel_engage_home` | Nombre de ubicación [!DNL Target] recuperado previamente que mostrará su contenido de oferta en la pantalla principal |
| `Constant.wetravel_engage_search` | Nombre de ubicación [!DNL Target] recuperado previamente que mostrará su contenido de oferta en la pantalla de resultados de la búsqueda. Dado que esta es una segunda ubicación en la recuperación previa, esta solicitud de recuperación previa se denomina &quot;solicitud de lote de recuperación previa&quot;. |
| setUp() | Una función definida por el usuario que procesa la pantalla principal de la aplicación después de que se recuperen previamente las ofertas [!DNL Target] |

### Acerca de Asincrónico frente a Sincrónico

Con el código que acabamos de implementar, la solicitud de recuperación previa se realiza como una llamada de bloqueo sincrónica, justo antes de que se procese la pantalla principal. Cuando pegamos el nuevo código en el controlador HomeActivity, movemos la ejecución de la función `setUp()` desde la función `onResume()` hasta después de la solicitud de Target. Esto puede resultar beneficioso en los casos en los que desee personalizar el contenido cuando la aplicación se abra por primera vez, ya que garantiza que el contenido personalizado de los servidores de Target haya regresado (o que se haya agotado el tiempo de espera) antes de que se procese la primera pantalla. Para permitir que las solicitudes se carguen de forma asíncrona (en segundo plano), simplemente llame a `setUp()` dentro de la función `onCreate()` en su lugar.

### Validación de la solicitud de recuperación previa por lotes

Vuelva a compilar la aplicación y abra el emulador de Android. (Las siguientes capturas de pantalla utilizan el píxel 2 en Android Q versión 9+, nivel de API 29). La respuesta de recuperación previa debe ser &quot;respuesta de recuperación previa recibida&quot;:

Cuando la pantalla de inicio se procesa, se debe cargar la solicitud de recuperación previa. Con Logcat, filtre [!DNL "Target"] para ver la solicitud y la respuesta:

![Validar las solicitudes en la pantalla principal](assets/prefetch_validation.jpg)

Si no ve una respuesta correcta, compruebe la configuración del archivo `ADBMobileConfig.json` y la sintaxis de código del archivo HomeActivity.

Dos ubicaciones ahora se almacenan en caché en el dispositivo. Los nombres de ubicación pronto se cargarán de forma diferida en la interfaz [!DNL Target], donde se pueden seleccionar en varios menús desplegables cuando los utilice en una actividad de .

### Agregar solicitudes de carga para cada ubicación en caché

Ahora que las ubicaciones se recuperan previamente y sus respuestas se almacenan en caché en el dispositivo, vamos a agregar el método `Target.loadRequest()` que recupera el contenido de la oferta de la caché para que pueda usarlo para actualizar su aplicación. Añadiremos un nuevo método personalizado llamado `engageMessage()` que se ejecutará con la solicitud de recuperación previa. `engageMessage()` llamará a  `Target.loadRequest()`. `engageMessage()` se ejecuta antes  `setUp()` de para garantizar que se llame a la solicitud de carga antes de configurar la pantalla.

En primer lugar, agregue la llamada y el método `engageMessage()` para la ubicación wetravel_engagement_home en HomeActivity:

![Añadir primera solicitud de carga](assets/wetravel_engage_home_loadRequest.jpg)

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

Ahora agregue la llamada y el método `engageMessage()` para la ubicación wetravel_engagement_search en SearchBusActivity. Observe que la llamada `engageMessage()` se establece en el método `onResume()` antes de la llamada a `setUpSearch()` para que se ejecute antes de que se configure la pantalla:

![Añadir segunda solicitud de carga](assets/wetravel_engage_search_loadRequest.jpg)

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

Como acaba de agregar métodos de Target a SearchBusActivity, asegúrese de importar las clases [!DNL Target] :

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## Agregar una solicitud en tiempo real

La siguiente solicitud que agregaremos a la aplicación será una solicitud en tiempo real en la pantalla de agradecimiento. Por &quot;tiempo real&quot; queremos decir que tanto la solicitud se realiza como la respuesta se aplican inmediatamente (no se almacenan en caché más adelante). En una lección posterior, se creará una experiencia con esta solicitud, que se personaliza con el destino de viaje del usuario.

Así que vamos a agregar una solicitud en tiempo real en la pantalla de agradecimiento. En el archivo thankYouActivity , realizaremos los cambios en rojo:
![Añada una ubicación en tiempo real en la pantalla de agradecimiento](assets/thankyou.jpg)

Desplácese hasta el final del archivo de actividades de agradecimiento. Comente las tres líneas de la función `getRecommandations()` y añada la invocación de la función `targetLoadRequest()`:

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

Agregue esta línea de código a la función `getRecommandations()` :

```java
targetLoadRequest(recommandation.recommandations);
```

Ahora, necesitamos definir la función `targetLoadRequest()` :
![Agregar una ubicación en tiempo real en la pantalla de agradecimiento](assets/thankyou2.jpg)

Agregue este bloque de código después de la función `filterRecommendationBasedOnOffer()` :

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

Como acaba de agregar métodos de Target a la actividad de agradecimiento, asegúrese de importar las clases de Target:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### Explicación de código de targetLoadRequest()

| Código | Descripción |
|--- |--- |
| `targetLoadRequest()` | Una función definida por el usuario (que no forma parte del SDK) que activa `Target.loadRequest()` y que carga y muestra la ubicación de wetravel_context_dest |
| `Target.loadRequest()` | El método SDK que realiza la solicitud al servidor de Target |
| Constant.wetravel_context_dest | El nombre de la ubicación asignado a la solicitud que usaremos más adelante cuando creemos la actividad en la interfaz [!DNL Target] |
| `filterRecommendationBasedOnOffer()` | Una función definida por el usuario en la aplicación que toma la oferta de la ubicación de la respuesta de Target y decide cómo debería cambiar la aplicación en función del contenido de la oferta |
| `recommandations.addAll()` | Una función definida por el usuario en la aplicación que se ejecutaba de forma predeterminada cuando se cargaba la pantalla de agradecimiento, pero que ahora se ejecuta después de que la respuesta de Target se haya recibido y analizado por `filterRecommendationBasedOnOffer()` |

Esta fue una actualización más sofisticada que hicimos en la aplicación y luego con la solicitud que agregamos a la pantalla principal, así que dediquemos un momento a revisar lo que hicimos:

1. Interrumpimos el comportamiento anterior de la aplicación de mostrar tres promociones predeterminadas al comentar las líneas de código
1. En su lugar, le dijimos a la aplicación que ejecutara una nueva función, que llamamos arbitrariamente targetLoadRequest
1. Hemos definido la función `targetLoadRequest` para realizar una solicitud a Target mediante el método Target.loadRequest y ejecutar inmediatamente la función `filterRecommendationBasedOnOffer()` cuando se reciba la respuesta de oferta [!DNL Target]
1. La función `filterRecommendationBasedOnOffer()` interpreta la respuesta y decide qué promociones deben aplicarse a la pantalla

Este es un patrón de uso muy común cuando se utiliza [!DNL Target] en aplicaciones móviles.  Es muy potente, ya que puede personalizar casi cualquier aspecto de su aplicación móvil. También requiere una coordinación entre el código de la aplicación y las ofertas que definiremos más adelante en la interfaz [!DNL Target]. Debido a esta coordinación, algunos casos de uso de personalización pueden requerir que actualice la aplicación en la tienda de aplicaciones para iniciar la actividad.

### Validación de la solicitud en tiempo real

Abra el emulador de Android y siga todos los pasos para reservar un viaje: Inicio > Resultados de búsqueda de bus > Selección de asientos, Opciones de pago (cualquier opción de pago con datos en blanco funcionará).

En la última pantalla de agradecimiento, observe Logcat para obtener la respuesta. La respuesta debe ser &quot;Se devolvió contenido predeterminado para &quot;wetravel_context_dest&quot;:

![Agregar una ubicación en tiempo real en la pantalla de agradecimiento](assets/thankyou_validation.jpg)

## Borrado de ubicaciones recuperadas previamente de la caché

Puede haber situaciones en las que sea necesario borrar las ubicaciones previamente recuperadas durante una sesión. Por ejemplo, cuando se realiza una reserva, tiene sentido borrar las ubicaciones en caché, ya que el usuario está ahora &quot;comprometido&quot; y comprende el proceso de reserva. Si reservan otro viaje durante su sesión, no necesitarán las ubicaciones originales en la pantalla de inicio y la pantalla de resultados de búsqueda para guiar su reserva. Tendría más sentido borrar las ubicaciones de la caché y recuperar previamente nuevas ofertas para tal vez una segunda reserva con descuento u otro escenario relevante. Se podría agregar lógica a la pantalla de inicio y a la pantalla de resultados de búsqueda para recuperar previamente nuevas ubicaciones si se ha realizado una reserva durante la sesión.

Para este ejemplo, solo borraremos las ubicaciones previamente recuperadas para la sesión cuando se realice una reserva. Esto se hace llamando a la función `Target.clearPrefetchCache()`. Establezca la función dentro de la función `targetLoadRequest()` como se muestra a continuación:

```java
Target.clearPrefetchCache()
```

![Borrar ubicaciones previamente recuperadas de la caché](assets/clearPrefetch.jpg)

¡Felicidades! La aplicación ahora tiene el marco para la personalización. En la siguiente lección, mejoraremos nuestras capacidades de personalización añadiendo parámetros a estas ubicaciones.

**[SIGUIENTE : &quot;Añadir parámetros&quot; >](add-parameters.md)**
