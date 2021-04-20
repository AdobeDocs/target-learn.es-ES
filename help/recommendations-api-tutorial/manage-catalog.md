---
title: Cómo administrar el catálogo de Recommendations mediante API
description: Esta parte del tutorial guía a los desarrolladores por los pasos necesarios para utilizar las API de Adobe Target para crear, actualizar, guardar, obtener y eliminar entidades en su catálogo de Recommendations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
thumbnail: null
author: Judy Kim
translation-type: tm+mt
source-git-commit: b89732fcca0be8bffc6e580e4ae0e62df3c3655d
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---


# Administrar el catálogo [!DNL Recommendations] mediante API

En este punto, ha aprendido a generar un token de acceso mediante el flujo de autenticación JWT para utilizar las API de administrador de Adobe Target con Adobe I/O.

Puede utilizar las [API de Recommendations](https://developers.adobetarget.com/api/recommendations/) para agregar, actualizar o eliminar elementos del catálogo de recomendaciones. Al igual que con el resto de las API de administración de Adobe Target, las API [!DNL Recommendations] requieren autenticación.

>[!TIP]
>
>Envíe el **[!UICONTROL IMS: Generar + autenticación JWT mediante la solicitud de token de usuario]** cada vez que necesite actualizar el token de acceso para la autenticación, ya que caduca a las 24 horas. Consulte [Configurar la autenticación de API de Adobe](../apis/configure-io-target-integration.md) para obtener instrucciones.

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>Antes de continuar, obtenga la [colección Postman de Recommendations](https://developers.adobetarget.com/api/recommendations/#section/Postman).

## Creación y actualización de elementos con la API Guardar entidades

Para rellenar la base de datos de productos [!DNL Recommendations] utilizando la API en lugar de una fuente de productos CSV o solicitudes [!DNL Target] que se activen en páginas de productos, utilice la [API para guardar entidades](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities). Esta solicitud agrega o actualiza un elemento en un único entorno [!DNL Target]. La sintaxis es:

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

Por ejemplo, Guardar entidades puede utilizarse para actualizar artículos siempre que se cumplan ciertos umbrales, como umbrales para inventario o precio, a fin de marcar esos artículos e impedir que se recomienden.

1. Vaya a **[!DNL Target]> [!UICONTROL Configuración] > [!UICONTROL Hosts] > [!UICONTROL Entornos]** para obtener el [!DNL Target] ID de entorno en el que desea agregar o actualizar un elemento.

   ![SaveEntities1](assets/SaveEntities01.png)

2. Compruebe que `TENANT_ID` y `API_KEY` hacen referencia a las variables de entorno de Postman establecidas anteriormente. Utilice la siguiente imagen para comparar. Si es necesario, modifique los encabezados y la ruta en su solicitud de API para que coincidan con los de la imagen siguiente.

   ![SaveEntities3](assets/SaveEntities03.png)

3. Introduzca su JSON como código **raw** en el **Body**. No olvide especificar su ID de entorno mediante la variable `environment` . (En el ejemplo siguiente, el ID de entorno es 6781).

   ![SaveEntities4.png](assets/SaveEntities04.png)

   >!![NOTE]
   A continuación, se muestra un ejemplo de JSON que agrega entity.id kit2001 con valores de entidad asociados para un producto de hornos de tostador al entorno 6781.

   ```
      {
      "entities": [{
              "name": "Toaster Oven",
              "id": "kit2001",
              "environment": 6781,
              "categories": [
                  "housewares:appliances"
              ],
              "attributes": {
                  "inventory": 77,
                  "margin": 23,
                  "message": "crashing helicopter",
                  "pageUrl": "www.foobar.foo.com/helicopter.html",
                  "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
              }
          }]
      }
   ```

4. Haga clic en **Enviar**. Debe recibir la siguiente respuesta.

   ![SaveEntities5.png](assets/SaveEntities05.png)

El objeto JSON se puede escalar para enviar varios productos. Por ejemplo, este JSON especifica dos entidades.

```
    {
        "entities": [{
                "name": "Toaster Oven",
                "id": "kit2001",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 89,
                    "margin": 11,
                    "message": "Toaster Oven",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 102.5
                }
            },
            {
                "name": "Blender",
                "id": "kit2002",
                "environment": 6781,
                "categories": [
                    "housewares:appliances"
                ],
                "attributes": {
                    "inventory": 36,
                    "margin": 5,
                    "message": "Blender",
                    "pageUrl": "www.foobar.foo.com/helicopter.html",
                    "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                    "value": 54.5
                }
            }
        ]
    }
```

1. ¡Ahora es tu turno! Utilice la API **Save Entities** para añadir los siguientes elementos al catálogo. Utilice el archivo JSON de muestra anterior como punto de partida. (Deberá ampliar el JSON para incluir entidades adicionales).

   ![SaveEntities5.png](assets/SaveEntities06.png)

Uy, parece que esos dos últimos artículos no pertenecen. Inspeccionémoslos usando la API **Get Entity** y, si es necesario, elimínelos mediante la API **Delete Entities**.

## Obtención de detalles del elemento con la API Get Entity

Para recuperar los detalles de un elemento existente, utilice la [Get Entity API](https://developers.adobetarget.com/api/recommendations/#operation/getEntity). La sintaxis es:

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

Los detalles de entidades solo se pueden recuperar para una sola entidad a la vez. Puede utilizar Obtener entidad para confirmar que las actualizaciones se realizaron en el catálogo como se esperaba, o para auditar de otro modo el contenido del catálogo.

1. En la solicitud de API, especifique el ID de entidad mediante la variable `entityId`. El siguiente ejemplo devolverá detalles para la entidad cuya entityId=kit2004.

   ![GetEntity1](assets/GetEntity1.png)

2. Compruebe que `TENANT_ID` y `API_KEY` hacen referencia a las variables de entorno de Postman establecidas anteriormente. Utilice la siguiente imagen para comparar. Si es necesario, modifique los encabezados y la ruta en su solicitud de API para que coincidan con los de la imagen siguiente.

   ![GetEntity2](assets/GetEntity2.png)

3. Envíe la solicitud.

   ![GetEntity3](assets/GetEntity3.png)
Si recibe un error que indica que no se encontró la entidad, como se muestra en el ejemplo anterior, compruebe que está enviando la solicitud al  [!DNL Target] entorno correcto.

   >[!NOTE]
   Si no se especifica ningún entorno explícitamente, Get Entity intenta obtener la entidad solo de su [entorno predeterminado](https://docs.adobe.com/content/help/en/target/using/administer/hosts.html#section_4F8539B07C0C45E886E8525C344D5FB0). Si desea extraer de cualquier entorno que no sea el predeterminado, debe especificar el ID de entorno.

4. Si es necesario, añada el parámetro `environmentId` y vuelva a enviar la solicitud.

   ![GetEntity4](assets/GetEntity4.png)

5. Envíe otra solicitud **Get Entity**, esta vez para inspeccionar la entidad cuya entityId=kit2005.

   ![GetEntity5](assets/GetEntity5.png)

Supongamos que decide que estas entidades deben eliminarse del catálogo. Usemos la API **Delete Entities**.

## Eliminación de elementos con la API de eliminación de entidades

Para eliminar elementos del catálogo, utilice la API [Delete Entities](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities). La sintaxis es:

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
Esta API elimina las entidades a las que hacen referencia los ID especificados.
Si no se proporcionan ID de entidad, se eliminan todas las entidades del entorno dado. Si no se proporciona ningún ID de entorno, las entidades se eliminarán de todos los entornos. ¡Utilícelo con precaución!

1. Vaya a **[!DNL Target]> [!UICONTROL Configuración] > [!UICONTROL Hosts] > [!UICONTROL Entornos]** para obtener el [!DNL Target] ID de entorno del que desea eliminar elementos.

   ![DeleteEntities1](assets/SaveEntities01.png)

2. En la solicitud de API, especifique los ID de entidad de las entidades que desea eliminar mediante la sintaxis `&ids=[comma-delimited-entity-ids]` (un parámetro de consulta). Al eliminar más de una entidad, separe los ID con comas.

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. Especifique la ID del entorno utilizando la sintaxis `&environment=[environmentId]`; de lo contrario, se eliminarán las entidades de todos los entornos.

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. Compruebe que `TENANT_ID` y `API_KEY` hacen referencia a las variables de entorno de Postman establecidas anteriormente. Utilice la siguiente imagen para comparar. Si es necesario, modifique los encabezados y la ruta en su solicitud de API para que coincidan con los de la imagen siguiente.

   ![DeleteEntities4](assets/DeleteEntities4.png)

5. Envíe la solicitud.

   ![DeleteEntities5](assets/DeleteEntities5.png)

6. Compruebe los resultados utilizando **Get Entity**, que ahora debería indicar que no se pueden encontrar las entidades eliminadas.

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

¡Felicidades! Ahora puede utilizar las API [!DNL Recommendations] para crear, actualizar, eliminar y obtener detalles sobre las entidades del catálogo. En la siguiente sección, aprenderá a administrar criterios personalizados.

[Siguiente: &quot;Administrar criterios personalizados&quot; >](manage-custom-criteria.md)
