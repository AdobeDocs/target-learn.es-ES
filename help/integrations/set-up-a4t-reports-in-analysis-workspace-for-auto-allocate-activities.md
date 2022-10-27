---
title: Configuración de informes de A4T en Analysis Workspace para actividades de asignación automática
description: Una vez que haya configurado la integración de Analytics for Target (A4T) y esté ejecutando actividades de asignación automática, ¿cómo puede asegurarse de que está interpretando los resultados correctamente? Siga estos pasos para configurar los informes de A4T en Analysis Workspace y obtener los resultados esperados al ejecutar actividades de asignación automática.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
source-git-commit: dfe191fe7dbe6fa1910fc0fdfd5b17a10ee175c1
workflow-type: tm+mt
source-wordcount: '1087'
ht-degree: 0%

---

# Configuración de informes de A4T en Analysis Workspace para [!DNL Auto-Allocate] actividades

Un [!DNL Auto-Allocate] actividad identifica un ganador entre dos o más experiencias y le reasigna automáticamente más tráfico mientras la prueba sigue ejecutándose y aprendiendo. La integración de Analytics for Target (A4T) para [!DNL Auto-Allocate] permite ver los datos de los informes en Adobe Analytics, e incluso puede optimizar eventos personalizados o métricas definidas en Adobe Analytics.

Aunque las funciones de análisis enriquecidos están disponibles en Adobe Analytics Analysis Workspace, algunas modificaciones de la **[!UICONTROL Analytics para Target]** para interpretar correctamente [!DNL Auto-Allocate] actividades, debido a los matices en [criterios de optimización](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported).

Este tutorial explica las modificaciones recomendadas para el análisis [!DNL Auto-Allocate] actividades en Workspace. Los conceptos clave son:

* Los visitantes siempre deben utilizarse como métrica de normalización en [!DNL Auto-Allocate] actividades.
* Cuando la métrica es una métrica de Adobe Analytics, el numerador apropiado para la tasa de conversión depende del tipo de criterios de optimización elegidos durante la configuración de la actividad.
   * El criterio de optimización &quot;maximizar la tasa de conversión de visitantes únicos&quot; tiene una tasa de conversión cuyo numerador es un recuento de los visitantes únicos con un valor positivo de la métrica.
   * El valor &quot;maximizar métrica por visitante* tiene una tasa de conversión cuyo numerador es el valor de métrica normal en Adobe Analytics. Esto se proporciona de forma predeterminada en la variable **[!UICONTROL Analytics para Target]** en Workspace.
* Cuando la métrica de optimización es una métrica de conversión definida en Target, la variable predeterminada **[!UICONTROL Analytics para Target]** del Workspace gestiona la configuración del panel.
* Los números de confianza que se ven en Workspace no reflejan la variable [estadísticas más conservadoras utilizadas por la asignación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=en#section_98388996F0584E15BF3A99C57EEB7629), y por lo tanto, debe eliminarse.


## Creación de A4T para [!DNL Auto-Allocate] panel en Workspace

Para crear un A4T para [!DNL Auto-Allocate] inicio del informe con la variable **[!UICONTROL Analytics para Target]** en Workspace, como se muestra a continuación. A continuación, realice las siguientes selecciones:

1. **[!UICONTROL Experiencia de control]**: Puede elegir cualquier experiencia
2. **[!UICONTROL Métrica de normalización]**: Seleccionar visitantes: la asignación automática siempre normaliza las tasas de conversión por visitantes únicos.
3. **[!UICONTROL Métricas de éxito]**: Seleccione la misma métrica que utilizó durante la creación de la actividad: si se trata de una métrica de conversión definida en Target, seleccione **Conversión de actividad**. De lo contrario, seleccione la métrica de Adobe Analytics que utilizó.

![AAFigure1.png](assets/AAFigure1.png)
*Figura 1: Configuración del panel Analytics for Target para [!DNL Auto-Allocate] actividades.*

>[!NOTE]
>
> También se puede llegar a un **[!UICONTROL Analytics para Target]** si hace clic en el vínculo desde la pantalla del informe en Adobe Target.

## Métricas de conversión de Target o métricas de Analytics con criterios de optimización &quot;Maximizar valor de métrica por visitante&quot;

Los controles predeterminados del panel de A4T [!DNL Auto-Allocate] actividades en las que la métrica de objetivo sea Conversión de Target o Métrica de Analytics con el criterio de optimización &quot;Maximizar el valor de métrica por visitante&quot;.

Se muestra un ejemplo de este panel para la métrica Ingresos, donde se seleccionó &quot;Maximizar valor de métrica por visitante&quot; como criterio de optimización en el momento de la creación de la actividad. Como se ha mencionado anteriormente, [!DNL Auto-Allocate] utiliza cálculos de confianza más conservadores comparados con los utilizados por la variable **[!UICONTROL Analytics para Target]** panel. Por lo tanto, se recomienda eliminar la métrica de confianza, así como las métricas de alza inferior y superior relacionadas.

![Figura 2.png](assets/AAFigure2.png)
*Figura 2: El informe recomendado para [!DNL Auto-Allocate] actividades con una métrica de Analytics Maximice el valor de las métricas por los criterios de optimización de los visitantes. Para estos tipos de métricas, así como las métricas de conversión definidas por Target, la variable predeterminada **[!UICONTROL Analytics para Target]**en workspace.*


## Métricas de Analytics con criterios de optimización &quot;Maximizar la tasa de conversión de visitantes únicos&quot;

Cuando se utiliza una métrica de Adobe Analytics con un criterio de optimización de *Maximizar la tasa de conversión de visitantes únicos*, el valor predeterminado **[!UICONTROL Analytics para Target]** del espacio de trabajo debe modificarse.

La métrica de éxito ahora es un recuento de visitantes únicos para los que la métrica de conversión fue positiva. Esto se puede lograr creando un segmento que filtre a las visitas con un valor positivo de la métrica. Cree este segmento de la siguiente manera:

1. Seleccione el **Componentes** > **Crear segmento** en la barra de herramientas de Workspace.
1. Arrastre la métrica utilizada en el momento de la creación de la actividad del panel izquierdo al panel **Definición** del segmento.
1. Seleccionar los valores de la métrica que se **bueno que** un valor numérico de 0.
1. En el **Incluir** menú desplegable, seleccione **Visitantes**
1. Asigne un nombre adecuado al segmento

En la figura siguiente se muestra un ejemplo de la creación de segmentos, donde seleccionamos visitantes para los que los Ingresos son positivos.

![Figura 3.png](assets/AAFigure3.png)
*Figura 3: Creación de segmentos para métricas de Adobe Analytics con criterios de optimización iguales a Maximizar la tasa de conversión de visitantes únicos. En este ejemplo, la métrica es Ingresos y el objetivo de optimización es maximizar el número de visitantes con ingresos positivos.*

Una vez creado el segmento correspondiente, el valor predeterminado es  **[!UICONTROL Analytics para Target]** en workspace se puede modificar.

1. Añadir un segundo **Visitantes únicos** métrica junto con la columna de métrica visitantes existente
2. Arrastre el segmento recién creado debajo de la primera columna para producir un panel similar a la Figura 4. Observe la diferencia: el número de visitantes únicos con ingresos positivos es una fracción del número total de visitantes únicos asignados a cada experiencia.
   ![Figura 4.png](assets/AAFigure4.png)
   *Figura 4: Filtrado de visitantes únicos por el segmento recién creado*
3. Una tasa de conversión puede ser [calculado rápidamente](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en) al resaltar la primera y la segunda columnas, hacer clic con el botón derecho, seleccionar **Crear métrica a partir de la selección** > **Dividir**. La tasa de conversión predeterminada debe eliminarse y reemplazarse por esta nueva métrica calculada, como se muestra en la imagen siguiente. Es posible que tenga que editar la métrica recién calculada para que se muestre como un **Formato** > **Porcentaje** hasta dos lugares decimales como se muestra.
   ![Figura 4.png](assets/AAFigure5.png)

   *Figura 4: El panel de asignación automática final que muestra las tasas de conversión de una métrica de conversión de ingresos binarizada*


## Conclusión

Los pasos anteriores han demostrado cómo configurar correctamente [!DNL Workspace] para mostrar los datos de informes de asignación automática. Para resumir:

* Cuando la métrica es una métrica de conversión definida en Target o una métrica de Adobe Analytics con criterio de optimización *Maximizar el valor de la métrica por visitante*, se debe utilizar el panel de espacio de trabajo predeterminado configurado con visitantes como métrica de normalización.
* Cuando la métrica es una métrica de Adobe Analytics con el criterio de optimización &quot;Maximizar la tasa de conversión de visitantes únicos&quot;, debe utilizar una tasa de conversión definida como la fracción de visitantes para los que la métrica es positiva. Esto se hace creando un segmento correspondiente, que filtra la métrica de visitantes únicos.
