---
title: Prácticas recomendadas para optimización
description: Conozca los seis aspectos básicos de la optimización de Adobe y cómo aplicarlos.
solution: Target
role: Leader, Architect, Developer, Admin
feature: Overview
level: Beginner
exl-id: dd29faea-bb67-4128-b261-fa407ba7158c
source-git-commit: d65720ae992a3079462ba59421c3b7a8d4f5ea7b
workflow-type: tm+mt
source-wordcount: '1236'
ht-degree: 0%

---

# Prácticas recomendadas para la optimización con Adobe Target

Conozca los seis aspectos básicos de la optimización de Adobe y cómo aplicarlos.

A la hora de crear una fuerte presencia digital, su equipo se enfrentará a una serie de desafíos. No solo tiene que atraer a cientos, incluso miles de clientes, además de eso, sus clientes muestran una variedad de comportamientos y preferencias únicos que cambiarán con el tiempo y depende de usted no solo mantenerse al día con esos cambios, sino también anticiparlos y ejecutar sus estrategias de manera eficiente y precisa. Es una carrera contra la competencia en una maratón de contenido perpetuo, que requiere iteración constante y la mejor tecnología de su clase.

Una solución a este desafío multifacético es la optimización con Adobe Target, que garantiza una presencia digital en evolución que sea relevante, valiosa y libre de fricción. La arquitectura técnica y los canales en los que implementa [!DNL Target] variarán considerablemente de un cliente a otro. Sin embargo, hemos seleccionado una lista de prácticas recomendadas y estrategias de optimización que todos los equipos pueden usar para aprovechar todas las capacidades de esta potente herramienta.

## Explicación de la optimización

La optimización se define como &quot;la acción de hacer el uso mejor o más efectivo de una situación o recurso&quot;. Es la forma más eficiente de asegurarse de que dispone de datos cualitativos que prueben que los cambios que está realizando son valiosos. Para optimizar de verdad, debe poder medir el impacto y el valor de sus esfuerzos. De lo contrario, los cambios que realice resultarán en un mayor coste, con una ganancia mínima. Para lograr esto de manera efectiva y eficiente, debe comenzar con la planificación estratégica. Sin incluir un plan estratégico en su optimización, simplemente estaría adivinando.

### Seis aspectos básicos de la optimización

1. **Estrategizar**: identifique oportunidades para actividades que estén alineadas con los objetivos de la empresa y que se basen en datos.
1. **Priorizar**: Clasifique y programe actividades en función de la alineación de la empresa, el nivel de esfuerzo y el impacto potencial.
1. **Diseño**: cree imágenes finalizadas de experiencias de actividad y desarrolle planes de actividad con criterios detallados.
1. **Generar y ejecutar**: Desarrolle la actividad, incluida la configuración de [!DNL Target], el desarrollo de código y las pruebas de control de calidad.
1. **Analizar**: inicia la actividad [!DNL Target] para generar y supervisar el rendimiento durante la actividad.
1. **Actuar e iterar**: Desarrolle recomendaciones basadas en el rendimiento de actividades de prueba o personalización.

Sabiendo que el cambio es una constante, nuestra estrategia de optimización debe ser un ciclo de ejecución iterativo para satisfacer las necesidades siempre cambiantes de sus clientes (Consulte la Figura 1 a continuación).

![Optimización y personalización](assets/optimize-and-personalize.png)

_Figura 1 - Ciclo iterativo de optimización_

## Creación de una estrategia de optimización

El proceso de desarrollo de una estrategia de optimización se puede desglosar en: (1) Creación de un plan de actividad de prueba y (2) Comprensión de los conceptos básicos de optimización.

1: El plan de actividad de prueba debe estar documentado. Esto garantiza que tenga un estándar mínimo de calidad en lo que respecta a la aplicación de actividad de prueba. El plan de actividades de prueba debe incluir lo siguiente:

* **Nombre y descripción:** Nombre intuitivo de la actividad y descripción del enfoque del experimento. &quot;¿Cómo? ¿Qué? ¿Cuándo? ¿Dónde? ¿Por qué?&quot;

* **Objetivo:** Propósito de la actividad y objetivo comercial alineado al que se está diseñando para afectar.

* **Hipótesis:** Una hipótesis es una predicción que crea antes de ejecutar un experimento. Claramente indica lo que se está probando, cuál cree que será el resultado y por qué cree que ese es el caso. La ejecución del experimento probará o refutará la hipótesis.

Una hipótesis completa consta de tres partes:

* Si _variable_
* Entonces _resultado_
* Debido a _razón_

* **Ubicación:** URL, sección de página y tipo de dispositivo.
* **Métrica de objetivo:** ¿Cómo se medirá el éxito?
* **Métricas secundarias:** otros indicadores clave de rendimiento (KPI) valiosos que se deben evaluar con el fin de comprender mejor el impacto y las iteraciones de planificación.
* **Audiencia de actividad:** Descripción del filtrado de exposición de prueba requerido.
* **Audiencias de informes:** Lista de descripciones de subconjuntos de visitantes que se utilizarán para el análisis.
* **Conceptos de experiencia:** maquetas, ejemplos, mallas metálicas y descripciones.

**Nota general:** Se puede probar cualquier elemento de una página web que pueda generar valor empresarial o proporcionar un valioso insight al comportamiento de los visitantes. Algunos tipos comunes de actividades de prueba incluyen:

* Texto de titular
* Texto de contenido
* Texto del botón
* Diseño de página
* Fotografía
* Color del botón
* Diseño del elemento
* Eliminación y adición de elementos
* Ordenación de navegación
* Taxonomía de navegación
* Énfasis de búsqueda

2: La segunda fase de la estrategia es Comprender los conceptos básicos de la optimización, que incluye la comprensión de los propios elementos de prueba. Los elementos de prueba de Optimización incluyen:

    A. Valor de elemento
    
    Esto se logra dando un paso atrás para preguntar por qué existe un elemento determinado en el sitio y si el contenido sirve para un propósito específico. Estas preguntas son un buen punto de partida si el sitio acaba de finalizar un rediseño o si se ha implementado recientemente una nueva función. La táctica utilizada para determinar el valor del elemento se denomina Pruebas de inclusión/exclusión. Las Pruebas de inclusión/exclusión proporcionan una buena lectura del valor en la página donde se muestra el elemento.
    
    B. Presentación de elementos
    
    Aquí es donde pensaría en el aspecto general del elemento y en cómo afecta a la presentación general de la página. La táctica utilizada para la presentación es centrarse en realizar cambios impactantes en el contenido y la página de elementos.
    
    C. Función Elemento
    
    Aquí preguntamos, ¿está el elemento de la página haciendo lo que se supone que debe hacer? ¿La interacción es satisfactoria y funciona según lo previsto? ¿Es la interacción natural o un punto de fricción? La táctica utilizada para la función es generar experiencias que se centren en una funcionalidad fácil de usar sin impacto de costo adicional.

## Optimización frente a personalización

Ahora que hemos analizado y enumerado los componentes de la estrategia, es importante distinguir entre los esfuerzos de optimización y los esfuerzos de Personalization. La optimización es la acción de hacer el uso mejor o más efectivo de una situación o recurso, mientras que Personalization es la acción de diseñar o producir algo para satisfacer los requisitos individuales de alguien.

En un nivel superior:

* La optimización se centra en las pruebas para encontrar lo que es más eficiente y ofrece el mejor rendimiento para TODOS los que interactúan con su presencia digital.
* Personalization está realizando pruebas para encontrar lo que es más eficiente y ofrece el mejor rendimiento para ALGUNAS de las personas que interactúan con su presencia digital.

Al centrarse en la optimización, las actividades de prueba más comunes son:

* **Pruebas A/B:** Pruebas en tiempo real de dos o más páginas o elementos de página entre sí para obtener insight cuantitativo en las preferencias del cliente.
* **Pruebas multivariable:** Comparar combinaciones de ofertas entre elementos de una página para ver qué combinación ofrece el mejor rendimiento. Además, la prueba multivariable identificará qué elemento de la página mejora más las conversiones.

Al centrarse en Personalization, es probable que vea las mismas actividades de prueba que en Optimización, pero están dirigidas a audiencias más específicas. Por ejemplo, en las pruebas A/B, es probable que añada páginas y audiencias dentro de las experiencias para mejorar su Personalization.

Personalization también incluye el tipo de actividad de prueba Segmentación de experiencias, que ofrece contenido a audiencias específicas en función de un conjunto de reglas y criterios definidos. A medida que empiece a crecer y a profundizar en Personalization, aquí es también donde aprovechará algunas de las funciones prémium de Target como:

* Tipo de actividades de Automated Personalization
* Tipo de actividades de recomendación

## Optimización antes de la personalización

Dada la comprensión anterior, Adobe recomienda optimizar antes de personalizar y avanzar Personalization de amplio a granular. Para madurar las actividades de Personalization de amplia a granular, empezará a utilizar un estilo de personalización de uno a varios (amplio) (mediante pruebas A/B) y, a continuación, pasará al estilo de personalización de uno a uno (granular) (mediante actividades de personalización automatizada).

Para obtener más información, lea [QuickStart para pruebas de personalización y creación de hoja de ruta](https://experienceleague.adobe.com/es/perspectives/quickstart-for-personalization-testing-and-roadmap-creation).

Obtenga más información sobre estrategia y liderazgo mental en el centro de [Perspectivas](https://experienceleague.adobe.com/es/perspectives).
