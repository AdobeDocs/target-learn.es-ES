---
title: Optimizar la implementación de Adobe Target
description: Obtenga información general sobre la implementación y estructura de Adobe Target. Obtenga información sobre cómo comprender y auditar la configuración de su organización. Conozca las técnicas comunes de solución de problemas y consejos sobre la creación de un repositorio de conocimientos para su equipo.
solution: Target
exl-id: 49b69f41-0993-437c-bb69-84392be427df
source-git-commit: 46f61d8f503f230a79b4072ea0d75edd41403708
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# Optimizar la implementación de Adobe Target

Si es nuevo en su organización y desea familiarizarse con lo que se establece a partir de una práctica de optimización y pruebas, este artículo le ayuda a iniciarse. Empezaremos con una descripción general de la implementación y estructura de Adobe Target. Aprenderá a comprender y auditar la configuración de su organización. Por último, analizaremos técnicas comunes de solución de problemas y sugerencias sobre la creación de un repositorio de conocimientos para su equipo.

Adobe Target es una herramienta que permite realizar pruebas y segmentar contenido único para distintos visitantes. Para obtener una descripción general de las funciones disponibles, [visite esta guía](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=en).

## Implementación y estructura de objetivos

Antes de profundizar en el proceso de implementación de Adobe Target o en cómo está estructurado, es útil comprender primero algunos aspectos básicos del software.

Adobe Target es una herramienta que permite probar y segmentar contenido único para distintos visitantes sin cambiar el código nativo del sitio web. Target cambia temporalmente la experiencia del usuario final, así como rastrea el comportamiento de los usuarios después de ver el cambio. Target también ofrece la capacidad de modificar la experiencia para los usuarios finales en función de la información de perfil o de acciones anteriores.

Existen tres tipos de actividades fundamentales de Target:

1. Prueba A/B
2. Pruebas multivariable (MVT)
3. Pruebas de experiencia

**La prueba A/B** compara dos o más experiencias para ver cuál mejora más las conversiones durante un periodo de prueba previamente establecido. La prueba A/B es un experimento altamente controlado con mediciones de tráfico, dividido por porcentajes en lugar de por una regla, que le permite:

* para analizar los datos de prueba.
* para obtener información sobre su audiencia.
* para determinar qué experiencia ofrece el mejor rendimiento.

**Pruebas multivariable** (MVT) compara combinaciones de ofertas entre elementos de una página para ver cuál ofrece el mejor rendimiento para una audiencia específica. Esta prueba también identifica qué elemento de la página mejora mejor las conversiones durante un periodo de prueba previamente establecido. MVT proporciona:

* Una forma de mostrar varias ofertas en varios elementos.
* Método para probar la experiencia única resultante con un objetivo específico.
* Comprender qué elementos tienen un impacto bueno negativo o positivo en las interacciones del visitante.

**Pruebas de experiencia** (Segmentación de experiencias) ofrece contenido a una audiencia específica en función de un conjunto de reglas y criterios definidos por expertos en marketing. Este método proporciona una forma de dirigir contenido específico a una audiencia específica en función de un conjunto de reglas de asignación definidas.

¿Cómo funciona Target?

Este es un ejemplo de alto nivel de cómo funciona Target:

1. Un visitante solicita una página del servidor y esta se muestra en el explorador.
1. Se establece una cookie de origen en el explorador del visitante para almacenar el comportamiento.
1. A continuación, la página llama a Adobe Target.
1. El contenido se muestra en función de las reglas de la actividad del usuario.
1. Adobe Target captura métricas específicas tal como se definen en la configuración de la actividad para medir el impacto de las experiencias de prueba.

Target se basa en un &quot;mbox global&quot; que proporciona la capacidad de afectar cualquier cosa en la página. Esta función se implementa al cargar la página como un vínculo codificado al archivo at.js o se entrega mediante un Administrador de etiquetas como Adobe Launch.

## Comprender la implementación actual

Para comprender su implementación actual, Adobe recomienda que revise su implementación de la interfaz de usuario de Target junto con su implementación del Administrador de etiquetas y la carga de página .

**Para revisar su [!DNL Target] interfaz de usuario:**

1. Comience la revisión en el [!DNL Target] IU:

   * Consulte la [!DNL Target] pila de tecnología
   * Confirmar las funciones disponibles
   * Identificar dónde está la implementación

1. Revise las actividades para conocer las prácticas recomendadas:

   * Revisar campañas históricas para la madurez del programa

1. Desactivar actividades antiguas:

   * Archivar y limpiar [!DNL Target] recurso que ya no tiene uso actual o futuro

1. Revise las audiencias.

1. Revise las definiciones de entorno y los dominios asociados.

1. Revisión de scripts de perfil para aplicabilidad

   * Todos los scripts de perfil se ejecutan en cada llamada de destino
   * Mantener la eficiencia de las llamadas eliminando secuencias de comandos no aplicables

Para revisar el administrador de etiquetas y la carga de la página:

1. Confirme lo siguiente en el administrador de etiquetas:

   * La implementación de la [!DNL Target] Código JavaScript
   * La solución de ocultación de contenido adecuada
   * Establezca las reglas necesarias para rellenar la variable [!DNL Target] llamadas con los parámetros esperados

1. Confirme lo siguiente durante la carga de la página:

   * Coincidencia de números de versión para la URL de solicitud y [!DNL Target] URL de solicitud
   * Valor de Experience Cloud ID rellenado (cuerpo de la nube)
   * Presente los valores de integración esperados (Cloud Body)
   * Rellenado [!DNL Target] parámetros en las páginas correspondientes

## [!DNL Target] actividades de auditoría

Para evitar pasar manualmente por cada página para auditar [!DNL Target] , utilice Adobe Auditor para comprender mejor el estado técnico actual de la implementación. Adobe Auditor cuenta con la tecnología de ObservePoint y se puede configurar para que se ejecute a nivel manual a fin de identificar problemas de implementación de alto nivel en el sitio.

Adobe Auditor proporciona:

* Un buen estado del sitio
* Llamadas rápidas para problemas de implementación

Adobe recomienda realizar auditorías manuales mensuales para:

* Identificar las páginas sin etiquetar
* Identificar versiones incoherentes
* Descubra las versiones obsoletas
* Proporcionar información detallada que se puede exportar

## Solución de problemas comunes

>[!NOTE]
>
>Adobe recomienda instalar Adobe Experience Platform Debugger.

A continuación encontrará sugerencias generales para la solución de problemas al entrar en Experience:

### Caché y cookies**

* Borrado de la caché y las cookies
* Tenga cuidado al utilizar el modo privado (por ejemplo: el modo privado en Firefox puede bloquear [!DNL Target])

### ¿Está cualificado para la actividad?

* Compruebe que haya realizado los mismos pasos que la audiencia utilizó en la actividad
* Uso `mboxTrace` o tokens de respuesta para comprobar los valores de perfil y segmento

### Sugerencias generales de resolución de problemas al validar visual/funcional

Si están en la variable [!DNL Target] experiencia y no ve la experiencia visual esperada:

Marque la [!DNL Target] Respuesta:

* Si el código no se ejecuta:

1. Comprobar actividades en conflicto
1. Contactar con Client Care

* Si se ejecuta el código:

1. Volver a trabajar el código en ese escenario

## Mantenimiento de un repositorio de conocimientos

Un repositorio de conocimientos es una plataforma en línea que se utiliza para documentar y compartir información. El repositorio de conocimientos contiene información específica sobre su implementación y puede contener información específica del equipo.

Lo ideal es que el repositorio permita la edición y el guardado automático dentro de la plataforma. Una vez configurada inicialmente, es fácil de mantener y mantener actualizado. El contenido del repositorio de conocimiento se selecciona en función de las funciones de usuario.

Los documentos típicos de un repositorio de conocimientos incluyen:

* **Documento de información general** - un documento utilizado para explicar claramente las metas, los objetivos, los procesos y la estructura del programa
* **Repositorio de ideas** - un documento utilizado para administrar y priorizar las ideas potenciales que no están listas para el proceso de prueba
* **Hoja de ruta del programa** : documento utilizado para administrar todos los aspectos de las actividades de prueba una vez que las ideas están listas para iniciar el proceso de prueba
* **Documento del plan de actividades** - un documento utilizado para delinear la información necesaria para crear e iniciar actividades
* **Documento del plan de actividades** - un documento utilizado para comunicar los resultados y los pasos siguientes recomendados a las partes interesadas
* **Panel del programa** : documento utilizado para realizar un seguimiento del rendimiento del programa, la cadencia y los beneficios de ingresos a lo largo del tiempo.

Para obtener más información, consulte [seminario web](https://adobecustomersuccess.adobeconnect.com/p4p7xlp7dh42mp4/) con el consultor principal, Wilder Freed.

Obtenga más información sobre la estrategia y el liderazgo mental en [Éxito del cliente](https://experienceleague.corp.adobe.com/docs/customer-success/customer-success/overview.html) hub.
