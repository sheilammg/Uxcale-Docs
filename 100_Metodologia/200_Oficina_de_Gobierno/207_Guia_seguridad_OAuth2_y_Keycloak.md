|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|14/03/2023|Axpe|Versión inicial|

# **Guía de Seguridad OAuth2 y Keycloak**
## Índice
- [Introducción](#introducción)
- [Glosario de términos generales](#glosario-de-términos-generales)
- [Glosario de términos Keycloak](#glosario-de-términos-keycloak)
- [Capa de transporte HTTPS](#capa-de-transporte-https)

- [Ciclo de vida OAuth](#ciclo-de-vida-oauth)
- [OpenID Connect y OAuth2](#openid-connect-y-oauth2)
- [SAML](#saml)
    - [Comparación SAML con OAuth2](#comparación-saml-con-oauth2)
- [Creación y uso de scopes](#creación-y-uso-de-scopes)
- [Sintaxis de las variables empleadas en OAuth2](#sintaxis-de-las-variables-empleadas-en-oauth2)
- [Acceso a APIs mediante OAuth2](#acceso-a-apis-mediante-oauth2)
    - [Qué Grant Type emplear](#qué-grant-type-emplear)
    - [Authorization code](#authorization-code)
    - [Implicit](#implicit)
    - [Password](#password)
    - [Client credentials](#client-credentials)
    - [Device code](#device-code)
    - [CIBA](#ciba)
- [Respuesta del token](#respuesta-del-token)
- [Tiempo de caducidad máximo de un token](#tiempo-de-caducidad-máximo-de-un-token)
- [Utilización del token](#utilización-del-token)
- [Refresco del token](#refresco-del-token)
- [Revocado del token](#revocado-del-token)


<div style="page-break-after: always;"></div>

# Introducción

El presente documento tiene como objetivo detallar toda la guía de referencia de la seguridad OAuth que se empleará en la exposición de las APIs dentro de la compañia **Axpe Consulting**. El objetivo principal de dicho documento es homogeneizar y estandarizar la seguridad para:

- Simplificar el consumo tanto por equipos internos de la compañía como proveedores externos.
- Facilitar la toma de decisiones en torno a la seguridad de las APIs.
- Acelerar los proyectos de los diferentes equipos.

Keycloak es un producto de software de código abierto que permite el inicio de sesión único (IdP) con Identity Management y Access Management para aplicaciones y servicios modernos. Este software está escrito en Java y es compatible de forma predeterminada con los protocolos de federación de identidad SAML v2 y OpenID Connect (OIDC) / OAuth2. Está bajo licencia de Apache y es compatible con Red Hat.

Sus principales características son:
-	Inicio y cierre de sesión único: Los usuarios se autentican con Keycloak en lugar de aplicaciones individuales. Esto significa que sus aplicaciones no tienen formularios de inicio de sesión, autenticación de usuarios y almacenamiento de usuarios. Una vez que han iniciado sesión en Keycloak, los usuarios no tienen que volver a iniciar sesión para acceder a una aplicación diferente. Esto también se aplica al cierre de sesión. Keycloak proporciona un cierre de sesión único.
-	Consola de administración.
-	Consola de administración de cuentas.
-	Protocolos estándar: Keycloak se basa en protocolos estándar y brinda soporte para OpenID Connect, OAuth 2.0 y SAML.
-	Servicios de autorización: Esto le permite administrar los permisos para todos sus servicios desde la consola de administración de Keycloak y le da el poder de definir exactamente las políticas que necesita.


<div style="page-break-after: always;"></div>

# Glosario de términos generales

**OAuth**

El marco de trabajo de autorización de OAuth 2.0 permite que una aplicación de terceros obtenga acceso limitado a un servicio HTTP, ya sea en nombre de un propietario de recurso mediante la organización de una interacción de aprobación entre el propietario del recurso y el servicio HTTP, o permitir que la aplicación de terceros obtenga acceso en su nombre. Todo ello se realizará según lo desarrollado en la RFC 6749.

**Token de acceso**

String largo de caracteres que sirve como una credencial que se usa para acceder a los recursos protegidos. Los tokens de recursos (también llamados tokens del portador) se pasan en los encabezados de autorización.

**Aplicación cliente**

Elemento que representa a un cliente/consumidor de las APIs expuestas.

**Nombre del cliente**

Nombre por el cual se identifica a un cliente/consumidor.

**Scope**

Cadena de texto que se emplea para limitar el acceso de las aplicaciones cliente a los recursos de las APIs expuestas. Estarán definidas con la ayuda de Gobierno API.

**Grant type**

Son los diferentes tipos de concesión de token de acceso para un servicio o una API.

<div style="page-break-after: always;"></div>

# Glosario de términos Keycloak

**Users**

Los usuarios son entidades que pueden iniciar sesión en su sistema. Pueden tener atributos asociados con ellos mismos, como correo electrónico, nombre de usuario, dirección, número de teléfono y cumpleaños. Se les puede asignar la pertenencia a un grupo y se les pueden asignar roles específicos.

**Authentication**

El proceso de identificación y validación de un usuario.

**Authorization**

El proceso de otorgar acceso a un usuario.

**Credentials**

Las credenciales son piezas de datos que Keycloak utiliza para verificar la identidad de un usuario. Algunos ejemplos son contraseñas, contraseñas de un solo uso, certificados digitales o incluso huellas dactilares.

**Roles**

Los roles identifican un tipo o categoría de usuario. Admin, user, managery employee son todos los roles típicos que pueden existir en una organización. Las aplicaciones a menudo asignan acceso y permisos a roles específicos en lugar de usuarios individuales, ya que tratar con los usuarios puede ser demasiado detallado y difícil de administrar.

**User role mapping**

Una asignación de funciones de usuario define una asignación entre una función y un usuario. Un usuario puede estar asociado con cero o más roles. Esta información de asignación de roles se puede encapsular en tokens y aserciones para que las aplicaciones puedan decidir los permisos de acceso en varios recursos que administran.

**Composite roles**

Un rol compuesto es un rol que se puede asociar con otros roles. Por ejemplo, un superuserrol compuesto podría asociarse con los roles sales-adminy.order-entry-admin. Si un usuario está asignado al superuserrol, también hereda los roles sales-adminy.order-entry-admin

**Groups**

Los grupos administran grupos de usuarios. Los atributos se pueden definir para un grupo. También puede asignar roles a un grupo. Los usuarios que se convierten en miembros de un grupo heredan los atributos y asignaciones de roles que define el grupo.

**Realms**

Un realm administra un conjunto de usuarios, credenciales, roles y grupos. Un usuario pertenece e inicia sesión en un reino. Los reinos están aislados unos de otros y solo pueden administrar y autenticar a los usuarios que controlan.

**Clients**

Los clientes son entidades que pueden solicitar Keycloak para autenticar a un usuario. La mayoría de las veces, los clientes son aplicaciones y servicios que desean usar Keycloak para protegerse y proporcionar una solución de inicio de sesión único. Los clientes también pueden ser entidades que solo desean solicitar información de identidad o un token de acceso para poder invocar de manera segura otros servicios en la red que están protegidos por Keycloak.

**Consent**

El consentimiento es cuando usted, como administrador, desea que un usuario otorgue permiso a un cliente antes de que ese cliente pueda participar en el proceso de autenticación. Después de que un usuario proporcione sus credenciales, Keycloak mostrará una pantalla que identifica al cliente que solicita un inicio de sesión y qué información de identidad se solicita del usuario. El usuario puede decidir si otorga o no la solicitud.

**Client scopes**

Cuando se registra un cliente, debe definir mapeadores de protocolos y asignaciones de ámbito de función para ese cliente. Suele ser útil almacenar un client-scope para facilitar la creación de nuevos clientes compartiendo algunas configuraciones comunes. Esto también es útil para solicitar que algunas notificaciones o roles se basen condicionalmente en el valor del scope. Keycloak proporciona el concepto de un alcance de cliente para esto.

**Client role**

Los clientes pueden definir roles que son específicos para ellos. Básicamente, se trata de un espacio de nombres de roles dedicado al cliente.

**Identity token**

Un token que proporciona información de identidad sobre el usuario. Parte de la especificación OpenID Connect.

**Access token**

Un token que se puede proporcionar como parte de una solicitud HTTP que otorga acceso al servicio que se invoca. Esto es parte de la especificación OpenID Connect y OAuth 2.0.

**Assertion**

Información sobre un usuario. Esto suele pertenecer a un blob XML que se incluye en una respuesta de autenticación SAML que proporcionó metadatos de identidad sobre un usuario autenticado.

**Service account**

Cada cliente tiene una cuenta de servicio integrada que le permite obtener un token de acceso.

**Direct grant**

Una forma de que un cliente obtenga un token de acceso en nombre de un usuario a través de una invocación REST.

**Protocol mappers**

Para cada cliente, puede personalizar qué claims y assertions se almacenan en el token OIDC o en la afirmación SAML. Esto se hace por cliente creando y configurando protocol mappers.

**Session**

Cuando un usuario inicia sesión, se crea una sesión para administrar la sesión de inicio de sesión. Una sesión contiene información como cuándo inició sesión el usuario y qué aplicaciones han participado en el inicio de sesión único durante esa sesión. Tanto los administradores como los usuarios pueden ver la información de la sesión.

**User federation provider**

Keycloak puede almacenar y administrar usuarios. A menudo, las empresas ya cuentan con servicios LDAP o Active Directory que almacenan información de usuarios y credenciales. Puede señalar Keycloak para validar las credenciales de esas tiendas externas y obtener información de identidad.

**Identity provider**

Un proveedor de identidad (IDP) es un servicio que puede autenticar a un usuario. Keycloak es un desplazado interno.

**Identity provider federation**

Keycloak se puede configurar para delegar la autenticación a uno o más IDP. El inicio de sesión social a través de Facebook o Google+ es un ejemplo de federación de proveedores de identidad. También puede conectar Keycloak para delegar la autenticación a cualquier otro IDP de OpenID Connect o SAML 2.0.

**Identity provider mappers**

Al realizar la IDP Federation, puede asignar tokens y aserciones entrantes a atributos de usuario y sesión. Esto lo ayuda a propagar la información de identidad del IDP externo a su cliente que solicita autenticación.

**Required actions**

Las acciones requeridas son acciones que un usuario debe realizar durante el proceso de autenticación. Un usuario no podrá completar el proceso de autenticación hasta que se completen estas acciones. Por ejemplo, un administrador puede programar que los usuarios restablezcan sus contraseñas cada mes. Se update passwordestablecería una acción requerida para todos estos usuarios.

**Authentication flows**

Los flujos de autenticación son flujos de trabajo que un usuario debe realizar cuando interactúa con ciertos aspectos del sistema. Un flujo de inicio de sesión puede definir qué tipos de credenciales se requieren. Un flujo de registro define qué información de perfil debe ingresar un usuario y si se debe usar algo como reCAPTCHA para filtrar los bots. El flujo de restablecimiento de credenciales define qué acciones debe realizar un usuario antes de poder restablecer su contraseña.

**Events**

Los eventos son flujos de auditoría que los administradores pueden ver y conectar.

**Themes**

Cada pantalla proporcionada por Keycloak está respaldada por un tema. Los temas definen plantillas HTML y hojas de estilo que puede anular según sea necesario.





<div style="page-break-after: always;"></div>

# Capa de transporte HTTPS

Todos los servicios son expuestos por https, no siendo posible emplear un canal no seguro para comunicarse con el API Gateway. Este comportamiento es global para todo el sistema, siendo imposible habilitar comunicaciones no seguras para algún servicio, o conjunto de estos.

Esto se verá ampliado en la Guía de diseño de las URL.

<div style="page-break-after: always;"></div>

# Ciclo de vida OAuth

En este apartado se describirán las operaciones que se podrán realizar en el Service Manager para gestionar correctamente el ciclo de vida de las credenciales oauth para un consumidor de APIs de AXPE.
-	**Alta de credenciales OAuth**: Antes de que una aplicación o un usuario externo a AXPE pueda consumir recursos de nuestras APIs expuestas en el Gateway. Se deberá solicitar en el Service Manager el alta de unas credenciales de cliente con los scopes adecuados que autoricen a consumir los recursos necesarios.
-	**Modificación de credenciales OAuth**: En el momento en que un consumidor de APIs de AXPE que ya cuenta con credenciales, necesite modificar su acceso a recursos se deberá realizar una petición de modificación al Service Manager donde se indiquen los scopes a modificar/eliminar. 
-	**Baja de credenciales OAuth**: Cuando un consumidor finalice su relación con AXPE, se debe realizar una petición de baja en el Service Manager para dar de baja las credenciales de dicho consumidor.

<div style="page-break-after: always;"></div>

# OpenID Connect y OAuth2

A continuación, se realiza la comparación entre OpenID Connect (OIDC) y OAuth 2.0.
-	El protocolo OpenID Connect (OIDC) se basa en el protocolo OAuth 2.0 y ayuda a autenticar a los usuarios y transmitir información sobre ellos. También es más obstinado que el simple OAuth 2.0, por ejemplo, en sus definiciones de alcance.
-	El protocolo OAuth 2.0 controla la autorización para acceder a un recurso protegido, como su aplicación web, aplicación nativa o servicio API.

OpenID Connect (OIDC) es un protocolo de autenticación que es una extensión de OAuth 2.0. Si bien OAuth 2.0 es solo un marco para crear protocolos de autorización y está principalmente incompleto, OIDC es un protocolo completo de autenticación y autorización. OIDC también hace un uso intensivo del conjunto de estándares Json Web Token (JWT). Estos estándares definen un formato JSON de token de identidad y formas de firmar y cifrar digitalmente esos datos de una manera compacta y compatible con la web.

El protocolo OAuth 2.0 proporciona seguridad API a través de tokens de acceso con alcance. OAuth 2.0 le permite delegar la autorización, mientras que OIDC le permite recuperar y almacenar información de autenticación sobre sus usuarios finales. OIDC amplía OAuth 2.0 al proporcionar autenticación de usuario y funcionalidad de inicio de sesión único (SSO).

<div style="page-break-after: always;"></div>

# SAML

SAML (Security Assertion Markup Language) es un estándar abierto basado en XML para transferir datos de identidad entre dos partes: un proveedor de identidad (IdP) y un proveedor de servicios (SP).
-	Proveedor de identidad: realiza la autenticación y pasa la identidad y el nivel de autorización del usuario al proveedor de servicios.
-	Proveedor de servicios: confía en el proveedor de identidad y autoriza al usuario dado a acceder al recurso solicitado.

Algunas de sus principales ventajas son las siguientes:

-	Gran Experiencia de usuario: los usuarios solo necesitan iniciar sesión una vez para acceder a múltiples proveedores de servicios, permitiendo un proceso de autenticación más rápido.
-	Alta seguridad: SAML proporciona un único punto de autenticación, que ocurre en un proveedor de identidad seguro. Luego, SAML transfiere la información de identidad a los proveedores de servicios. Esta forma de autenticación garantiza que las credenciales solo se envíen directamente al proveedor de identidad.

## Comparación SAML con OAuth2
SAML admite el inicio de sesión único (simple-sign-on, SSO) y, al mismo tiempo, admite la autorización mediante la ruta de consulta de atributos. OAuth se centra en la autorización, incluso si con frecuencia se lo obliga a desempeñar una función de autenticación, por ejemplo, cuando se utiliza el inicio de sesión social como "iniciar sesión con una cuenta de Facebook". Independientemente, OAuth2 no admite SSO.

Por otro lado, SAML define un formato de token, su cifrado es complicado y el tamaño de los mensajes intercambiados es significativo. Por el contrario, OAuth2 no usa ningún cifrado de mensajes (se basa en HTTPS) y no define un formato de token.

El atractivo de OAuth2 radica en la facilidad de uso y la flexibilidad: se puede usar en dispositivos móviles, dispositivos inteligentes (por ejemplo, televisores inteligentes), aplicaciones web, aplicaciones de una sola página, etc. Muchas bibliotecas están disponibles para facilitar el proceso de integración con diferentes tipos de clientes y proveedores de servicios. SAML, por el contrario, no se diseñó teniendo en cuenta estas aplicaciones modernas, lo que dificulta su uso en estos sistemas. Se usa comúnmente con aplicaciones web tradicionales.

<div style="page-break-after: always;"></div>

# Creación y uso de scopes

Los scopes son cadenas de texto que se emplean para limitar el acceso de las aplicaciones cliente a los recursos de las APIs expuestas. Estarán definidas con la ayuda de Gobierno API. La descripción del recurso al que se al que solicita acceso y la acción deseada viene definida por el scope. 

Los scopes definidos en aAXPE siguen la siguiente estructura:

	{id_api}.{id_recurso}.{id_operacion}

| **Atributo**       | **Obligatorio/Opcional**  | **Descripción**                             |
|--------------------|---------------------------|---------------------------------------------|
| **{id_api}**       | Obligatorio               | Identificador de la API                     |
| **{id_recurso}**   | Opcional, puede valer ALL | Identificador del recurso                   |
| **{id_operacion}** | Opcional, puede valer ALL | Identificador (método HTTP) de la operación |

Además, se presentan diferentes opciones:

- **scope: {id_api}.{id_recurso}.{id_operacion}**

Permite ejecutar la operación id_operacion sobre el recurso id_recurso de la API id_api.

- **scope: {id_api}.{id_recurso}.ALL**

Permite ejecutar cualquier operación sobre el recurso id_recurso de la API id_api.

- **scope: {id_api}.ALL.{id_operacion}**

Permite ejecutar la operación id_operacion sobre cualquier recurso de la API id_api.

- **scope: {id_api}.ALL.ALL**

Permite ejecutar cualquier operación sobre cualquier recurso de la API id_api.

Aclaraciones respecto a los scopes:
-	Solo se incluirán los scopes solicitados para los que el consumidor tiene acceso.
-	Si no se especifica ningún scope, el sistema concederá uno por defecto.
-	En el caso de que se solicite acceso a un scope no autorizado devolverá error.
-	Si además de los scopes autorizados, se solicita acceso a algún scope no autorizado, solo se otorgará acceso a los scopes autorizados.

<div style="page-break-after: always;"></div>

# Sintaxis de las variables empleadas en OAuth2

En este apartado se detallará la sintaxis de las variables que se emplearán a través de OAuth2. El uso de estas variables dependerá del tipo de flujo empleado.

Se emplearán las siguientes definiciones:

-	VSCHAR     = %x20-7E
-	NQCHAR     = %x21 / %x23-5B / %x5D-7E
-	NQSCHAR    = %x20-21 / %x23-5B / %x5D-7E
-	UNICODECHARNOCRLF = %x09 /%x20-7E / %x80-D7FF / %xE000-FFFD / %x10000-10FFFF

Las posibles variables para emplear son:

-	“client_id” : *VSCHAR
-	“client_secret” : *VSCHAR
-	“response_type” : response-name *( SP response-name )
    - response-name = 1*response-char
    -	response-char = "_" / DIGIT / ALPHA
-	“scope” : scope-token *( SP scope-token )
    -	scope-token = 1*NQCHAR
-	“state” : 1*VSCHAR
-	“redirect_uri” : URI-reference
-	"error" : 1*NQSCHAR
-	"error_description" : 1*NQSCHAR
-	"error_uri" : URI-reference
-	"grant_type" : grant-name / URI-reference
    -	grant-name = 1*name-char
    -	name-char  = "-" / "." / "_" / DIGIT / ALPHA
-	"code" : 1*VSCHAR
-	"access_token" : 1*VSCHAR
-	"token_type" : type-name / URI-reference
    -	type-name  = 1*name-char
    -	name-char  = "-" / "." / "_" / DIGIT / ALPHA
-	"expires_in" : 1*DIGIT
-	"username" : *UNICODECHARNOCRLF
-	"password" : *UNICODECHARNOCRLF
-	"refresh_token" : 1*VSCHAR
-	Endpoint Parameter Syntax
    -	param-name = 1*name-char
    -	name-char  = "-" / "." / "_" / DIGIT / ALPHA 

<div style="page-break-after: always;"></div>

# Acceso a APIs mediante OAuth2

La seguridad en el acceso a APIs en AXPE está implementada mediante el uso de OAuth2 ya que permite acceder al uso de más de un recurso de una o varias APIs mediante un único proceso de login.

OAuth2 es un framework de autorización que permite a aplicaciones acceder a recursos protegidos delegando la autenticación en un servidor de autorización.

El sistema se basa en el uso de tokens para la autenticación y una serie de scopes predefinidos para la autorización.

A continuación, se presenta un esquema con los principales tipos de flujo, su descripción, casos de uso y su credibilidad.

Mediante OAuth2, una aplicación que quiera acceder a las APIs ofrecidas por AXPE podrá acceder de forma segura a los recursos (APIs) definidos en el modelo de seguridad para dicha aplicación.

El control del acceso se basa en la utilización de un token que permitirá identificar a la aplicación que efectúa el acceso a las APIs y los recursos a los que puede acceder.

Keycloak permite los siguientes Grant Types:

```json
"grant_types_supported": [
  "authorization_code",
  "implicit",
  "refresh_token",
  "password",
  "client_credentials",
  "urn:ietf:params:oauth:grant-type:device_code",
  "urn:openid:params:grant-type:ciba"
],

```

## Qué Grant Type emplear

El hecho de emplear un grant type u otro depende del tipo de cliente que usará en usuario final y la experiencia que se busca para sus usuarios. Un grant type es un método para obtener un token de acceso (Acess Token). 

Para decidir un Grant Type u otro se estudian diferentes opciones:

-	**¿Cliente propio o de terceros?**: Un cliente propio es un cliente que confía lo suficiente para emplear credenciales de autorización del usuario final. Un ejemplo, la aplicación para iPhone de Spotify es propiedad y esta desarrollada por Spotify.
-	**¿Propietario del Access token?**: Un Access token representa un permiso otorgado a un cliente para acceder a algunos recursos protegidos. Si está autorizando una máquina para acceder a los recursos y no necesita el permiso de un usuario para acceder a dichos recursos, debe implementar el grant type Client Credentials. Si necesita el permiso de un usuario para acceder a los recursos, debe determinar el tipo de cliente.
-	**¿Tipo de cliente?**: Dependiendo si puede o no guardar las credenciales, dependerá del grant type que se emplee.
    -	Si el cliente es una aplicación web que tiene un componente del lado del servidor, debe implementar el grant type de Authorization Code.
    -	Si el cliente es una aplicación web que se ejecuta completamente en el front-end (por ejemplo, una aplicación web de una sola página), debe implementar el grant type de password para clientes de primera parte y el grant type Implicit para clientes de terceros.
    -	Si el cliente es una aplicación nativa, como una aplicación móvil, debe implementar el grant type de password.

<div align="center">  <img src="src/DiagramaFlujoGrantTypes.png" alt="Diagrama de flujo Grant Types"  width="80%"/></div>

## Authorization code

El flujo entre el servicio OAuth y la aplicación del cliente se inicia a través de solicitudes HTTP. Una vez que el usuario acepta la solicitud de acceso se le otorga un authorizarion code a la aplicación cliente, que se comunica con el servicio OAuth para obtener el Access token. Este token permite realizar llamadas a la API para obtener los datos de usuario.

Después de esta comunicación inicial, todas las comunicaciones (servidor-servidor) se realizan a través de canales secundarios seguros, establecidos durante el registro con el servicio OAuth, al generarse también un Client Secret. El usuario final no está expuesto a estas comunicaciones.

Si bien este grant type es compatible por sí solo, generalmente se recomienda combinarlo con identity tokens, lo que lo convierte en el llamado Hybrid flow. Hybrid flow le brinda funciones adicionales importantes, como respuestas de protocolo firmado.

Dado que la mayoría de los datos confidenciales (como el token de acceso y los datos del usuario) no se envían a través del navegador, este grant type se recomienda para aplicaciones del servidor.

<div align="center">  <img src="src/AuthorizationCode.png" alt="Authorization Code"  width="80%"/></div>

## Implicit

El grant type Implicit está optimizado para aplicaciones basadas en navegador. Ya sea solo para autenticación de usuario (aplicaciones JavaScript y del lado del servidor) o solicitudes de autenticación y token de acceso (aplicaciones JavaScript).

En Implicit, todos los tokens se transmiten a través del navegador y, por lo tanto, no se permiten funciones avanzadas como tokens de actualización.

Este grant type se emplea para clientes basados en agentes de usuario (por ejemplo, aplicaciones web de una sola página) que no puedan mantener un Client Secret dado que se puede acceder fácilmente a todo el código de la aplicación y al almacenamiento (no se puede garantizar la confidencialidad del Client Secret). 

<div align="center">  <img src="src/Implicit.png" alt="Implicit"  width="80%"/></div>

## Password

El grant type de resource owner password permite solicitar tokens en nombre de un usuario enviando el nombre y la contraseña del usuario al token endpoint. Esto se denomina autenticación "no interactiva" y, por lo general, no se recomienda.

En lugar de redirigir al usuario al authorization server, el propio cliente le pedirá al usuario el nombre de usuario y la contraseña del propietario del recurso. El cliente enviará estas credenciales al authorization server junto con las credenciales del cliente. A continuación, el servidor devuelve el Access token.

<div align="center">  <img src="src/Password.png" alt="Password"  width="80%"/></div>

## Client Credentials

Este es el grant type más simple y se usa para la comunicación de servidor a servidor: los tokens siempre se solicitan en nombre de un cliente, no de un usuario. Esto se vuelve relevante cuando el cliente está solicitando acceso a recursos protegidos bajo su control directo o los de otro dueño que han sido previamente concertados con el servidor de autorizaciones.

Con este grant type, envía un token request al token endpoint y obtiene un token de acceso que representa al cliente. Los clientes pueden utilizar cualquiera de los métodos de autenticación de clientes admitidos por Keycloak. Por ejemplo, client_id/client_secret o JWT.

<div align="center">  <img src="src/ClientCredentials.png" alt="Client credentials"  width="80%"/></div>

## Device Code

El nombre completo del Grant Type es: urn:ietf:params:oauth:grant-type:device_code

Este grant type está diseñado para dispositivos conectados a internet con capacidades de entrada limitadas o con carencias de un navegador adecuado donde ingresar fácilmente las credenciales. Un ejemplo de esto son los televisores inteligentes, dispositivos IoT, o aplicCaciones de consola en servidores donde no se puede cargar un navegador web.  

<div align="center">  <img src="src/DeviceCode.png" alt="Device code"  width="80%"/></div>

## CIBA

El nombre completo del Grant Type es: urn:openid:params:grant-type:ciba

Este grant type define un protocolo para admitir el inicio de la autenticación sin interacción del usuario desde un consumer device. La autenticación se realiza a través de un Authentication Device por parte del usuario que da si consentimiento (si es necesario) a la request. CIBA se conoce como flujo desacoplado.

El flujo comienza con una solicitud de autenticación al endpoint. El servidor de autorización devuelve un acuse de recibo con un identificador de transacción. A continuación, el usuario se autentica a través de un mecanismo aparte, por ejemplo, un móvil. Mientras, el cliente sondea el servidor de autorización con regularidad y busca el token. El servidor de autorización devuelve el token con un error si está pendiente, o los tokens si están disponibles.

<div align="center">  <img src="src/Ciba.png" alt="CIBA"  width="80%"/></div>
<div style="page-break-after: always;"></div>

# Respuesta del token

La respuesta tipo ante una solicitud de token que ha pasado el proceso de validación, será similar al siguiente:

```json
200 OK { 
  "access_token":"de1a83b0-4e6c-44b4-8b0f-31b318761634",
  "token_type":"Bearer",
  "expires_in":57600,
  "refresh_token":"d75fa868-0a9f-4433-9d00-8d3d3be33a68",
  "scope":"read" 
}
```
Donde:
-	access_token:  token generado
-	token_type: Valor fijo “Bearer”
-	expires_in: Tiempo de vida del token expresado en segundos
-	refresh_token: Token de refresco
-	scope: Scopes de negocio a los que autoriza el token devuelto

En el caso de devolver un error de autenticación, se recibe:
```json
401 Unauthorized { 
  "error":" login_required",
  "error_description":"The resource owner could not be authenticated due to missing or invalid credentials" 
}
```

<div style="page-break-after: always;"></div>

# Tiempo de caducidad máximo de un token

Se emplean los tokens OAuth para autenticar a los usuarios y transmitir información sobre ellos. Un token es una cadena de caracteres que sirve como una credencial que se usa para acceder a los recursos protegidos

Cuando un usuario accede al portal proporciona una serie de datos. Esos datos se encapsulan en un token que le otorga acceso. Junto a ese token, se envía su tiempo de vida en segundos y los scopes a los que da acceso. Adicionalmente, dependiendo del tipo de flujo, se enviará también un token de refresco.

Cuando se emite un token para un usuario, éste puede acceder al sistema hasta que el token caduque. Cuando caduca, el usuario debe volver a autenticarse en el sistema.

Se recomienda que los tokens de acceso tengan una duración de 15 minutos (900 segundos). Por otra parte, también se recomienda que los tokens de refresco tengan una duración máxima de 60 minutos (3600 segundos).

<div style="page-break-after: always;"></div>

# Utilización del token

Con el token OAuth obtenido, una aplicación puede invocar a las APIs de AXPE. Dependiendo de la API y del scope incluido en el token, se permitirá o no el acceso.

Para utilizar un token en las llamadas al API Gateway, se debe indicar el token como una cabecera de autorización de tipo Bearer.

En caso de solicitar acceso a un API con un token inválido o un scope insuficiente para el configurado en dicho API, la respuesta obtenida será un código http 401 – Unauthorized.

<div style="page-break-after: always;"></div>

# Refresco del token

El tiempo de validez de un token viene expresado en segundos en el campo expires_in en el momento de la obtención del token. Si el token expira, deja de ser válido para las llamadas a las APIs.

Para obtener un nuevo token sin obligar al usuario a autenticarse de nuevo, se puede utilizar el token de refresco obtenido en la llamada original.

Mediante una llamada POST a la URL */token* con los siguientes parámetros, se puede obtener un nuevo token:

-	client_id: de la aplicación cliente
-	client_secret: de la aplicación cliente
-	refresh_token: el token de refresco obtenido al generar el token anterior
-	grant_type: el valor *“*refresh*”*

Esta petición devuelve un nuevo token de acceso más un nuevo token de refresco. El nuevo token tendrá los mismos scope que el original, con el tiempo de validez inicializado.

<div align="center">  <img src="src/RefreshToken.png" alt="Refresh Token"  width="80%"/></div>

**Excepción:** En el caso de que el token de refresco haya caducado, se obtiene una respuesta 400 para que el usuario vuelva a iniciar sesión.

<div style="page-break-after: always;"></div>

# Revocado del token

La aplicación cliente puede querer revocar un token existente por razones de seguridad, por ejemplo, al hacer logout el usuario autenticado.

Para revocar un token, se debe hacer una petición POST a la URL */revoke* con los siguientes parámetros:

-	client_id: de la aplicación cliente
-	client_secret: de la aplicación cliente
-	token: el token a revocar

Si la llamada es correcta, el token queda inutilizado y se devuelve el mensaje:

```json
200 OK { 
  "result":"revoked"
}
```








