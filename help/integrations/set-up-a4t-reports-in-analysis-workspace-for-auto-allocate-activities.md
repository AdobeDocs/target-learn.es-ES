---
title: Configurar informes de A4T en  [!DNL Analysis Workspace] para [!UICONTROL Auto-Allocate] actividades
description: ¿Cómo configuro informes de [!UICONTROL Analytics for Target] (A4T) en  [!DNL Adobe] [!DNL Analysis Workspace] al ejecutar actividades de [!UICONTROL Auto-Allocate]?
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 190a67832f378e15090115420bfaf8a4af4b9cb9
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%

---

# Configurar informes de A4T en [!DNL Analysis Workspace] para [!DNL Auto-Allocate] actividades

Una actividad [[!UICONTROL Auto-Allocate]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=es){target=_blank} en [!DNL Adobe Target] identifica un ganador entre dos o más experiencias y le reasigna automáticamente el tráfico de visitantes mientras la prueba sigue ejecutándose y aprendiendo. La integración de [!UICONTROL Analytics for Target] (A4T) para [!UICONTROL Auto-Allocate] le permite ver los datos de informes en [!DNL Adobe Analytics] y optimizar para los eventos personalizados o las métricas definidas en [!DNL Analytics].

Aunque las funcionalidades de análisis enriquecidas están disponibles en [!DNL Adobe Analytics] [!DNL Analysis Workspace], es posible que se requieran algunas modificaciones en el panel predeterminado [!UICONTROL Analytics for Target] para interpretar correctamente las actividades de [!UICONTROL Auto-Allocate]. Estas modificaciones son necesarias debido a los matices en [criterios de métricas de optimización](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=es#supported){target=_blank}.

Cada tipo de métrica de optimización requiere una configuración de informe diferente en A4T, como se indica a continuación:

* Usando una métrica [!DNL Analytics]

   * [!UICONTROL Maximize metric value per visitor]
   * [!UICONTROL Maximize unique visitor conversion rate]

* Usando una métrica de conversión definida por [!DNL Target]

Este tutorial cubre las directrices generales de A4T y los pasos de configuración de informes específicos de criterios.

## Métricas de Analytics con criterios de optimización &quot;[!UICONTROL Maximize Metric Value Per Visitor]&quot;

**Definición**: (Valor de métrica general) / (# de visitantes)

Para configurar el informe, realice los siguientes cambios en el informe de A4T:

| Cambios necesarios | Informe activado por [!DNL Target] | Informe del panel de A4T |
| --- | --- | --- |
| Maximizar valor de métrica para una métrica [!DNL Analytics] | <ul><li>Eliminar [!UICONTROL Confidence] métricas.</li><li>Quitar [!UICONTROL Lift (Low)] y [!UICONTROL Lift (High)]. Conservar [!UICONTROL Lift (Med)].</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Conversion Rate] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li><li>Cambie el nombre de la métrica de tasa [!UICONTROL Conversion] a &quot;Métrica/Visitante&quot;.</li></ul> | <ul><li>Eliminar [!UICONTROL Confidence] métricas.</li><li>Quitar [!UICONTROL Lift (Low)] y [!UICONTROL Lift (High)] conservar [!UICONTROL Lift (Med)].</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Conversion Rate] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li><li>Cambie el nombre de la métrica de tasa [!UICONTROL Conversion] a &quot;Métrica/Visitante&quot;.</li><li>Asegúrese de que los intervalos de fecha y hora se alinean con los valores que ve en el informe [!DNL Target]. Consulte [Directrices generales para A4T](#guidance) a continuación.</li></ul> |

![Maximizar el valor de la métrica para los ingresos](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] métricas con criterios de optimización &quot;[!UICONTROL Unique Visitor Conversion Rate]&quot;

**Definición**: (# de visitantes únicos con un valor positivo de la métrica) / (Total de visitantes únicos)

Ejemplo: Supongamos que su métrica de optimización es [!UICONTROL Revenue]. Hay cinco visitantes únicos en la actividad y tres de ellos realizan una compra. En este ejemplo, este valor = (3 visitantes para los que [!UICONTROL Revenue] es positivo) / (5 visitantes únicos totales) = 0,6 = 60 %.

>[!NOTE]
>
>La tasa de conversión a la que se hace referencia aquí puede referirse a acciones fuera de pedidos, como clics, impresiones, etc. En estos casos, el criterio seguiría siendo maximizar el recuento de visitantes que hacen clic o ven la página, respectivamente.

Para configurar el informe, realice los siguientes cambios en el informe de A4T:

| Cambios necesarios | Informe activado por Target | Informe del panel de A4T |
| --- | --- | --- |
| Maximizar conversiones para una métrica [!DNL Analytics] | <ul><li>Eliminar [!UICONTROL Confidence] métricas.</li><li>Elimine las tres métricas [!UICONTROL Lift].</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Conversion Rate] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li></ul> | <ul><li>Eliminar [!UICONTROL Confidence] métricas.</li><li>Elimine las tres métricas [!UICONTROL Lift].</li><li>Cree un segmento para filtrar a los visitantes con un valor de métrica positivo que vieron la actividad analizada. Consulte [Crear un segmento](#segment) a continuación.</li><li>Reemplace la métrica [!UICONTROL Conversion Rate] que se rellena automáticamente de modo que sea la división entre [!UICONTROL Unique visitors] con un valor de métrica positivo y visitantes únicos. Consulte [Actualizar la métrica Tasa de conversión](#update-conversion-metric) a continuación.</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Conversion Rate] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li><li>Asegúrese de que los intervalos de fecha y hora se alinean con los valores que ve en el informe [!DNL Target]. Consulte [Directrices generales para A4T](#guidance) a continuación.</li></ul> |

### Informe del panel A4T predeterminado: directrices adicionales

Las secciones siguientes contienen más información sobre directrices adicionales al configurar el informe del panel A4T predeterminado.

#### Creación de segmentos {#segment}

1. Haga clic en el signo **&quot;+&quot;** junto a **[!UICONTROL Segments]** en el carril izquierdo.

   ![Signo más junto a los segmentos en el carril izquierdo.](/help/integrations/assets/plus-sign.png)

1. Asigne un título al segmento &quot;Visitantes con valor de métrica positivo&quot;.
1. En **[!UICONTROL Definition]**, junto a **[!UICONTROL Include]**, seleccione **[!UICONTROL Visitor]**.
1. En **[!UICONTROL Definition]**, seleccione la métrica de optimización de su actividad.

   En este ejemplo, suponga [!UICONTROL Revenue] como métrica de optimización.

1. Seleccione el operador &quot;[!UICONTROL is greater than]&quot; y después especifique &quot;0&quot;.

   Esta configuración filtra todos los visitantes con un valor de métrica positivo.

1. Haga clic en **[!UICONTROL Save]**.

   ![Valor de métrica positivo](/help/integrations/assets/positive-metric-value.png)

1. Agregue el segmento recién creado &quot;Visitantes con valor de métrica positivo&quot; al panel A4T.
1. Arrastre y suelte la métrica [!UICONTROL Unique Visitors] en la misma columna que &quot;Visitantes con valor de métrica positivo&quot;.

   Esta configuración crea un segmento de todos los visitantes únicos para los que el valor de la métrica es positivo. En este ejemplo, todos los visitantes únicos cuyos ingresos fueran superiores a cero.

#### Actualizar la métrica [!UICONTROL Conversion Rate] {#update-conversion-metric}

1. Si aún no lo ha hecho, quite la columna [!UICONTROL Conversion Rate] existente del panel, como se explica a continuación.
1. Agregue una métrica haciendo clic en el signo &quot;+&quot; junto a la sección **[!UICONTROL Metrics]** en el carril izquierdo.
1. Asigne a la métrica el nombre &quot;Tasa de conversión&quot; y defínala como &quot;([!UICONTROL Unique Visitors] con valor de métrica positivo)&quot; dividido por &quot;Visitantes únicos&quot;, como se muestra a continuación.

   Añada el segmento recién creado (pasos definidos a continuación) de Visitantes con valor de métrica positivo, el operador de división, la métrica Visitantes únicos en el numerador y Visitantes únicos como denominador.

   ![Tasa de conversión en el panel A4T.](/help/integrations/assets/conversion-rate.png)

1. Haga clic en **[!UICONTROL Save]**.

1. Arrastre y suelte la métrica &quot;Tasa de conversión&quot; recién creada en el panel existente.
1. Haga clic en el icono de engranaje y, a continuación, anule la selección de la casilla de verificación **[!UICONTROL Percent]**, ya que este valor puede generar confusión.

   La configuración correcta del informe debería generar un resultado similar a la siguiente ilustración:

   ![Tasa de conversión de visitas única en el informe del panel A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## Tasa de conversión definida por [!DNL Target]

Para configurar el informe, realice los siguientes cambios en el informe de A4T:

| Cambios necesarios | Informe activado por Target | Informe del panel de A4T |
| --- | --- | --- |
| Informes de [!DNL Analytics] con [!DNL Target] métrica de conversión | <ul><li>Eliminar [!UICONTROL Confidence] métricas.</li><li>Quitar [!UICONTROL Lift (Low)] y [!UICONTROL Lift (High)]. Mantener el alza (Med).</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Conversion Rate] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li></ul> | <ul><li>Eliminar [!UICONTROL Confidence] métricas.</li><li>Quitar [!UICONTROL Lift (Low)] y [!UICONTROL Lift (High)]. Conservar [!UICONTROL Lift (Med)].</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Conversion Rate] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li><li>Asegúrese de que los intervalos de fecha y hora se alinean con los valores que ve en el informe [!DNL Target]. Consulte [Directrices generales para A4T](#guidance) a continuación.</li></ul> |

La configuración correcta del informe debería generar un resultado similar a la siguiente ilustración:

![Conversiones de actividades](/help/integrations/assets/optimized-table.png)

## Directrices generales para A4T {#guidance}

Puede navegar a un panel [!UICONTROL Analytics for Target] generado previamente si hace clic en el vínculo desde la pantalla del informe en [!UICONTROL Target] (esto se conoce más adelante en esta guía como el informe activado por [!DNL Target]). También puede crear el panel A4T en [!DNL Analytics] (los detalles se encuentran más adelante en esta sección).

Las siguientes secciones especifican qué configuraciones son necesarias, según cuál de estos métodos elija. Sin embargo, los siguientes pasos sirven como guía general para A4T:

* Elimine las métricas de confianza del panel A4T independientemente del método de creación del panel (ambos se detallan a continuación). En su lugar, haga referencia a estos valores en los informes de [!DNL Target]. Además, los ganadores de las actividades se pueden identificar en los informes de [!DNL Target]. Encontrará detalles sobre la identificación del ganador de la actividad en la sección [Identificar al ganador de la actividad](#winner) a continuación.
&#x200B;>>
* Para evitar confusiones, desmarque la presentación &quot;[!UICONTROL Percent]&quot; de la métrica [!UICONTROL Conversion Rate]. Ver [Ocultar el porcentaje de la columna [!UICONTROL Conversion Rate]](#hide-percentage) a continuación.
&#x200B;>>
* Si está creando un panel de A4T, asegúrese de que los intervalos de fecha y hora coinciden con los del informe [!DNL Target]. Consulte [Alinear la fecha y la hora en el panel A4T](#aligning-date-and-time) a continuación.

### Ocultar el porcentaje de la columna [!UICONTROL Conversion Rate] {#hide-percentage}

1. Haga clic en el icono **engranaje** junto al título de la columna [!UICONTROL Conversion Rate].

   ![Icono de engranaje en la columna Tasa de conversión](/help/integrations/assets/coversion-rate-gear-icon.png)

   Se muestra el cuadro de diálogo de configuración de [!UICONTROL Column]:

   ![Cuadro de diálogo de configuración de columna](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Anule la selección de la casilla **[!UICONTROL Percent]**.

   El panel de A4T ahora no incluye porcentajes como [!UICONTROL Conversion Rate] y coincide con [!DNL Target], como se muestra a continuación:

   ![Columna Tasa de conversión sin porcentajes](/help/integrations/assets/no-percentages.png)

### Alinee la fecha y la hora en el panel A4T {#aligning-date-and-time}

1. Debajo de cada panel, compruebe el intervalo de fechas al que hace referencia el panel para asegurarse de que el intervalo de fechas coincide con el del informe [!DNL Target].

   ![Intervalo de fecha en el panel A4T](/help/integrations/assets/date-range.png)

1. En [!DNL Analytics], establezca el intervalo de tiempo en 12:00am - 11:59pm.

### Identificación del ganador de la actividad {#winner}

Se seleccionan [!DNL Auto-Allocate] ganadores de actividad cuando existe una tasa de conversión ganadora con valores de confianza superiores o iguales al 95 %. Se debe hacer referencia a estos valores en los informes [!DNL Target], ya que los cálculos de confianza reflejan las recomendaciones de los métodos más conservadores [!DNL Target] para las actividades [!UICONTROL Auto-Allocate]. Consulte [Garantías estadísticas de asignación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html?lang=es#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} en *[!UICONTROL Adobe Target Business Practitioner Guide]*.

>[!NOTE]
>
>Los distintivos &quot;Ningún ganador aún&quot; y &quot;Ganador&quot; no están disponibles en el panel A4T de [!DNL Analysis Workspace]. Además, se debe ignorar el distintivo de &quot;estrella&quot; ganadora que se muestra en los informes [!DNL Target] para las actividades [!UICONTROL Auto-Allocate]. Ver [Asignación automática](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=es#aa){target=_blank} en *Compatibilidad de A4T con actividades de Asignación automática y Segmentación automática* en *[!UICONTROL Adobe Target Business Practitioner Guide]*.

### Crear A4T para el panel [!UICONTROL Auto-Allocate] en [!DNL Analysis Workspace]

1. Para crear un panel de A4T para un informe de actividad [!UICONTROL Auto-Allocate], comience con el panel [!UICONTROL Analytics for Target] en [!DNL Analysis Workspace], como se muestra a continuación.

   ![Informe de asignación automática de Analytics for Target](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Realice las siguientes selecciones:

   * **[!UICONTROL Control Experience]**: elija cualquier experiencia.
   * **[!UICONTROL Normalizing Metric]**: seleccione **[!UICONTROL Visitors]** (incluido en el panel A4T de forma predeterminada). [!UICONTROL Auto-Allocate] siempre normaliza las tasas de conversión para los visitantes únicos.
   * **Métricas de éxito**: seleccione la misma métrica (optimización) que utilizó durante la creación de la actividad. Si esta era una métrica de conversión definida por [!DNL Target], seleccione **[!UICONTROL Activity Conversion]**. De lo contrario, seleccione la métrica [!DNL Adobe Analytics] que utilizó.









