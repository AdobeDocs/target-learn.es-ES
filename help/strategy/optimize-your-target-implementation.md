---
title: Optimizar la implementación de Adobe Target
description: Obtenga información general sobre la implementación y estructura de Adobe Target. Obtenga información sobre cómo comprender y auditar la configuración de su organización. Conozca las técnicas comunes de solución de problemas y sugerencias para crear un repositorio de conocimientos para su equipo.
solution: Target
feature: Overview
role: Leader, User
exl-id: 49b69f41-0993-437c-bb69-84392be427df
source-git-commit: 20bd1eb17ef6e287f7b76e14f727456e12d6f115
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---

# Optimizar la implementación de Adobe Target

Si es nuevo en su organización y desea familiarizarse con las funciones de una práctica de pruebas y optimización, este artículo le ayuda a empezar. Empezaremos con una descripción general de la implementación y estructura de Adobe Target. Aprenderá a comprender y auditar la configuración de su organización. Por último, analizaremos técnicas comunes de resolución de problemas y sugerencias para crear un repositorio de conocimientos para su equipo.

Adobe Target es una herramienta que permite probar y segmentar contenido único para diferentes visitantes. Para obtener una descripción general de las características disponibles, [visite esta guía](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=es).

## Implementación y estructura de Target

Antes de profundizar en el proceso de implementación de Adobe Target o en cómo está estructurado, es útil conocer primero algunos aspectos básicos del software.

Adobe Target es una herramienta que permite probar y dirigir contenido único a distintos visitantes sin cambiar el código nativo del sitio web. Target cambia temporalmente la experiencia del usuario final, así como rastrea el comportamiento de los usuarios después de ver el cambio. Target también ofrece la capacidad de modificar la experiencia de los usuarios finales en función de la información del perfil o de acciones anteriores.

Existen tres tipos de actividades fundamentales de Target:

1. Prueba A/B
2. Pruebas multivariable (MVT)
3. Pruebas de experiencia

**La prueba A/B** compara dos o más experiencias para ver cuál mejora más las conversiones durante un período de prueba previamente establecido. La prueba A/B es un experimento muy controlado con mediciones de tráfico, divididas por porcentajes en lugar de por una regla, lo que le permite:

* para analizar los datos de prueba.
* para obtener información sobre su audiencia.
* para determinar qué experiencia ofrece el mejor rendimiento.

**Pruebas multivariable** (MVT) compara combinaciones de ofertas entre elementos de una página para ver cuál ofrece el mejor resultado para una audiencia específica. Esta prueba también identifica qué elemento de la página mejora más las conversiones durante un periodo de prueba previamente establecido. MVT proporciona:

* Una forma de mostrar varias ofertas en varios elementos.
* Un método para probar la experiencia única resultante con un objetivo específico.
* Insight especifica qué elementos tienen el mayor impacto negativo o positivo en las interacciones de los visitantes.

**Pruebas de experiencia** (Segmentación de experiencias) ofrece contenido a una audiencia específica en función de un conjunto de reglas y criterios definidos por expertos en marketing. Este método proporciona una forma de dirigir contenido específico a una audiencia específica en función de un conjunto de reglas de asignación definidas.

¿Cómo funciona Target?

Este es un ejemplo de alto nivel de cómo funciona Target:

1. Un visitante solicita una página del servidor y esta se muestra en el explorador.
1. Se establece una cookie de origen en el explorador del visitante para almacenar el comportamiento.
1. A continuación, la página llama a Adobe Target.
1. El contenido se muestra en función de las reglas de la actividad del usuario.
1. Adobe Target captura métricas específicas tal como se definen en la configuración de la actividad para medir el impacto de las experiencias de prueba.

Target se basa en un &quot;mbox global&quot; que permite afectar a cualquier elemento de la página. Esta función se implementa al cargar la página como vínculo codificado al archivo at.js o se entrega con un Administrador de etiquetas como Adobe Launch.

## Comprender la implementación actual

Para comprender su implementación actual, Adobe le recomienda que revise la implementación de la interfaz de usuario de Target junto con la implementación del Administrador de etiquetas y la implementación de carga de página.

**Para revisar la interfaz de usuario de [!DNL Target]:**

1. Empiece a revisar en la interfaz de usuario de [!DNL Target]:

   * Revisar la pila de tecnología [!DNL Target]
   * Confirmar las funciones disponibles
   * Identificar dónde se encuentra activa la implementación

1. Revise las actividades para conocer las prácticas recomendadas:

   * Revisar campañas históricas para la madurez del programa

1. Desactivar actividades antiguas:

   * Archivar y limpiar [!DNL Target] recurso que ya no tenga uso actual o futuro

1. Revisar audiencias.

1. Revise las definiciones de entorno y los dominios asociados.

1. Revisar scripts de perfil para aplicabilidad

   * Todos los scripts de perfil se ejecutan en cada llamada de destino
   * Mantenga la eficacia de las llamadas eliminando los scripts no aplicables

Para revisar el administrador de etiquetas y la carga de página:

1. Confirme lo siguiente en el administrador de etiquetas:

   * Implementación del código JavaScript [!DNL Target] esperado
   * La solución de ocultación de contenido adecuada
   * Establezca las reglas necesarias para rellenar las llamadas de [!DNL Target] con los parámetros esperados

1. Confirme lo siguiente durante la carga de la página:

   * Números de versión coincidentes para la dirección URL de solicitud y la dirección URL de solicitud [!DNL Target]
   * Valor de Experience Cloud ID rellenado (cuerpo de nube)
   * Presentar los valores de integración esperados (cuerpo de nube)
   * Se rellenaron [!DNL Target] parámetros en las páginas apropiadas

## [!DNL Target] actividades de auditoría

Para evitar pasar manualmente por cada página para auditar [!DNL Target] actividades, use Adobe Auditor para comprender el estado técnico actual de la implementación. Adobe Auditor funciona con ObservePoint y se puede configurar para que se ejecute de forma manual a fin de identificar los problemas de implementación de alto nivel en su sitio.

Adobe Auditor proporciona lo siguiente:

* Un buen estado del sitio
* Llamadas rápidas para problemas de implementación

Adobe recomienda realizar auditorías manuales mensuales para:

* Identificación de páginas sin etiquetar
* Identificación de versiones incoherentes
* Búsqueda de versiones no actualizadas
* Proporcione información detallada que se pueda exportar

## Solución de problemas común

>[!NOTE]
>
>Adobe recomienda instalar Adobe Experience Platform Debugger.

A continuación se ofrecen sugerencias generales para la resolución de problemas al entrar en Experience Cloud:

### Caché y cookies**

* Borrando la caché y las cookies
* Tenga cuidado al utilizar el modo privado (por ejemplo: el modo privado en Firefox puede bloquear [!DNL Target])

### ¿Cumple los requisitos para la actividad?

* Compruebe que ha realizado los mismos pasos que la audiencia utilizó en la actividad
* Utilice `mboxTrace` o tokens de respuesta para comprobar los valores de perfil y segmento

### Sugerencias generales para la resolución de problemas al validar elementos visuales/funcionales

Si se encuentra en la experiencia [!DNL Target] y no ve la experiencia visual esperada:

Compruebe la respuesta de [!DNL Target]:

* Si no se ejecuta el código:

1. Compruebe las actividades en conflicto
1. Contactar con Atención al cliente

* Si se ejecuta el código:

1. Volver a trabajar el código en ese escenario

## Mantenimiento de un repositorio de conocimientos

Un repositorio de conocimientos es una plataforma en línea que se utiliza para documentar y compartir información. El repositorio de conocimientos contiene información específica sobre la implementación y puede contener información específica sobre el equipo.

Lo ideal es que el repositorio permita la edición y el guardado automático dentro de la plataforma. Una vez configurada inicialmente, es fácil de mantener y mantenerse al día. El contenido del repositorio de conocimientos se depura según las funciones de los usuarios.

Entre los documentos habituales de un repositorio de conocimientos se incluyen:

* **Documento de información general**: documento utilizado para explicar claramente las metas, los objetivos, los procesos y la estructura del programa
* **Repositorio de ideas**: un documento que se usa para administrar y priorizar ideas potenciales que no están listas para el proceso de prueba
* **Hoja de ruta del programa**: un documento usado para administrar todos los aspectos de las actividades de prueba una vez que las ideas estén listas para iniciar el proceso de prueba
* **Documento de plan de actividades**: documento utilizado para esbozar la información necesaria para generar e iniciar actividades
* **Documento de plan de actividades**: documento utilizado para comunicar los resultados y los pasos siguientes recomendados a las partes interesadas
* **Panel del programa**: un documento que se usa para rastrear el rendimiento del programa, la cadencia y los beneficios de ingresos a lo largo del tiempo.

Para obtener más información, revise nuestro [seminario web](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) con el consultor sénior Wilder Freed.

Obtenga más información sobre estrategia y liderazgo mental en el centro de [Éxito del cliente](https://experienceleague.adobe.com/docs/customer-success/customer-success/overview.html?lang=es).
