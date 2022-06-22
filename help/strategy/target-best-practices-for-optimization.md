---
title: Prácticas recomendadas para optimización
description: Conozca los seis aspectos básicos de la optimización de Adobe y cómo aplicarlos.
solution: Target
exl-id: dd29faea-bb67-4128-b261-fa407ba7158c
source-git-commit: 46f61d8f503f230a79b4072ea0d75edd41403708
workflow-type: tm+mt
source-wordcount: '1246'
ht-degree: 0%

---

# Prácticas recomendadas para la optimización con Adobe Target

Conozca los seis aspectos básicos de la optimización de Adobe y cómo aplicarlos.

Cuando se trata de construir una fuerte presencia digital, hay una serie de desafíos que su equipo enfrentará. Además de eso, sus clientes no solo tienen la tarea de captar a cientos, sino a miles de clientes, sino que además muestran una variedad de comportamientos y preferencias únicos que cambiarán con el tiempo y es usted quien debe no solo mantenerse al día con esos cambios, sino también anticiparlos y ejecutar sus estrategias de forma eficiente y precisa. Es una carrera contra competidores en una maratón de contenido perpetuo, que requiere iteración constante y la mejor tecnología de su clase.

Una solución a este desafío multifacético es la optimización con Adobe Target, que garantiza una presencia digital en evolución que sea relevante, valiosa y libre de fricciones. La arquitectura técnica y los canales en los que implementa [!DNL Target] variará considerablemente entre los clientes, pero hemos seleccionado una lista de prácticas recomendadas y estrategias de optimización que cada equipo puede utilizar para aprovechar todas las capacidades de esta potente herramienta.

## Información sobre la optimización

La optimización se define como &quot;la acción de hacer el mejor o más eficaz uso de una situación o recurso&quot;. Es la forma más eficaz de garantizar que dispone de datos cualitativos que prueben que los cambios que está realizando son valiosos. Para optimizar, debe poder medir el impacto y el valor de sus esfuerzos. De lo contrario, los cambios que realice resultarán en un coste mayor, con una ganancia mínima. Para lograrlo de manera eficaz y eficiente, debe comenzar con la planificación estratégica. Sin incluir un plan estratégico en su optimización, simplemente estaría adivinando.

### Seis aspectos básicos de la optimización

1. **Enfoque**: Identifique oportunidades para actividades que estén alineadas con los objetivos del negocio y que estén basadas en datos.
1. **Prioridad**: Clasificar y programar actividades basadas en la alineación del negocio, el nivel de esfuerzo y el impacto potencial.
1. **Diseño**: Cree imágenes finalizadas de experiencias de actividad y desarrolle planes de actividad con criterios detallados.
1. **Generar y ejecutar**: Desarrollar actividad, incluido [!DNL Target] configuración, desarrollo de código y pruebas de control de calidad.
1. **Analizar**: Launch [!DNL Target] actividad a producción y monitorizar el rendimiento durante la actividad.
1. **Actuar e iterar**: Desarrolle recomendaciones basadas en el rendimiento de la actividad de prueba o personalización.

Sabiendo que el cambio es una constante, nuestra estrategia de optimización debería ser un ciclo de ejecución iterativo para satisfacer las necesidades cambiantes de sus clientes (ver Figura 1 a continuación).

![Optimización y personalización](assets/optimize-and-personalize.png)

_Figura 1 - Ciclo interactivo de optimización_

## Creación de una estrategia de optimización

El proceso de desarrollo de una estrategia de optimización se puede desglosar en: (1) Crear un plan de actividad de prueba y (2) Comprender los conceptos básicos de optimización.

1: Se debe documentar el plan de actividad de prueba. Esto garantiza que tenga un estándar de calidad mínimo cuando se trata de la aplicación de actividad de prueba. El plan de actividad de prueba debe incluir:

* **Nombre y descripción:** Nombre intuitivo de la actividad y descripción de en qué se centra el experimento. &quot;¿Cómo? ¿Qué? Al? Donde? ¿Por qué?&quot;

* **Objetivo:** Objetivo de la actividad y objetivo comercial alineado que se está diseñando para afectar.

* **Hipótesis:** Una hipótesis es una predicción que se crea antes de ejecutar un experimento. Indica claramente lo que se está probando, lo que se cree que será el resultado y por qué se cree que es así. La ejecución del experimento probará o refutará la hipótesis.

Una hipótesis completa consta de tres partes:

* If _variable_
* Entonces _result_
* Porque _racionalidad_

* **Ubicación:** Dirección URL, sección de página y tipo de dispositivo.
* **Métrica de objetivo:** ¿Cómo se medirá el éxito?
* **Métricas secundarias:** Otros indicadores clave de rendimiento (KPI) valiosos que se deben evaluar con el fin de comprender mejor el impacto y las iteraciones de planificación.
* **Audiencia de actividad:** Descripción del filtro de exposición de ensayo requerido.
* **Audiencias de informes:** Lista de descripciones de subconjuntos de visitantes que se utilizarán para el análisis.
* **Conceptos de la experiencia:** Mockups, ejemplos de estructuras metálicas y descripciones.

**Nota general:** Se puede probar cualquier elemento de una página web que pueda generar valor empresarial o proporcionar una valiosa perspectiva del comportamiento de los visitantes. Algunos tipos comunes de actividades de prueba son:

* Texto de encabezado
* Texto de contenido
* Texto de botón
* Diseño de página
* Fotografía
* Color del botón
* Diseño de elementos
* Eliminación y adición de elementos
* Ordenación de navegación
* taxonomía de navegación
* Enfoque de búsqueda

2: La segunda etapa de la estrategia es comprender los fundamentos de la optimización, lo que incluye la comprensión de los propios elementos de prueba. Los elementos de prueba de la optimización incluyen:

    A. Valor del elemento
    
    Esto se logra dando un paso atrás para preguntar, por qué existe un determinado elemento en el sitio y si el contenido cumple un propósito específico. Estas preguntas son un buen punto de partida si el sitio acaba de finalizar un rediseño o si recientemente se ha implementado una nueva función. La táctica utilizada para determinar el valor del elemento se denomina Prueba de inclusión/exclusión. La prueba de inclusión/exclusión proporciona una buena lectura del valor en la página donde se muestra el elemento.
    
    B. Presentación de elementos
    
    Aquí es donde pensaría sobre el aspecto general del elemento y cómo afecta a la presentación general de la página. La táctica utilizada para la presentación es centrarse en realizar cambios impactantes en el contenido y en la página de elementos.
    
    C. Función de los elementos
    
    Aquí nos preguntamos: ¿el elemento de la página está haciendo lo que se supone que debe hacer? ¿La interacción es exitosa y funciona según lo previsto? ¿Es la interacción natural o un punto de fricción? La táctica utilizada para la función es crear experiencias que se centren en la funcionalidad fácil de usar sin un impacto de coste adicional.

## Optimización frente a personalización

Ahora que hemos analizado y enumerado los componentes de la estrategia, es importante establecer una distinción entre los esfuerzos de optimización y los esfuerzos de personalización. La optimización es la acción de hacer el mejor o más eficaz uso de una situación o recurso, mientras que la personalización es la acción de diseñar o producir algo para satisfacer los requisitos individuales de una persona.

En un nivel superior:

* La optimización se centra en pruebas para encontrar lo que es más eficiente y de mejor rendimiento para TODOS los que interactúan con su presencia digital.
* La personalización está probando para encontrar lo que es más eficiente y de mejor rendimiento para ALGUNOS de los que interactúan con su presencia digital.

Al centrarse en la optimización, las actividades de prueba más comunes son:

* **Prueba A/B:** Pruebas en tiempo real de dos o más páginas o elementos de página entre sí para obtener una perspectiva cuantitativa de las preferencias del cliente.
* **Pruebas multivariable:** Comparar combinaciones de ofertas entre elementos de una página para ver cuál de ellas ofrece el mejor rendimiento. Además, la prueba multivariada identificará qué elemento de la página mejora mejor las conversiones.

Al centrarse en la personalización, es probable que vea las mismas actividades de prueba que en Optimización, pero están dirigidas a audiencias más específicas. Por ejemplo, en las pruebas A/B, es probable que añada páginas y audiencias dentro de las experiencias para profundizar la personalización.

La personalización también incluye el tipo de actividad de prueba de segmentación de experiencias, que envía contenido a audiencias específicas en función de un conjunto de reglas y criterios definidos. A medida que vaya creciendo y profundizando en la personalización, también aprovechará algunas de las funciones principales de Target, como:

* Tipo de actividades de Automated Personalization
* Tipo de actividades de recomendación

## Optimización antes de la personalización

Teniendo en cuenta lo anterior, Adobe recomienda optimizar antes de personalizar y avanzar en la personalización de un amplio a otro nivel. Para madurar las actividades de personalización de amplio a granular, comenzará a utilizar un estilo de personalización (amplio) de uno a varios (con pruebas A/B) y, a continuación, pasará a un estilo de personalización (granular) uno a uno (con actividades de personalización automatizada).

Para obtener más información, escuche [seminario web sobre cómo comprender y optimizar su implementación de Adobe Target](https://adobecustomersuccess.adobeconnect.com/pkfafpzd9yarmp4/), con Business Consultant, Katie Cozby.

Obtenga más información sobre la estrategia y el liderazgo mental en [Éxito del cliente](https://experienceleague.corp.adobe.com/docs/customer-success/customer-success/overview.html) hub.
