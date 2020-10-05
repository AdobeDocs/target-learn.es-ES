---
title: Configurar la autenticación para las API de Adobe Target
keywords: recommendations;adobe recommendations;premium;api;apis
description: Adobe Target Recommendations incluye un conjunto dedicado de API que le permiten administrar su catálogo de productos y/o contenido recomendables; administrar los algoritmos y campañas de las recomendaciones; y envíe recomendaciones en objetos JSON, HTML o XML para que se muestren en web, móviles, de correo electrónico, IOT y otros canales.
kt: null
audience: developer
doc-type: tutorial
activity: use
feature: api
topics: recommendations;adobe recommendations;premium;api;apis
solution: Target
author: Judy Kim
translation-type: tm+mt
source-git-commit: 7e57febf5f552d697260283a3f98f9b403663f28
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 2%

---


# Configurar la autenticación para las API de Adobe Target

Las API de administración de Adobe Target, incluidas las API de [!DNL Recommendations] administración, están protegidas mediante autenticación para garantizar que solo los usuarios autorizados las utilicen para acceder a Adobe Target. Utilice la consola [de desarrollador de](https://console.adobe.io/) Adobe para administrar esta autenticación en todas las soluciones de Adobe Experience Cloud, incluida [!DNL Target].

En esta lección se explican los pasos preliminares necesarios para generar los tokens de autenticación necesarios para interactuar correctamente con las API de Adobe Target. En las secciones siguientes, podrá:

1. Cree un proyecto (anteriormente denominado integración) en Adobe Developer Console.
2. Exporte los detalles del proyecto a Postman.
3. Generar un token de acceso portador.
4. Compruebe el token de acceso del soporte.

## Requisitos previos

| Recurso | Detalles |
| --- | --- |
| Postman | Para completar estos pasos correctamente, obtenga la aplicación [](https://www.postman.com/downloads/) Postman para su sistema operativo. Postman Basic es gratis con la creación de cuentas. Aunque no es necesario para utilizar las API de Adobe Target en general, Postman facilita los flujos de trabajo de API y Adobe Target proporciona varias colecciones de Postman para ayudar a ejecutar sus API y aprender a funcionar. El resto de este tutorial asume el conocimiento práctico de Postman. Para obtener ayuda, consulte la documentación [de](https://learning.getpostman.com/)Postman. |
| Referencias | Durante el resto de este tutorial se asume la familiaridad con los siguientes recursos:<UL><li>[Github de E/S Adobe](https://github.com/adobeio)</li><li>[Documentación de E/S de Adobe de destinatario](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentación de la API de Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## Creación de un proyecto de E/S de Adobe

En esta sección, accederá a Adobe Developer Console y creará un proyecto para [!DNL Adobe Target]. Para obtener más información, consulte la [documentación sobre proyectos](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md).

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. En [Adobe Admin Console](https://adminconsole.adobe.com/), asegúrese de que su cuenta de usuario de Adobe tenga acceso a nivel de administrador [de](https://helpx.adobe.com/enterprise/using/admin-roles.html) productos y de [desarrollador](https://helpx.adobe.com/enterprise/using/manage-developers.html) a [!DNL Target].

2. En la consola [de desarrollador de](https://console.adobe.io/)Adobe, seleccione la organización de Experience Cloud para la que desea crear esta integración. (Tenga en cuenta que es probable que solo tenga acceso a una única organización Experience Cloud).

   ![configure-io-destinatario-create project2.png](assets/configure-io-target-createproject2.png)

3. Click **[!UICONTROL Create new project]**.

   ![configure-io-destinatario-create project3.png](assets/configure-io-target-createproject3.png)

4. Haga clic en **[!UICONTROL Añadir API]** para agregar una API de REST a su proyecto para acceder a los servicios y productos de Adobe.

   ![Añadir API](assets/configure-io-target-createproject4.png)

5. Seleccione **[!DNL Adobe Target]** como el servicio de Adobe con el que desea realizar la integración. Haga clic en el botón **[!UICONTROL Siguiente]** que aparece.

   ![configure-io-target-createproject5](assets/configure-io-target-createproject5.png)

6. Seleccione una opción para asociar claves públicas y privadas con la integración de cuenta de servicio que está creando para Destinatario. Para este tutorial, seleccione **[!UICONTROL Opción 1: Genere un par]** de claves y haga clic en **[!UICONTROL Generar par]**de claves.
   ![configure-io-target-createproject6](assets/configure-io-target-createproject6.png)

7. ¡Observe los resultados! Como se indica en las instrucciones, tenga en cuenta el archivo de configuración (`config`) descargado automáticamente, que contiene la clave privada. Haga clic en **[!UICONTROL Siguiente]**.
   ![configure-io-target-createproject7](assets/configure-io-target-createproject7.png)
8. En el sistema de archivos, compruebe la ubicación de `config`, que es el archivo de configuración comprimido creado en el paso anterior. De nuevo, este `config` archivo contiene su clave privada, que necesitará más adelante. La ubicación exacta dentro del sistema de archivos puede diferir de la que se muestra aquí.
   ![configure-io-target-createproject8](assets/configure-io-target-createproject8.png)
9. Vuelva a la consola de desarrollador de Adobe y seleccione los perfiles de [producto](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html) correspondientes a las propiedades en las que está utilizando [!DNL Recommendations]. (Si no utiliza propiedades, seleccione la opción Espacio de trabajo predeterminado). Haga clic en **[!UICONTROL Guardar API]**configurada.
   ![configure-io-target-createproject9](assets/configure-io-target-createproject9.png)

10. Haga clic en **[!UICONTROL Crear integración]**. Debe recibir un mensaje temporal que indique que la API se ha configurado correctamente.

11. Como último paso, cambie el nombre del proyecto a un nombre más significativo que el original `Project 1`. Para ello, vaya al proyecto utilizando la ruta de navegación como se muestra, haga clic en **[!UICONTROL Editar proyecto]** para acceder al modo **[!UICONTROL Editar proyecto] y cambie el nombre del proyecto.

![configure-io-target-createproject11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>En este tutorial, llamamos a nuestro proyecto &quot;Integración de Destinatario&quot;. Si tiene previsto usar su proyecto para más de Adobe Target, puede que desee asignarle un nombre acorde. Por ejemplo, puede elegir llamarlo &quot;API de Adobe&quot; o &quot;API de Experience Cloud&quot;, ya que se puede utilizar con otras soluciones en Adobe Experience Cloud.

## Exportar detalles del proyecto

Ahora que tiene un proyecto de Adobe que puede utilizar para acceder a él [!DNL Target], debe asegurarse de enviar los detalles de ese proyecto junto con las solicitudes de API de Adobe. Estos detalles son necesarios para interactuar con varias API de Adobe, incluidas varias [!DNL Target] API. Por ejemplo, los detalles de la integración incluyen la información de autorización y autenticación requerida por las API de [!DNL Target] administración. Por lo tanto, para utilizar las API con Postman, debe obtener esos detalles en Postman.

Existen muchas formas de especificar los detalles de su proyecto en Postman, pero en esta sección, aprovechamos algunas funciones y colecciones prediseñadas. En primer lugar (en esta sección), exportará los detalles de la integración en un entorno Postman. A continuación (en la sección siguiente), generará un token de acceso al portador para permitirle acceder a los recursos de Adobe necesarios.

>[!NOTE]
>
>Para ver las instrucciones de vídeo aplicables a cualquier solución de Experience Cloud, incluso [!DNL Target], consulte [Uso de Postman con API](https://docs.adobe.com/content/help/en/platform-learn/tutorials/apis/postman.html)de Experience Platform. Las siguientes secciones son relevantes para las [!DNL Target] API:
>
> 1. Exportar detalles de integración de E/S de Adobe a Postman
> 2. Generar un Token de acceso con Postman

>
> 
Estos pasos también se describen a continuación.

1. En la consola [para desarrolladores de](https://console.adobe.io/)Adobe, vaya a la vista de las credenciales de la cuenta **[!UICONTROL de servicio (JWT)]** del nuevo proyecto. Utilice la sección de navegación izquierda o la sección **[!UICONTROL Credenciales]** como se muestra.
   ![JWT1](assets/configure-io-target-jwt1.png)En los detalles **[!UICONTROL de]** Credenciales, tenga en cuenta que puede realizar vistas a su clave **pública**, ID **de cliente**y otra información relacionada con su cuenta de servicio.
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. Haga clic para navegar a la información sobre la API de **[!UICONTROL Adobe Target]** . Utilice la sección de navegación izquierda o la sección de productos y servicios **** conectados como se muestra.
   ![JWT2](assets/configure-io-target-jwt2.png)
3. Haga clic en **[!UICONTROL Descargar para Postman]** > Cuenta **[!UICONTROL de servicio (JWT)]** para crear un archivo JSON que capture la información de autenticación de un entorno Postman.
   ![JWT3](assets/configure-io-target-jwt3.png)Observe el archivo JSON en el sistema de archivos.
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. En Postman, haga clic en el icono de engranaje para administrar sus entornos y, a continuación, haga clic en **Importar** para importar el archivo JSON (entorno).
   ![JWT4](assets/configure-io-target-jwt4.png)
5. Elija el archivo y haga clic en **Abrir**.
   ![JWT5](assets/configure-io-target-jwt5.png)
6. En el modal **Administrar Entornos** de Postman, haga clic en el nombre del entorno recién importado para inspeccionarlo. (Es posible que el nombre de su entorno sea diferente del que se muestra aquí. Edite el nombre como desee. No es necesario que coincida necesariamente con el nombre del proyecto de Adobe).
   ![JWT6](assets/configure-io-target-jwt6.png)
7. Nota `CLIENT_SECRET` y `API_KEY` (junto con otras variables) tienen sus valores previamente rellenados, tomados de su integración como se define en Adobe Developer Console. (La variable Postman `CLIENT_SECRET` debe coincidir con la credencial de `CLIENT SECRET` Adobe tal como se muestra en la Consola de programadores, y `API_KEY` en Postman debe coincidir también `CLIENT ID` en la Consola de programadores). Por el contrario, la nota `PRIVATE_KEY`, `JWT_TOKEN`y `ACCESS_TOKEN` están en blanco. Inicios proporcionando el `PRIVATE_KEY` valor.
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**¡Sorpresa!**
   >
   >¡Prueba emergente! ¿Puedes recordar dónde está tu clave privada?
   >Así es, está en el archivo `config` descargado anteriormente desde la consola de desarrolladores de Adobe!

8. En el sistema de archivos, abra el `config` archivo y abra el archivo de `private` clave.
   ![JWT8](assets/configure-io-target-jwt8.png)
9. Seleccione y copie todo el contenido del archivo de `private` claves.
   ![JWT9](assets/configure-io-target-jwt9.png)
10. En Postman, pegue el valor de la clave privada en los campos VALOR **** INICIAL y VALOR **** ACTUAL.
   ![JWT10](assets/configure-io-target-jwt10.png)
11. Haga clic en **[!UICONTROL Actualizar]** y cierre el modal de Entornos.


## Generar el token de acceso portador

En esta sección, puede generar su token de acceso al portador, que es necesario para autenticar su interacción con las API de Adobe Target. Para generar su token de acceso portador, debe enviar los datos de integración (establecidos en las secciones anteriores) al Servicio Identity Management de [Adobe (IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md). Existen varias formas de hacerlo, pero en este tutorial hemos creado una solicitud de POST personalizada para la API de IMS. Sólo bromeo. En este tutorial, aprovechamos una colección Postman que contiene una llamada IMS prediseñada que hace que el proceso sea directo y fácil. Una vez importada la colección, puede volver a utilizarla cuando sea necesario para generar nuevos tokens no solo para Adobe Target, sino también para otras API de Adobe.

1. Vaya a las llamadas [de muestra de la API de servicio Identity Management de](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)Adobe.
   ![token1](assets/configure-io-target-generatetoken1.png)
2. Haga clic en la colección **de Postman de generación de Tokenes de acceso de E/S de**Adobe.
   ![token2](assets/configure-io-target-generatetoken2.png)
3. Obtenga el JSON sin procesar de esta colección haciendo clic en **Sin procesar**y copiando el JSON resultante en el portapapeles. (Como alternativa, puede guardar el JSON sin procesar como archivo .json).
   ![token3](assets/configure-io-target-generatetoken3.png)
4. En Postman, importe la colección pegando y enviando el JSON sin procesar desde el portapapeles. (Como alternativa, puede cargar el archivo .json que guardó). Haga clic en **Continuar**.
   ![token4](assets/configure-io-target-generatetoken4.png)
5. Seleccione el **[!UICONTROL IMS: JWT Generar + autenticación mediante solicitud de token]** de usuario en la colección Postman de generación de Tokenes de acceso de E/S de Adobe, asegúrese de que el entorno está seleccionado y haga clic en **Enviar** para generar el token.

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >Este token de acceso portador será válido durante 24 horas. Vuelva a enviar la solicitud siempre que necesite generar un nuevo token.

6. Vuelva a abrir el modal Administrar Entornos y seleccione el entorno.
   ![token6](assets/configure-io-target-jwt11.png)
7. Tenga en cuenta que los valores `ACCESS_TOKEN` y `JWT_TOKEN` ya están rellenados.
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>P: ¿Debo usar la colección Postman de generación de Tokenes de acceso de E/S de Adobe para generar el testigo web JSON (JWT) y el token de acceso al portador?
>
>A: ¡No! La colección Postman de generación de Tokenes de acceso de E/S de Adobe está disponible como una conveniencia para generar más fácilmente el token de acceso JWT y portador en Postman. También puede utilizar las funciones de la consola de desarrollador de Adobe para generar manualmente el token de acceso portador.

## Comprobación del token de acceso del soporte

En este ejercicio, utilizará su nuevo token de acceso de portador enviando una solicitud de API que recupere una lista de actividades de su [!DNL Target] cuenta. Una respuesta correcta indica que el proyecto de Adobe y la autenticación funcionan según lo esperado para utilizar la API.

1. Importe las API de administración de [Adobe Target en Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection). Siga todas las indicaciones hasta que se importe la colección en Postman.
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. Expanda la colección y anote la solicitud de actividades **[!UICONTROL de]** Lista.
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. Tenga en cuenta que las variables como `{{access_token}}` están inicialmente sin resolver. Esto se puede resolver de varias formas diferentes (por ejemplo, se puede definir una nueva variable de recopilación llamada `{{access_token}}`), pero en este tutorial, se cambiará la solicitud de API para aprovechar el entorno Postman que se estaba utilizando anteriormente. Esto permitirá que el entorno siga funcionando como una consolidación única y coherente de todas las variables comunes en las API de Adobe.
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. Escriba para reemplazar `{{access_token}}` por `{{ACCESS_TOKEN}}`.
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. Escriba para reemplazar `{{api_key}}` por `{{API_KEY}}`.
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. Escriba para reemplazar `{{tenant}}` por `{{TENANT_ID}}`. Aún no se reconoce la nota `{{TENANT_ID}}` .
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. Abra el modal Administrar Entornos y seleccione el entorno.
   ![JWT11](assets/configure-io-target-jwt11.png)
1. Escriba para agregar una nueva variable `{{TENANT_ID}}` de entorno. Copie y pegue el valor de ID de inquilino en los campos VALOR **** INICIAL y VALOR **** ACTUAL para la nueva variable de `TENANT_ID` entorno.
   ![testtoken5](assets/configure-io-target-testtoken5.png)
   >[!NOTE]
   >
   >El Id. del inquilino es diferente del [!DNL Target] suyo `clientcode`. El ID del inquilino existe en la dirección URL cuando se inicia sesión en [!DNL Target]. Para obtener su ID de inquilino, inicie sesión en la [!DNL Adobe Experience Cloud], abra [!DNL Target]y haga clic en la [!DNL Target] tarjeta. Utilice el valor de ID de inquilino como se indica en el subdominio de URL.
   >
   >Por ejemplo, si la dirección URL al iniciar sesión en Adobe Target es
   ><https://mycompany.experiencecloud.adobe.com/...>
   >su ID de inquilino es &quot;mi empresa&quot;.

1. Envíe su solicitud después de asegurarse de que ha seleccionado el entorno correcto. Debe recibir una respuesta que contenga su lista de actividades.
   ![testtoken6](assets/configure-io-target-testtoken6.png)

¡Felicitaciones! Ahora que ha verificado la autenticación de Adobe, puede utilizarla para interactuar con las API de Adobe Target (así como con otras API de Adobe). Por ejemplo, puede [utilizar las API](https://docs.adobe.com/content/help/en/target-learn/recommendations-api-tutorial/recs-api-overview.html) de Recommendations para crear o administrar recomendaciones.
