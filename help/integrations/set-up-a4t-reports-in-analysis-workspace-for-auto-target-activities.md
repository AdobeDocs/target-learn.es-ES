---
title: Configuración de informes de A4T en Analysis Workspace para actividades de segmentación automática
description: Una vez que haya configurado la integración de Analytics for Target (A4T) y esté ejecutando actividades de segmentación automática, ¿cómo puede asegurarse de que está interpretando los resultados correctamente? Siga estos pasos para configurar los informes de A4T en Analysis Workspace y obtener los resultados esperados al ejecutar actividades de segmentación automática.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 58006a25-851e-43c8-b103-f143f72ee58d
source-git-commit: 1c09ae58070d9f55aab555531f9a03dacbb26f03
workflow-type: tm+mt
source-wordcount: '2653'
ht-degree: 1%

---

# Configuración de informes de A4T en Analysis Workspace para [!DNL Auto-Target] actividades

La integración de Analytics for Target (A4T) para [!DNL Auto-Target] las actividades utilizan los algoritmos de aprendizaje automático (ML) del ensamblado de Adobe Target para elegir la mejor experiencia para cada visitante en función de su perfil, comportamiento y contexto, todo ello mientras utiliza una métrica de objetivos de Adobe Analytics.

Aunque las funciones de análisis enriquecidos están disponibles en Adobe Analytics Analysis Workspace, algunas modificaciones de la **[!UICONTROL Analytics para Target]** para interpretar correctamente [!DNL Auto-Target] actividades, debido a diferencias entre actividades de experimentación (A/B manual y asignación automática) y actividades de personalización ([!DNL Auto-Target]).

Este tutorial explica las modificaciones recomendadas para el análisis [!DNL Auto-Target] actividades en Workspace, que se basan en los siguientes conceptos clave:

* La variable **[!UICONTROL Control y segmentación]** se puede utilizar para distinguir entre las experiencias de control y las que proporciona el [!DNL Auto-Target] ensamblado algoritmo ML.
* Las visitas deben utilizarse como métrica de normalización cuando se vean desgloses de rendimiento en el nivel de experiencia. Además, [La metodología de recuento predeterminada de Adobe Analytics puede incluir visitas en las que el usuario no ve realmente el contenido de la actividad](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-viewing-reports.html?lang=en#metrics), pero este comportamiento predeterminado se puede modificar utilizando un segmento con ámbitos adecuados (detalles a continuación).
* La atribución de ámbitos de retrospectiva de visita (también conocida como la &quot;ventana de retrospectiva de visita&quot; en el modelo de atribución prescrito) la utilizan los modelos ML de Adobe Target durante sus fases de formación y se debe utilizar el mismo modelo de atribución (no predeterminado) al desglosar la métrica de objetivo.

## Creación de A4T para [!DNL Auto-Target] panel en Workspace

Para crear un A4T para [!DNL Auto-Target] informe, comience con la variable **[!UICONTROL Analytics para Target]** en Workspace, como se muestra a continuación, o comenzar con una tabla improvisada. A continuación, realice las siguientes selecciones:

1. **[!UICONTROL Experiencia de control]**: Puede elegir cualquier experiencia; sin embargo, anulará esta opción más adelante. Tenga en cuenta que para [!DNL Auto-Target] , la experiencia de control es realmente una estrategia de control, que puede ser a) Servir aleatoriamente entre todas las experiencias o b) Servir una sola experiencia (esta opción se realiza en el momento de la creación de la actividad en Adobe Target). Incluso si optó por la opción (b), su [!DNL Auto-Target] actividad designada como una experiencia específica como Control; debe seguir el enfoque descrito en este tutorial para analizar A4T para [!DNL Auto-Target] actividades.
2. **[!UICONTROL Métrica de normalización]**: Seleccione Visitas.
3. **[!UICONTROL Métricas de éxito]**: Aunque puede seleccionar cualquier métrica en la que desee informar, generalmente debe ver los informes sobre la misma métrica que se eligió para la optimización durante la creación de la actividad en Adobe Target.

![Figura 1.png](assets/Figure1.png)
*Figura 1: Configuración del panel Analytics for Target para [!DNL Auto-Target] actividades.*

>[!NOTE]
>
>Para configurar el panel Analytics for Target para actividades de segmentación automática , elija cualquier experiencia de control, elija Visitas como métrica de normalización y elija la misma métrica de objetivo que se eligió para la optimización durante la creación de la actividad de Target.

## Utilice la dimensión Control vs. Targeted para comparar el modelo ML de ensamblado de Adobe Target con su control

El panel predeterminado de A4T está diseñado para pruebas A/B clásicas (manuales) o actividades de asignación automática, cuyo objetivo es comparar el rendimiento de experiencias individuales con la experiencia de control. En [!DNL Auto-Target] sin embargo, las actividades de la primera comparación de pedidos deberían estar entre el Control *estrategia* y el objetivo *estrategia* (es decir, determinar el alza del rendimiento global de la variable [!DNL Auto-Target] modelo ML de ensamblado sobre la estrategia de control).

Para realizar esta comparación, utilice el **[!UICONTROL Control y segmentación (Analytics para Target)]** dimensión. Arrastre y suelte para reemplazar la variable **[!UICONTROL Experiencias de Target]** en el informe predeterminado de A4T.

Tenga en cuenta que esta sustitución invalida los cálculos predeterminados de Alza y confianza en el panel de A4T. Para evitar confusiones, puede eliminar estas métricas del panel predeterminado y dejar el siguiente informe:

![Figura 2.png](assets/Figure2.png)
*Figura 2: El informe de base recomendado para [!DNL Auto-Target] actividades. Este informe se ha configurado para comparar el tráfico segmentado (servido por el modelo ML de ensamblado) con el tráfico de Control.*

>[!NOTE]
>
>Actualmente, los números de Alza y Confianza no están disponibles para dimensiones de Control o Segmentación en informes de A4T para Segmentación automática. Hasta que no se añada la compatibilidad, el alza y la confianza se pueden calcular manualmente descargando la variable [calculadora de confianza](https://experienceleague.adobe.com/docs/target/assets/complete_confidence_calculator.xlsx?lang=en).

## Agregar desgloses de métricas a nivel de experiencia

Para obtener más información sobre el rendimiento del modelo ML de ensamblado, puede examinar los desgloses de nivel de experiencia del **[!UICONTROL Control y segmentación]** dimensión. En Workspace, arrastre el **[!UICONTROL Experiencias de Target]** en el informe y, a continuación, desglose cada una de las dimensiones Control y Segmentación por separado.

![Figura 3.png](assets/Figure3.png)
*Figura 3: Desglose de la dimensión objetivo por experiencias de Target*

Aquí se muestra un ejemplo del informe resultante.

![Figura 4.png](assets/Figure4.png)
*Figura 4: Una [!DNL Auto-Target] informe con desgloses de nivel de experiencia. Tenga en cuenta que la métrica de objetivo puede ser diferente y que la estrategia de control puede tener una única experiencia.*

>[!TIP]
>
>En Workspace, haga clic en el icono de engranaje para ocultar los porcentajes en la columna Tasa de conversión y así mantener el foco en las tasas de conversión de la experiencia. Tenga en cuenta que las tasas de conversión tendrán un formato de decimales, pero las interpretarán como porcentajes según corresponda.

## Por qué &quot;Visitas&quot; es la métrica de normalización correcta para [!DNL Auto-Target] actividades

Al analizar un [!DNL Auto-Target] actividad, seleccione siempre Visitas como métrica de normalización predeterminada. [!DNL Auto-Target] personalización selecciona una experiencia para un visitante una vez por visita (formalmente, una vez por sesión de Adobe Target), lo que significa que la experiencia mostrada a un usuario puede cambiar en cada visita. Por lo tanto, si usa Visitantes únicos como métrica de normalización, el hecho de que un solo usuario termine viendo varias experiencias (en diferentes visitas) podría conllevar tasas de conversión confusas.

Un ejemplo sencillo demuestra este punto: considere un escenario en el que dos visitantes entren a una campaña que solo tenga dos experiencias. El primer visitante visita dos veces. Se les asigna la Experiencia A en la primera visita, pero la Experiencia B en la segunda visita (debido a que el estado de su perfil cambia en esa segunda visita). Después de la segunda visita, el visitante convierte realizando un pedido. La conversión se atribuye a la experiencia mostrada más recientemente (Experiencia B). El segundo visitante también visita dos veces y se muestra Experiencia B ambas veces, pero nunca convierte.

Permita comparar los informes de nivel de visitante y de nivel de visita:

| Experiencia | Visitantes únicos | Visitas | Conversiones | Norma de visitante. Conv. de pulsaciones | La norma de la visita. Conv. de pulsaciones |
| --- | --- | --- | --- | --- | --- |
| Una | 1 | 1 | - | 0% | 0% |
| B | 2 | 3 | 1 | 50% | 33,3 % |
| Totales | 2 | 4 | 1 | 50 % | 25 % |
*Tabla 1: Ejemplo que compara informes normalizados por visitantes con informes normalizados por visitas para un escenario en el que las decisiones se mantienen fieles a una visita (y no al visitante, como sucede con las pruebas A/B normales). Las métricas normalizadas por visitantes son confusas en este escenario.*

Como se muestra en la tabla, hay una clara incongruencia de los números de nivel de visitante. A pesar de que hay dos visitantes únicos totales, no se trata de una suma de visitantes únicos individuales para cada experiencia. Aunque la tasa de conversión a nivel de visitante no es necesariamente incorrecta, cuando se compara una experiencia individual, las tasas de conversión a nivel de visita probablemente tengan mucho más sentido. Formalmente, la unidad de análisis (&quot;visitas&quot;) es la misma que la unidad de adherencia en la toma de decisiones, lo que significa que se pueden agregar y comparar desgloses de métricas a nivel de experiencia.

## Filtro para visitas reales a la actividad

La metodología de contabilización predeterminada de Adobe Analytics para las visitas a una actividad de Target puede incluir las visitas en las que el usuario no interactuó con la actividad de Target. Esto se debe a la forma en que las asignaciones de actividades de Target se mantienen en el contexto de visitante de Analytics. Como resultado, el número de visitas a la actividad de Target a veces se puede aumentar, lo que resulta en una disminución de las tasas de conversión.

Si prefiere informar sobre las visitas en las que el usuario interactuó realmente con la actividad de segmentación automática (ya sea mediante la entrada en la actividad, un evento de visualización/visita o una conversión), puede:

1. Cree un segmento específico que incluya visitas de la actividad de Target en cuestión y, a continuación,
1. Filtre la métrica Visitas con este segmento.

**Para crear el segmento:**

1. Seleccione el **[!UICONTROL Componentes > Crear segmento]** en la barra de herramientas de Workspace.
2. Escriba un **[!UICONTROL Título]** para su segmento. En el ejemplo que se muestra a continuación, se nombra el segmento [!DNL "Hit with specific Auto-Target activity"].
3. Arrastre el **[!UICONTROL Actividades de Target]** dimensión al segmento **[!UICONTROL Definición]** para obtener más información.
4. Utilice la variable **[!UICONTROL es igual que]** operador.
5. Busque su actividad de Target específica.
6. Seleccione el icono de engranaje y seleccione **[!UICONTROL Modelo de atribución > Instancia]** como se muestra en la figura siguiente.
7. Haga clic en **[!UICONTROL Guardar]**.

![Figura 5.png](assets/Figure5.png)
*Figura 5: Utilice un segmento como el que se muestra aquí para filtrar la métrica Visitas de su A4T para [!DNL Auto-Target] informe*

Una vez creado el segmento, utilícelo para filtrar la métrica Visitas, de modo que la métrica Visitas solo incluya las visitas en las que el usuario interactuó con la actividad de Target.

**Para filtrar Visitas con este segmento:**

1. Arrastre el segmento recién creado desde la barra de herramientas de componentes y pase el ratón por encima de la base del **[!UICONTROL Visitas]** etiqueta de métrica hasta un azul **[!UICONTROL Filtrar por]** aparece.
2. Libere el segmento. El filtro se aplicará a esa métrica.

El panel final aparecerá de la siguiente manera.

![Figura 6.png](assets/Figure6.png)
*Figura 6: Panel de informes con el segmento &quot;Visita con actividad de segmentación automática específica&quot; aplicado a la variable [!UICONTROL Visitas] métrica. Esto garantiza que solo se incluyan en el informe las visitas en las que un usuario interactuó realmente con la actividad de Target en cuestión.*

## Asegúrese de que la métrica de objetivo y la atribución estén alineadas con su criterio de optimización

La integración de A4T permite [!DNL Auto-Target]Modelo ML de *entrenado* uso de los mismos datos de evento de conversión que utiliza Adobe Analytics para *generar informes de rendimiento*. Sin embargo, hay ciertas hipótesis que deben emplearse para interpretar estos datos al entrenar los modelos ML, que difieren de los supuestos predeterminados realizados durante la fase de notificación en Adobe Analytics.

Específicamente, los modelos ML de Adobe Target utilizan un modelo de atribución con ámbito de visita. Es decir, asumen que una conversión debe ocurrir en la misma visita como una visualización de contenido para la actividad, para que la conversión se &quot;atribuya&quot; a la decisión tomada por el modelo ML. Esto es necesario para que Target garantice la formación oportuna de sus modelos; Target no puede esperar hasta 30 días para una conversión (la ventana de atribución predeterminada para informes en Adobe Analytics) antes de incluirla en los datos de capacitación de sus modelos.

Por lo tanto, la diferencia entre la atribución utilizada por los modelos de Target (durante la formación) y la atribución predeterminada utilizada en la consulta de datos (durante la generación del informe) puede provocar discrepancias. Incluso puede parecer que los modelos ML tienen un rendimiento deficiente, cuando de hecho el problema reside en la atribución.


>[!TIP]
>
>Si los modelos ML están optimizando una métrica que se atribuye de forma diferente a la de las métricas que está viendo en un informe, es posible que los modelos no funcionen como se espera. Para evitarlo, asegúrese de que las métricas de objetivo de su informe utilicen la misma definición de métrica y atribución utilizada por los modelos ML de Target.

La definición exacta de la métrica y la configuración de atribución dependen de la variable [criterio de optimización](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported) especificado durante la creación de la actividad.


### Conversiones definidas de Target o métricas de Analytics con *Maximizar el valor de la métrica por visita*

Cuando la métrica es una conversión de Target o una métrica de Analytics con **Maximizar el valor de la métrica por visita**, la definición de métrica de objetivo permite que se produzcan varios eventos de conversión en la misma visita.
Para ver las métricas de objetivo que tienen la misma metodología de atribución utilizada por los modelos ML de Adobe Target, siga estos pasos:

1. Pase el ratón sobre el icono de engranaje de la métrica de objetivo:
   ![gearicon.png](assets/gearicon.png)
1. Desde el menú resultante, desplácese hasta **[!UICONTROL Configuración de datos]**.
1. Select **[!UICONTROL Uso de modelos de atribución no predeterminados]** (si no está seleccionado):
   ![non-defaultattributionmodel.png](assets/non-defaultattributionmodel.png)
1. Haga clic en **[!UICONTROL Editar]**.
1. Select **[!UICONTROL Modelo]**: **[!UICONTROL Participación]** y **[!UICONTROL Ventana retroactiva]**: **[!UICONTROL Visita]**.
   ![Participación por visita.png](assets/ParticipationbyVisit.png)
1. Haga clic en **[!UICONTROL Aplicar]**. 

Estos pasos garantizan que el informe atribuirá la métrica de objetivo a la visualización de la experiencia, si se ha producido el evento de métrica de objetivo *en cualquier momento* (&quot;participación&quot;) en la misma visita en la que se mostró una experiencia.

### Métricas de Analytics con *Tasas de conversión de visitas únicas*

**Definir la visita con el segmento de métrica positiva**

En el escenario en el que seleccionó *Maximizar la tasa de conversión de visitas únicas* como criterio de optimización, la definición correcta de la tasa de conversión es la fracción de visitas en las que el valor de la métrica es positivo. Esto se puede lograr creando un segmento que filtre a las visitas con un valor positivo de la métrica y luego filtrando la métrica de visitas.


1. Como antes, seleccione **[!UICONTROL Componentes > Crear segmento]** en la barra de herramientas de Workspace.
2. Escriba un **[!UICONTROL Título]** para su segmento. En el ejemplo que se muestra a continuación, se nombra el segmento [!DNL "Visits with an order"].
3. Arrastre la métrica base que utilizó en su objetivo de optimización al segmento . En el ejemplo que se muestra a continuación, utilizamos la variable **pedidos** de modo que la tasa de conversión mida la fracción de visitas en las que se registra un pedido.
4. En la parte superior izquierda del contenedor de definición de segmento, seleccione **[!UICONTROL Incluir]** **Visita**.
5. Utilice la variable **[!UICONTROL es bueno que]** y establezca el valor en 0 (es decir, este segmento incluye visitas en las que la métrica pedidos es positiva)
6. Haga clic en **[!UICONTROL Guardar]**.

![Figura 7.png](assets/Figure7.png)
*Figura 7: El filtro de definición de segmento para las visitas con un orden positivo. En función de la métrica de optimización de su actividad, deberá reemplazar los pedidos por una métrica adecuada*

**Aplicar esto a las visitas en la métrica filtrada de actividad**

Este segmento ahora se puede usar para filtrar visitas con un número positivo de pedidos y en las que se produjo una visita para la variable [!DNL Auto-Target]actividad. El procedimiento para filtrar una métrica es similar al de antes y después de aplicar el nuevo segmento a la métrica de visitas ya filtrada, el panel de informes debería parecerse a la Figura 8

![Figura8.png](assets/Figure8.png)
*Figura 8: El panel de informe con la métrica de conversión de visita única correcta, es decir, el número de visitas en las que se registró una visita de la actividad y en las que la métrica de conversión (pedidos en este ejemplo) no fue cero.*


## Paso final: Cree una tasa de conversión que capture la magia de arriba

Con las modificaciones realizadas en las métricas Visita y Objetivo de las secciones anteriores, la modificación final que debe realizar en su A4T predeterminado para [!DNL Auto-Target] el panel de informes tiene como objetivo crear tasas de conversión que sean la proporción correcta (la de la métrica de objetivo corregida) y una métrica &quot;Visitas&quot; filtrada correctamente.

Para ello, cree una métrica calculada siguiendo los pasos siguientes:

1. Seleccione el **[!UICONTROL Componentes > Crear métrica]** en la barra de herramientas de Workspace.
1. Escriba un **[!UICONTROL Título]** para su métrica. Por ejemplo, &quot;Tasa de conversión corregida por la visita para la actividad XXX&quot;.
1. Select **[!UICONTROL Formato]** = Porcentaje y **[!UICONTROL Lugares decimales]** = 2.
1. Arrastre la métrica de objetivo correspondiente a su actividad (por ejemplo, Conversiones de actividad) a la definición y utilice el icono de engranaje de esta métrica de objetivo para ajustar el modelo de atribución a (Participación|Visita), como se describió anteriormente.
1. Select **[!UICONTROL Agregar > Contenedor]** desde la parte superior derecha de la **[!UICONTROL Definición]** para obtener más información.
1. Seleccione el operador de división () entre los dos contenedores.
1. Arrastre el segmento creado anteriormente, denominado &quot;Visita con [!DNL Auto-Target] actividad&quot; en este tutorial: para este específico [!DNL Auto-Target] actividad.
1. Arrastre el **[!UICONTROL Visitas]** en el contenedor de segmento.
1. Haga clic en **[!UICONTROL Guardar]**.

>[!TIP]
>
> También puede crear esta métrica utilizando la variable [funcionalidad de métrica calculada rápida](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en).

La definición completa de la métrica calculada se muestra aquí.

![Figura9.png](assets/Figure9.png)
*Figura 9: La definición de métrica de tasa de conversión del modelo corregida por la visita y la atribución. (Tenga en cuenta que esta métrica depende de la métrica y la actividad de objetivos. En otras palabras, esta definición de métrica no se puede reutilizar en todas las actividades).*

>[!IMPORTANT]
>
>La métrica Tasa de conversión del panel de A4T no está vinculada al evento de conversión ni a la métrica de normalización de la tabla. Al realizar las modificaciones sugeridas en este tutorial, la tasa de conversión no se adapta automáticamente a los cambios. Por lo tanto, si realiza la modificación a una (o ambas) atribución de evento de conversión y a la métrica de normalización, debe recordar como último paso para modificar también la tasa de conversión, como se muestra arriba.

## Resumen: Panel de Workspace de muestra final para [!DNL Auto-Target] informes

Al combinar todos los pasos anteriores en un solo panel, la figura siguiente muestra una vista completa del informe recomendado para [!DNL Auto-Target] Actividades de A4T. Este informe es el mismo que el utilizado por los modelos de aprendizaje automático de Target para optimizar la métrica de objetivos e incorpora todos los matices y recomendaciones que se tratan en este tutorial. Este informe es también el más cercano a las metodologías de contabilización utilizadas en los informes tradicionales de Target [!DNL Auto-Target] actividades.

![Figura 10.png](assets/Figure10.png)
*Figura 10: El A4T final [!DNL Auto-Target] en Adobe Analytics Workspace, que combina todos los ajustes a las definiciones de métricas descritas en las secciones anteriores de este documento.*
