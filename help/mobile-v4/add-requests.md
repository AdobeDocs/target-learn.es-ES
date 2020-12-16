---
title: Añadir solicitudes de Adobe Target
description: 'El SDK de Adobe Mobile Services (v4) proporciona métodos y funcionalidades de Adobe Target que le permiten personalizar su aplicación con diferentes experiencias para distintos usuarios.   '
feature: mobile
kt: 3040
audience: developer
doc-type: tutorial
activity-type: implement
translation-type: tm+mt
source-git-commit: b331bb29c099bd91df27300ebe199cafa12516db
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 0%

---


# Añadir solicitudes de Adobe Target

El SDK de Adobe Mobile Services (v4) proporciona métodos y funcionalidades de Adobe Target que le permiten personalizar su aplicación con diferentes experiencias para distintos usuarios. Normalmente, se realizan una o más solicitudes desde la aplicación al Adobe Target para recuperar el contenido personalizado y medir el impacto de dicho contenido.

En esta lección, preparará la aplicación We.Travel para personalización mediante la implementación de [!DNL Target] solicitudes.

## Requisitos previos  

Asegúrese de [descargar y actualizar la aplicación de ejemplo](download-and-update-the-sample-app.md).

## Objetivos de aprendizaje

Al final de esta lección, podrá:

* Almacenar en caché varias [!DNL Target] ofertas (es decir, contenido personalizado) mediante una solicitud de recuperación previa por lotes
* Cargar ubicaciones de [!DNL Target] recuperación previa
* Cargue una ubicación [!DNL Target] en tiempo real (no recuperada previamente)
* Borrar ubicaciones recuperadas previamente de la caché
* Validar solicitudes recuperadas previamente y en tiempo real

## Terminología  

A continuación se describen algunos de los términos clave de Destinatario que usaremos en el resto de este tutorial.

* **Solicitud:**  una solicitud de red a los servidores de Adobe Target
* **Oferta:**  un fragmento de código u otro contenido basado en texto, definido en la interfaz de  [!DNL Target] usuario (o con API), que se entrega en la respuesta. Normalmente, JSON cuando [!DNL Target] se utiliza en aplicaciones móviles nativas.
* **Ubicación:**  un nombre definido por el usuario para una solicitud, utilizado en la  [!DNL Target] interfaz para asociar ofertas con solicitudes específicas
* **Solicitud por lotes:**  una sola solicitud que incluye varias ubicaciones
* **Solicitud de recuperación previa:**  una sola solicitud que recupera ofertas y las almacena en caché en la memoria para su uso futuro en la aplicación
* **Solicitud de recuperación previa por lotes:**  una sola solicitud que busca previamente ofertas para varias ubicaciones
* **Audiencia:**  un grupo de visitantes definidos en la  [!DNL Target] interfaz o compartidos con otras aplicaciones  [!DNL Target] de Adobe (p. ej. &quot;visitantes iPhone X&quot;, &quot;visitantes en California&quot;, &quot;Primera aplicación abierta&quot;)
* **Actividad:**  una  [!DNL Target] construcción, definida en la interfaz de  [!DNL Target] usuario (o con API) que vincula ubicaciones, ofertas y Audiencias para crear una experiencia personalizada

## Añadir una solicitud de recuperación previa por lotes

La primera solicitud que implementaremos en We.Travel es una solicitud de recuperación previa por lotes con dos [!DNL Target] ubicaciones en la pantalla principal. En una lección posterior, configuraremos ofertas para estas ubicaciones que muestran mensajes para ayudar a guiar a los nuevos usuarios a través del proceso de reservación.

Una solicitud de recuperación previa obtiene el contenido [!DNL Target] lo más mínimo posible almacenando en caché la respuesta del servidor de Adobe Target (oferta). Una solicitud de recuperación previa por lotes recupera y almacena en caché varias ofertas, cada una asociada con una ubicación diferente. Todas las ubicaciones recuperadas previamente se almacenan en caché en el dispositivo para su uso futuro en la sesión del usuario. Al recuperar previamente varias ubicaciones en la pantalla de inicio, podemos recuperar ofertas para usarlas más adelante, a medida que el visitante navega por la aplicación. Consulte la [documentación de recuperación previa](https://docs.adobe.com/content/help/en/mobile-services/android/target-android/c-mob-target-prefetch-android.html) para obtener más detalles sobre los métodos de recuperación previa.

### Añadir la solicitud de recuperación previa por lotes

Actualicemos el controlador HomeActivity (el código fuente de la pantalla principal), que se encuentra en app > main > java > com.wetravel > Controller. Agregaremos los dos bloques de código que se muestran en rojo:

Inicios con el controlador HomeActivity (el código fuente de la pantalla principal), que se encuentra en app > main > java > com.wetravel > Controller.

Agregaremos los dos bloques de código que se muestran en rojo:

![Código de recuperación previa de HomeActivity](assets/homeactivity.jpg)

Desplácese hacia abajo hasta el final del código de HomeActivity y agregue el código que se proporciona a continuación después de la función `setHeader()` y *reemplazando* la función `onResume()` actual:

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

Su IDE probablemente le avisará de que no tiene importadas las clases [!DNL Target] en el archivo. Asegúrese de importar las clases [!DNL Target] en la parte superior del controlador HomeActivity como se muestra en rojo abajo:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

![Importar las clases de Destinatario](assets/import.jpg)

Probablemente también verá errores para &quot;no se puede encontrar la variable de símbolo wetravel_engagement_home&quot; y &quot;no se puede encontrar la variable de símbolo wetravel_engagement_search&quot;. Añada estos elementos en el archivo `Constant.java` (en app > src > main > java > com > wetravel > Utils):

```java
public static final String wetravel_engage_home = "wetravel_engage_home";
public static final String wetravel_engage_search = "wetravel_engage_search";
```

![Añadir los nombres de ubicación en el archivo Constant.java](assets/constants.jpg)

### Explicación del código de solicitud de recuperación previa por lotes

| Código | Descripción |
|--- |--- |
| `targetPrefetchContent()` | Una función definida por el usuario (que no forma parte del SDK) que utiliza métodos [!DNL Target] para recuperar y almacenar en caché dos ubicaciones [!DNL Target]. |
| `prefetchContent()` | El método SDK [!DNL Target] que envía la solicitud de recuperación previa |
| `Constant.wetravel_engage_home` | Nombre de ubicación [!DNL Target] recuperado previamente que mostrará su contenido de oferta en la pantalla de inicio |
| `Constant.wetravel_engage_search` | Nombre de ubicación [!DNL Target] recuperado previamente que mostrará su contenido de oferta en la pantalla de resultados de búsqueda. Dado que esta es una segunda ubicación en la recuperación previa, esta solicitud de recuperación previa se denomina &quot;solicitud de lote de recuperación previa&quot;. |
| setUp() | Una función definida por el usuario que procesa la pantalla de inicio de la aplicación después de recuperar previamente las ofertas [!DNL Target] |

### Acerca de Asincrónico vs. Sincrónico

Con el código que acabamos de implementar, la solicitud de recuperación previa se realiza como una llamada de bloqueo sincrónica, justo antes de que se procese la pantalla principal. Cuando pegamos el nuevo código en el controlador HomeActivity, movemos la ejecución de la función `setUp()` desde la función `onResume()` hasta después de la solicitud de Destinatario. Esto puede resultar beneficioso en situaciones en las que desea personalizar el contenido cuando la aplicación se abre por primera vez porque garantiza que el contenido personalizado de los servidores de Destinatario ha regresado (o que se ha agotado el tiempo de espera) antes de que se procese la primera pantalla. Para permitir que las solicitudes se carguen asincrónicamente (en segundo plano), simplemente llame a `setUp()` dentro de la función `onCreate()` en su lugar.

### Validar la solicitud de recuperación previa por lotes

Vuelva a compilar la aplicación y abra el emulador de Android. (Las siguientes capturas de pantalla utilizan el Pixel 2 en Android Q versión 9+, API nivel 29). La respuesta de recuperación previa debe decir &quot;respuesta de recuperación previa recibida&quot;:

Cuando se procesa la pantalla de inicio, se debe cargar la solicitud de recuperación previa. Con Logcat, filtre [!DNL "Target"] para ver la solicitud y la respuesta:

![Validar las solicitudes en la pantalla principal](assets/prefetch_validation.jpg)

Si no ve una respuesta correcta, compruebe la configuración del archivo `ADBMobileConfig.json` y la sintaxis del código en el archivo HomeActivity.

Dos ubicaciones ahora se almacenan en caché en el dispositivo. Los nombres de ubicación se cargarán poco después en la interfaz [!DNL Target], donde se pueden seleccionar en varios menús desplegables cuando se utilizan en una actividad.

### Añadir solicitudes de carga para cada ubicación en caché

Ahora que las ubicaciones se recuperan previamente y sus respuestas se almacenan en caché en el dispositivo, vamos a agregar el método `Target.loadRequest()` que recupera el contenido de oferta de la caché para que pueda utilizarlo para actualizar la aplicación. Agregaremos un nuevo método personalizado llamado `engageMessage()` que se ejecutará con la solicitud de recuperación previa. `engageMessage()` llamaremos  `Target.loadRequest()`. `engageMessage()` se ejecuta antes  `setUp()` para garantizar que se llame a la solicitud de carga antes de configurar la pantalla.

En primer lugar, agregue la `engageMessage()` llamada y método para la ubicación wetravel_engagement_home en HomeActivity:

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

Ahora agregue la `engageMessage()` llamada y método para la ubicación wetravel_engagement_search en SearchBusActivity. Observe que la llamada `engageMessage()` se establece en el método `onResume()` antes de la llamada a `setUpSearch()` para que se ejecute antes de que se configure la pantalla:

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

Dado que acaba de agregar métodos de Destinatario a SearchBusActivity, asegúrese de importar las clases [!DNL Target]:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

## Añadir una solicitud en tiempo real

La siguiente solicitud que agregaremos a la aplicación será una solicitud en tiempo real en la pantalla de agradecimiento. Por &quot;tiempo real&quot; significamos que tanto la solicitud se hará como la respuesta se aplicará inmediatamente (no se almacenará en caché más adelante). En una lección posterior, crearemos una experiencia con esta solicitud, personalizada para el destino del viaje del usuario.

Así que vamos a agregar una solicitud en tiempo real en la pantalla de agradecimiento. En el archivo de actividades de agradecimiento, realizaremos los cambios que se muestran en rojo:
![Añada una ubicación en tiempo real en la pantalla de agradecimiento](assets/thankyou.jpg)

Desplácese hasta el final del archivo de actividades de agradecimiento. Comente las tres líneas de la función `getRecommandations()` y agregue la invocación de la función `targetLoadRequest()`:

```java
// AppDialogs.dialogLoaderHide();
// recommandations.addAll(recommandation.recommandations);
// recommandationbAdapter.notifyDataSetChanged();
```

Añada esta línea de código a la función `getRecommandations()`:

```java
targetLoadRequest(recommandation.recommandations);
```

Ahora, necesitamos definir la función `targetLoadRequest()`:
![Añada una ubicación en tiempo real en la pantalla de agradecimiento](assets/thankyou2.jpg)

Añada este bloque de código después de la función `filterRecommendationBasedOnOffer()`:

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

Dado que acaba de agregar métodos de Destinatario a la actividad de agradecimiento, asegúrese de importar las clases de Destinatario:

```java
import com.adobe.mobile.Target;
import com.adobe.mobile.TargetPrefetchObject;
```

### Explicación del código de targetLoadRequest()

| Código | Descripción |
|--- |--- |
| `targetLoadRequest()` | Una función definida por el usuario (que no forma parte del SDK) que activa `Target.loadRequest()` y que carga y muestra la ubicación wetravel_context_dest |
| `Target.loadRequest()` | El método SDK que realiza la solicitud al servidor de Destinatario |
| Constant.wetravel_context_dest | El nombre de ubicación asignado a la solicitud que usaremos más adelante cuando generemos la actividad en la interfaz [!DNL Target] |
| `filterRecommendationBasedOnOffer()` | Función definida por el usuario en la aplicación que toma la oferta de la ubicación de la respuesta de Destinatario y decide cómo debe cambiar la aplicación en función del contenido de la oferta |
| `recommandations.addAll()` | Una función definida por el usuario en la aplicación que se ejecutaba de forma predeterminada cuando se cargaba la pantalla de agradecimiento, pero que ahora se ejecuta después de recibir la respuesta de Destinatario y analizarla por `filterRecommendationBasedOnOffer()` |

Esta fue una actualización más sofisticada que hicimos en la aplicación y luego con la solicitud que agregamos a la pantalla de inicio, así que dediquemos un momento a revisar lo que hicimos:

1. Hemos interrumpido el comportamiento anterior de la aplicación de mostrar tres promociones predeterminadas al comentar las líneas de código
1. En su lugar, le pedimos a la aplicación que ejecutara una nueva función, a la que llamamos targetLoadRequest de forma arbitraria
1. Definimos la función `targetLoadRequest` para realizar una solicitud al Destinatario mediante el método Destinatario.loadRequest y ejecutar inmediatamente la función `filterRecommendationBasedOnOffer()` cuando se recibe la respuesta de oferta [!DNL Target]
1. La función `filterRecommendationBasedOnOffer()` interpreta la respuesta y decide qué promociones deben aplicarse a la pantalla

Este es un patrón de uso muy común al usar [!DNL Target] en aplicaciones móviles.  Ambos son muy poderosos, ya que puedes personalizar casi cualquier aspecto de tu aplicación móvil. También requiere la coordinación entre el código de la aplicación y las ofertas que definiremos más adelante en la interfaz [!DNL Target]. Debido a esta coordinación, algunos casos de uso de personalización pueden requerir que actualice la aplicación en el almacén de aplicaciones para iniciar la actividad.

### Validar la solicitud en tiempo real

Abra el emulador de Android y siga todos los pasos para reservar un viaje: Inicio > Resultados de búsqueda de bus > Selección de asientos, Opciones de pago (cualquier opción de pago con datos en blanco funcionará).

En la pantalla de agradecimiento final, vea Logcat para obtener la respuesta. La respuesta debe decir &quot;Se devolvió contenido predeterminado para &quot;wetravel_context_dest&quot;:

![Añadir una ubicación en tiempo real en la pantalla de agradecimiento](assets/thankyou_validation.jpg)

## Borrado de ubicaciones recuperadas previamente de la caché

Puede haber situaciones en las que las ubicaciones recuperadas previamente deban borrarse durante una sesión. Por ejemplo, cuando se realiza una reservación, tiene sentido borrar las ubicaciones en caché, ya que el usuario está ahora &quot;comprometido&quot; y comprende el proceso de reservación. Si reservan otro viaje durante la sesión, no necesitarán las ubicaciones originales en la pantalla de inicio y en la pantalla de resultados de búsqueda para guiar su reservación. Tendría más sentido borrar las ubicaciones de la memoria caché y recuperar previamente nuevas ofertas para, tal vez, una segunda reservación con descuento u otro escenario relevante. Se puede agregar lógica a la pantalla de inicio y a la pantalla de resultados de búsqueda para recuperar previamente nuevas ubicaciones si se ha realizado una reservación durante la sesión.

Para este ejemplo, solo borraremos las ubicaciones recuperadas previamente para la sesión cuando se realice una reservación. Esto se realiza llamando a la función `Target.clearPrefetchCache()`. Configure la función dentro de la función `targetLoadRequest()` como se muestra a continuación:

```java
Target.clearPrefetchCache()
```

![Borrar ubicaciones recuperadas previamente de la caché](assets/clearPrefetch.jpg)

¡Felicitaciones! Su aplicación ahora tiene el marco para la personalización. En la siguiente lección, mejoraremos nuestras capacidades de personalización agregando parámetros a estas ubicaciones.

**[SIGUIENTE: &quot;Añadir parámetros&quot; >](add-parameters.md)**
