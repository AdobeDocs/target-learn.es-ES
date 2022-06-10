---
title: QuickStart para pruebas de personalización y creación de hojas de ruta
description: 'Obtenga información sobre un marco que puede utilizar para empezar a validar actividades de personalización y crear una hoja de ruta de personalización para ejecutarla a través de Adobe Target y Adobe Analytics.  '
solution: Target,Analytics
source-git-commit: fd679d3fc2c72b9852d8129adf8c1187bf22b25f
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# QuickStart para pruebas de personalización y creación de hojas de ruta

La personalización puede ser potente, pero debe validarse probando para garantizar que realmente genera valor. Las pruebas son la estrategia más eficaz para identificar quién, cómo y qué debe personalizar.

A medida que iniciamos la segunda década del siglo XXI, organizaciones como la suya están dividiendo sus caminos con estrategias obsoletas de segmentación de consumidores y análisis de datos inexactos. Este es el amanecer de la personalización, una era en la que los consumidores han llegado a esperar nada menos que una experiencia personalizada. La personalización en el nivel empresarial es un proceso complejo y cambiante, pero cuando se realiza de manera efectiva, maximizará la satisfacción del cliente y aumentará sustancialmente el ROI.

El siguiente artículo proporciona un marco que puede utilizar para empezar a validar actividades de personalización y crear una hoja de ruta de personalización para ejecutarla a través de Adobe Target y Adobe Analytics. El marco de inicio rápido del Adobe incluye:

1. **Identificar oportunidades de personalización** : aproveche el análisis de datos para identificar oportunidades de afectar a los indicadores clave de rendimiento del sitio, vinculados a los objetivos del negocio de su organización.

1. **Desarrollar casos de uso** : defina los objetivos de su actividad de personalización teniendo en cuenta los atributos específicos del visitante, sea explícito sobre cómo mejorará la experiencia del visitante con el contenido depurado, establezca con antelación el aspecto del éxito y las acciones que se pueden realizar a partir de los conocimientos de la prueba.

1. **Crear una hoja de ruta** - agregue una lista y priorice los casos de uso de personalización, asegúrese de que sus esfuerzos se centren en actividades de alto valor; esperan perfeccionar y revisar los casos de uso y la hoja de ruta en función de los conocimientos.

1. **Diseño y ejecución** : cree e inicie las actividades de Adobe Target para ofrecer contenido depurado para sus audiencias prioritarias.

1. **Actuar sobre los resultados** : analice el rendimiento de la actividad y resuma los resultados de la actividad, las perspectivas, las recomendaciones y los pasos siguientes.

## Paso 1: Identificar oportunidades de personalización{#personalization}

Este es el punto de partida en el que comienza a formar la hoja de ruta de personalización. Al ejecutar un programa de personalización exitoso, es esencial centrarse en los objetivos clave del negocio y en los indicadores clave de rendimiento. Los esfuerzos de personalización deben alinearse en consecuencia para proporcionar valor. Paul Morris, consultor de negocios de Adobe, afirma: &quot;Si todo lo que se hace se alimenta de estos objetivos, es muy probable que su programa genere un valor significativo. Sin embargo, si tiene un enfoque disperso de las pruebas, es probable que obtenga algunos beneficios, pero su programa general no tendrá tanto éxito&quot;.

>[!NOTE]
>
>Si no sabe inmediatamente cuáles son sus objetivos comerciales clave, es importante identificarlos lo antes posible. Asegúrese de:


* Establezca la alineación entre sus objetivos comerciales y su hipótesis procesable. Esto le permitirá priorizar los casos de uso que proporcionen el valor bueno a su negocio.

* Consiga que sus objetivos se puedan medir con fines de seguimiento y se correlacionen con el impacto en los ingresos.

* Alinear cada oportunidad debería afectar a una única métrica de objetivos.

A veces, es posible que tenga objetivos que inicialmente también parezcan intangibles, como el valor de la marca o la lealtad. Es fundamental que pueda medirlas para utilizarlas como métricas de objetivo para las actividades de personalización. Normalmente, estos tipos de objetivos aún se pueden alinear con el impacto en los ingresos, como el valor del cliente o los costes de adquisición de por vida. A medida que avanza, asegúrese de revisar periódicamente el rendimiento del programa en relación con sus objetivos clave del negocio para asegurarse de que el valor se está derivando de su programa de personalización.

Enfoque el análisis de datos para identificar áreas específicas del sitio web que se pueden mejorar. Adobe recomienda empezar con Adobe Analytics para generar casos de uso segmentados. Si dispone de un equipo de Analytics, pídale que consulte lo siguiente:

1. Tablas de preformulario personales : característica de ideación que proporciona desgloses ilimitados y puede ayudarle a responder a cualquier pregunta o suposición que pueda tener.
1. Segmentación avanzada: IQ de segmentación le permite comparar visitantes entre diferentes secciones del sitio.
1. Revisiones juristicas : identifique qué partes del sitio se beneficiarían más de la personalización. Estas revisiones le permiten dar un paso atrás y recorrer su sitio como lo haría un cliente.
1. Análisis de la competencia: es probable que otras empresas se enfrenten a los mismos desafíos que usted. Este análisis no se limita a las empresas del mismo sector.

El objetivo de este paso es generar una perspectiva procesable en forma de hipótesis. Una hipótesis es una predicción que se crea antes de ejecutar un experimento. Indica claramente lo que se está cambiando, cuál crees que será el resultado y por qué piensas que es así. La ejecución del experimento probará o refutará la hipótesis. Al final de este paso, debe tener un conjunto de hipótesis para las oportunidades de personalización que mejorarán la satisfacción del sitio web y del visitante.

## Paso 2: Desarrollar casos de uso{#use-cases}

Comience con la hipótesis generada en el paso 1 y, a continuación, desarrolle sus actividades a su alrededor. Ahora puede desarrollar las tablas de preformulario creadas en el paso 1A; cada KPI tiene un conjunto de hipótesis, que luego se convierten en pruebas individuales dentro de Adobe Target. Si tiene dificultades para llegar a este punto, comience de la forma más sencilla posible, por ejemplo centrándose en los visitantes de retorno que frecuentan el sitio. Piense en las formas de adaptar la página principal a los visitantes que regresan. Una vez que tenga su conjunto de hipótesis, deberá definir cada actividad para priorizar efectivamente cada caso de uso.

1. Defina las audiencias prioritarias a las que desea ofrecer contenido personalizado, teniendo en cuenta los atributos de visitante único que definen quiénes son y qué desean (por ejemplo, clientes existentes frente a clientes potenciales). Los deseos y las necesidades de las audiencias prioritarias deben coincidir con los objetivos comerciales

1. Identifique la ubicación específica en el recorrido del visitante donde el contenido personalizado será el más impactante. Céntrese en páginas donde esperaría visitantes de una amplia gama de personalidades o visitantes con diversas necesidades o intenciones.

1. Empiece a planificar algún trabajo de diseño de la variante. El contenido debe ser cuidadosamente depurado teniendo en cuenta las necesidades y necesidades específicas de la audiencia, teniendo en cuenta dónde se encuentran en su recorrido. El contenido correcto debe ser distinto y diferenciado.

## Paso 3: Crear una hoja de ruta, agregar y priorizar casos de uso

Agregue una lista completa de oportunidades de personalización que capture al menos la ubicación, la idea y la prioridad de las actividades de personalización.

El paso de priorización se divide en dos factores:

**Valor:** Utilice la investigación de la industria, las pruebas comparativas y casos de uso similares del pasado para comprender el valor esperado que cada una de sus hipótesis puede impulsar. Desea que su valor se vincule directamente a uno de sus Resultados comerciales clave (KBO) y que esté en un formato estándar para que cada uno de sus casos de uso se pueda comparar entre sí. El método más común es aplicar un valor monetario a cada caso de uso para su comparación.

* Coste : existe un coste natural asociado a la creación de variantes de diseño dentro de Target y luego al posible despliegue. Ahora tendrá que calcular el coste asociado a cada caso de uso. El coste incluye el tiempo y los recursos necesarios para crear experiencias de prueba, programar y realizar análisis de publicaciones de prueba.

Adobe recomienda clasificar cada uno de los casos de uso en una escala de 1 a 5; con 1 simple y 5 complejo. Ahora tiene un conjunto de actividades priorizadas que puede probar en Adobe Target. Estas actividades formarán la base de sus actividades de personalización anuales. Adobe recomienda volver a evaluar regularmente la Hoja de ruta de personalización. Las lecciones de cada actividad deben influir en las prioridades de su hoja de ruta orientada al futuro. Las experiencias y recomendaciones tendrán más impacto si se adoptan a tiempo. Las prioridades a lo largo del año pueden cambiar, pero llevar a cabo una metodología iterativa garantiza que siempre tiene un plan de acción estratégico y que puede rastrear los objetivos de su equipo y compañía.

## Paso 4: Diseño y ejecución

Aprovechando la documentación creada para estratégicamente el caso de uso de personalización, construya la actividad de personalización dentro de Target para entregar contenido depurado para sus audiencias prioritarias. Asegúrese de que el tipo de actividad, la configuración, las experiencias y las funciones de informes estén alineados con los objetivos del caso de uso. El diseño, el control de calidad y el lanzamiento de su esfuerzo de personalización son más eficientes cuando entran en los procesos de organización existentes.

## Paso 5: Actuar sobre los resultados

Una vez que su actividad de personalización haya atraído una muestra representativa de visitantes, puede empezar a analizar aprovechando las perspectivas para guiar los pasos siguientes. Establezca los datos en el análisis, vincule las recomendaciones a la hipótesis de casos de uso e ilustre claramente el impacto en los objetivos empresariales.

### Más información

Le recomendamos que vea este vídeo en el que se describen cada uno de estos pasos: [https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/](https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/)