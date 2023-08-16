|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|06/05/2023|Axpe|Versión inicial|


# **Principales consumidores de Renta4 Banco**

## Índice
---
[1. Introducción](#introduccion)

[2. Tipos de APIs según su exposición](#tipos-de-apis)

[3. Principales consumidores](#principales-consumidores)

[4. Principales consumidores de Renta4 Banco](#principales-consumidores-renta4)

[5. Tipos de APIs en Renta4 según los consumidores](#tipos-apis-renta4-segun-consumidores)


<a id="introduccion"></a>

## 1. Introducción
Consumir una API significa interactuar con esa API. Es un proceso por el cual el consumidor accede a las diversas APIs que se encuentran expuestas y utiliza los datos de dichas APIs. Esto normalmente implica tener que iniciar sesión en un API Portal. 

En este proceso identificamos dos roles principales:
- **Consumidor de la API:** puede ser un desarrollador o un cliente. También puede ser externo/interno.
- **Proveedor de la API o API Provider:** persona u organización a la que pertenece la API que se consume. 

Consumir las APIs es el objetivo de publicar una API y, por lo tanto, es una parte fundamental del ciclo de vida API. Las APIs se crean y se publican para que alguien pueda consumirlas, es decir, para que tanto los **desarrolladores** como los **clientes**  puedan conectar con esas APIs y acceder a aplicaciones y servicios. Inicialmente, la mayoría de las APIs estaban destinadas a ser consumidas por desarrolladores, pero hoy en día muchas APIs se encuentran expuestas a consumidores externos para aprovechar el negocio y monetizar la información. 

En este documento se describirán los principales consumidores y subscriptores de Renta4 Banco. De esta manera, se podrá realizar un análisis de la forma de consumir las APIs y ver si son externas o internas, para así poder realizar una mejor gestión de las mismas.  

<a id="tipos-de-apis"></a>

## 2. Tipos de APIs según su exposición
En función de si la API va a ser consumida por clientes externos o se va a dedicar únicamente al consumo interno por parte de la organización, habrá que tener en cuenta la forma de exponerlas, su seguridad y su nivel de rendimiento. En el documento de Estándares y Patrones (referencia) se hace una distinción entre APIs externas e internas, pero en este apartado profundizaremos un poco más en cada tipo:

### APIs externas o públicas
Este tipo de APIs se encuentran disponibles para terceros, es decir, para clientes o desarrolladores externos a la organización a la cuál pertenece la API. Este tipo de APIs pueden estar monetizadas. Además, al ser públicas, hay que implementar una seguridad mayor, que involucre un proceso de autorización y autenticación para poder consumirlas. Las APIs externas son **APIs Backend for Frontend (BFF) o APIs de Experiencia**. Las **APIs de Negocio** pueden variar, de manera que podrían ser tanto externas como internas, dependiendo del caso. 

### APIs internas
Estas APIs no se encuentran expuestas a terceros, y están pensadas para ser consumidas por los desarrolladores de la empresa a la cuál pertenece la API. A menudo son APIs que conectan diferentes sistemas dentro de la propia organización, y permiten el acceso a la información y los datos del backend y a las funcionalidades de las aplicaciones. Este tipo de APIs normalmente presentan una seguridad mucho más laxa que las APIs públicas o, incluso, a menudo carecen de seguridad por completo, aunque esto último no es una práctica recomendada. Las APIs internas son **APIs de Sistema** o, en algunos casos, **APIs de Negocio**. 

### APIs de socios o Partner APIs
Este tipo de APIs únicamente se encuentran disponibles para clientes externos específicos, que han sido seleccionados y autorizados para poder consumirlas. Normalmente son APIs que facilitan el Business-to-Business. Son APIs que tienen usos bastante específicos, y los clientes que las utilizan tienen unas licencias y unos derechos claros sobre dichas APIs. No suelen estar monetizadas directamente, como las APIs públicas, aunque sí que ofrecen oportunidades de negocio, ya que las empresas pagan por estos servicios, aunque no lo hagan directamente por la API. Este tipo de APIs suelen tener una seguridad bastante robusta. 

### APIs compuestas o APIs Composite 
Algunas clasificaciones diferencian las **APIs compuestas (o Composite APIs)**. Estas APIs ejecutan una serie de solicitudes en una sola llamada. El output de una solicitud inicial se puede utilizar como input en una solicitud posterior. Esto permite ahorrar en el uso de datos y aumentar la eficacia de la aplicación, ya que mantiene la cantidad de llamadas a la API al mínimo. Normalmente son públicas, pero esta categoría no atiende directamente al nivel de exposición de la API, aunque se considera interesante incluirla aquí.

Para obtener una información más detallada acerca de las APIs BFF o Experiencia, APIs de Negocio y APIs de Sistema, se puede consultar el documento de Tipificación de las APIs (referenciar). 

### Seguridad recomendada

La seguridad recomendada para cada tipo de API es la siguiente: 

- **APIs externas o públicas:** se recomienda un protocolo de seguridad completo, como OAuth 2.0 con un flujo Code o Implicit, o OpenId Connect. 

- **APIs internas:** como necesitan menos seguridad, se recomienda implementar APIKey o HTTP Basic. 

- **Partner APIs:** seguridad robusta, como Oauth 2.0 con un flujo Password o Client Credentials, OpenId Connect o Mutual TLS. 

- **APIs de Negocio:** la seguridad variará en función de si son externas o internas. Algunas recomendaciones son utilizar OAuth 2.0 o una seguridad tipo HTTP Bearer, por ejemplo.

Para información más detallada acerca de la seguridad API, consultar el documento de Capas de seguridad (referenciar).

<a id="principales-consumidores"></a>

## 3. Principales consumidores 
A la hora de consumir nuestras APIs y de determinar su nivel de exposición (si va a ser una API externa, interna o partner) es necesario identificar los principales consumidores con los que cuenta nuestra organización, y a quién se va a dirigir cada API.

De forma genérica, podemos identificar tres grandes grupos de consumidores de APIs:
### Aplicaciones internas
Este tipo de consumidor es el más habitual ya que, al final, la mayor parte de las APIs dentro de una organización van a ser consumidas por otras aplicaciones de la propia organización. Son desarrolladores internos y microservicios de la organización que dependen de la funcionalidad de nuestras APIs. 
### Plataformas de experiencia digital 
Permiten definir experiencias de usuario para un rango de clientes muy amplio, en diferentes dispositivos. Pueden interaccionar con el usuario a través de páginas web, de dispositivos móviles, etc.
### Frontends personalizados
Puede ser una interfaz de usuario web personalizada, aplicaciones mobile nativas, redes sociales, servicios integrados, etc. 


Es importante tener un inventario de todos los consumidores (internos y externos) en una organización y atender a sus particularidades y necesidades concretas. Algunas consideraciones y características que hay que tener a la hora de identificar clientes, son las siguientes:

- **Idioma:** El tipo de lenguaje que se va a usar para consumir la API (REST, basado en Java, en .Net...)
- **Latencia:** ¿qué tiempos de latencia son aceptables para el consumidor? ¿desde dónde se consume geográficamente la API? ¿qué dispositivo se utiliza para consumirla?
- **Banda ancha:** es importante tener en cuenta las restricciones de ancho de banda, es decir, la velocidad. 
- **Poder de procesamiento:** hay que tener en cuenta las limitaciones que tienen algunos clientes en cuanto a poder de procesamiento, ya que esto afectará a la manera en que consumen o llaman a la API. 
- **Capacidad de almacenamiento en caché:** es importante analizar si el clinete puede almacenar en caché, y hasta qué grado. 
- **Seguridad:** como ya se ha mencionado en el apartado anterior, dependiendo del tipo de consumidor y de la exposición de la API, se impelementará un tipo de seguridad u otra. 

<a id="principales-consumidores-renta4"></a>

## 4. Principales consumidores de Renta4 Banco
( Se muestra un ejemplo del banco Renta4, aplicar a cada cliente de manera personalizada)
A continuación, se expone una tabla de los principales consumidores de Renta4 Banco, las credenciales y las APIs a las que tienen acceso. 

Las credenciales para terceros implican consumidores externos, mientras que **APIs Digital** y **R4 Apificación** se refieren a los equipos internos de desarrollo de APIs de Renta4 Banco. 

### Credenciales

Consumidor | Credenciales |
---------|----------|
 DAComisiones | Credenciales para terceros (deshabilitada) | 
 Digital | Credenciales para APIs Digital | 
 Digital - Internal | Credenciales para APIs Digital |
 Everis-Finbow | Credenciales para APIs Digital | 
 Finect | Credenciales para APIs Digital | 
 IOBuilders_ID | Credenciales para terceros | 
 Kit Conexion Cliente | Credenciales de prueba kit de conexion| 
 Mocks APP | Credenciales para consumo de mocks generados para app movil |  
 OauthTest | Credenciales de prueba cliente OAuth |
 Patrimonio | Credenciales de prueba cliente OAuth |
 R4Apificacion | Credenciales de prueba equipo r4apificacion |
 R4App | Credenciales de la web logada de Renta4 (token generado desde Gauss por flujo web) |
 R4com | Credenciales de prueba equipo r4comtech |
 R4ComTech | Credenciales de prueba equipo r4apificacion |
 R4NoLogado | Credenciales para web pública no logada (front) |
 R4NoLogado-Server | Credenciales para web no logada (servidor) |
 R4Shell | Credenciales para APIs Digital |
 Rankia | Credenciales para APIs Digital |
 Renta4IA | Credenciales para terceros |
 Salesforce | Credenciales para Salesforce (uso desde la red de oficinas) |

 ### APIs a las que se tiene acceso

 Consumidor | APIs a las que tiene acceso |
---------|----------|
 DAComisiones | Apificación-Digital Advisor Comisiones | 
 Digital | Allfunds-Corporate Actions Allfunds-Family Fund, Allfunds-Internal, Allfunds-Legal Docs, Apificación-Buscador, Apificación-Patrimonios v1, APP-Infovalor v1, Digital-CMS, Digital-Fondotop 2.0, Digital-R4Com-Fondos | 
 Digital-Internal | Apificación-Patrimonios v1 |
 Everis-Finbow | Digital-R4Com-Public | 
 Finect | Digital-R4Com-Public | 
 IOBuilders_ID | Apificación-Información Usuario Digital Assets, Apificación-Obtener datos de usuario, Apificación-Patrimonios v1, Apificación-Validar token   | 
 Kit Conexion Cliente | Apificación-Obtener datos de usuario, Apificación-Patrimonios v1, Apificación-Validar token| 
 Mocks APP | API Contracts v2, API Mifid v2, Apificación-Buscador, Apificación-Patrimonios v1, APP-Consulta Resultados Derivados v1, APP-Buscador Externo v1,APP-Carteras v1, APP-Contacts v1, APP-Contratacion Fondos v1 |  
 OauthTest | Digital-Utils, PruebaOauth |
 Patrimonio | Apificación-Obtener datos de usuario, Apificación-Patrimonios v1, Apificación-Validar token|
 R4Apificacion | Credenciales de prueba equipo r4apificacion |
 R4App | - |
 R4com | Allfunds-Corporate Actions, Allfunds-Family Fund, Allfunds-Legal Docs, API Avisos v1, API Perfil v1, API Utrils v1, Apificación-Adeudos, Apificación-Impuestos-INTERNA, APificación-Inicio de pago Inespay |
 R4ComTech | Allfunds-Corporate Actions, Allfunds-Family Fund, Allfunds-Legal Docs, Digital-Fondotop 2.0, Digital-Vadeum Carteras, Infobolsa-Cotizaciones, Infobolsa-Noticias, Infobolsa-Series, Infobolsa-Utils, Morningstar-Data  |
 R4NoLogado | Apificación-Buscador, Digital-Fondotop 2.0, Digital-R4Com-Fondos, Digital R4Com-Public, Digital-Vadeum Carteras, Infobolsa-Cotizaciones, Infobolsa-Series, Infobolsa-Utils, Morgningstar-Data, Morgningstar-Series History  |
 R4NoLogado-Server | Digital-R4Com-Fondos, Digital-R4Com-Maestro de valores |
 R4Shell | Allfunds-Corporate Actions, Allfunds-Family Fund, Allfunds-Legal Docs, Digital-Fondotop 2.0, Digital-Vadeum Carteras, Infobolsa-Cotizaciones, Infobolsa-Noticias  |
 Rankia | Digital-R4Com-Public |
 Renta4IA | Apificación-Datos mifid cliente, Infobolsa-Series, Apificación-Digital Advisor Comisiones, Digital-Series, Infobolsa-Cotizaciones, Morningstar-Data, Morgningstar-Series History |
 Salesforce | Apificación-Patrimonios v1, Apificación-Transferencias SEPA instantánes-INTERNA, MPM-Pólizas |


<a id="tipos-apis-renta4-segun-consumidores"></a>

## 5. Tipos de APIs en Renta4 según los consumidores

( Se muestra un ejemplo del banco Renta4, aplicar a cada cliente de manera personalizada)

Una vez que hemos identificado los diferentes consumidores de las APIs de Renta4 Banco, y diferenciándolos en consumidores externos e internos, se puede hacer una clasificación de las APIs en externas e internas, basándonos en las tablas del apartado anterior. 

La clasificación en **APIs externas e internas** de Renta4 Banco se encuentra en el documento de Estándares y Patrones (hacer referencia)

