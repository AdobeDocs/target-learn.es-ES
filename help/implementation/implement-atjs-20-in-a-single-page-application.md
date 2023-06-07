---
title: SPA Implementación de at.js 2.0 en una aplicación de una sola página ()
description: at.js 2.0 de Adobe Target proporciona conjuntos de funciones enriquecidos que equipan su empresa para ejecutar personalizaciones en tecnologías de próxima generación de lado del cliente. SPA Siga estos pasos para implementar at.js 2.0 en una aplicación de una sola página ().
role: Developer
level: Intermediate
topic: SPA, Architecture, Development
feature: Implementation
doc-type: technical video
kt: null
author: Daniel Wright
exl-id: 955f0571-5791-4dbb-9931-e6d5c8bb42a7
source-git-commit: 80208b3ecbc0d627d2afe72f882e91c9800d2726
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Implementar at.js 2.0 de Adobe Target SPA en una aplicación de una sola página ()

Adobe Target `at.js` 2.0 proporciona conjuntos de funciones enriquecidos que equipan su empresa para ejecutar personalizaciones en tecnologías de próxima generación del lado del cliente. Esta versión se centra en la actualización `at.js` SPA para tener interacciones armoniosas con aplicaciones de una sola página ().

>[!VIDEO](https://video.tv.adobe.com/v/26248?quality=12)

## SPA Implementación de at.js 2.0 en un entorno de trabajo de

* Implementación `at.js` 2.0 en &lt;head> de la aplicación de una sola página.
* Implementación de `adobe.target.triggerView()` SPA función cada vez que cambia la vista en el. SPA Para ello, se pueden emplear varias técnicas, como escuchar cambios de hash de URL, escuchar eventos personalizados activados por el usuario o incrustar el elemento de configuración de la dirección URL de la aplicación () `triggerView()` codifique directamente en la aplicación. Debe elegir la opción que mejor se adapte a su aplicación específica de una sola página.
* El nombre de la vista es el primer parámetro del `triggerView()` función. Use nombres sencillos, claros y únicos para que sea más fácil seleccionarlos en el compositor de experiencias visuales de Target.
* Puede aplicar déclencheur SPA a las vistas en pequeños cambios de vista, así como en contextos que no sean de tipo de datos, como la mitad de la ruta hacia abajo de una página con desplazamiento infinito.
* `at.js` 2.0 y `triggerView()` se puede implementar mediante una solución de administración de etiquetas, como Adobe Experience Platform Launch.

## Limitaciones de at.js 2.0

Tenga en cuenta las siguientes limitaciones de `at.js` 2.0 antes de la actualización:

* El seguimiento entre dominios no es compatible con `at.js` 2,0
* Los parámetros de URL mboxOverride.browserIp y mboxSession no son compatibles con `at.js` 2,0
* Las funciones heredadas mboxCreate, mboxDefine y mboxUpdate están en desuso en `at.js` 2.0. Se mostrará el contenido predeterminado y no se realizarán solicitudes de red.

## Código de pie de página de la biblioteca utilizado en el vídeo

El código siguiente se ha añadido a la sección Pie de página de la biblioteca de `at.js` durante el vídeo. Se activa cuando la aplicación se carga por primera vez y, a continuación, cuando se producen cambios de hash en la aplicación. Utiliza una versión limpiada del hash como nombre de vista y &quot;home&quot; cuando el hash está vacío. SPA Tenga en cuenta que, para identificar la, el código busca el texto &quot;react/&quot; en la dirección URL, que probablemente necesite actualizarse en el sitio. SPA Tenga en cuenta, también, que podría ser más apropiado para que su equipo de trabajo de la dispare `triggerView()` de eventos personalizados o incrustando el código directamente en la aplicación.

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

* [Funcionamiento de at.js 2.0 (Diagramas de arquitectura)](understanding-how-atjs-20-works.md)
* [Uso del Compositor de experiencias visuales de Adobe Target SPA para aplicaciones de una sola página (VEC de)](../experiences/use-the-visual-experience-composer-for-single-page-applications.md)
