---
title: Administrar criterios personalizados
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations incluye un conjunto dedicado de API que le permiten administrar su catálogo de productos y/o contenido recomendables; administrar los algoritmos y campañas de las recomendaciones; y envíe recomendaciones en objetos JSON, HTML o XML para que se muestren en web, móviles, de correo electrónico, IOT y otros canales.
kt: 3815
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Adobe Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 78b30bc0018527f9d8b2a5b50edee86e877d14c7
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# Administrar criterios personalizados

A veces, los algoritmos proporcionados por [!DNL Recommendations] no salen a la superficie elementos concretos que desee promocionar. En este caso, los criterios personalizados proporcionan una forma de entregar un conjunto específico de elementos recomendados para un elemento clave o una categoría determinada. La asignación se define entre el elemento clave o la categoría y los elementos recomendados, y se importa como criterio personalizado. Este proceso se describe en la documentación [de criterios](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html)personalizados. Como se indica en esa documentación, puede crear, editar y eliminar criterios personalizados a través de la interfaz de usuario (IU) [!DNL Target] . Sin embargo, [!DNL Target] también proporciona un conjunto de API de criterios personalizados que permiten una administración más detallada de los criterios personalizados.

>[!IMPORTANT]
>
>Siga esta guía de uso para conocer los criterios personalizados:
>
> Lleve a cabo todas las acciones (crear, editar, eliminar) de un criterio personalizado determinado mediante las API o bien realice todas las acciones (crear, editar, eliminar) mediante la interfaz de usuario. La administración de los criterios personalizados mediante una combinación de la interfaz de usuario y la API puede generar información en conflicto o resultados inesperados. Por ejemplo, la creación de criterios personalizados en la interfaz de usuario pero su edición mediante API no reflejará las actualizaciones en la interfaz de usuario, aunque se actualicen en segundo plano, como se ve a través de la API.

## Crear criterios personalizados

Para crear criterios personalizados con la API [](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom)Crear criterios personalizados, la sintaxis es:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Los criterios personalizados creados con la API Crear criterios personalizados, tal como se describe en este ejercicio, aparecerán en la interfaz de usuario, donde persistirán. No podrá editarlos ni eliminarlos de la interfaz de usuario. Puede editarlos o eliminarlos **mediante API**, pero de cualquier forma, seguirán apareciendo en la [!DNL Target] interfaz de usuario. Para mantener la opción de editar o eliminar de la interfaz de usuario, cree los criterios personalizados con la IU según [la documentación](https://docs.adobe.com/content/help/en/target/using/recommendations/criteria/recommendations-csv.html), en lugar de usar la API Crear criterios personalizados.

Continúe con este tutorial después de haber leído la advertencia anterior y se sienta cómodo creando nuevos criterios personalizados que no se pueden eliminar posteriormente de la interfaz de usuario.

1. Compruebe `TENANT_ID` y `API_KEY` para **Crear una referencia de criterios** personalizados, haga referencia a las variables de entorno de Postman establecidas anteriormente. Use la siguiente imagen para realizar comparaciones.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. Añada su **trabajo** como JSON **sin procesar** que define la ubicación del archivo CSV de criterios personalizados. Utilice el ejemplo que se proporciona en la documentación [Crear API](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) de criterios personalizados como plantilla, proporcionando los valores `environmentId` y otros según sea necesario. Para este ejemplo, utilizamos LAST_PURCHASED como clave.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. Envíe la solicitud y observe la respuesta, que contiene los detalles de los criterios personalizados que acaba de crear.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. Para comprobar si se han creado los criterios personalizados, vaya a **[!UICONTROL Recommendations]>[!UICONTROL Criterios]** en Adobe Target y busque los criterios por nombre, o utilice la API **de criterios personalizados de** Lista en el paso siguiente.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

En este caso, tenemos un error. Analicemos el error examinando los criterios personalizados con mayor detenimiento, utilizando la API **de criterios personalizados de** Lista.

## Criterios personalizados de Lista

Para recuperar una lista de todos los criterios personalizados junto con los detalles de cada uno, utilice la API [de criterios personalizados de](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom)Lista. La sintaxis es:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Verifique `TENANT_ID` y `API_KEY` como antes y envíe la solicitud. En la respuesta, tenga en cuenta la ID de los criterios personalizados, así como los detalles relativos al mensaje de error que se ha indicado anteriormente.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

En este caso, el error se produjo porque la información del servidor es incorrecta, lo que significa que no [!DNL Target] puede acceder al archivo CSV que contiene la definición de criterios personalizados. Editemos los criterios personalizados para corregir esto.

## Editar criterios personalizados

Para cambiar los detalles de una definición de criterio personalizada, utilice la API [](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom)Editar criterio personalizado. La sintaxis es:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Verificar `TENANT_ID` y `API_KEY`, como antes.
   ![EditCustomCriteria1](assets/EditCustomCriteria1.png)

1. Especifique el ID de criterio de los criterios personalizados (únicos) que desea editar.
   ![EditCustomCriteria2](assets/EditCustomCriteria2.png)

1. En el cuerpo, proporcione a JSON actualizado la información correcta del servidor. (Para este paso, especifique el acceso mediante FTP a un servidor al que pueda acceder).
   ![EditCustomCriteria3](assets/EditCustomCriteria3.png)

1. Envíe la solicitud y anote la respuesta.
   ![EditCustomCriteria4](assets/EditCustomCriteria4.png)

Verifiquemos el éxito de los criterios personalizados actualizados mediante la **obtención de la API** de criterios personalizados.

## Obtener criterios personalizados

Para vista de detalles de criterios personalizados para un criterio personalizado específico, utilice la [Obtención de la API](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom)de criterios personalizados. La sintaxis es:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique el ID de criterio de los criterios personalizados cuyos detalles desee obtener. Envíe la solicitud y revise la respuesta.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Verificar si la operación se ha realizado correctamente. (En nuestro caso, compruebe que no haya más errores de FTP).
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Opcional) Compruebe que la actualización se refleja correctamente en la interfaz de usuario.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Eliminar criterios personalizados

Con el ID de criterios indicado anteriormente, elimine los criterios personalizados mediante la API [](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom)Eliminar criterios personalizados. La sintaxis es:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique el ID de criterio de los criterios personalizados (únicos) que desea eliminar. Haga clic en **Enviar**.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Verifique que los criterios se hayan eliminado mediante Obtener criterios personalizados.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)En este caso, el error 404 esperado indica que no se pueden encontrar los criterios eliminados.

>[!NOTE]
>Como recordatorio, los criterios no se eliminarán de la interfaz de usuario aunque se hayan eliminado, ya que se crearon con la API Crear criterios personalizados. [!DNL Target]

¡Felicitaciones! Ahora puede crear, lista, editar, eliminar y obtener detalles sobre criterios personalizados mediante la [!DNL Recommendations] API. En la siguiente sección, utilizará la API de [!DNL Target] Envío para recuperar las recomendaciones.

[Siguiente &quot;Buscar Recommendations con la API de Envío del lado del servidor&quot; >](fetch-recs-server-side-delivery-api.md)