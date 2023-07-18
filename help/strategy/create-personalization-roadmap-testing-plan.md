---
title: QuickStart para pruebas de personalización y creación de hoja de ruta
description: Conozca un marco de trabajo que puede utilizar para empezar a validar actividades de personalización y crear una hoja de ruta de personalización para ejecutarla a través de Adobe Target y Adobe Analytics.
solution: Target,Analytics
level: Intermediate
role: Leader, Architect, Developer, Admin
exl-id: c0b6f9a0-7074-4e25-81e6-9781a54e2156
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# QuickStart para pruebas de personalización y creación de hoja de ruta

La personalización puede ser potente, pero debe validarse realizando pruebas para garantizar que realmente aporta valor. Las pruebas son la estrategia más eficaz para identificar quién, cómo y qué debe personalizar.

A medida que nos adentramos en la segunda década del siglo XXI, organizaciones como la suya se están separando con estrategias de segmentación de consumidores obsoletas y análisis de datos inexactos. Este es el amanecer de la personalización, una era en la que los consumidores han llegado a esperar nada menos que una experiencia personalizada. La personalización a nivel empresarial es un proceso complejo y en constante cambio, pero cuando se realiza de forma eficaz, maximiza la satisfacción del cliente y aumenta sustancialmente el retorno de la inversión.

El siguiente artículo proporciona un marco de trabajo que puede utilizar para empezar a validar actividades de personalización y crear una hoja de ruta de personalización para ejecutarla a través de Adobe Target y Adobe Analytics. La estructura de inicio rápido de Adobe incluye:

1. **Identificación de oportunidades de personalización** : aproveche el análisis de datos para identificar oportunidades que puedan afectar a los indicadores de rendimiento clave del sitio, vinculados a los objetivos empresariales de la organización.

1. **Desarrollo de casos de uso** : defina los objetivos de su actividad de personalización teniendo en cuenta atributos específicos del visitante, sea explícito con respecto a cómo mejorará el contenido depurado la experiencia del visitante, establezca de antemano cómo se verá el éxito y qué acciones se pueden tomar de las lecciones de las pruebas.

1. **Creación de una hoja de ruta** : añada una lista y priorice casos de uso de personalización, asegúrese de que sus esfuerzos se centren en actividades de alto valor; espere refinar y revisar casos de uso y hoja de ruta basados en las lecciones aprendidas.

1. **Diseño y ejecución** : cree e inicie actividades de Adobe Target para ofrecer contenido depurado para sus audiencias prioritarias.

1. **Acción en los resultados** : analice el rendimiento de la actividad y resuma los resultados, las perspectivas, las recomendaciones y los pasos siguientes de la actividad.

## Paso 1: Identificar las oportunidades de personalización{#personalization}

Este es el punto de partida en el que empieza a formar la hoja de ruta de personalización. Al ejecutar un programa de personalización exitoso, es esencial centrarse en sus objetivos comerciales clave y en los indicadores de rendimiento clave. Los esfuerzos de personalización deben alinearse en consecuencia para proporcionar valor. Paul Morris, Adobe Business Consultant, afirma: &quot;Si todo lo que hace se integra en estos objetivos, es muy probable que su programa genere un valor significativo. Sin embargo, si tiene un enfoque disperso en las pruebas, es probable que encuentre algunas victorias, pero su programa general no tendrá tanto éxito&quot;.

>[!NOTE]
>
>Si no sabe inmediatamente cuáles son sus objetivos comerciales clave, es importante identificarlos lo antes posible. Asegúrese de:


* Establezca la alineación entre sus objetivos empresariales y su hipótesis procesable. Esto le permite priorizar los casos de uso que ofrecen el valor más bueno a su empresa.

* Haga que sus objetivos sean mensurables para fines de seguimiento y correlacionarlos con el impacto en los ingresos.

* Alinee cada oportunidad debe afectar a una única métrica de objetivo.

A veces, puede tener objetivos que inicialmente también parecen intangibles, como el valor de la marca o la lealtad. Es crucial que pueda medirlos para usarlos como métricas de objetivo para las actividades de Personalización. Normalmente, estos tipos de objetivos se pueden alinear con el impacto en los ingresos, como el valor del cliente durante la vida útil o los costes de adquisición. A medida que avance, asegúrese de revisar el rendimiento del programa con respecto a los objetivos comerciales clave periódicamente para garantizar que el valor se obtiene de su programa de personalización.

Enfoque el análisis de datos para identificar áreas específicas del sitio web que se pueden mejorar. Adobe recomienda empezar con Adobe Analytics para generar casos de uso segmentados. Si tiene un equipo de Analytics, pídale que observe lo siguiente:

1. Tablas personales previas al formulario: una función de ideación que proporciona desgloses ilimitados y puede ayudarle a responder a cualquier pregunta o suposición que pueda tener.
1. Segmentación avanzada: Segmentación IQ permite comparar visitantes entre diferentes secciones del sitio.
1. Revisiones jurídicas: identifique las partes del sitio que más se beneficiarían de la personalización. Estas revisiones le permiten dar un paso atrás y recorrer el sitio como lo haría un cliente.
1. Análisis de la competencia: lo más probable es que otras empresas se enfrenten a los mismos desafíos que usted. Este análisis no se limita a las empresas del mismo sector.

El objetivo de este paso es generar una perspectiva procesable en forma de hipótesis. Una hipótesis es una predicción que se crea antes de ejecutar un experimento. Establece claramente lo que se está cambiando, cuál cree que será el resultado y por qué cree que es el caso. La ejecución del experimento probará o refutará la hipótesis. Al final de este paso, debe tener un conjunto de hipótesis para las oportunidades de personalización que mejorarán su sitio web y la satisfacción del visitante.

## Paso 2: Desarrollar casos de uso{#use-cases}

Comience con las hipótesis generadas en el paso 1 y, a continuación, desarrolle sus actividades en torno a ellas. Ahora puede desarrollar las tablas prediseñadas creadas en el paso 1A; cada KPI tiene un conjunto de hipótesis, que luego se convierten en pruebas individuales dentro de Adobe Target. Si tiene dificultades para llegar a este punto, comience de la forma más sencilla posible, por ejemplo, centrándose en los visitantes de retorno que frecuentan el sitio. Piense en las formas en que puede adaptar la página principal a los visitantes que regresan. Una vez que tenga el conjunto de hipótesis, deberá definir cada actividad para priorizar de forma eficaz cada caso de uso.

1. Defina las audiencias prioritarias a las que desea ofrecer contenido personalizado, teniendo en cuenta los atributos únicos del visitante que definen quién es y qué desea (por ejemplo, cliente existente o cliente potencial). Los deseos y necesidades de las audiencias prioritarias deben coincidir con los objetivos de su negocio

1. Identifique la ubicación específica del recorrido del visitante donde el contenido personalizado tenga un mayor impacto. Céntrese en páginas donde quiera que haya visitantes de una amplia gama de personalidades o visitantes con diversas necesidades o intenciones.

1. Empiece a planificar el trabajo de diseño de su variante. El contenido debe depurarse cuidadosamente teniendo en cuenta las necesidades y deseos específicos de la audiencia, teniendo en cuenta dónde se encuentran en su recorrido. El contenido adecuado debe ser distinto y diferenciado.

## Paso 3: Crear una hoja de ruta, agregar y priorizar casos de uso

Agregue una lista completa de oportunidades de personalización que capture como mínimo la ubicación, idea y prioridad de las actividades de personalización.

El paso de priorización se divide en dos factores:

**Valor:** Utilice la investigación del sector, las pruebas comparativas y casos de uso similares del pasado para comprender el valor esperado que cada una de sus hipótesis puede impulsar. Desea que su valor esté directamente vinculado a uno de sus resultados empresariales clave (KBO) y que esté en un formato estándar para que cada uno de sus casos de uso se pueda comparar entre sí. El método más común es aplicar un valor monetario a cada caso de uso para la comparación.

* Coste: existe un coste natural asociado con la creación de las variantes de diseño dentro de Target y con el posible despliegue. Ahora tendrá que estimar el coste asociado a cada caso de uso. El coste incluye el tiempo y los recursos necesarios para crear experiencias de prueba, la programación y el análisis posterior a la prueba.

El Adobe recomienda clasificar cada uno de los casos de uso en una escala del 1 al 5; siendo 1 simple y 5 complejo. Ahora tiene un conjunto de actividades priorizadas que puede probar en Adobe Target. Estas actividades constituyen la base de sus actividades anuales de personalización. El Adobe recomienda volver a evaluar la hoja de ruta de personalización con regularidad. Las lecciones aprendidas de cada actividad deben influir en las prioridades de la hoja de ruta orientada al futuro. Los aprendizajes y las recomendaciones serán más impactantes si se llevan a cabo en el momento oportuno. Las prioridades a lo largo del año pueden cambiar, pero llevar a cabo una metodología iterativa garantiza que siempre tenga un plan estratégico de acción y que pueda rastrear en contra de los objetivos de su equipo y compañía.

## Paso 4: Diseño y ejecución

Aproveche la documentación creada para diseñar una estrategia para el caso de uso de la personalización y construya la actividad de personalización dentro de Target para ofrecer contenido depurado para sus audiencias prioritarias. Asegúrese de que el tipo de actividad, la configuración, las experiencias y las funciones de creación de informes estén alineados con los objetivos del caso de uso. El diseño, el control de calidad y el inicio de su esfuerzo de personalización son los más eficientes cuando se incluyen en los procesos de organización existentes.

## Paso 5: tomar medidas sobre los resultados

Una vez que su actividad de personalización haya atraído a una muestra representativa de visitantes, puede comenzar el análisis aprovechando las perspectivas para guiar los pasos siguientes. Sea impulsado por datos en su análisis, vinculando las recomendaciones a su hipótesis de caso de uso e ilustrando claramente el impacto en los objetivos comerciales.

### Más información

Le recomendamos que vea este vídeo en el que se analiza cada uno de estos pasos: [https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/](https://adobecustomersuccess.adobeconnect.com/pvsqvdvunpai/)

Obtenga más información sobre estrategia y liderazgo mental en [Éxito del cliente](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html) hub.