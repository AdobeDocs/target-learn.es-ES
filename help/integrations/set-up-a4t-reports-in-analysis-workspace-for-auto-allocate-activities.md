---
title: Configuración de informes de A4T en [!DNL Analysis Workspace] para [!UICONTROL Asignación automática] Actividades
description: ¿Cómo configuro los informes de A4T en? [!DNL Analysis Workspace] para obtener los resultados esperados al ejecutar [!UICONTROL Asignación automática] actividades.
badgeBeta: label="Beta" type="Informative"
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: ba33152906afda02ebf65365d9783ba8a4ea3c83
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 0%

---

# Configuración de informes de A4T en [!DNL Analysis Workspace] para [!DNL Auto-Allocate] actividades

>[!NOTE]
>
>Esta funcionalidad está actualmente en versión beta y estará disponible para todos los usuarios [!UICONTROL Target] clientes en una próxima versión.

Un [!DNL Auto-Allocate] actividad identifica un ganador entre dos o más experiencias y le reasigna automáticamente a este más tráfico mientras la prueba sigue ejecutándose y aprendiendo. El [!UICONTROL Analytics for Target] Integración de (A4T) para [!UICONTROL Asignación automática] le permite ver los datos de los informes en [!DNL Adobe Analytics]e incluso puede optimizar para eventos personalizados o métricas definidas en [!DNL Analytics].

Aunque las funcionalidades de análisis enriquecidas están disponibles en [!DNL Adobe Analytics] [!DNL Analysis Workspace], algunas modificaciones en el valor predeterminado **[!UICONTROL Analytics for Target]** Los paneles deben interpretar correctamente [!DNL Auto-Allocate] actividades, debido a los matices en [criterios de optimización](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#supported).

Este tutorial muestra las modificaciones recomendadas para el análisis [!DNL Auto-Allocate] actividades en [!DNL Analysis Workspace]. Los conceptos clave son:

* [!UICONTROL Visitantes] siempre debe utilizarse como métrica de normalización en [!DNL Auto-Allocate] actividades.
* Cuando la métrica es un [!DNL Adobe Analytics] , el numerador adecuado para la tasa de conversión depende del tipo de criterios de optimización elegidos durante la configuración de la actividad.
   * El criterio de optimización &quot;maximizar la tasa de conversión de visitantes únicos&quot; tiene una tasa de conversión cuyo numerador es un recuento de los visitantes únicos con un valor positivo de la métrica.
   * El valor de métrica &quot;maximizar&quot; por visitante* tiene una tasa de conversión cuyo numerador es el valor de métrica normal en [!DNL Adobe Analytics]. Esto se proporciona de forma predeterminada en la **[!UICONTROL Analytics for Target]** panel en [!DNL Analysis Workspace].
* Cuando la métrica de optimización sea un [!DNL Target] métrica de conversión definida, la predeterminada **[!UICONTROL Analytics for Target]** panel en [!DNL Analysis Workspace] controla la configuración del panel.
* El [!UICONTROL Confianza] números vistos en [!DNL Analysis Workspace] no reflejan el [estadísticas más conservadoras utilizadas por [!UICONTROL Asignación automática]](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html?lang=en#section_98388996F0584E15BF3A99C57EEB7629), por lo que se debe eliminar.

## Creación de A4T para [!DNL Auto-Allocate] panel en [!DNL Analysis Workspace]

Para crear un A4T para [!DNL Auto-Allocate] inicio del informe con **[!UICONTROL Analytics for Target]** panel en [!DNL Analysis Workspace], como se muestra a continuación. A continuación, realice las siguientes selecciones:

1. **[!UICONTROL Experiencia de control]**: puede elegir cualquier experiencia.
2. **[!UICONTROL Métrica de normalización]**: seleccione Visitantes. [!DNL Auto-Allocate] siempre normaliza las tasas de conversión de los visitantes únicos.
3. **[!UICONTROL Métricas de éxito]**: Seleccione la misma métrica que utilizó durante la creación de la actividad. Si esto fuera un [!DNL Target] métrica de conversión definida, seleccione **Conversión de actividad**. De lo contrario, seleccione la [!DNL Adobe Analytics] métrica que ha utilizado.

![[!UICONTROL Analytics for Target] configuración del panel para [!DNL Auto-Allocate] actividades.](assets/AAFigure1.png)

*Figura 1: [!UICONTROL Analytics for Target] configuración del panel para [!DNL Auto-Allocate] actividades.*

>[!NOTE]
>
> También puede llegar a una versión prediseñada **[!UICONTROL Analytics for Target]** panel si hace clic en el vínculo desde la pantalla del informe en [!DNL Adobe Target].

## [!DNL Target] [!UICONTROL Conversión] métricas o [!DNL Analytics] métricas con criterios de optimización &quot;Maximizar el valor de las métricas por visitante&quot;

El panel predeterminado de A4T gestiona [!DNL Auto-Allocate] actividades en las que la métrica objetivo es una [!DNL Target] conversión o una [!DNL Analytics] métrica con el criterio de optimización &quot;Maximizar el valor de la métrica por visitante&quot;.

Se muestra un ejemplo de este panel para [!UICONTROL Ingresos] , donde &quot;Maximizar el valor de la métrica por visitante&quot; se seleccionó como criterio de optimización en el momento de la creación de la actividad. Como se mencionó anteriormente, [!DNL Auto-Allocate] utiliza cálculos de confianza más conservadores en comparación con los utilizados en el **[!UICONTROL Analytics for Target]** panel. El Adobe recomienda eliminar la métrica de confianza, así como las métricas de alza inferior y superior relacionadas.

![[!UICONTROL Informe de asignación automática de Analytics for Target] panel](assets/AAFigure2.png)

*Figura 2: El informe recomendado para [!DNL Auto-Allocate] actividades con un [!DNL Analytics] métrica &quot;Maximizar el valor de la métrica según los criterios de optimización de visitantes&quot;. Para estos tipos de métricas, así como [!DNL Target] métricas de conversión definidas, la opción predeterminada **[!UICONTROL Analytics for Target]**panel en [!DNL Analysis Workspace] se puede utilizar.*

## [!DNL Analytics] métricas con criterios de optimización &quot;Maximizar la tasa de conversión de visitantes únicos&quot;

Cuando un [!DNL Adobe Analytics] se utiliza con un criterio de optimización de *Maximizar la tasa de conversión de visitantes únicos*, el valor predeterminado **[!UICONTROL Analytics for Target]** panel en [!DNL Analysis Workspace] debe modificarse.

La métrica de éxito ahora es un recuento de visitantes únicos para los que la métrica de conversión fue positiva. Esto se puede lograr creando un segmento que filtre las visitas individuales con un valor positivo de la métrica. Cree este segmento como se indica a continuación:

1. Seleccione el **[!UICONTROL Componentes]** > **[!UICONTROL Crear segmento]** en la opción [!DNL Analysis Workspace] barra de herramientas.
1. Arrastre la métrica utilizada en el momento de la creación de la actividad desde el panel izquierdo al **[!UICONTROL Definición]** del segmento.
1. Seleccionar valores de la métrica que son **bueno que** un valor numérico de 0.
1. Desde el **[!UICONTROL Incluir]** menú desplegable, seleccione **[!UICONTROL Visitantes]**.
1. Asigne un nombre apropiado al segmento.

En la figura siguiente, donde selecciona, se muestra un ejemplo de la creación de segmentos [!UICONTROL Visitantes con ingresos positivos].

![[!UICONTROL Visitantes con ingresos positivos] segmentar en [!DNL Analysis Workspace]](assets/AAFigure3.png)

*Figura 3: Creación de segmentos para [!DNL Adobe Analytics] métricas con criterios de optimización iguales a &quot;[!UICONTROL Maximizar la tasa de conversión de visitantes únicos].&quot; En este ejemplo, la métrica es [!UICONTROL Ingresos]y el objetivo de optimización es maximizar el número de visitantes con ingresos positivos.*

Una vez creado el segmento correspondiente, el valor predeterminado  **[!UICONTROL Analytics for Target]** panel en [!DNL Analysis Workspace] se puede modificar.

1. Añada un segundo **Visitantes únicos** junto con la existente [!UICONTROL Visitantes] columna de métrica.
2. Arrastre el segmento recién creado debajo de la primera columna para generar un panel similar a la Figura 4. Observe la diferencia: la cantidad de visitantes únicos con ingresos positivos es una fracción del número total de visitantes únicos asignados a cada experiencia.

   ![Figura 4.png](assets/AAFigure4.png)

   *Figura 4: Filtrado [!UICONTROL Visitantes únicos] por el segmento recién creado*

3. Una tasa de conversión puede ser [calculado rápidamente](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/components/calculated-metrics/quick-calculated-metrics-in-analysis-workspace.html?lang=en) resaltando la primera y la segunda columna, haciendo clic con el botón derecho, seleccionando **[!UICONTROL Crear métrica a partir de selección]** > **[!UICONTROL Dividir]**.

   La tasa de conversión predeterminada debe eliminarse y reemplazarse por esta nueva métrica calculada, como se muestra en la imagen siguiente. Es posible que tenga que editar la métrica calculada recién creada para mostrarla como una **[!UICONTROL Formato]** > **[!UICONTROL Porcentaje]** hasta dos decimales, como se muestra.

   ![Figura 5.png](assets/AAFigure5.png)

   *Figura 5: La [!UICONTROL Asignación automática] panel que muestra las tasas de conversión de una métrica de conversión de ingresos binarizada*

## Resumen

Los pasos de este tutorial muestran cómo configurar correctamente [!DNL Analysis Workspace] para mostrar [!UICONTROL Asignación automática] datos de informes.

Para resumir:

* Cuando la métrica es un [!DNL Target] métrica de conversión definida para una [!DNL Adobe Analytics] métrica con el criterio de optimización &quot;Maximizar el valor de la métrica por visitante&quot;, se debe utilizar el panel predeterminado del espacio de trabajo configurado con los visitantes como métrica de normalización.
* Cuando la métrica es un [!DNL Adobe Analytics] métrica con el criterio de optimización &quot;Maximizar la tasa de conversión de visitantes únicos&quot;, debe utilizar una tasa de conversión que se defina como la fracción de visitantes para los que la métrica es positiva. Esto se hace creando un segmento correspondiente que filtra el [!UICONTROL Visitante único] métrica.
