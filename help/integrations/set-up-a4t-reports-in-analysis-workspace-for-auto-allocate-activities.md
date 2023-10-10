---
title: Configuración de informes de A4T en [!DNL Analysis Workspace] para [!UICONTROL Asignación automática] Actividades
description: ¿Cómo configuro? [!UICONTROL Analytics for Target] Informes de (A4T) en [!DNL Adobe] [!DNL Analysis Workspace] al ejecutar [!UICONTROL Asignación automática] actividades.
role: User
level: Intermediate
topic: Personalization, Integrations
feature: Analytics for Target (A4T), Auto-Target, Integrations
doc-type: tutorial
kt: null
exl-id: 7d53adce-cc05-4754-9369-9cc1763a9450
source-git-commit: 3afbb97e2276ed98ea05e254026c8943acc6fee0
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 0%

---

# Configuración de informes de A4T en [!DNL Analysis Workspace] para [!DNL Auto-Allocate] actividades

Un [!UICONTROL Asignación automática] actividad en [!DNL Adobe Target] identifica un ganador entre dos o más experiencias y le reasigna automáticamente el tráfico de visitantes mientras la prueba sigue ejecutándose y aprendiendo. El [!UICONTROL Analytics for Target] Integración de (A4T) para [!UICONTROL Asignación automática] permite ver los datos de informes en [!DNL Adobe Analytics]y puede optimizar para eventos personalizados o métricas definidas en [!DNL Analytics].

Aunque las funcionalidades de análisis enriquecidas están disponibles en [!DNL Adobe Analytics] [!DNL Analysis Workspace], algunas modificaciones en el valor predeterminado [!UICONTROL Analytics for Target] el panel puede ser necesario para interpretar correctamente [!UICONTROL Asignación automática] actividades. Estas modificaciones son necesarias debido a los matices en [criterios de métrica de optimización](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html#supported){target=_blank}.

Cada tipo de métrica de optimización requiere una configuración de informe diferente en A4T, como se indica a continuación:

* Uso de un [!DNL Analytics] métrica

   * [!UICONTROL Maximizar el valor de la métrica por visitante]
   * [!UICONTROL Maximizar la tasa de conversión de visitantes únicos]

* Uso de un [!DNL Target]Métrica de conversión definida por el usuario

Este tutorial cubre las directrices generales de A4T y los pasos de configuración de informes específicos de criterios.

## Directrices generales para [!UICONTROL Analytics for Target] (A4T) {#guidance}

Puede ir a una versión prediseñada [!UICONTROL Analytics for Target] haciendo clic en el vínculo de la pantalla del informe en [!UICONTROL Adobe Target] (más adelante en esta guía se hace referencia a esto como &quot;[!DNL Target]informe activado por el usuario&quot;). También puede crear el panel A4T en [!DNL Analytics] (detalles más adelante en esta sección).

Las siguientes secciones especifican qué configuraciones son necesarias, según cuál de estos métodos elija:

* Las métricas de confianza deben eliminarse del panel A4T independientemente del método de creación del panel (ambos se detallan a continuación). En su lugar, consulte estos valores en [!DNL Target] informes. Además, los ganadores de las actividades pueden identificarse en [!DNL Target] informes. Encontrará más información sobre la identificación del ganador de la actividad en la [Identificar al ganador de la actividad](#winner) más abajo.
>>
* Para evitar confusiones, desmarque la opción &quot;[!UICONTROL Porcentaje]&quot; presentación de la [!UICONTROL Tasa de conversión] métrica. Para obtener más información, consulte [Ocultar el porcentaje de [!UICONTROL Tasa de conversión] columna](#hide-percentage) más abajo.
>>
* Si está creando un panel de A4T, asegúrese de que los intervalos de fecha y hora coinciden con los de su [!DNL Target] informe. Para obtener más información, consulte [Alinee la fecha y la hora en el panel A4T](#aligning-date-and-time) más abajo.

### Ocultar el porcentaje de [!UICONTROL Tasa de conversión] columna {#hide-percentage}

1. Haga clic en **engranaje** junto al título de la lista [!UICONTROL Tasa de conversión] columna.

   ![Icono de engranaje en la columna Tasa de conversión](/help/integrations/assets/coversion-rate-gear-icon.png)

   El [!UICONTROL Columna] se muestra el cuadro de diálogo configuración:

   ![Cuadro de diálogo Configuración de columna](/help/integrations/assets/column-settings-dialog-box.png){width="200"}

1. Anule la selección de **[!UICONTROL Porcentaje]** casilla de verificación

   El panel de A4T ahora no incluye porcentajes como tasa de conversión y coincide con [!DNL Target], como se muestra a continuación:

   ![Columna Tasa de conversión sin porcentajes](/help/integrations/assets/no-percentages.png)

### Alinee la fecha y la hora en el panel A4T {#aligning-date-and-time}

1. Sobre cada panel, compruebe el intervalo de fechas al que hace referencia el panel para asegurarse de que el intervalo de fechas coincide con el del panel [!DNL Target] informe.

   ![Intervalo de fechas en el panel A4T](/help/integrations/assets/date-range.png)

1. Entrada [!DNL Analytics], establezca el intervalo de tiempo de 12:00 a 23:59.

### Identificación del ganador de la actividad {#winner}

[!DNL Auto-Allocate] los ganadores de la actividad se seleccionan cuando hay una tasa de conversión ganadora con valores de confianza superiores o iguales al 95 %. Se debe hacer referencia a estos valores en la variable [!DNL Target] informes, ya que los cálculos de confianza reflejan los métodos más conservadores [!DNL Target] recomendaciones para [!UICONTROL Asignación automática] actividades. Para obtener más información, consulte [Garantías estadísticas de asignación automática](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/determine-winner.html#section_7AF3B93E90BA4B80BC9FC4783B6A389C){target=_blank} en el *[!UICONTROL Guía para profesionales de Adobe Target Business]*.

>[!NOTE]
>
Los distintivos &quot;Ningún ganador aún&quot; y &quot;Ganador&quot; no están disponibles en el panel A4T de [!DNL Analysis Workspace]. Además, el distintivo de &quot;estrella&quot; ganadora se muestra en [!DNL Target] informes para [!UICONTROL Asignación automática] Las actividades de deben ignorarse. Para obtener más información, consulte [Asignación automática](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-at-aa.html?lang=en#aa){target=_blank} in *Compatibilidad de A4T con actividades de asignación automática y segmentación automática* en el *[!UICONTROL Guía para profesionales de Adobe Target Business]*.

## Creación de A4T para [!UICONTROL Asignación automática] panel en [!DNL Analysis Workspace]

1. Para crear un panel de A4T para una [!UICONTROL Asignación automática] informe de actividad, empiece con [!UICONTROL Analytics for Target] panel en [!DNL Analysis Workspace], como se muestra a continuación.

   ![Analytics for Target: informe de asignación automática](/help/integrations/assets/a4t-auto-allocate-report.png)

1. Realice las siguientes selecciones:

   * **[!UICONTROL Experiencia de control]**: elija cualquier experiencia.
   * **[!UICONTROL Métrica de normalización]**: Seleccionar **[!UICONTROL Visitantes]** (incluido en el panel A4T de forma predeterminada). [!UICONTROL Asignación automática] siempre normaliza las tasas de conversión de los visitantes únicos.
   * **Métricas de éxito**: Seleccione la misma métrica (optimización) que utilizó durante la creación de la actividad. Si esto fuera un [!DNL Target]Métrica de conversión definida por el usuario, seleccione **[!UICONTROL Conversión de actividad]**. De lo contrario, seleccione la [!DNL Adobe Analytics] métrica que ha utilizado.

## Métricas de Analytics con &quot;[!UICONTROL Maximizar El Valor De Las Métricas Por Visitante]&quot; criterios de optimización

**Definición**: (Valor de métrica general) / (número de visitantes)

Para configurar el informe, realice los siguientes cambios en el informe de A4T:

![Maximizar el valor de la métrica para los ingresos](/help/integrations/assets/maximize-metric-value-revenue.png)

| Cambios necesarios | [!DNL Target]Informe activado por el sistema | Informe del panel de A4T |
| --- | --- | --- |
| Maximizar el valor de la métrica para un [!DNL Analytics] métrica | <ul><li>[!UICONTROL Confianza] Las métricas de se deben eliminar.</li><li>[!UICONTROL Alza (baja)] y [!UICONTROL Alza (alta)] debe eliminarse.</li><li>Se debe cambiar el nombre de la métrica de tasa de conversión a &quot;Métrica/Visitante&quot;.</li><li>Anule la selección de la presentación porcentual en [!UICONTROL Tasa de conversión] para evitar confusiones. Para obtener más información, consulte [Orientación general](#guidance) arriba.</li></ul> | <ul><li>[!UICONTROL Confianza] Las métricas de se deben eliminar.</li><li>[!UICONTROL Alza (baja)] y [!UICONTROL Alza (alta)] debe eliminarse.</li><li>Se debe cambiar el nombre de la métrica de tasa de conversión a &quot;Métrica/Visitante&quot;.</li><li>Anule la selección de la presentación porcentual en [!UICONTROL Tasa de conversión] para evitar confusiones. Para obtener más información, consulte [Orientación general](#guidance) arriba.</li><li>Asegúrese de que los intervalos de fecha y hora se alinean con los valores que ve en la variable [!DNL Target] informe. Para obtener más información, consulte [Orientación general](#guidance) arriba.</li></ul> |

## [!DNL Analytics] métricas con &quot;[!UICONTROL Tasa de conversión de visitante único]&quot; criterios de optimización

**Definición**: (# de visitantes únicos con un valor positivo de la métrica) / (Total de visitantes únicos)

Ejemplo: Supongamos que la métrica de optimización es [!UICONTROL Ingresos]. Hay cinco visitantes únicos en la actividad y tres de ellos realizan una compra. En este ejemplo, este valor = (3 visitantes para los cuales [!UICONTROL Ingresos] es positivo) / (5 visitantes únicos totales) = 0,6 = 60 %.

>[!NOTE]
>
La tasa de conversión a la que se hace referencia aquí puede referirse a acciones fuera de pedidos, como clics, impresiones, etc. En estos casos, el criterio seguiría siendo maximizar el recuento de visitantes que hacen clic o ven la página, respectivamente.

Para configurar el informe, realice los siguientes cambios en el informe de A4T:

| Cambios necesarios | Informe activado por Target | Informe del panel de A4T |
| --- | --- | --- |
| Maximización de conversiones para un [!DNL Analytics] métrica | <ul><li>[!UICONTROL Confianza] Las métricas de se deben eliminar.</li><li>Todo [!UICONTROL Alza] Las métricas de se deben eliminar.</li><li>Anule la selección de la presentación porcentual en [!UICONTROL Tasa de conversión] para evitar confusiones. (Para obtener más información, consulte [Orientación general](#guidance) arriba.</li></ul> | <ul><li>[!UICONTROL Confianza] Las métricas de se deben eliminar.</li><li>Todo [!UICONTROL Alza] Las métricas de se deben eliminar.</li><li>Cree un segmento para filtrar a los visitantes con un valor de métrica positivo que vieron la actividad analizada. Para obtener más información, consulte [Crear un segmento](#segment) más abajo.</li><li>Reemplace el que se rellena automáticamente [!UICONTROL Tasa de conversión] métrica, de modo que esa sea la división entre [!UICONTROL Visitantes únicos] con un valor de métrica positivo y visitantes únicos. Para obtener más información, consulte [Actualizar la métrica Tasa de conversión](#update-conversion-metric) más abajo.</li><li>Anule la selección de la presentación porcentual en [!UICONTROL Tasa de conversión] para evitar confusiones. Para obtener más información, consulte [Orientación general](#guidance) arriba.</li><li>Asegúrese de que los intervalos de fecha y hora se alinean con los valores que ve en la variable [!DNL Target] informe. Para obtener más información, consulte [Orientación general](#guidance) arriba.</li></ul> |

### Informe del panel A4T predeterminado: directrices adicionales

Las secciones siguientes contienen más información sobre directrices adicionales al configurar el informe del panel A4T predeterminado.

#### Creación de segmentos {#segment}

1. Haga clic en **Signo &quot;+&quot;** junto a **[!UICONTROL Segmentos]** en el carril izquierdo.

   ![Un signo más junto a los segmentos en el carril izquierdo.](/help/integrations/assets/plus-sign.png)

1. Asigne un título al segmento &quot;Visitantes con valor de métrica positivo&quot;.
1. En **[!UICONTROL Definición]**, junto a **[!UICONTROL Incluir]**, seleccione **[!UICONTROL Visitante]**.
1. En **[!UICONTROL Definición]**, seleccione la métrica de optimización en la actividad.

   En este ejemplo, supongamos que [!UICONTROL Ingresos] como métrica de optimización.

1. Seleccione el &quot;[!UICONTROL is greater than]&quot; y después especifique &quot;0&quot;.

   Esta configuración filtra todos los visitantes con un valor de métrica positivo.

1. Haga clic en **[!UICONTROL Guardar]**.

   ![Valor de métrica positivo](/help/integrations/assets/positive-metric-value.png)

1. Agregue el segmento recién creado &quot;Visitantes con valor de métrica positivo&quot; al panel A4T.
1. Arrastre y suelte el [!UICONTROL Visitantes únicos] en la misma columna que &quot;Visitantes con valor de métrica positivo&quot;.

   Esta configuración crea un segmento de todos los visitantes únicos para los que el valor de la métrica es positivo. En este ejemplo, todos los visitantes únicos cuyos ingresos fueran superiores a cero.

#### Actualice el [!UICONTROL Tasa de conversión] métrica {#update-conversion-metric}

1. Si aún no lo ha hecho, elimine el existente [!UICONTROL Tasa de conversión] del panel, como se explica más arriba.
1. Para agregar una métrica, haga clic en el signo &quot;+&quot; junto al **[!UICONTROL Métricas]** en el carril izquierdo.
1. Asigne a la métrica el nombre &quot;Tasa de conversión&quot; y defina como &quot;([!UICONTROL Visitantes únicos] con valor de métrica positivo)&quot; dividido por &quot;Visitantes únicos&quot;, como se muestra a continuación.

   Añada el segmento recién creado (pasos definidos anteriormente) de &quot;Visitantes con valor de métrica positivo&quot;, el operador de división, la métrica &quot;Visitantes únicos&quot; en el numerador y &quot;Visitantes únicos&quot; como denominador.

   ![Tasa de conversión en el panel A4T.](/help/integrations/assets/conversion-rate.png)

1. Haga clic en **[!UICONTROL Guardar]**.

1. Arrastre y suelte la métrica &quot;Tasa de conversión&quot; recién creada en el panel existente.
1. Haga clic en el icono de engranaje y, a continuación, deseleccione **[!UICONTROL Porcentaje]** , ya que este valor puede generar confusión.

   La configuración correcta del informe debería generar un resultado similar a la siguiente ilustración:

   ![Tasa de conversión de visita única en el informe del panel A4T](/help/integrations/assets/a4t-aa-maximize-metric-value-revenue.png)

## [!DNL Target]Tasa de conversión definida por el usuario

Para configurar el informe, realice los siguientes cambios en el informe de A4T:

| Cambios necesarios | Informe activado por Target | Informe del panel de A4T |
| --- | --- | --- |
| [!DNL Analytics] informar con [!DNL Target] métrica de conversión | <ul><li>[!UICONTROL Confianza] Las métricas de se deben eliminar.</li><li>[!UICONTROL Alza (baja)] y [!UICONTROL Alza (alta)] debe eliminarse.</li><li>Anule la selección de la presentación porcentual en [!UICONTROL Tasa de conversión] para evitar confusiones. Para obtener más información, consulte [Orientación general](#guidance) arriba.</li></ul> | <ul><li>[!UICONTROL Confianza] Las métricas de se deben eliminar.</li><li>[!UICONTROL Alza (baja)] y [!UICONTROL Alza (alta)] debe eliminarse.</li><li>Anule la selección de la presentación porcentual en [!UICONTROL Tasa de conversión] para evitar confusiones. Para obtener más información, consulte [Orientación general](#guidance) arriba.</li><li>Asegúrese de que los intervalos de fecha y hora se alinean con los valores que ve en la variable [!DNL Target] informe. Para obtener más información, consulte [Orientación general](#guidance) arriba.</li></ul> |

La configuración correcta del informe debería generar un resultado similar a la siguiente ilustración:

![Conversiones de actividad](/help/integrations/assets/optimized-table.png)









