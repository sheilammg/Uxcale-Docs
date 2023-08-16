|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|11/04/2023|Axpe|Versión inicial|

# **Capas de Seguridad del ecosistema API**
La seguridad del ecosistema API es crucial para proteger los datos, sistemas y usuarios que interactúan con las API. Los riesgos incluyen vulnerabilidades de seguridad, ataques de malware, exposición de datos sensibles y acceso no autorizado a los recursos de la API. Para mitigar estos riesgos, se deben implementar medidas de seguridad sólidas, como la autenticación, autorización y cifrado de datos, junto con la monitorización y el análisis continuos de la actividad de la API. Al hacerlo, se puede garantizar un entorno seguro y confiable para el intercambio de información y servicios a través de las APIs.

## Índice
---

[1. Capas de seguridad](#capas-seguridad)
  - [1.1. Perímetro](#perimetro)
  - [1.2. Red](#red)
  - [1.3. Host](#host)
  - [1.4. Aplicación](#aplicacion)
  - [1.5. Data](#data)

[2. Casos de uso API](#casos-de-uso-api)

[3. Tokens](#tokens)

  - [3.1. OAuth](#oauth)
  - [3.2. OpenId Connect](#openid-connect)
  - [3.3. API key](#api-key)
  - [3.4. Token UUID](#tokenuuid)
  - [3.5. Refresh Tokens](#refresh-tokens)
  - [3.6. Stateless vs stateful Tokens](#stateless-vs-stateful-tokens)

[4. North-South Security & East-West Security](#north-south-security-east-west-security)
   - [4.1. North-South Security](#north-south-security)
   - [4.2. East-West Security](#east-west-security)

<a id="capas-seguridad"></a>
## 1. Capas de seguridad 

En la seguridad del Ecosistema API se tiene que trabajar la seguridad en las 5 capas. Éstas 5 capas son Perímetro, Red, Host, Aplicación y Data.

<a id="perimetro"></a>
### 1.1. Perímetro

- **AntiDDoS:** tiene que estar gestionado en la primera capa expuesta internet. No forma parte de la capa API, se tiene que gestionar a nivel de infraestructura.

- **WAF:** el WebApplicationFirewall será la primera línea de control del flujo entrando, para controlar ataques de manipulación de las request tipo SQLInjection, XSS,… No forma parte de la capa API, se tiene que gestionar a nivel de infraestructura.

- **Rate Quota:** para las APIs expuesta, tenemos que poner límites de acceso por cliente. Hay diferentes tipos de Quotas que tenemos que poner según la API.
  - APIs de Experiencia: el quota dependerá del cliente según el uso previsto de la API
  - APIs de BaaS
  - APIs de sistema: Gestionado por el gateway
  - Bot Attack
  - Next Generation firewall

<a id="red"></a>
  ### 1.2. Red

  - **TLS:** el gateway podría servir como TLS terminación, pero todas nuestras comunicaciones tendrían que ir con TLS.

- **IP filtering:** para APIs privadas con clientes restringidos, más sencillo que mTLS. Gestionado por el gateway.

- **mutualTLS:** para APIs privadas con clientes restringidos. Comunicación interna podria ir con mTLS mientras tenemos mesh para gestionarlo. Gestionado por el gateway.

- **VPN:** no hace parte de la capa API, se tiene que gestionar a nivel de infraestructura 

- **Network segregation:** separar los diferentes niveles de API en diferentes redes sin comunicación directa excepto pasando por las gateways

- **Secure DNS:** Prevent DNS attack. No hace parte de la capa API, se tiene que gestionar a nivel de infraestructura.



Consumidor | SSL | MTLS | Pinin | IP filtering 
---------|----------|--------- |--------- |---------
 WebApp | Si | 
 Mobile App| Si |     | Si 
 Server Tercero (tpp)| Si | Si |      | Si
 Server Interno| Si | Si |      | Si

<a id="host"></a>
### 1.3. Host
- **Services segregation:** para evitar ataques East-west hay que tener muy controlado qué servicios llaman a qué servicio. Las opciones son:

  - Control de acceso de servicio a servicio por APIKey
  - Bloqueo de llamadas entre servicio de misma capa (ejemplo control de routing tipo Istio)
  - Endpoint Protection Platform (EPP)
  - Endpoint Detection and Response (EDR)

<a id="aplicacion"></a>
### 1.4. Aplicación 
- **Scopes:** Token oAuth para la gestión de scopes. Los scopes tendrán la siguiente estructura: 
> {Oauth:Operacion}.{Recurso\_API}.{id\_operación}. 

Esto se ve ampliado en el documento de referencia Guía de OAuth.Previsto en la parte API.

- **Authentication:** para la autenticación en todas las APIs se empleará OAuth según lo descrito en el documento Guía Referencia OAuth. Previsto en la parte API.

- **2FA:** en estos determinados casos, cuando es necesario un mayor nivel de seguridad se emplea OTP.

- **Content & Schema verification:** gestionado por el gateway.

- **Fraud prevention Engine:** incluirlo en el TokenUpgrade para obtener el token antes de pasar a la capa bancaria.

<a id="data"></a>
### 1.5. Data

- **Encrypt at rest:** no hace parte de la capa API.

- **Obfuscate sensitive Data (logs, data returned):** se recomienda la utilización de un sistema de ofuscación de los datos sensibles en logs.

- **Encryption mechanism for sensitive Data exposed by API:** se recomienda la utilización de un mecanismo de encriptación de datos sensibles expuestos en las APIs.

- **HSM:** en el caso que sea necesario se podría usar HSM para la encriptación comentada previamente vigilando el rendimiento. (test de rendimiento y performance). No hace parte de la capa API.

- **DLP (data lost prevention)**
- **Audit/SIEM**

<a id="casos-de-uso-api"></a>
## 2. Casos de uso API

- **APIs públicas**: APIs que están publicadas para ser usadas para clientes externos a la organización. Este caso de uso es el que necesita ser más securizado porque no nos podemos fiar en estos clientes externos en ser seguros.
- **APIs para aplicaciones internet**: Los clientes de estas APIs son aplicaciones de canales de la organización. Pero como estas APIs tienen que estar publicadas a internet el riesgo es también muy elevado.
- **APIs para aplicaciones extranet**: Estas APIs estarán solo expuestas a clientes que están en la red de la organización, y por eso necesitan menos control de seguridad (control perimetral).

<a id="tokens"></a>
## 3. Tokens
<a id="oauth"></a>
### 3.1. Oauth
OAuth2 es un framework de autorización que permite a aplicaciones acceder a recursos protegidos delegando la autenticación en un servidor de autorización.

El sistema se basa en el uso de tokens para la autenticación y una serie de scopes predefinidos para la autorización.

*flujo authorization code*: flujo estándar para aplicaciones donde el acceso a recursos se limita según el usuario logado mediante flujo OAuth2

*flujo client credentials*: flujo estándar para aplicaciones con acceso independiente del usuario logado.

*flujo implícito:* se trata de un flujo optimizado para aplicaciones basadas en navegador.


<a id="openid-connect"></a>
### 3.1. OpenId connect

El protocolo OpenID Connect (OIDC) se basa en el protocolo OAuth 2.0 y ayuda a autenticar a los usuarios y transmitir información sobre ellos. También es más estricto que el simple OAuth 2.0, por ejemplo, en sus definiciones de alcance.

<a id="api-key"></a>
### 3.1. API key 

API keys sirven a identificar el cliente del API (id la aplicación que usa el API), se puede integrar con los flujos oAuth si usamos el API key como contraseña del cliente.

<a id="tokenuuid"></a>
### 3.1. Token UUID

Los tokens empleados en la mayoría de organizaciones son tokens UUID.

<a id="refresh-tokens"></a>
### 3.1. Refresh Tokens

El tiempo de validez de un token viene expresado en segundos en el campo expires\_in en el momento de la obtención del token. Si el token expira, deja de ser válido para las llamadas a las APIs.

Para obtener un nuevo token sin obligar al usuario a autenticarse de nuevo, se puede utilizar el token de refresco obtenido en la llamada original. El tiempo de duración de los tokens de refresco viene desarrollado en el documento Guía referencia Oauth.

<a id="stateless-vs-stateful-tokens"></a>
### 3.1. Stateless VS stateful Tokens

Los Sesion token no contienen toda la información, porque están mantenidos en el API Manager. Las ventajas que tienen son de ser menos pesados, más opacos, revocables. El problema es que necesitan una llamada al API Manager para consultar su contenido.

Los Restful Tokens, contienen toda la información (en este caso tokens ciegos UUID), y por eso están mucho más validos por un entorno distribuido donde se consulta el contenido del token varias veces en elementos diferentes de la arquitectura.

<a id="north-south-security-east-west-security"></a>
## 4. North-South Security & East-West Security

<a id="north-south-security"></a>
### 4.1. North-South Security 

- *Capa de Producto o de Negocio*

Esta capa recibirá el token en la cabecera **Authorization**. El gateway no hará ningún control del contenido de este token, solo verificara que es un token correcto (firma). 
  
**Scopes de acceso a recurso:** Estos scopes se definen desde la capa de Baas. Tendrían la estructura: 
> **{Oauth:Operacion}.{Recurso\_API}.{id\_operacion}** ejemplo : *Oauth:Client\_credentials.RSI\_TSI.read*. 
Tendríamos que definir también los otros scopes por gestionar : 
- cualquier acceso a una API: 
> **{Oauth:Operacion}.{Recurso\_API}.ALL** 
En general los métodos de acceso serán: read o write. Los scopes vendrán definido según lo acordado en esta capa. En el gateway se podrá verificar estos scopes después de ejecutar el intercambio de token.

- *Capa de Sistema*

La seguridad de las APIs de esta capa es la misma que en la capa de Negocio. Todas las conexiones se realizarán a través del gateway.

- *Capa Backend for Frontend (BFF)*

La seguridad de las APIs de esta capa es la misma que en la capa de Negocio. Todas las conexiones se realizarán a través del gateway.

<a id="east-west-security"></a>
### 4.2. East-West Security
Para comunicarse entre microservicios se realizará la conexión a través del gateway.
