---
title: Configuración de informes de A4T en [!DNL Analysis Workspace] para [!UICONTROL Asignación automática] Actividades
description: ¿Cómo configuro los informes de A4T en? [!DNL Analysis Workspace] para obtener los resultados esperados al ejecutar [!UICONTROL Asignación automática] actividades.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 8ef61ac0abf008039561bebe7d8d20b84f447487
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# Configuración de informes de A4T en [!DNL Analysis Workspace] para [!DNL Auto-Allocate] actividades

Un [!DNL Auto-Allocate] La actividad identifica un ganador entre dos o más experiencias y le reasigna automáticamente el tráfico mientras la prueba sigue ejecutándose y aprendiendo. El [!UICONTROL Analytics for Target] Integración de (A4T) para [!UICONTROL Asignación automática] le permite ver los datos de los informes en [!DNL Adobe Analytics]e incluso puede optimizar para eventos personalizados o métricas definidas en [!DNL Analytics].

Aunque las funcionalidades de análisis enriquecidas están disponibles en [!DNL Adobe Analytics] [!DNL Analysis Workspace], algunas modificaciones en el valor predeterminado **[!UICONTROL Analytics for Target]** el panel puede ser necesario para interpretar correctamente [!DNL Auto-Allocate] actividades, debido a los matices en [criterios de métrica de optimización](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Este tutorial muestra las modificaciones recomendadas para el análisis [!DNL Auto-Allocate] actividades en [!DNL Analysis Workspace]. Los conceptos clave son:

* [!UICONTROL Visitantes] siempre debe utilizarse como métrica de normalización en [!DNL Auto-Allocate] actividades.
* Cuando la métrica es un [!DNL Adobe Analytics] métrica, el cálculo de la tasa de conversión varía, según el tipo de criterios de optimización definidos durante la configuración de la actividad.
   * La tasa de conversión &quot;maximizar el valor de la métrica por visitante&quot;: numerador es el valor de métrica normal en [!DNL Adobe Analytics] (esto se proporciona de forma predeterminada en las [!UICONTROL Analytics for Target] panel en [!DNL Analysis Workspace]).
      * Qué significa esto: maximiza el número de conversiones por visitante (&quot;contar cada uno por visitante&quot;).
      * Este método no requiere un segmento adicional para que coincida con la tasa de conversión mostrada en la variable [!DNL Target] IU.
   * La tasa de conversión &quot;maximizar la tasa de conversión de visitantes únicos&quot;: numerador es un recuento de los visitantes únicos con un valor positivo de la métrica.
      * Qué significa esto: maximiza el número de visitantes que realizan la conversión (&quot;contar una vez por visitante&quot;).
      * Este método *HACE* requiere la creación de un segmento adicional en los informes para que coincida con la tasa de conversión mostrada en la [!DNL Target] IU.

* Cuando la métrica de optimización sea un [!DNL Target] métrica de conversión definida, la predeterminada **[!UICONTROL Analytics for Target]** panel en [!DNL Analysis Workspace] controla la configuración del panel.
* Para todos [!UICONTROL Asignación automática] actividades creadas antes de [!DNL Target Standard/Premium] Versión 23.3.1 (30 de marzo de 2023) [!DNL Analytics Workspace] y [!DNL Target] mostrar el mismo valor para [!UICONTROL Confianza].

  Para todos [!UICONTROL Asignación automática] las actividades creadas después del 30 de marzo de 2023, los valores de intervalo de confianza vistos en [!DNL Analysis Workspace] no reflejan el [estadísticas más conservadoras utilizadas por [!UICONTROL Asignación automática]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html#section_98388996F0584E15BF3A99C57EEB7629){target=_blank} en si estas actividades tienen *ambos* de las siguientes condiciones:

   * [!DNL Analytics] como fuente de informes (A4T)
   * [!DNL Analytics] métricas de optimización

  Las métricas de confianza deben eliminarse del panel A4T. En su lugar, consulte estos valores en [!DNL Target] informes.

## Creación de A4T para [!DNL Auto-Allocate] panel en [!DNL Analysis Workspace]

Para crear un panel de A4T para una [!DNL Auto-Allocate] inicio del informe con **[!UICONTROL Analytics for Target]** panel en [!DNL Analysis Workspace], como se muestra a continuación. A continuación, realice las siguientes selecciones:

1. **[!UICONTROL Experiencia de control]**: puede elegir cualquier experiencia.
1. **[!UICONTROL Métrica de normalización]**: Seleccionar visitantes (los visitantes se incluyen en el panel A4T de forma predeterminada). [!DNL Auto-Allocate] siempre normaliza las tasas de conversión de los visitantes únicos.
1. **[!UICONTROL Métricas de éxito]**: Seleccione la misma métrica que utilizó durante la creación de la actividad. Si esto fuera un [!DNL Target] métrica de conversión definida, seleccione **Conversión de actividad**. De lo contrario, seleccione la [!DNL Adobe Analytics] métrica que ha utilizado.

![[!UICONTROL Analytics for Target] configuración del panel para [!DNL Auto-Allocate] actividades.](assets/AAFigure1.png)

*Figura 1: [!UICONTROL Analytics for Target] configuración del panel para [!DNL Auto-Allocate] actividades.*

También puede llegar a una versión prediseñada **[!UICONTROL Analytics for Target]** panel si hace clic en el vínculo desde la pantalla del informe en [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversión] métricas o [!DNL Analytics] métricas con criterios de optimización &quot;Maximizar el valor de las métricas por visitante&quot;

Cuando la métrica de objetivo es:

* Una métrica de conversión de Target
* Métrica de Analytics con el criterio de optimización &quot;Maximizar el valor de la métrica por visitante&quot;

El panel predeterminado de A4T configura automáticamente el informe.

Se muestra un ejemplo de este panel para [!UICONTROL Ingresos] , donde &quot;Maximizar el valor de la métrica por visitante&quot; se seleccionó como criterio de optimización en el momento de la creación de la actividad. Como se mencionó anteriormente, [!DNL Auto-Allocate] utiliza cálculos de confianza más conservadores en comparación con los utilizados en el **[!UICONTROL Analytics for Target]** panel. El Adobe recomienda eliminar la métrica de confianza del panel A4T, así como las métricas de alza inferior y superior relacionadas. En su lugar, consulte los valores de confianza en [!DNL Target] informes.

>[!NOTE]
>
>Los valores de confianza en los informes de A4T son menos conservadores que [!DNL Target] y podría indicar prematuramente un ganador para una [!UICONTROL Asignación automática] actividad.


![[!UICONTROL Informe de asignación automática de Analytics for Target] panel](assets/AAFigure2.png)

*Figura 2: El informe recomendado para [!DNL Auto-Allocate] actividades con un [!DNL Analytics] métrica &quot;Maximizar el valor de la métrica según los criterios de optimización de visitantes&quot;. Para estos tipos de métricas, así como [!DNL Target] métricas de conversión definidas, la opción predeterminada **[!UICONTROL Analytics for Target]**panel en [!DNL Analysis Workspace] se puede utilizar.*

## [!DNL Analytics] métricas con criterios de optimización &quot;Maximizar la tasa de conversión de visitantes únicos&quot;

El criterio de optimización &quot;Maximizar la tasa de conversión de visitantes únicos&quot; hace referencia al recuento de visitantes para los que el valor de la métrica es positivo. Por ejemplo: si la tasa de conversión se define como &quot;Ingresos&quot;, el criterio &quot;Maximizar tasa de conversión de visitante único&quot; se optimizaría en cuanto a la cantidad de visitantes únicos para los cuales los ingresos fueron buenos. En otras palabras, este criterio maximizaría el recuento de visitantes que generan ingresos, en lugar del valor de los ingresos en sí.

>[!NOTE]
>
>La tasa de conversión a la que se hace referencia aquí puede referirse a acciones fuera de pedidos, como clics, impresiones, etc. En estos casos, el criterio seguiría siendo maximizar el recuento de visitantes que hacen clic o ven la página, respectivamente.

El [!DNL Analytics for Target] panel en [!DNL Analysis Workspace] debe modificarse si este criterio de optimización se utiliza con un [!DNL Adobe Analytics] métrica.

Cuando se utiliza este criterio de optimización, la métrica de éxito es un recuento de visitantes únicos para los que la métrica de conversión fue positiva. Por lo tanto, para ver este valor, se debe crear un nuevo segmento que filtre a las visitas con un valor positivo para la métrica.

Cree este segmento como se indica a continuación:

1. Seleccione el **[!UICONTROL Componentes]** > **[!UICONTROL Crear segmento]** en la opción [!DNL Analysis Workspace] barra de herramientas.
1. Arrastre la métrica utilizada en el momento de la creación de la actividad desde el panel izquierdo al **[!UICONTROL Definición]** del segmento.
1. Seleccionar valores de la métrica que son **bueno que** un valor numérico de 0.
1. Desde el **[!UICONTROL Incluir]** menú desplegable, seleccione **[!UICONTROL Visitantes]**.
1. Asigne un nombre apropiado al segmento.

En la figura siguiente se muestra un ejemplo de la creación de segmentos, donde la métrica de éxito es [!UICONTROL Visitantes con ingresos positivos].

![[!UICONTROL Visitantes con ingresos positivos] segmentar en [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figura 3: Creación de segmentos para [!DNL Adobe Analytics] métricas con criterios de optimización iguales a &quot;[!UICONTROL Maximizar la tasa de conversión de visitantes únicos].&quot; En este ejemplo, la métrica es [!UICONTROL Ingresos]y el objetivo de optimización es maximizar el número de visitantes con ingresos positivos.*

Una vez creado el segmento correspondiente, puede modificar el valor predeterminado  **[!UICONTROL Analytics for Target]** panel en [!DNL Analysis Workspace] para ver los valores de los criterios de optimización. Esto se logra haciendo lo siguiente:

1. Añada un segundo **Visitantes únicos** junto con la existente [!UICONTROL Visitantes] columna de métrica.
2. Arrastre el segmento recién creado debajo de la primera columna para generar un panel similar a la Figura 4. Observe la diferencia en los valores de las columnas: la cantidad de visitantes únicos con ingresos positivos debe ser una fracción de la cantidad total de visitantes únicos asignados a cada experiencia (como se muestra a continuación).

   ![Figura 4.png](assets/AAFigure4.png)

   *Figura 4: Filtrado [!UICONTROL Visitantes únicos] por el segmento recién creado*

3. Una tasa de conversión puede ser [calculado rápidamente](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html) resaltando la primera y la segunda columna, haciendo clic con el botón derecho, seleccionando **[!UICONTROL Crear métrica a partir de selección]** > **[!UICONTROL Dividir]**.

   La tasa de conversión predeterminada debe eliminarse y reemplazarse por esta nueva métrica calculada, como se muestra en la imagen siguiente. Es posible que tenga que editar la métrica calculada recién creada para mostrarla como una **[!UICONTROL Formato]** > **[!UICONTROL Porcentaje]** hasta dos decimales, como se muestra.

   ![Figura 5.png](assets/AAFigure5.png)

   *Figura 5: La [!UICONTROL Asignación automática] panel que muestra las tasas de conversión de una métrica de conversión de ingresos binarizada*

## Resumen

Los pasos de este tutorial muestran cómo configurar correctamente [!DNL Analysis Workspace] para mostrar [!UICONTROL Asignación automática] datos de informes.

Para resumir:

* Cuando la métrica es un [!DNL Target] métrica de conversión definida para una [!DNL Adobe Analytics] métrica con el criterio de optimización &quot;Maximizar el valor de la métrica por visitante&quot;, se debe utilizar el panel predeterminado del espacio de trabajo configurado con los visitantes como métrica de normalización.
* Cuando la métrica es un [!DNL Adobe Analytics] métrica con el criterio de optimización &quot;Maximizar la tasa de conversión de visitantes únicos&quot;, debe determinar la fracción de visitantes con un valor de métrica positivo sobre el total de visitantes. Esto se hace creando un segmento correspondiente que filtra el [!UICONTROL Visitante único] en esa métrica.
