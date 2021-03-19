---
title: Implementación de at.js 2.0 en una aplicación de una sola página (SPA)
description: Adobe Target at.js 2.0 proporciona conjuntos de funciones enriquecidos que equipan su negocio para ejecutar personalizaciones en tecnologías de próxima generación del lado cliente. Siga estos pasos para implementar at.js 2.0 en una aplicación de una sola página (SPA).
role: Desarrollador
level: Intermedio
topic: SPA, arquitectura, desarrollo
feature: Implementación
doc-type: technical video
kt: null
thumbnail: null
author: Daniel Wright
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Implementar Adobe Target at.js 2.0 en una aplicación de una sola página (SPA)

Adobe Target `at.js` 2.0 proporciona conjuntos de funciones enriquecidos que equipan su negocio para ejecutar la personalización en tecnologías de próxima generación del lado cliente. Esta versión se centra en actualizar `at.js` para tener interacciones armoniosas con aplicaciones de una sola página (SPA).

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## Implementación de at.js 2.0 en una SPA

* Implemente `at.js` 2.0 en el &lt;head> de la aplicación de una sola página.
* Implemente la función `adobe.target.triggerView()` siempre que la vista cambie en la SPA. Se pueden emplear varias técnicas para hacerlo, como escuchar los cambios hash de la URL, escuchar los eventos personalizados activados por el SPA o incrustar el código `triggerView()` directamente en la aplicación. Debe elegir la opción que mejor funcione para la aplicación de una sola página específica.
* El nombre de la vista es el primer parámetro de la función `triggerView()`. Utilice nombres sencillos, claros y únicos para que sea más fácil seleccionarlos en el compositor de experiencias visuales de Target.
* Las vistas se pueden almacenar en déclencheur en cambios de vista pequeños, así como en contextos no SPA, como la mitad de la página con desplazamiento infinito.
* `at.js` 2.0 y se  `triggerView()` pueden implementar mediante una solución de administración de etiquetas, como Adobe Experience Platform Launch.

## Limitaciones de at.js 2.0

Tenga en cuenta las siguientes limitaciones de `at.js` 2.0 antes de actualizar:

* El seguimiento entre dominios no es compatible en `at.js` 2.0
* Los parámetros mboxOverride.browserIp y mboxSession URL no son compatibles con `at.js` 2.0
* Las funciones heredadas mboxCreate, mboxDefine, mboxUpdate están en desuso en `at.js` 2.0. Se mostrará el contenido predeterminado y no se realizarán solicitudes de red.

## Código de pie de página de biblioteca utilizado en el vídeo

El código siguiente se agregó a la sección Pie de página de la biblioteca `at.js` durante el vídeo. Se activa cuando la aplicación se carga por primera vez y, a continuación, en cualquier cambio hash en la aplicación. Utiliza una versión limpia del hash como nombre de vista y &quot;home&quot; cuando el hash está vacío. Tenga en cuenta que para identificar la SPA, el código busca el texto &quot;react/&quot; en la dirección URL, que muy probablemente necesite actualizarse en su sitio. Tenga en cuenta también que puede que sea más apropiado que su SPA active `triggerView()` fuera de los eventos personalizados o incrustando el código directamente en su aplicación.

```javascript
function sanitizeViewName(viewName) {
  if (viewName.startsWith('#')) {
    viewName = viewName.substr(1);
  }
  if (viewName.startsWith('/')) {
    viewName = viewName.substr(1);
  }
  return viewName;
}
function triggerView(viewName) {
  viewName = sanitizeViewName(viewName) || 'home';
  // Validate if the Target Libraries are available on your website
  if (typeof adobe != 'undefined' && adobe.target && typeof adobe.target.triggerView === 'function') {
    adobe.target.triggerView(viewName);
    console.log('AT: View triggered on page load: '+viewName)
  }
}
//fire triggerView when the SPA loads and when the hash changes in the SPA
if(window.location.pathname.indexOf('react/') >-1){
    triggerView(location.hash);
}
window.onhashchange = function() {
    if(window.location.pathname.indexOf('react/') >-1){
        triggerView(location.hash);
    }
}
```

## Recursos adicionales

* [Cómo funciona at.js 2.0 (Diagramas de arquitectura)](understanding-how-atjs-20-works.md)
* [Uso del Compositor de experiencias visuales de Adobe Target para aplicaciones de una sola página (SPA VEC)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
* [Actualización de la documentación de at.js 1.x a at.js 2.0](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/upgrading-from-atjs-1x-to-atjs-20.html)