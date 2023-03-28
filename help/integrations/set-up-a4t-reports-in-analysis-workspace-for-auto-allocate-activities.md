---
title: Configuración de informes de A4T en [!DNL Analysis Workspace] para [!UICONTROL Asignación automática] Actividades
description: ¿Cómo configuro los informes de A4T en [!DNL Analysis Workspace] para obtener los resultados esperados al ejecutar [!UICONTROL Asignación automática] actividades.
role: User
badgeBeta: label="Beta" type="Informative" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#beta newtab=true" tooltip="What are Target Beta release features?"
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: b29362ea45196d09dcbfbceeaaed5bc20467ea16
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Configuración de informes de A4T en [!DNL Analysis Workspace] para [!DNL Auto-Allocate] actividades

Un [!DNL Auto-Allocate] actividad identifica un ganador entre dos o más experiencias y le reasigna automáticamente más tráfico mientras la prueba sigue ejecutándose y aprendiendo. La variable [!UICONTROL Analytics para Target] Integración de (A4T) para [!UICONTROL Asignación automática] permite ver los datos de los informes en [!DNL Adobe Analytics]e incluso puede optimizar para eventos personalizados o métricas definidos en [!DNL Analytics].

Aunque las funciones de análisis enriquecidos están disponibles en [!DNL Adobe Analytics] [!DNL Analysis Workspace], algunas modificaciones al valor predeterminado **[!UICONTROL Analytics para Target]** para interpretar correctamente [!DNL Auto-Allocate] actividades, debido a los matices en [criterios de optimización](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Este tutorial explica las modificaciones recomendadas para el análisis [!DNL Auto-Allocate] actividades en [!DNL Analysis Workspace]. Los conceptos clave son:

* [!UICONTROL Visitantes] siempre debe utilizarse como métrica de normalización en [!DNL Auto-Allocate] actividades.
* Cuando la métrica es un [!DNL Adobe Analytics] , el numerador apropiado para la tasa de conversión depende del tipo de criterios de optimización elegidos durante la configuración de la actividad.
   * El criterio de optimización &quot;maximizar la tasa de conversión de visitantes únicos&quot; tiene una tasa de conversión cuyo numerador es un recuento de los visitantes únicos con un valor positivo de la métrica.
   * El valor &quot;maximizar métrica por visitante&quot; tiene una tasa de conversión cuyo numerador es el valor de métrica normal en [!DNL Adobe Analytics]. Esto se proporciona de forma predeterminada en la variable **[!UICONTROL Analytics para Target]** panel en [!DNL Analysis Workspace].
* Cuando la métrica de optimización sea [!DNL Target] métrica de conversión definida, la variable predeterminada **[!UICONTROL Analytics para Target]** panel en [!DNL Analysis Workspace] gestiona la configuración del panel.
* Para todos [!UICONTROL Asignación automática] actividades creadas antes de la [!DNL Target Standard/Premium] Versión 23.3.1 (30 de marzo de 2023) [!DNL Analytics Workspace] y [!DNL Target] mostrar el mismo valor para [!UICONTROL Confianza].

   Para todos [!UICONTROL Asignación automática] actividades creadas después del 30 de marzo de 2023, los valores de intervalo de confianza observados en [!DNL Analysis Workspace] no refleja el [estadísticas más conservadoras utilizadas por [!UICONTROL Asignación automática]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} si estas actividades tienen *both* de las condiciones siguientes:

   * [!DNL Analytics] como fuente de informes (A4T)
   * [!DNL Analytics] métricas de optimización

   If *both* de estas condiciones, las métricas de confianza deben eliminarse del panel A4T. En su lugar, haga referencia a estos valores en [!DNL Target] informes.

## Creación de A4T para [!DNL Auto-Allocate] panel en [!DNL Analysis Workspace]

Para crear un A4T para [!DNL Auto-Allocate] inicio del informe con la variable **[!UICONTROL Analytics para Target]** panel en [!DNL Analysis Workspace], como se muestra a continuación. A continuación, realice las siguientes selecciones:

1. **[!UICONTROL Experiencia de control]**: Puede elegir cualquier experiencia.
2. **[!UICONTROL Métrica de normalización]**: Seleccione Visitantes. [!DNL Auto-Allocate] normaliza siempre las tasas de conversión de visitantes únicos.
3. **[!UICONTROL Métricas de éxito]**: Seleccione la misma métrica que utilizó durante la creación de la actividad. Si era un [!DNL Target] métrica de conversión definida, seleccione **Conversión de actividad**. De lo contrario, seleccione la [!DNL Adobe Analytics] métrica que ha utilizado.

![[!UICONTROL Analytics para Target] configuración del panel para [!DNL Auto-Allocate] actividades.](assets/AAFigure1.png)

*Figura 1: [!UICONTROL Analytics para Target] configuración del panel para [!DNL Auto-Allocate] actividades.*

>[!NOTE]
>
> También puede llegar a un **[!UICONTROL Analytics para Target]** si hace clic en el vínculo desde la pantalla del informe en [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversión] métricas o [!DNL Analytics] métricas con criterios de optimización &quot;Maximizar valor de métrica por visitante&quot;

Los controles predeterminados del panel de A4T [!DNL Auto-Allocate] actividades en las que la métrica de objetivo sea una [!DNL Target] conversión o [!DNL Analytics] métrica con criterio de optimización &quot;Maximizar valor de métrica por visitante&quot;.

Se muestra un ejemplo de este panel para el [!UICONTROL Ingresos] , donde se seleccionó &quot;Maximizar valor de métrica por visitante&quot; como criterio de optimización en el momento de creación de la actividad. Como se ha mencionado anteriormente, [!DNL Auto-Allocate] utiliza cálculos de confianza más conservadores comparados con los utilizados en la variable **[!UICONTROL Analytics para Target]** panel. Adobe recomienda eliminar la métrica de confianza del panel de A4T, así como las métricas de alza inferior y superior relacionadas. En su lugar, consulte estos valores en [!DNL Target] informes.

![[!UICONTROL Analytics para Target: Informe de asignación automática] panel](assets/AAFigure2.png)

*Figura 2: El informe recomendado para [!DNL Auto-Allocate] actividades con un [!DNL Analytics] métrica &quot;Maximizar el valor de la métrica por optimización de visitante&quot;. Para estos tipos de métricas, así como [!DNL Target] métricas de conversión definidas, la variable predeterminada **[!UICONTROL Analytics para Target]**panel en [!DNL Analysis Workspace] se puede usar.*

## [!DNL Analytics] métricas con criterios de optimización &quot;Maximizar la tasa de conversión de visitantes únicos&quot;

Cuando una [!DNL Adobe Analytics] se usa con un criterio de optimización de *Maximizar la tasa de conversión de visitantes únicos*, el valor predeterminado **[!UICONTROL Analytics para Target]** panel en [!DNL Analysis Workspace] debe modificarse.

La métrica de éxito ahora es un recuento de visitantes únicos para los que la métrica de conversión fue positiva. Esto se puede lograr creando un segmento que filtre a las visitas con un valor positivo de la métrica. Cree este segmento de la siguiente manera:

1. Seleccione el **[!UICONTROL Componentes]** > **[!UICONTROL Crear segmento]** en la [!DNL Analysis Workspace] barra de herramientas.
1. Arrastre la métrica utilizada en el momento de la creación de la actividad del panel izquierdo al panel **[!UICONTROL Definición]** del segmento.
1. Seleccionar los valores de la métrica que se **bueno que** un valor numérico de 0.
1. En el **[!UICONTROL Incluir]** desplegable, seleccione **[!UICONTROL Visitantes]**.
1. Asigne un nombre adecuado al segmento.

En la figura siguiente se muestra un ejemplo de la creación de segmentos, donde selecciona [!UICONTROL Visitantes con ingresos positivos].

![[!UICONTROL Visitantes con ingresos positivos] segmento en [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figura 3: Creación de segmentos para [!DNL Adobe Analytics] métricas con criterios de optimización iguales a &quot;[!UICONTROL Maximizar la tasa de conversión de visitantes únicos].&quot; En este ejemplo, la métrica es [!UICONTROL Ingresos], y el objetivo de optimización es maximizar el número de visitantes con ingresos positivos.*

Una vez creado el segmento apropiado, el valor predeterminado es  **[!UICONTROL Analytics para Target]** panel en [!DNL Analysis Workspace] se puede modificar.

1. Añadir un segundo **Visitantes únicos** junto con la [!UICONTROL Visitantes] columna de métrica.
2. Arrastre el segmento recién creado debajo de la primera columna para producir un panel similar a la Figura 4. Observe la diferencia: el número de visitantes únicos con ingresos positivos es una fracción del número total de visitantes únicos asignados a cada experiencia.

   ![Figura 4.png](assets/AAFigure4.png)

   *Figura 4: Filtrado [!UICONTROL Visitantes únicos] por el segmento recién creado*

3. Una tasa de conversión puede ser [calculado rápidamente](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) resaltando la primera y la segunda columnas, haciendo clic con el botón derecho, seleccionando **[!UICONTROL Crear métrica a partir de la selección]** > **[!UICONTROL Dividir]**.

   La tasa de conversión predeterminada debe eliminarse y reemplazarse con esta nueva métrica calculada, como se muestra en la imagen siguiente. Es posible que tenga que editar la métrica recién calculada para que se muestre como un **[!UICONTROL Formato]** > **[!UICONTROL Porcentaje]** hasta dos lugares decimales como se muestra.

   ![Figura 5.png](assets/AAFigure5.png)

   *Figura 5: El final [!UICONTROL Asignación automática] panel que muestra las tasas de conversión de una métrica de conversión de ingresos binarizada*

## Resumen

Los pasos de este tutorial muestran cómo configurar correctamente [!DNL Analysis Workspace] para mostrar [!UICONTROL Asignación automática] datos de informes.

Para resumir:

* Cuando la métrica es un [!DNL Target] métrica de conversión definida o [!DNL Adobe Analytics] con el criterio de optimización &quot;Maximizar valor de métrica por visitante&quot;, se debe utilizar el panel de espacio de trabajo predeterminado configurado con los visitantes como métrica de normalización.
* Cuando la métrica es un [!DNL Adobe Analytics] con el criterio de optimización &quot;Maximizar la tasa de conversión de visitantes únicos&quot;, debe utilizar una tasa de conversión definida como la fracción de visitantes para los que la métrica es positiva. Esto se hace creando un segmento correspondiente que filtra el [!UICONTROL Visitante único] métrica.
