---
title: Cómo administrar el catálogo de Recommendations mediante API
description: Esta parte del tutorial guía a los desarrolladores por los pasos necesarios para utilizar las API de Adobe Target para crear, actualizar, guardar, obtener y eliminar entidades en su catálogo de Recommendations.
role: Developer
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Recommendations, Administration & Configuration
doc-type: tutorial
kt: 3815
author: Judy Kim
exl-id: 8060b69b-e8e5-4fe7-895f-742410d8ed45
source-git-commit: cee2618bb92284da1f82d108a0aff0d39340a15b
workflow-type: tm+mt
source-wordcount: '918'
ht-degree: 2%

---

# Administre su [!DNL Recommendations] Catálogo mediante API

En este punto, ha aprendido a generar un token de acceso mediante el flujo de autenticación JWT para utilizar las API de administrador de Adobe Target con Adobe I/O.

Puede usar la variable [API de Recommendations](https://developers.adobetarget.com/api/recommendations/) para agregar, actualizar o eliminar artículos del catálogo de recomendaciones. Al igual que con el resto de las API de administración de Adobe Target, la variable [!DNL Recommendations] Las API requieren autenticación.

>[!TIP]
>
>Envíe el **[!UICONTROL IMS: Generación + autenticación de JWT mediante token de usuario]** solicite cada vez que necesite actualizar el token de acceso para la autenticación, ya que caduca a las 24 horas. Consulte [Configuración de la autenticación de API de Adobe](https://developer.adobe.com/target/before-administer/configure-authentication/){target=&quot;_blank&quot;} para obtener instrucciones.

![JWT3ff](assets/configure-io-target-jwt3ff.png)

>[!NOTE]
>
>Antes de continuar, obtenga la variable [Colección Recommendations Postman](https://developers.adobetarget.com/api/recommendations/#section/Postman).

## Creación y actualización de elementos con la API Guardar entidades

Para rellenar el [!DNL Recommendations] base de datos de productos utilizando la API en lugar de una fuente de producto CSV o [!DNL Target] solicitudes que se activan en páginas de productos, use la variable [API para guardar entidades](https://developers.adobetarget.com/api/recommendations/#operation/saveEntities). Esta solicitud agrega o actualiza un elemento en un solo [!DNL Target] entorno. La sintaxis es:

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

Por ejemplo, Guardar entidades puede utilizarse para actualizar artículos siempre que se cumplan ciertos umbrales, como umbrales para inventario o precio, a fin de marcar esos artículos e impedir que se recomienden.

1. Vaya a **[!DNL Target]> [!UICONTROL Configuración] > [!UICONTROL Hosts] > [!UICONTROL Entornos]** para obtener el [!DNL Target] ID de entorno en el que desea agregar o actualizar un elemento.

   ![SaveEntities1](assets/SaveEntities01.png)

2. Verificar `TENANT_ID` y `API_KEY` haga referencia a las variables de entorno de Postman establecidas anteriormente. Utilice la siguiente imagen para comparar. Si es necesario, modifique los encabezados y la ruta en su solicitud de API para que coincidan con los de la imagen siguiente.

   ![SaveEntities3](assets/SaveEntities03.png)

3. Escriba su JSON como **raw** en el **Cuerpo**. No olvide especificar su ID de entorno mediante la variable `environment` variable. (En el ejemplo siguiente, el ID de entorno es 6781).

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

1. ¡Ahora es tu turno! Utilice la variable **Guardar entidades** para añadir los siguientes elementos al catálogo. Utilice el archivo JSON de muestra anterior como punto de partida. (Deberá ampliar el JSON para incluir entidades adicionales).

   ![SaveEntities 6.png](assets/SaveEntities06.png)

Uy, parece que esos dos últimos artículos no pertenecen. Inspeccionémoslos usando el **Obtener entidad** y, si es necesario, elimínelos utilizando la **Eliminar entidades** API.

## Obtención de detalles del elemento con la API Get Entity

Para recuperar los detalles de un elemento existente, utilice el [Obtener API de entidad](https://developers.adobetarget.com/api/recommendations/#operation/getEntity). La sintaxis es:

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

Los detalles de entidades solo se pueden recuperar para una sola entidad a la vez. Puede utilizar Obtener entidad para confirmar que las actualizaciones se realizaron en el catálogo como se esperaba, o para auditar de otro modo el contenido del catálogo.

1. En la solicitud de API, especifique el ID de entidad mediante la variable `entityId`. El siguiente ejemplo devolverá detalles para la entidad cuya entityId=kit2004.

   ![GetEntity1](assets/GetEntity1.png)

2. Verificar `TENANT_ID` y `API_KEY` haga referencia a las variables de entorno de Postman establecidas anteriormente. Utilice la siguiente imagen para comparar. Si es necesario, modifique los encabezados y la ruta en su solicitud de API para que coincidan con los de la imagen siguiente.

   ![GetEntity2](assets/GetEntity2.png)

3. Envíe la solicitud.

   ![GetEntity3](assets/GetEntity3.png)
Si recibe un error que indica que no se ha encontrado la entidad, como se muestra en el ejemplo anterior, compruebe que está enviando la solicitud al [!DNL Target] entorno.

   >[!NOTE]
   Si no se especifica ningún entorno explícitamente, Get Entity intenta obtener la entidad de su [entorno predeterminado](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=en) solo. Si desea extraer de cualquier entorno que no sea el predeterminado, debe especificar el ID de entorno.

4. Si es necesario, agregue la variable `environmentId` y vuelva a enviar la solicitud.

   ![GetEntity4](assets/GetEntity4.png)

5. Enviar otro **Obtener entidad** esta vez para inspeccionar la entidad cuya entityId=kit2005.

   ![GetEntity5](assets/GetEntity5.png)

Supongamos que decide que estas entidades deben eliminarse del catálogo. Usemos el **Eliminar entidades** API.

## Eliminación de elementos con la API de eliminación de entidades

Para eliminar elementos del catálogo, use el [API de eliminación de entidades](https://developers.adobetarget.com/api/recommendations/#operation/deleteEntities). La sintaxis es:

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
Esta API elimina las entidades a las que hacen referencia los ID especificados.
Si no se proporcionan ID de entidad, se eliminan todas las entidades del entorno dado. Si no se proporciona ningún ID de entorno, las entidades se eliminarán de todos los entornos. ¡Utilícelo con precaución!

1. Vaya a **[!DNL Target]> [!UICONTROL Configuración] > [!UICONTROL Hosts] > [!UICONTROL Entornos]** para obtener el [!DNL Target] ID del entorno desde el que desea eliminar elementos.

   ![DeleteEntities1](assets/SaveEntities01.png)

2. En la solicitud de API, especifique los ID de entidad de las entidades que desea eliminar, utilizando la sintaxis `&ids=[comma-delimited-entity-ids]` (un parámetro de consulta). Al eliminar más de una entidad, separe los ID con comas.

   ![DeleteEntities2](assets/DeleteEntities2.png)

3. Especifique el ID de entorno mediante la sintaxis `&environment=[environmentId]`, de lo contrario, se eliminarán las entidades de todos los entornos.

   ![DeleteEntities3](assets/DeleteEntities3.png)

4. Verificar `TENANT_ID` y `API_KEY` haga referencia a las variables de entorno de Postman establecidas anteriormente. Utilice la siguiente imagen para comparar. Si es necesario, modifique los encabezados y la ruta en su solicitud de API para que coincidan con los de la imagen siguiente.

   ![DeleteEntities4](assets/DeleteEntities4.png)

5. Envíe la solicitud.

   ![DeleteEntities5](assets/DeleteEntities5.png)

6. Compruebe los resultados utilizando **Obtener entidad**, que ahora debería indicar que las entidades eliminadas no se pueden encontrar.

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

¡Felicidades! Ahora puede usar la variable [!DNL Recommendations] API para crear, actualizar, eliminar y obtener detalles sobre las entidades de su catálogo. En la siguiente sección, aprenderá a administrar criterios personalizados.

[Siguiente: &quot;Administrar criterios personalizados&quot; >](https://developer.adobe.com/target/before-administer/recs-api/manage-custom-criteria/){target=&quot;_blank&quot;}
