---
title: Cómo configurar informes de A4T en  [!DNL Analysis Workspace] para actividades de [!UICONTROL asignación automática]
description: ¿Cómo configuro los informes de [!UICONTROL Analytics for Target] (A4T) en  [!DNL Adobe] [!DNL Analysis Workspace] al ejecutar las actividades de [!UICONTROL Asignación automática]?
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
TQID: https://experienceleague.adobe.com/5oQMgqqxw2VN-6cb29j4bwEP6VYmGRLXIp5AMJ3WWM4
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: df62f171-ac37-440f-8f0f-f41a72ebdd34
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: c0b4abf2d4ead4d58a8db6e8970857b7b50dbe5c
workflow-type: tm+mt
source-wordcount: 1546
ht-degree: 0%

---

# Configurar informes de A4T en [!DNL Analysis Workspace] para [!DNL Auto-Allocate] actividades

Una actividad [[!UICONTROL de asignación automática]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html){target=_blank} en [!DNL Adobe Target] identifica un ganador entre dos o más experiencias y le reasigna automáticamente el tráfico de visitantes mientras la prueba sigue ejecutándose y aprendiendo. La integración de [!UICONTROL Analytics for Target] (A4T) para [!UICONTROL Asignación automática] le permite ver los datos de informes en [!DNL Adobe Analytics] y optimizar para los eventos personalizados o las métricas definidas en [!DNL Analytics].

Aunque hay funcionalidades de análisis enriquecidas disponibles en [!DNL Adobe Analytics] [!DNL Analysis Workspace], es posible que se necesiten algunas modificaciones en el panel predeterminado de [!UICONTROL Analytics for Target] para interpretar correctamente las actividades de [!UICONTROL Asignación automática]. Estas modificaciones son necesarias debido a los matices en [criterios de métricas de optimización](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Cada tipo de métrica de optimización requiere una configuración de informe diferente en A4T, como se indica a continuación:

* Usando una métrica [!DNL Analytics]

   * [!UICONTROL Maximizar valor de métrica por visitante]
   * [!UICONTROL Maximizar tasa de conversión de visitantes únicos]

* Usando una métrica de conversión definida por [!DNL Target]

Este tutorial cubre las directrices generales de A4T y los pasos de configuración de informes específicos de criterios.

## Métricas de Analytics con criterios de optimización &quot;[!UICONTROL Maximizar valor de métrica por visitante]&quot;

**Definición**: (Valor de métrica general) / (# de visitantes)

Para configurar el informe, realice los siguientes cambios en el informe de A4T:

| Cambios necesarios | Informe activado por [!DNL Target] | Informe del panel de A4T |
| --- | --- | --- |
| Maximizar valor de métrica para una métrica [!DNL Analytics] | <ul><li>Quitar métricas de [!UICONTROL Confianza].</li><li>Eliminar [!UICONTROL Alza (baja)] y [!UICONTROL Alza (alta)]. Mantener [!UICONTROL Alza (Med)].</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Tasa de conversión] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li><li>Cambie el nombre de la métrica de tasa de conversión [!UICONTROL Conversion] a &quot;Métrica/Visitante&quot;.</li></ul> | <ul><li>Quitar métricas de [!UICONTROL Confianza].</li><li>Eliminar [!UICONTROL Alza (baja)] y [!UICONTROL Alza (alta)] Mantener [!UICONTROL Alza (media)].</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Tasa de conversión] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li><li>Cambie el nombre de la métrica de tasa de conversión [!UICONTROL Conversion] a &quot;Métrica/Visitante&quot;.</li><li>Asegúrese de que los intervalos de fecha y hora se alinean con los valores que ve en el informe [!DNL Target]. Consulte [Directrices generales para A4T](#guidance) a continuación.</li></ul> |

![Maximizar el valor de la métrica para los ingresos](/help/integrations/assets/maximize-metric-value-revenue.png)

## [!DNL Analytics] métricas con criterios de optimización &quot;[!UICONTROL Tasa única de conversión de visitantes]&quot;

**Definición**: (# de visitantes únicos con un valor positivo de la métrica) / (Total de visitantes únicos)

Ejemplo: supongamos que su métrica de optimización es [!UICONTROL Ingresos]. Hay cinco visitantes únicos en la actividad y tres de ellos realizan una compra. En este ejemplo, este valor = (3 visitantes para los cuales [!UICONTROL Ingresos] es positivo) / (5 visitantes únicos totales) = 0,6 = 60 %.

>[!NOTE]
>
>La tasa de conversión a la que se hace referencia aquí puede referirse a acciones fuera de pedidos, como clics, impresiones, etc. En estos casos, el criterio seguiría siendo maximizar el recuento de visitantes que hacen clic o ven la página, respectivamente.

Para configurar el informe, realice los siguientes cambios en el informe de A4T:

| Cambios necesarios | Informe activado por Target | Informe del panel de A4T |
| --- | --- | --- |
| Maximizar conversiones para una métrica [!DNL Analytics] | <ul><li>Quitar métricas de [!UICONTROL Confianza].</li><li>Elimine las tres métricas de [!UICONTROL Lift].</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Tasa de conversión] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li></ul> | <ul><li>Quitar métricas de [!UICONTROL Confianza].</li><li>Elimine las tres métricas de [!UICONTROL Lift].</li><li>Cree un segmento para filtrar a los visitantes con un valor de métrica positivo que vieron la actividad analizada. Consulte [Crear un segmento](#segment) a continuación.</li><li>Reemplace la métrica [!UICONTROL Tasa de conversión] que se rellena automáticamente, de modo que sea la división entre [!UICONTROL visitantes únicos] con un valor de métrica positivo y visitantes únicos. Consulte [Actualizar la métrica Tasa de conversión](#update-conversion-metric) a continuación.</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Tasa de conversión] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li><li>Asegúrese de que los intervalos de fecha y hora se alinean con los valores que ve en el informe [!DNL Target]. Consulte [Directrices generales para A4T](#guidance) a continuación.</li></ul> |

### Informe del panel A4T predeterminado: directrices adicionales

Las secciones siguientes contienen más información sobre directrices adicionales al configurar el informe del panel A4T predeterminado.

#### Creación de segmentos {#segment}

1. Haga clic en el signo **&quot;+&quot;** junto a **[!UICONTROL Segmentos]** en el carril izquierdo.

   ![Signo más junto a los segmentos en el carril izquierdo.](/help/integrations/assets/plus-sign.png)

1. Asigne un título al segmento &quot;Visitantes con valor de métrica positivo&quot;.
1. En **[!UICONTROL Definición]**, junto a **[!UICONTROL Incluir]**, seleccione **[!UICONTROL Visitante]**.
1. En **[!UICONTROL Definición]**, seleccione la métrica de optimización de su actividad.

   En este ejemplo, suponga [!UICONTROL Revenue] como métrica de optimización.

1. Seleccione el operador &quot;[!UICONTROL es mayor que]&quot; y después especifique &quot;0&quot;.

   Esta configuración filtra todos los visitantes con un valor de métrica positivo.

1. Haga clic en **[!UICONTROL Guardar]**.

   ![Valor de métrica positivo](/help/integrations/assets/positive-metric-value.png)

1. Agregue el segmento recién creado &quot;Visitantes con valor de métrica positivo&quot; al panel A4T.
1. Arrastre y suelte la métrica [!UICONTROL Visitantes únicos] en la misma columna que &quot;Visitantes con valor de métrica positivo&quot;.

   Esta configuración crea un segmento de todos los visitantes únicos para los que el valor de la métrica es positivo. En este ejemplo, todos los visitantes únicos cuyos ingresos fueran superiores a cero.

#### Actualizar la métrica [!UICONTROL Tasa de conversión] {#update-conversion-metric}

1. Si aún no lo ha hecho, quite la columna [!UICONTROL Tasa de conversión] existente del panel, como se explica a continuación.
1. Agregue una métrica haciendo clic en el signo &quot;+&quot; junto a la sección **[!UICONTROL Métricas]** en el carril izquierdo.
1. Asigne a la métrica el nombre &quot;Tasa de conversión&quot; y defínala como &quot;([!UICONTROL Visitantes únicos] con valor de métrica positivo)&quot; dividido por &quot;Visitantes únicos&quot;, como se muestra a continuación.

   Añada el segmento recién creado (pasos definidos a continuación) de Visitantes con valor de métrica positivo, el operador de división, la métrica Visitantes únicos en el numerador y Visitantes únicos como denominador.

   ![Tasa de conversión en el panel A4T.](/help/integrations/assets/conversion-rate.png)

1. Haga clic en **[!UICONTROL Guardar]**.

1. Arrastre y suelte la métrica &quot;Tasa de conversión&quot; recién creada en el panel existente.
1. Haga clic en el icono de engranaje y, a continuación, anule la selección de la casilla de verificación **[!UICONTROL Percent]**, ya que este valor puede generar confusión.

   La configuración correcta del informe debería generar un resultado similar a la siguiente ilustración:

   ![Tasa de conversión de visitas única en el informe del panel A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## Tasa de conversión definida por [!DNL Target]

Para configurar el informe, realice los siguientes cambios en el informe de A4T:

| Cambios necesarios | Informe activado por Target | Informe del panel de A4T |
| --- | --- | --- |
| Informes de [!DNL Analytics] con [!DNL Target] métrica de conversión | <ul><li>Quitar métricas de [!UICONTROL Confianza].</li><li>Eliminar [!UICONTROL Alza (baja)] y [!UICONTROL Alza (alta)]. Mantener el alza (Med).</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Tasa de conversión] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li></ul> | <ul><li>Quitar métricas de [!UICONTROL Confianza].</li><li>Eliminar [!UICONTROL Alza (baja)] y [!UICONTROL Alza (alta)]. Mantener [!UICONTROL Alza (Med)].</li><li>Anule la selección de la presentación porcentual de la columna [!UICONTROL Tasa de conversión] para evitar confusiones. Consulte [Directrices generales para A4T](#guidance) a continuación.</li><li>Asegúrese de que los intervalos de fecha y hora se alinean con los valores que ve en el informe [!DNL Target]. Consulte [Directrices generales para A4T](#guidance) a continuación.</li></ul> |

La configuración correcta del informe debería generar un resultado similar a la siguiente ilustración:

![Conversiones de actividades](/help/integrations/assets/optimized-table.png)

## Directrices generales para A4T {#guidance}

Puede navegar a un panel [!UICONTROL Analytics for Target] generado previamente si hace clic en el vínculo desde la pantalla del informe en [!UICONTROL Target] (este se denomina más adelante en esta guía como el &quot;[!DNL Target] informe activado&quot;). También puede crear el panel A4T en [!DNL Analytics] (los detalles se encuentran más adelante en esta sección).

Las siguientes secciones especifican qué configuraciones son necesarias, según cuál de estos métodos elija. Sin embargo, los siguientes pasos sirven como guía general para A4T:

* Elimine las métricas de confianza del panel A4T independientemente del método de creación del panel (ambos se detallan a continuación). En su lugar, haga referencia a estos valores en los informes de [!DNL Target]. Además, los ganadores de las actividades se pueden identificar en los informes de [!DNL Target]. Encontrará detalles sobre la identificación del ganador de la actividad en la sección [Identificar al ganador de la actividad](#winner) a continuación.
>>
* Para evitar confusiones, desmarque la presentación &quot;[!UICONTROL Percent]&quot; de la métrica [!UICONTROL Tasa de conversión]. Ver [Ocultar el porcentaje de la [!UICONTROL columna Tasa de conversión]](#hide-percentage) a continuación.
>>
* Si está creando un panel de A4T, asegúrese de que los intervalos de fecha y hora coinciden con los del informe [!DNL Target]. Consulte [Alinear la fecha y la hora en el panel A4T](#aligning-date-and-time) a continuación.

### Ocultar el porcentaje de la columna [!UICONTROL Tasa de conversión] {#hide-percentage}

1. Haga clic en el icono **engranaje** junto al título de la columna [!UICONTROL Tasa de conversión].

   ![Icono de engranaje en la columna Tasa de conversión](/help/integrations/assets/coversion-rate-gear-icon.png)

   Se muestra el cuadro de diálogo de configuración [!UICONTROL Columna]:

   ![Cuadro de diálogo de configuración de columna](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Anule la selección de la casilla de verificación **[!UICONTROL Porcentaje]**.

   El panel de A4T ahora no incluye porcentajes como [!UICONTROL Tasa de conversión] y coincide con [!DNL Target], como se muestra a continuación:

   ![Columna Tasa de conversión sin porcentajes](/help/integrations/assets/no-percentages.png)

### Alinee la fecha y la hora en el panel A4T {#aligning-date-and-time}

1. Debajo de cada panel, compruebe el intervalo de fechas al que hace referencia el panel para asegurarse de que el intervalo de fechas coincide con el del informe [!DNL Target].

   ![Intervalo de fecha en el panel A4T](/help/integrations/assets/date-range.png)

1. En [!DNL Analytics], establezca el intervalo de tiempo en 12:00am - 11:59pm.

### Identificación del ganador de la actividad {#winner}

Se seleccionan [!DNL Auto-Allocate] ganadores de actividad cuando existe una tasa de conversión ganadora con valores de confianza superiores o iguales al 95 %. Se debe hacer referencia a estos valores en los informes [!DNL Target], ya que los cálculos de confianza reflejan las recomendaciones de los métodos más conservadores [!DNL Target] para las actividades [!UICONTROL Asignación automática]. Consulte [Garantías estadísticas de asignación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} en la *[!UICONTROL Guía para profesionales de Adobe Target]*.

>[!NOTE]
>
>Los distintivos &quot;Ningún ganador aún&quot; y &quot;Ganador&quot; no están disponibles en el panel A4T de [!DNL Analysis Workspace]. Además, se debe ignorar el distintivo de &quot;estrella&quot; ganador que se muestra en los informes [!DNL Target] para las actividades [!UICONTROL Asignación automática]. Consulte [Asignación automática](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} en *Compatibilidad de A4T con actividades de asignación automática y segmentación automática* en la *[!UICONTROL Guía para profesionales de Adobe Target]*.

### Crear A4T para el panel [!UICONTROL Asignación automática] en [!DNL Analysis Workspace]

1. Para crear un panel de A4T para un informe de actividad [!UICONTROL Asignación automática], comience con el panel [!UICONTROL Analytics for Target] en [!DNL Analysis Workspace], como se muestra a continuación.

   ![Informe de asignación automática de Analytics for Target](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Realice las siguientes selecciones:

   * **[!UICONTROL Experiencia de control]**: Elija cualquier experiencia.
   * **[!UICONTROL Métrica de normalización]**: seleccione **[!UICONTROL Visitantes]** (incluidos en el panel A4T de forma predeterminada). [!UICONTROL Asignación automática] siempre normaliza las tasas de conversión para los visitantes únicos.
   * **Métricas de éxito**: seleccione la misma métrica (optimización) que utilizó durante la creación de la actividad. Si esta era una métrica de conversión definida por [!DNL Target], seleccione **[!UICONTROL Conversión de actividad]**. De lo contrario, seleccione la métrica [!DNL Adobe Analytics] que utilizó.









