---
title: Configuración de la autenticación para las API de Adobe Target
description: Este tutorial guía a los desarrolladores por los pasos necesarios para generar los tokens de autenticación necesarios para interactuar correctamente con las API de Adobe Target. Siga estos pasos para utilizar la consola de Adobe Developer para generar y probar el token de acceso al portador, que es necesario para utilizar las API de Target.
role: Developer, Admin, Architect
level: Intermediate
topic: Personalization, Administration, Integrations, Development
feature: APIs/SDKs, Administration & Configuration
doc-type: tutorial
kt: null
author: Judy Kim
exl-id: 8a1e93e4-67b2-4942-a8da-fc0f2cbb2df2
source-git-commit: 0ecfde208b3e201de135512d5aab70192fc2b826
workflow-type: tm+mt
source-wordcount: '1882'
ht-degree: 3%

---

# Configuración de la autenticación para las API de Adobe Target

Las API de administración de Adobe Target, incluidas [!DNL Recommendations] Las API de administrador están seguras mediante autenticación para garantizar que solo los usuarios autorizados las utilicen para acceder a Adobe Target. Utilice la variable [Consola de Adobe Developer](https://console.adobe.io/) para administrar esta autenticación en todas las soluciones de Adobe Experience Cloud, incluidas [!DNL Target].

Esta lección explica los pasos preliminares necesarios para generar los tokens de autenticación necesarios para interactuar correctamente con las API de Adobe Target. En las secciones que siguen, debe hacer lo siguiente:

1. Cree un proyecto (anteriormente denominado integración) en la consola de Adobe Developer.
2. Exportar detalles del proyecto a Postman.
3. Genere un token de acceso al portador.
4. Compruebe el token de acceso del portador.

## Requisitos previos

| Recurso | Detalles |
| --- | --- |
| Postman | Para completar estos pasos correctamente, obtenga la variable [aplicación Postman](https://www.postman.com/downloads/) para su sistema operativo. Postman básico es gratuito con la creación de cuentas. Aunque no es necesario para utilizar las API de Adobe Target en general, Postman facilita los flujos de trabajo de las API y Adobe Target proporciona varias colecciones de Postman para ayudar a ejecutar sus API y aprender a funcionar. El resto de este tutorial asume el conocimiento práctico de Postman. Para obtener ayuda, consulte la [Documentación de Postman](https://learning.getpostman.com/). |
| Referencias | Durante el resto de este tutorial se asume la familiaridad con los siguientes recursos:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Documentación del Adobe I/O de Target](https://developers.adobetarget.com/api/#introduction)</li><li>[Documentación de la API de Recommendations](https://developers.adobetarget.com/api/recommendations/)</li></ul> |

## Creación de un proyecto de Adobe I/O

En esta sección, accederá a la consola de Adobe Developer y creará un proyecto para [!DNL Adobe Target]. Para obtener más información, consulte [documentación sobre proyectos](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects.md).

<!--1. Generate your private key and public certificate, per the [documentation on authentication](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWTCertificate.md). //<!--as described in **Step 1** of [How to set up Adobe IO: Authentication - Step by Step](https://helpx.adobe.com/marketing-cloud-core/kb/adobe-io-authentication-step-by-step.html). After completing Step 1, return to this tutorial and resume with Step 2, below. // The outcome of this step should be the creation of a `private.key` file and a `certificate_pub.crt` file. Return to this tutorial once you have generated these two files.-->

1. En el [Adobe Admin Console](https://adminconsole.adobe.com/), asegúrese de que su cuenta de usuario de Adobe haya obtenido ambos [Administrador de productos](https://helpx.adobe.com/enterprise/using/admin-roles.html) y [Desarrollador](https://helpx.adobe.com/enterprise/using/manage-developers.html) acceso a nivel [!DNL Target].

2. En el [Consola de Adobe Developer](https://console.adobe.io/), seleccione la organización del Experience Cloud para la que desea crear esta integración. (Tenga en cuenta que es probable que solo tenga acceso a una única organización de Experience Cloud).

   ![configure-io-target-create2.png](assets/configure-io-target-createproject2.png)

3. Haga clic en **[!UICONTROL Crear nuevo proyecto]**.

   ![configure-io-target-create3.png](assets/configure-io-target-createproject3.png)

4. Haga clic en **[!UICONTROL Añadir API]** para agregar una API de REST al proyecto para acceder a los servicios y productos de Adobe.

   ![Añadir API](assets/configure-io-target-createproject4.png)

5. Select **[!DNL Adobe Target]** como el servicio de Adobe con el que desea integrarse. Haga clic en el **[!UICONTROL Siguiente]** que aparece.

   ![configure-io-target-create5](assets/configure-io-target-createproject5.png)

6. Seleccione una opción para asociar claves públicas y privadas con la integración de cuenta de servicio que está creando para Target. Para este tutorial, seleccione **[!UICONTROL Opción 1: Generación de un par de claves]** y haga clic en **[!UICONTROL Generar par de teclas]**.
   ![configure-io-target-create6](assets/configure-io-target-createproject6.png)

7. ¡Observe los resultados! Como se indica, tenga en cuenta el archivo de configuración descargado automáticamente (`config`), que contiene su clave privada. Haga clic en **[!UICONTROL Siguiente]**.
   ![configure-io-target-create7](assets/configure-io-target-createproject7.png)
8. En el sistema de archivos, compruebe la ubicación de `config`, que es el archivo de configuración comprimido creado en el paso anterior. Una vez más, esto `config` contiene su clave privada, que necesitará más adelante. La ubicación exacta dentro del sistema de archivos puede diferir de la que se muestra aquí.
   ![configure-io-target-create8](assets/configure-io-target-createproject8.png)
9. En la consola de Adobe Developer, seleccione la opción [perfiles de producto](https://helpx.adobe.com/enterprise/using/manage-products-and-profiles.html) correspondiente a las propiedades en las que se utiliza [!DNL Recommendations]. (Si no utiliza propiedades, seleccione la opción Espacio de trabajo predeterminado ). Haga clic en **[!UICONTROL Guardar la API configurada]**.
   ![configure-io-target-create9](assets/configure-io-target-createproject9.png)

10. Haga clic en **[!UICONTROL Crear integración]**. Debe recibir un mensaje temporal que indique que la API se ha configurado correctamente.

11. Por último, cambie el nombre del proyecto por un nombre más significativo que el original `Project 1`. Para ello, vaya al proyecto utilizando la ruta de navegación como se muestra, haga clic en **[!UICONTROL Editar proyecto]** para acceder a **[!UICONTROL Editar proyecto] y cambie el nombre del proyecto.

![configure-io-target-create11](assets/configure-io-target-createproject11.png)

>[!NOTE]
> 
>En este tutorial, denominamos a nuestro proyecto &quot;Integración de Target&quot;. Si tiene previsto usar el proyecto para algo más que Adobe Target, es posible que desee asignarle un nombre acorde. Por ejemplo, puede elegir llamarlo &quot;API de Adobe&quot; o &quot;API de Experience Cloud&quot;, ya que se puede utilizar con otras soluciones de Adobe Experience Cloud.

## Exportar detalles del proyecto

Ahora que tiene un proyecto de Adobe que puede utilizar para acceder a [!DNL Target], debe asegurarse de enviar los detalles de ese proyecto junto con las solicitudes de API de Adobe. Estos detalles son necesarios para interactuar con varias API de Adobe, incluidas varias [!DNL Target] API. Por ejemplo, los detalles de la integración incluyen la información de autorización y autenticación requerida por el [!DNL Target] API de administrador. Por lo tanto, para utilizar las API con Postman, debe obtener esos detalles en Postman.

Existen muchas formas de especificar los detalles del proyecto en Postman, pero en esta sección aprovechamos algunas funciones y colecciones prediseñadas. En primer lugar (en esta sección), exportará los detalles de su integración a un entorno de Postman. A continuación (en la sección siguiente), generará un token de acceso de portador para concederle acceso a los recursos de Adobe necesarios.

>[!NOTE]
>
>Para instrucciones de vídeo aplicables a cualquier solución de Experience Cloud, incluyendo [!DNL Target], consulte [Uso de Postman con API de Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=en). Las secciones siguientes son relevantes para la variable [!DNL Target] API:
>
> 1. Exportar detalles de integración de Adobe I/O a Postman
> 2. Generar un token de acceso con Postman

>
> Estos pasos también se proporcionan a continuación.

1. Todavía en el [Consola de Adobe Developer](https://console.adobe.io/), desplácese para ver el nuevo proyecto **[!UICONTROL Cuenta de servicio (JWT)]** credenciales. Utilice el menú de navegación izquierdo o el **[!UICONTROL Credenciales]** como se muestra.
   ![JWT1](assets/configure-io-target-jwt1.png)
En **[!UICONTROL Detalles de la credencial]**, tenga en cuenta que puede ver su **Clave(s) pública(s)**, **ID de cliente**y otra información relacionada con su cuenta de servicio.
   ![JWT1a](assets/configure-io-target-jwt1a.png)
2. Haga clic para navegar a la información sobre la variable **[!UICONTROL Adobe Target]** API. Utilice el menú de navegación izquierdo o el **[!UICONTROL Productos y servicios conectados]** como se muestra.
   ![JWT2](assets/configure-io-target-jwt2.png)
3. Haga clic en **[!UICONTROL Descargar para Postman]** > **[!UICONTROL Cuenta de servicio (JWT)]** para crear un archivo JSON que capture la información de autenticación de un entorno de Postman.
   ![JWT3](assets/configure-io-target-jwt3.png)
Tenga en cuenta el archivo JSON en su sistema de archivos.
   ![JWT3a](assets/configure-io-target-jwt3a.png)
4. En Postman, haga clic en el icono de engranaje para administrar los entornos y, a continuación, haga clic en **Importar** para importar el archivo JSON (entorno).
   ![JWT4](assets/configure-io-target-jwt4.png)
5. Elija el archivo y haga clic en **Apertura**.
   ![JWT5](assets/configure-io-target-jwt5.png)
6. En Postman **Administrar entornos** modal, haga clic en el nombre del entorno recién importado para inspeccionarlo. (El nombre del entorno puede ser diferente del que se muestra aquí. Edite el nombre como desee. No es necesario que coincida necesariamente con el nombre del proyecto de Adobe).
   ![JWT6](assets/configure-io-target-jwt6.png)
7. Nota `CLIENT_SECRET` y `API_KEY` (junto con otras variables) tienen sus valores rellenados previamente, tomados de la integración tal como se define en la consola de Adobe Developer. (El Postman `CLIENT_SECRET` debe coincidir con la variable `CLIENT SECRET` Credenciales de Adobe tal como se muestran en Developer Console, y `API_KEY` en Postman debe coincidir de la misma manera `CLIENT ID` en Developer Console). Por el contrario, observe `PRIVATE_KEY`, `JWT_TOKEN`y `ACCESS_TOKEN` están en blanco. Empecemos por proporcionar la variable `PRIVATE_KEY` valor.
   ![JWT7](assets/configure-io-target-jwt7.png)

   >[!NOTE]
   >
   >**¡Sorpresa!**
   >
   >¡Preguntas más frecuentes! ¿Recuerdas dónde está tu llave privada?
   >Está bien, está en el `config` archivo descargado anteriormente desde la consola de Adobe Developer!

8. En el sistema de archivos, abra el `config` y abra el `private` archivo de clave.
   ![JWT8](assets/configure-io-target-jwt8.png)
9. Seleccione y copie todo el contenido del `private` archivo de clave.
   ![JWT9](assets/configure-io-target-jwt9.png)
10. En Postman, pegue el valor de la clave privada en la **VALOR INICIAL** y **VALOR ACTUAL** campos.
   ![JWT10](assets/configure-io-target-jwt10.png)
11. Haga clic en **[!UICONTROL Actualizar]** y cierre el modal Entornos .


## Generar el token de acceso del portador

En esta sección, se genera el token de acceso de portador, que es necesario para autenticar la interacción con las API de Adobe Target. Para generar el token de acceso al portador, debe enviar los detalles de integración (establecidos en las secciones anteriores) al [Servicio Identity Management de Adobe (IMS)](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/AuthenticationGuide.md). Existen varias formas de hacerlo, pero en este tutorial tenemos que crear una solicitud de POST personalizada para la API de IMS. Estoy bromeando. En este tutorial, aprovechamos una colección de Postman que contiene una llamada IMS prediseñada que hace que el proceso sea directo y fácil. Una vez importada la colección, puede volver a utilizarla cuando sea necesario para generar nuevos tokens no solo para Adobe Target, sino también para otras API de Adobe.

1. Vaya a la [Ejemplo de llamadas de API del servicio Identity Management de Adobe](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims).
   ![token1](assets/configure-io-target-generatetoken1.png)
2. Haga clic en el **Colección Postman de generación de tokens de acceso a Adobes I/O**.
   ![token2](assets/configure-io-target-generatetoken2.png)
3. Obtenga el JSON sin procesar para esta colección haciendo clic en **Sin procesar**y, a continuación, copiando el JSON resultante en el portapapeles. (Como alternativa, puede guardar el JSON sin procesar como archivo .json).
   ![token3](assets/configure-io-target-generatetoken3.png)
4. En Postman, importe la colección pegando y enviando el JSON sin procesar desde el portapapeles. (Como alternativa, puede cargar el archivo .json que guardó). Haga clic en **Continuar**.
   ![token4](assets/configure-io-target-generatetoken4.png)
5. Seleccione el **[!UICONTROL IMS: Generación + autenticación de JWT mediante token de usuario]** solicite en la colección Postman de generación de tokens de acceso a Adobe I/O, asegúrese de que el entorno está seleccionado y haga clic en **Enviar** para generar el token.

   ![token5](assets/configure-io-target-generatetoken5.png)

   >[!NOTE]
   >
   >Este token de acceso al portador será válido durante 24 horas. Vuelva a enviar la solicitud siempre que necesite generar un token nuevo.

6. Vuelva a abrir el modal Administrar entornos y seleccione el entorno.
   ![token6](assets/configure-io-target-jwt11.png)
7. Tenga en cuenta que `ACCESS_TOKEN` y `JWT_TOKEN` los valores de ahora se rellenan.
   ![token7](assets/configure-io-target-generatetoken7.png)

>[!NOTE]
>
>P: ¿Tengo que usar la colección Postman de generación de tokens de acceso a Adobe I/O para generar el token web JSON (JWT) y el token de acceso al portador?
>
>A: ¡No! La colección Postman de generación de tokens de acceso a Adobe I/O está disponible como una conveniencia para generar más fácilmente el JWT y el token de acceso al portador en Postman. Como alternativa, puede utilizar las funcionalidades de la consola de Adobe Developer para generar manualmente el token de acceso al portador.

## Comprobación del token de acceso del portador

En este ejercicio, utilizará el nuevo token de acceso de portador enviando una solicitud de API que recupera una lista de actividades de su [!DNL Target] cuenta. Una respuesta correcta indica que el proyecto de Adobe y la autenticación funcionan según lo esperado para utilizar la API.

1. Importe el [Recopilación de API de administración de Adobe Target en Postman](https://developers.adobetarget.com/api/#admin-postman-collection). Siga todas las indicaciones hasta que la colección se importe en Postman.
   ![testtoken1](assets/configure-io-target-testtoken0.png)
1. Expanda la colección y anote la **[!UICONTROL Enumerar actividades]** solicitud.
   ![testtoken1](assets/configure-io-target-testtoken1.png)
1. Tenga en cuenta que las variables como `{{access_token}}` no se han resuelto inicialmente. Esto se puede resolver de varias maneras diferentes; por ejemplo, puede definir una nueva variable de colección llamada `{{access_token}}`—pero en este tutorial, cambiará la solicitud de API para aprovechar el entorno de Postman que estaba utilizando anteriormente. Esto permitirá que el entorno siga funcionando como una consolidación única y coherente de todas las variables comunes entre las API de Adobe.
   ![testtoken2](assets/configure-io-target-testtoken2.png)
1. Tipo que se va a reemplazar `{{access_token}}` con `{{ACCESS_TOKEN}}`.
   ![testtoken3](assets/configure-io-target-testtoken3.png)
1. Tipo que se va a reemplazar `{{api_key}}` con `{{API_KEY}}`.
   ![testtoken4](assets/configure-io-target-testtoken4.png)
1. Tipo que se va a reemplazar `{{tenant}}` con `{{TENANT_ID}}`. Nota `{{TENANT_ID}}` aún no se reconoce.
   ![testtoken4](assets/configure-io-target-testtoken4a.png)
1. Abra el modal Manage Environments y seleccione su entorno.
   ![JWT11](assets/configure-io-target-jwt11.png)
1. Escriba para agregar un nuevo `{{TENANT_ID}}` variable de entorno. Copie y pegue su valor de ID de inquilino en la variable **VALOR INICIAL** y **VALOR ACTUAL** campos para las nuevas `TENANT_ID` variable de entorno.

   ![testtoken5](assets/configure-io-target-testtoken5.png)

   >[!NOTE]
   >
   >El ID del inquilino es diferente del de [!DNL Target] `clientcode`. El ID del inquilino existe en la dirección URL cuando ha iniciado sesión en [!DNL Target]. Para obtener su ID de inquilino, inicie sesión en la [!DNL Adobe Experience Cloud], abra [!DNL Target]y haga clic en el botón [!DNL Target] tarjeta. Utilice el valor de ID de inquilino como se indica en el subdominio de URL.
   >
   >Por ejemplo, si la dirección URL cuando se inicia sesión en Adobe Target es
   >
   >`<https://mycompany.experiencecloud.adobe.com/...>`
   >
   >su ID de inquilino es &quot;mycompany&quot;.

1. Envíe la solicitud después de asegurarse de que ha seleccionado el entorno correcto. Debe recibir una respuesta que contenga su lista de actividades.
   ![testtoken6](assets/configure-io-target-testtoken6.png)

¡Felicidades! Ahora que ha comprobado la autenticación de su Adobe, puede utilizarla para interactuar con las API de Adobe Target (así como con otras API de Adobe). Por ejemplo, puede [Uso de las API de Recommendations](https://developer.adobe.com/target/before-administer/recs-api/){target=_blank} para crear o administrar recomendaciones.
