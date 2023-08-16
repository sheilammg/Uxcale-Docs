
#  **Politicas comunes**
|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|28/07/2023|Axpe|Versión inicial.|



# Índice 

- [1. Introducción](#introducción)

- [2. Tipos de políticas](#tipos-de-políticas)

    - [2.1 Gestión de tráfico](#gestión-de-tráfico)

    - [2.2 Mediación o transformación](#mediación-o-transformación) 

    - [2.3 Seguridad ](#seguridad)

    - [2.4 Personalizadas o de extension](#personalizadas-o-de-extensión)

    - [3. Conclusión ](#conclusión)






<a id="introducción"></a>

# Introducción

Una política es un módulo que implementa una función específica y
limitada a nuestra API. Las políticas te permiten cambiar y gestionar el
comportamiento de una API sin escribir código. Una política es un
archivo de configuración que tiene formato XML, donde también se
encuentra la lógica de negocio. El código XML se puede cambiar y editar
de manera que cumpla los requerimientos que se necesitan.

Las políticas nos permiten agregar capacidades específicas de
administración a nuestra API de manera más sencilla y proporcionan
funciones como seguridad, límites de frecuencia, transformación y
mediación. También permiten controlar el tráfico, mejorar el rendimiento
y aumentar la utilidad de las APIs sin necesidad de modificar el
microservicio.

Normalmente las políticas se pueden inyectar en el proxy de la API, de
manera que la aplicación real de la política se produce dentro de la
propia aplicación de proxy, que procesa la solicitud recibida.

Para la gestión y el uso de políticas, se pueden utilizar políticas
estándar que ya están definidas y que permiten todas estas funciones
mencionadas. De todas maneras, las políticas también pueden ser
personalizables, de manera que se pueden escribir secuencias de comandos
y códigos propios que extiendan la funcionalidad de la API.


<a id="tipos-de-políticas"></a>

# Tipos de políticas

Las políticas se pueden clasificar según su función y no hay un sistema
de clasificación único. Se ha decidido agruparlas en cuatro grandes
grupos:

 - **Políticas de gestión de tráfico:** permiten configurar el
almacenamiento caché, controlar cuotas, mitigar los efectos de los
picos, establecer los límites de velocidad concurrentes, interruptores
automáticos, limitación de solicitudes, etc. En general, ayudan a
mantener la calidad del servicio y a asegurar que la carga de los
servicios se encuentra dentro de unos límites saludables.

 - **Políticas de mediación o transformación:** permiten realizar la
transformación, análisis y validación de mensajes, generar fallas y
alertas.

 - **Políticas de seguridad:** permiten controlar los puntos de acceso a
las API con OAuth, validar las claves API, etc. Incluyen políticas de
autenticación y validación y de protección contra accesos maliciosos.

 - **Políticas personalizadas o de extensión:** políticas personalizadas
que satisfacen necesidades específicas y extienden la funcionalidad. Se
puede modificar una política existente o crear una completamente nueva.

Dentro de cada tipo existen diferentes políticas particulares, de las
cuáles a continuación se seleccionan las que se recomienda usar en
la compañía.

<a id="gestión-de-tráfico"></a>

## 2.1 Gestión de tráfico

-   **Política de gestión de picos**: para controlar el tráfico de la
    API y limitar la velocidad, controlar los aumentos repentinos o
    picos en el tráfico y limitar la cantidad de solicitudes que se
    procesan en el API proxy. Ejemplo: [Time
    out](https://docs.konghq.com/mesh/2.1.x/policies/timeout/) o
    [ConcurrateRateLimit
    policy](https://docs.apigee.com/release/deprecated-features)

-   **Política de cuota**: para configurar el número de mensajes que
    permite un API proxy. Ejemplo: [Quota
    policy](https://docs.apigee.com/api-platform/reference/policies/quota-policy)

-   **Políticas de caché**: relacionadas con la información almacenada
    en la memoria caché. Son políticas que permiten eliminar los valores
    almacenados, recuperarlos, o definir cómo deben recuperarse dichos
    datos. Ejemplo: [InvalidateCache
    policy](https://docs.apigee.com/api-platform/reference/policies/invalidate-cache-policy)

-   **Políticas de registro y observabilidad de tráfico**: políticas
    para las métricas, el rastreo y registro del tráfico y hacer
    seguimiento y chequeo de la salud o estado de la API. Ejemplo:
    [Traffic
    Trace](https://docs.konghq.com/mesh/2.1.x/policies/traffic-trace/)

<a id="mediación-o-transformación"></a>

## 2.2 Mediación o transformación

-   **Políticas de transformación de mensajes**: son políticas que
    permiten cambiar de un formato de mensaje a otro. Por ejemplo,
    cambiar de XML a JSON y viceversa. Ejemplo: [JSON to XML
    policy](https://docs.apigee.com/api-platform/reference/policies/json-xml-policy)

-   **Políticas de transformación de cabeceras**: por ejemplo, para
    añadir o eliminar cabeceras. Ejemplo: [Header
    Injection](https://docs.mulesoft.com/policies/policies-included-header-injection)
    o [Header
    Removal](https://docs.mulesoft.com/policies/policies-included-header-removal)

<a id="seguridad"></a>

## 2.3 Seguridad

-   **Políticas de autenticación:** sirven para hacer autenticaciones de
    usuario, usuario y contraseña, credenciales, etc. Ejemplo: [Basic
    Authentication LDAP
    Policy](https://docs.mulesoft.com/policies/policies-included-basic-auth-ldap)
    o [Basic Authentication
    Policy](https://docs.apigee.com/api-platform/reference/policies/basic-authentication-policy)

-   **Políticas de protección contra amenazas**: se pueden usar para
    proteger contra amenazas XML o JSON, sobre todo. Ejemplo:
    [XMLThreatProtection
    policy](https://docs.apigee.com/api-platform/reference/policies/xml-threat-protection-policy)
    o [JSON Threat
    Protection](https://docs.mulesoft.com/policies/policies-included-json-threat-protection)

-   **Políticas OAuth 2.0:** son las políticas relacionadas con el
    método de seguridad OAuth 2.0 y sus tipos. Permiten realizar
    acciones con tokens, códigos de autorización, etc. Ejemplo: [Oauth
    2.0 Authentication](https://docs.konghq.com/hub/kong-inc/oauth2/) o
    [OpenID Connect OAuth 2.0 Token Enforcement
    Policy](https://docs.mulesoft.com/policies/policies-included-openid-token-enforcement)

-   **Políticas JWT**: relacionadas con la seguridad JSON Web Token.
    Ejemplo: [JWT](https://docs.konghq.com/hub/kong-inc/jwt/) o [JWT
    Validation](https://docs.mulesoft.com/policies/policies-included-jwt-validation)

<a id="personalizadas_o_de_extensión"></a>

## 2.4 Personalizadas o de extensión

Estas políticas son personalizadas y permiten definir funcionalidades
concretas. La funcionalidad dependerá de los requerimientos de negocio o
de la necesidad específica que se quiera cubrir. Por ejemplo, se pueden
generar políticas que habilitan el uso de secuencias de comandos en
Java, Javascript, Python, etc. para definir estas políticas
personalizadas. Ejemplo: [Javascript
policy](https://docs.apigee.com/api-platform/reference/policies/javascript-policy)

<a id="conclusión"></a>

# Conclusión

Este documento es una guía genérica que explica los diferentes tipos de
políticas API que existen, atendiendo a su funcionalidad y ofreciendo
ejemplos de cada uno. El documento está pensado para orientar a la
organización en la comprensión general de las políticas y exponer
distintas categorías y funciones de las mismas, que pueden ser de
utilidad a la hora de implementar las propias.

Sin embargo, el uso de políticas concretas dependerá de las necesidades
específicas cada cliente y del API Manager que utilice, ya que cada
API Manager ofrece una serie de políticas propias. Además de esto, el
propio cliente podrá crear sus políticas personalizadas, en caso de que
sea necesario o de que las incluidas en el API Manager no cumplan
totalmente con los requerimientos.
