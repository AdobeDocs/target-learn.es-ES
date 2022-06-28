---
title: Cómo administrar criterios personalizados
description: Esta parte del tutorial guía a los desarrolladores por los pasos necesarios para utilizar las API de Adobe Target para administrar, crear, enumerar, editar, obtener y eliminar criterios de Recommendations de Adobe Target.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: ee63bd3e-200a-4c08-b364-9f17a479033b
source-git-commit: 0ecfde208b3e201de135512d5aab70192fc2b826
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 1%

---

# Administrar criterios personalizados

A veces, los algoritmos proporcionados por [!DNL Recommendations] no pueden mostrar elementos concretos que desee promocionar. En tal situación, los criterios personalizados permiten entregar un conjunto específico de artículos recomendados para un elemento clave o categoría determinados. La asignación se define entre el elemento clave o la categoría y los artículos recomendados, y se importa como criterio personalizado. Este proceso se describe en la sección [documentación de criterios personalizados](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en). Como se indica en esa documentación, puede crear, editar y eliminar criterios personalizados mediante la variable [!DNL Target] interfaz de usuario (IU). Sin embargo, [!DNL Target] también proporciona un conjunto de API de criterios personalizados que permiten una administración más detallada de los criterios personalizados.

>[!IMPORTANT]
>
>Siga esta guía de uso para criterios personalizados:
>
> Haga todo (crear, editar, eliminar) para un criterio personalizado determinado mediante las API o haga todo (crear, editar, eliminar) mediante la interfaz de usuario. La administración de los criterios personalizados mediante una combinación de la interfaz de usuario y la API puede dar lugar a información conflictiva o a resultados inesperados. Por ejemplo, la creación de criterios personalizados en la interfaz de usuario, pero luego su edición mediante API, no reflejarán las actualizaciones en la interfaz de usuario, aunque se actualicen en el servidor, como se puede ver en la API.

## Crear criterios personalizados

Para crear criterios personalizados con la variable [Crear API de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/createCriteriaCustom), la sintaxis es:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

>[!WARNING]
>
>Los criterios personalizados creados con la API Crear criterios personalizados , tal como se describe en este ejercicio, aparecerán en la interfaz de usuario, donde persistirán. No podrá editarlas ni eliminarlas de la interfaz de usuario. Puede editarlas o eliminarlas **mediante API**, pero de cualquier manera, seguirán apareciendo en la variable [!DNL Target] IU. Para mantener la opción de editar o eliminar de la interfaz de usuario, cree los criterios personalizados empleando la interfaz de usuario de [la documentación](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/recommendations-csv.html?lang=en), en lugar de usar la API Crear criterio personalizado .

Continúe solo con este tutorial después de haber leído la advertencia anterior y se sienta cómodo creando nuevos criterios personalizados que no se pueden eliminar posteriormente de la interfaz de usuario.

1. Verificar `TENANT_ID` y `API_KEY` para **Crear criterios personalizados** haga referencia a las variables de entorno de Postman establecidas anteriormente. Utilice la siguiente imagen para comparar.

   ![CreateCustomCriteria1](assets/CreateCustomCriteria1.png)

2. Agregue la **Cuerpo** como **raw** JSON que define la ubicación del archivo CSV de criterios personalizados. Utilice el ejemplo proporcionado en la variable [Crear API de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom) documentación como plantilla, que proporciona su `environmentId` y otros valores según sea necesario. Para este ejemplo, utilizamos LAST_PURCHASED como clave.

   ![CreateCustomCriteria2](assets/CreateCustomCriteria2.png)

3. Envíe la solicitud y observe la respuesta, que contiene los detalles de los criterios personalizados que acaba de crear.

   ![CreateCustomCriteria3](assets/CreateCustomCriteria3.png)

4. Para comprobar que se han creado los criterios personalizados, vaya a **[!UICONTROL Recommendations] > [!UICONTROL Criterios]** y busque sus criterios por nombre, o use el **API de criterios personalizados de lista** en el siguiente paso.

   ![CreateCustomCriteria4](assets/CreateCustomCriteria4.png)

En este caso, tenemos un error. Investiguemos el error examinando los criterios personalizados más detenidamente, usando la variable **API de criterios personalizados de lista**.

## Enumerar criterios personalizados

Para recuperar una lista de todos los criterios personalizados junto con los detalles de cada uno, use la variable [API de criterios personalizados de lista](https://developers.adobetarget.com/api/recommendations/#operation/getAllCriteriaCustom). La sintaxis es:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom`

1. Verificar `TENANT_ID` y `API_KEY` como antes, y envíe la solicitud. En la respuesta, tenga en cuenta el ID de criterios personalizados, así como los detalles relativos al mensaje de error que ya se han indicado.
   ![ListCustomCriteria](assets/ListCustomCriteria.png)

En este caso, el error se produjo porque la información del servidor es incorrecta, lo que significa que [!DNL Target] no puede acceder al archivo CSV que contiene la definición de criterios personalizados. Editemos los criterios personalizados para corregirlos.

## Editar criterios personalizados

Para cambiar los detalles de una definición de criterios personalizados, use la variable [Editar API de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/updateCriteriaCustom). La sintaxis es:

`POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Verificar `TENANT_ID` y `API_KEY`, como antes.
   ![EditarCriteriosPersonalizados1](assets/EditCustomCriteria1.png)

1. Especifique el ID de criterio de los criterios personalizados (únicos) que desea editar.
   ![EditarCriteriosPersonalizados2](assets/EditCustomCriteria2.png)

1. En el cuerpo, proporcione JSON actualizado con la información correcta del servidor. (Para este paso, especifique el acceso FTP a un servidor al que puede acceder).
   ![EditarCriteriosPersonalizados3](assets/EditCustomCriteria3.png)

1. Envíe la solicitud y anote la respuesta.
   ![EditarCriteriosPersonalizados4](assets/EditCustomCriteria4.png)

Comprobemos el éxito de los criterios personalizados actualizados mediante el **Obtener API de criterios personalizados**.

## Obtener criterios personalizados

Para ver los detalles de criterios personalizados de un criterio personalizado específico, use la variable [Obtener API de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/getCriteriaCustom). La sintaxis es:

`GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique el ID de criterio de los criterios personalizados cuyos detalles desee obtener. Envíe la solicitud y revise la respuesta.
   ![GetCustomCriteria.png](assets/GetCustomCriteria.png)
1. Verifique que se ha realizado correctamente. (En nuestro caso, compruebe que no haya más errores de FTP).
   ![GetCustomCriteria1.png](assets/GetCustomCriteria1.png)
1. (Opcional) Compruebe que la actualización se refleja con precisión en la interfaz de usuario.
   ![GetCustomCriteria2.png](assets/GetCustomCriteria2.png)

## Eliminar criterios personalizados

Con el ID de criterios que se ha indicado anteriormente, elimine los criterios personalizados con la variable [Eliminar API de criterios personalizados](https://developers.adobetarget.com/api/recommendations/#operation/deleteCriteriaCustom). La sintaxis es:

`DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/criteria/custom/:criteriaId`

1. Especifique el ID de criterio de los criterios personalizados (únicos) que desee eliminar. Haga clic en **Enviar**.
   ![DeleteCustomCriteria1](assets/DeleteCustomCriteria1.png)

1. Compruebe que los criterios se han eliminado mediante Obtener criterios personalizados.
   ![DeleteCustomCriteria2](assets/DeleteCustomCriteria2.png)
En este caso, el error 404 esperado indica que no se pueden encontrar los criterios eliminados.

>[!NOTE]
>Como recordatorio, los criterios no se eliminarán del [!DNL Target] Aunque se haya eliminado, ya que se creó con la API Crear criterios personalizados .

¡Felicidades! Ahora puede crear, enumerar, editar, eliminar y obtener detalles sobre criterios personalizados mediante el [!DNL Recommendations] API. En la siguiente sección, utilizará la variable [!DNL Target] API de envío para recuperar recomendaciones.

[Siguiente: &quot;Buscar Recommendations con la API de envío del lado del servidor&quot; >](https://developer.adobe.com/target/before-administer/recs-api/fetch-recs-server-side-delivery-api/){target=_blank}
