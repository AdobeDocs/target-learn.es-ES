---
title: Configuración de informes de A4T en [!DNL Analysis Workspace] para [!DNL Auto-Target] Actividades
description: ¿Cómo configuro los informes de A4T en [!DNL Analysis Workspace] para obtener los resultados esperados al ejecutar [!UICONTROL Segmentación automática] actividades?
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#premium newtab=true" tooltip="See what's included in Target Premium."
badgeBeta: label="Beta" type="Informative" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en#beta newtab=true" tooltip="What are Target Beta release features?"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
thumbnail: null
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 0c15c9f448556ba4f5746de62f0673c16202d65f
workflow-type: tm+mt
source-wordcount: '2253'
ht-degree: 1%

---

# Configuración de informes de A4T en [!DNL Analysis Workspace] para [!DNL Auto-Target] actividades

>[!IMPORTANT]
>
>Para [!UICONTROL Segmentación automática] actividades, debe registrar los informes en [!DNL Analytics Workspace] y cree manualmente un panel de A4T.

La variable [!UICONTROL Analytics para Target] Integración de (A4T) para [!DNL Auto-Target] las actividades utilizan el [!DNL Adobe Target] ensamblar algoritmos de aprendizaje automático (ML) para elegir la mejor experiencia para cada visitante en función de su perfil, comportamiento y contexto, todo ello mientras utiliza un [!DNL Adobe Analytics] métrica de objetivo.

Aunque las funciones de análisis enriquecidos están disponibles en [!DNL Adobe Analytics] [!DNL Analysis Workspace], algunas modificaciones al valor predeterminado **[!UICONTROL Analytics para Target]** para interpretar correctamente [!DNL Auto-Target] actividades, debido a diferencias entre las actividades de experimentación (manual [!UICONTROL Prueba A/B] y [!UICONTROL Asignación automática]) y actividades de personalización ([!UICONTROL [!UICONTROL Segmentación automática]]).

Este tutorial explica las modificaciones recomendadas para el análisis [!UICONTROL Segmentación automática] actividades en [!DNL Analysis Workspace], que se basan en los siguientes conceptos clave:

* La variable **[!UICONTROL Control y segmentación]** se puede utilizar para distinguir entre [!UICONTROL Control] experiencias en comparación con las que ofrece el [!UICONTROL Segmentación automática] ensamblado algoritmo ML.
* Las visitas deben utilizarse como métrica de normalización al ver desgloses de rendimiento a nivel de experiencia. Además, [La metodología de recuento predeterminada de Adobe Analytics puede incluir visitas en las que el usuario no ve realmente el contenido de la actividad](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics), pero este comportamiento predeterminado se puede modificar utilizando un segmento con ámbitos adecuados (detalles a continuación).
* La atribución de ámbito de retrospectiva de visita, también conocida como &quot;ventana de retrospectiva de visita&quot; en el modelo de atribución prescrito, la utiliza el [!DNL Adobe Target] Los modelos ML durante sus fases de formación y el mismo modelo de atribución (no predeterminado) deben utilizarse al desglosar la métrica de objetivo.

## Creación de A4T para [!UICONTROL Segmentación automática] panel en [!DNL Analysis Workspace]

Para crear un A4T para [!UICONTROL Segmentación automática] informe, comience con la variable **[!UICONTROL Analytics para Target]** panel en [!DNL Analysis Workspace], como se muestra a continuación, o comenzar con una tabla improvisada. A continuación, realice las siguientes selecciones:

1. **[!UICONTROL Experiencia de control]**: Puede elegir cualquier experiencia; sin embargo, anulará esta opción más adelante. Tenga en cuenta que para [!UICONTROL Segmentación automática] actividades, la experiencia de control es realmente una estrategia de control, que puede ser a) Servir aleatoriamente entre todas las experiencias o b) Servir una sola experiencia (esta opción se realiza en el momento de la creación de la actividad en [!DNL Adobe Target]). Incluso si optó por elegir (b), su [!UICONTROL Segmentación automática] actividad designó una experiencia específica como control. Debería seguir el enfoque descrito en este tutorial para analizar A4T para [!UICONTROL Segmentación automática] actividades.
2. **[!UICONTROL Métrica de normalización]**: Select [!UICONTROL Visitas].
3. **[!UICONTROL Métricas de éxito]**: Aunque puede seleccionar cualquier métrica de la que informar, generalmente debe ver los informes sobre la misma métrica que se eligió para la optimización durante la creación de la actividad en [!DNL Target].

   ![[!UICONTROL Analytics para Target] configuración del panel para [!UICONTROL Segmentación automática] actividades.](assets/Figure1.png)

   *Figura 1: [!UICONTROL Analytics para Target] configuración del panel para [!UICONTROL Segmentación automática] actividades.*

>[!TIP]
>
>Para configurar su [!UICONTROL Analytics para Target] panel para [!UICONTROL Segmentación automática] actividades, elegir cualquier experiencia de control, elegir [!UICONTROL Visitas] como la métrica de normalización y elija la misma métrica de objetivo que se eligió para la optimización durante [!DNL Target] creación de actividad.

## Utilice la variable [!UICONTROL Control y segmentación] para comparar la dimensión [!DNL Target] ensamblar el modelo ML a su control

El panel predeterminado de A4T está diseñado para Classic (manual) [!UICONTROL Prueba A/B] o [!UICONTROL Asignación automática] actividades en las que el objetivo es comparar el rendimiento de experiencias individuales con la experiencia de control. En [!UICONTROL Segmentación automática] sin embargo, las actividades de la primera comparación de pedidos deben estar entre el control *estrategia* y el objetivo *estrategia*. En otras palabras, determinar el alza del rendimiento general de la variable [!UICONTROL Segmentación automática] ensemble el modelo ML sobre la estrategia de control.

Para realizar esta comparación, utilice el **[!UICONTROL Control y segmentación (Analytics para Target)]** dimensión. Arrastre y suelte para reemplazar la variable **[!UICONTROL Experiencias de Target]** en el informe predeterminado de A4T.

Tenga en cuenta que esta sustitución invalida el valor predeterminado [!UICONTROL Alza y confianza] cálculos en el panel A4T. Para evitar confusiones, puede eliminar estas métricas del panel predeterminado y dejar el siguiente informe:

![[!UICONTROL Experiencias por conversiones de actividad] panel en [!DNL Analysis Workspace]](assets/Figure2.png)

*Figura 2: El informe de base recomendado para [!DNL Auto-Target] actividades. Este informe se ha configurado para comparar el tráfico de destino (servido por el modelo ML de ensamblado) con el tráfico de control.*

>[!NOTE]
>
>Actualmente, [!UICONTROL Alza y confianza] los números no están disponibles para [!UICONTROL Control y segmentación] dimensiones para informes de A4T para [!UICONTROL Segmentación automática]. Hasta que se añada la compatibilidad, [!UICONTROL Alza y confianza] se puede calcular manualmente descargando el [calculadora de confianza](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## Agregar desgloses de métricas a nivel de experiencia

Para obtener más información sobre el rendimiento del modelo ML de ensamblado, puede examinar los desgloses de nivel de experiencia del **[!UICONTROL Control y segmentación]** dimensión. En [!DNL Analysis Workspace], arrastre el **[!UICONTROL Experiencias de Target]** en el informe y, a continuación, desglose cada una de las dimensiones de control y de destino por separado.

![[!UICONTROL Experiencias por conversiones de actividad] panel en [!DNL Analysis Workspace]](assets/Figure3.png)

*Figura 3: Desglose de la dimensión objetivo por experiencias de Target*

Aquí se muestra un ejemplo del informe resultante.

![[!UICONTROL Experiencias por conversiones de actividad] panel en [!DNL Analysis Workspace]](assets/Figure4.png)

*Figura 4: Una [!UICONTROL Segmentación automática] informe con desgloses de nivel de experiencia. Tenga en cuenta que la métrica de objetivos puede ser diferente y que la estrategia de control puede tener una única experiencia.*

>[!TIP]
>
>En [!DNL Analysis Workspace], haga clic en el icono de engranaje para ocultar los porcentajes en la [!UICONTROL Tasa de conversión] para ayudar a mantener el foco en las tasas de conversión de la experiencia. Las tasas de conversión tendrán el formato de decimales, pero las interpretarán como porcentajes según corresponda.

## Por qué:[!UICONTROL Visitas]&quot; es la métrica de normalización correcta para [!UICONTROL Segmentación automática] actividades

Al analizar un [!UICONTROL Segmentación automática] actividad, elija siempre [!UICONTROL Visitas] como métrica de normalización predeterminada. [!UICONTROL Segmentación automática] personalización selecciona una experiencia para un visitante una vez por visita (formalmente, una vez por [!DNL Target] sesión), lo que significa que la experiencia mostrada a un visitante puede cambiar en cada visita. Por lo tanto, si usa [!UICONTROL Visitantes únicos] como métrica de normalización, el hecho de que un solo usuario termine viendo varias experiencias (en diferentes visitas) podría conllevar tasas de conversión confusas.

Un ejemplo sencillo demuestra este punto: considere un escenario en el que dos visitantes entren a una campaña que solo tenga dos experiencias. El primer visitante visita dos veces. Se les asigna la Experiencia A en la primera visita, pero la Experiencia B en la segunda visita (debido a que el estado de su perfil cambia en esa segunda visita). Después de la segunda visita, el visitante convierte realizando un pedido. La conversión se atribuye a la experiencia mostrada más recientemente (Experiencia B). El segundo visitante también visita dos veces y se muestra Experiencia B ambas veces, pero nunca convierte.

Permita comparar los informes de nivel de visitante y de nivel de visita:

| Experiencia | Visitantes únicos | Visitas | Conversiones | Tasa de conversión normalizada por visitantes | Tasa de conversión normalizada de visitas |
| --- | --- | --- | --- | --- | --- |
| Una | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33.3% |
| Totales | 2 | 4 | 1 | 50% | 25 % |

*Tabla 1: Ejemplo que compara informes normalizados por visitantes con informes normalizados por visitas para un escenario en el que las decisiones se mantienen fieles a una visita (y no al visitante, como sucede con las pruebas A/B normales). Las métricas normalizadas por visitantes son confusas en este escenario.*

Como se muestra en la tabla, hay una clara incongruencia de los números de nivel de visitante. A pesar de que hay dos visitantes únicos totales, no se trata de una suma de visitantes únicos individuales para cada experiencia. Aunque la tasa de conversión a nivel de visitante no es necesariamente incorrecta, cuando se compara una experiencia individual, las tasas de conversión a nivel de visita probablemente tengan mucho más sentido. Formalmente, la unidad de análisis (&quot;visitas&quot;) es la misma que la unidad de adherencia en la toma de decisiones, lo que significa que se pueden agregar y comparar desgloses de métricas a nivel de experiencia.

## Filtro para visitas reales a la actividad

La variable [!DNL Adobe Analytics] metodología de contabilización predeterminada para visitas a un [!DNL Target] la actividad puede incluir visitas en las que el usuario no interactuó con la [!DNL Target] actividad. Esto se debe al camino [!DNL Target] las asignaciones de actividad se mantienen en la variable [!DNL Analytics] contexto del visitante. Como resultado, el número de visitas al [!DNL Target] a veces la actividad puede estar inflada, lo que resulta en una depresión de las tasas de conversión.

Si prefiere informar sobre las visitas en las que el usuario interactuó con la variable [!UICONTROL Segmentación automática] actividad (mediante la entrada en la actividad, un evento de visualización o visita o una conversión), puede:

1. Cree un segmento específico que incluya las visitas desde la [!DNL Target] actividad en cuestión y, a continuación,
1. Filtre el [!UICONTROL Visitas] con este segmento.

**Para crear el segmento:**

1. Seleccione el **[!UICONTROL Componentes > Crear segmento]** en la [!DNL Analysis Workspace] barra de herramientas.
2. Especifique un **[!UICONTROL Título]** para su segmento. En el ejemplo que se muestra a continuación, se nombra el segmento [!DNL "Hit with specific Auto-Target activity"].
3. Arrastre el **[!UICONTROL Actividades de Target]** dimensión al segmento **[!UICONTROL Definición]** para obtener más información.
4. Utilice la variable **[!UICONTROL es igual que]** operador.
5. Busque su [!DNL Target] actividad.
6. Haga clic en el icono del engranaje y, a continuación, seleccione **[!UICONTROL Modelo de atribución > Instancia]** como se muestra en la figura siguiente.
7. Haga clic en **[!UICONTROL Guardar]**.

![Segmentar en [!DNL Analysis Workspace]](assets/Figure5.png)

*Figura 5: Utilice un segmento como el que se muestra aquí para filtrar la variable [!UICONTROL Visitas] en A4T para [!UICONTROL Segmentación automática] informe*

Una vez creado el segmento, utilícelo para filtrar el [!UICONTROL Visitas] , por lo que la variable [!UICONTROL Visitas] Esta métrica solo incluye las visitas en las que el usuario interactuó con la variable [!DNL Target] actividad.

**Para filtrar [!UICONTROL Visitas] uso de este segmento:**

1. Arrastre el segmento recién creado desde la barra de herramientas de componentes y pase el ratón por encima de la base del **[!UICONTROL Visitas]** etiqueta de métrica hasta un azul **[!UICONTROL Filtrar por]** aparece.
2. Libere el segmento. El filtro se aplica a esa métrica.

El panel final aparece de la siguiente manera:

![[!UICONTROL Experiencias por conversiones de actividad] panel en [!DNL Analysis Workspace]](assets/Figure6.png)

*Figura 6: Panel de informes con el segmento &quot;Visita con actividad de segmentación automática específica&quot; aplicado a la variable [!UICONTROL Visitas] métrica. Este segmento garantiza que solo las visitas en las que un usuario interactuó con la variable [!DNL Target] la actividad en cuestión se incluye en el informe.*

## Alinee la atribución entre la formación del modelo ML y la generación de métricas de objetivo

La integración de A4T permite el uso de [!UICONTROL Segmentación automática] Modelo ML que debe ser *entrenado* utilizando los mismos datos de evento de conversión que [!DNL Adobe Analytics] usa para *generar informes de rendimiento*. Sin embargo, hay ciertas hipótesis que deben emplearse para interpretar estos datos al entrenar los modelos ML, que difieren de las hipótesis por defecto realizadas durante la fase de notificación en [!DNL Adobe Analytics].

Específicamente, la variable [!DNL Adobe Target] Los modelos ML utilizan un modelo de atribución de ámbito de visita. Es decir, los modelos ML asumen que debe producirse una conversión en la misma visita como una visualización de contenido para la actividad a fin de que la conversión se &quot;atribuya&quot; a la decisión tomada por el modelo ML. Esto es necesario para [!DNL Target] garantizar la formación oportuna de sus modelos; [!DNL Target] no puede esperar hasta 30 días para una conversión (la ventana de atribución predeterminada para los informes de [!DNL Adobe Analytics]) antes de incluirlo en los datos de formación de sus modelos.

Por lo tanto, la diferencia entre la atribución utilizada por la variable [!DNL Target] Los modelos (durante la formación) frente a la atribución predeterminada utilizada en la consulta de datos (durante la generación de informes) pueden provocar discrepancias. Incluso puede parecer que los modelos ML tienen un rendimiento deficiente, cuando de hecho el problema reside en la atribución.

>[!TIP]
>
>Si los modelos ML están optimizando una métrica que se atribuye de forma diferente a la de las métricas que está viendo en un informe, es posible que los modelos no funcionen como se espera. Para evitar esta situación, asegúrese de que las métricas de objetivo del informe utilizan la misma atribución utilizada por la variable [!DNL Target] Modelos ML.

Para ver las métricas de objetivo que tienen la misma metodología de atribución utilizada por la variable [!DNL Target] Modelos ML, siga estos pasos:

1. Pase el ratón sobre el icono de engranaje de la métrica de objetivo:

   ![gearicon.png](assets/gearicon.png)

1. Desde el menú resultante, desplácese hasta **[!UICONTROL Configuración de datos]**.
1. Select **[!UICONTROL Uso de modelos de atribución no predeterminados]** (si no está seleccionada).

   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)

1. Haga clic en **[!UICONTROL Editar]**.
1. Select **[!UICONTROL Modelo]**: **[!UICONTROL Participación]** y **[!UICONTROL Ventana retroactiva]**: **[!UICONTROL Visita]**.

   ![Participación por visita.png](assets/ParticipationbyVisit.png)

1. Haga clic en **[!UICONTROL Aplicar]**. 

Estos pasos garantizan que el informe atribuya la métrica de objetivo a la visualización de la experiencia, si se ha producido el evento de métrica de objetivo *en cualquier momento* (&quot;participación&quot;) en la misma visita en la que se mostró una experiencia.

## Paso final: Cree una tasa de conversión que capture la magia de arriba

Con las modificaciones de la variable [!UICONTROL Visita] y métricas de objetivo en secciones anteriores, la modificación final que debe realizar para su A4T predeterminado para [!UICONTROL Segmentación automática] el panel de informes es crear tasas de conversión que sean la proporción correcta (la de una métrica de objetivo con la atribución correcta), a una métrica filtrada apropiadamente [!UICONTROL Visitas] métrica.

Para ello, cree un [!UICONTROL Métrica calculada] siguiendo estos pasos:

1. Seleccione el **[!UICONTROL Componentes > Crear métrica]** en la [!DNL Analysis Workspace] barra de herramientas.
1. Especifique un **[!UICONTROL Título]** para su métrica. Por ejemplo, &quot;Tasa de conversión corregida por la visita para la actividad XXX&quot;.
1. Select **[!UICONTROL Formato]** = Porcentaje y **[!UICONTROL Lugares decimales]** = 2.
1. Arrastre la métrica de objetivo correspondiente a su actividad (por ejemplo, [!UICONTROL Conversiones de actividades]) en la definición y utilice el icono de engranaje de esta métrica de objetivo para ajustar el modelo de atribución a (Participación|Visita), como se describió anteriormente.
1. Select **[!UICONTROL Agregar > Contenedor]** desde la parte superior derecha de la **[!UICONTROL Definición]** para obtener más información.
1. Seleccione el operador de división () entre los dos contenedores.
1. Arrastre el segmento creado anteriormente, denominado &quot;Visita con [!UICONTROL Segmentación automática] actividad&quot; en este tutorial para esta [!DNL Auto-Target] actividad.
1. Arrastre el **[!UICONTROL Visitas]** en el contenedor de segmento.
1. Haga clic en **[!UICONTROL Guardar]**.

La definición completa de la métrica calculada se muestra aquí.

![Figura 7.png](assets/Figure7.png)

*Figura 7: La definición de métrica de tasa de conversión del modelo corregida por la visita y la atribución. (Tenga en cuenta que esta métrica depende de la métrica y la actividad de objetivos. En otras palabras, esta definición de métrica no se puede reutilizar en todas las actividades).*

>[!IMPORTANT]
>
>La variable [!UICONTROL Conversión] la métrica de tasa del panel de A4T no está vinculada al evento de conversión o a la métrica de normalización de la tabla. Cuando realice las modificaciones sugeridas en este tutorial, la variable [!UICONTROL Conversión] la tasa no se adapta automáticamente a los cambios. Por lo tanto, si realiza la modificación en la atribución de evento de conversión o en la métrica de normalización (o en ambos), debe recordar como paso final para modificar también la variable [!UICONTROL Conversión] , como se muestra arriba.

## Resumen: Ejemplo final [!DNL Analysis Workspace] panel para [!UICONTROL Segmentación automática] informes

Al combinar todos los pasos anteriores en un solo panel, la figura siguiente muestra una vista completa del informe recomendado para [!UICONTROL Segmentación automática] Actividades de A4T. Este informe es el mismo que el utilizado por la variable [!DNL Target] Modelos ML para optimizar su métrica de objetivos. El informe incorpora todos los matices y recomendaciones examinados en este tutorial. Este informe es también el más cercano a las metodologías de contabilización utilizadas en la [!DNL Target]-basado en informes [!UICONTROL Segmentación automática] actividades.

Haga clic en para expandir la imagen.

![Informe final de A4T en [!DNL Analysis Workspace]](assets/Figure8.png "Informe de A4T en Analysis Workspace"){width="600" zoomable="yes"}

*Figura 8: El A4T final [!UICONTROL Segmentación automática] informe en [!DNL Adobe Analytics] [!DNL Workspace], que combina todos los ajustes a las definiciones de métricas descritas en las secciones anteriores de este tutorial.*
