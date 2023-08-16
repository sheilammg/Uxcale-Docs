|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|16/03/2023|Axpe|Versión inicial|

# **Documentación técnica: PRISM**
## Índice
---
[1. Introducción](#introducción)

[2. Trabajar con PRISM](#trabajar-prism)

  - [2.1. Hosted Prism](#hosted-prism)

  - [2.2. Self-hosted Prism](#self-hosted-prism)

[3. Instalación](#instalacion)

[4. Pruebas](#pruebas)

  - [4.1. HTTP Mocking](#http-mocking)

    - [4.1.1 Response](#response)

    - [4.1.2 Request Validation](#request-validation)

  - [4.2. Validation Proxy](#validation-proxy)

    - [4.2.1 Ayudar a la integración del consumidor de la API](#ayudar-integracion)

    - [4.2.2 Pruebas de contrato extremo a extremo](#pruebas-contrato)

    - [4.2.3 Las operaciones no implementadas serán simuladas](#operaciones-no-implementadas)

    - [4.2.4 Operaciones en desuso](#operaciones-desuso)

[5. Mensajes de error](#mensajes-error)
  - [5.1. Errores de enrutamiento](#errores-enrutamiento)
  - [5.2. Errores de validación](#errores-validacion)
  - [5.3. Errores de seguridad](#errores-seguridad)
  - [5.4. Errores de negociación](#errores-negociacion)
  - [5.5. Error desconocido](#error-desconocido)
[6. Docker-compose](#docker-compose)

<div id='introduccion'/>

## 1. Introducción
Prism es un conjunto de paquetes para simulación de API y pruebas de contrato con OpenAPI v2 (anteriormente conocido como Swagger) y OpenAPI v3.x. 

Prism nos proporciona diferentes características: 

- Servidores simulados: servidores simulados realistas de cualquier documento de especificación de API. 

- Proxy de validación: pruebas de contrato para consumidores y desarrolladores de API. 

- Compatibilidad integral con las especificaciones de la API: OpenAPI v3.1, OpenAPI v3.0, OpenAPI v2.0 (anteriormente Swagger) y Postman Collections. 

<div id='trabajar-prism'/>

## 2. Trabajar con PRISM

<div id='hosted-prism'/>

### 2.1. Hosted Prism
Stoplight proporciona servidores simulados para que los consumidores de API puedan experimentar con una API sin necesidad de tener un código de back-end.

Dentro de Stopligth nos encontramos dos opciones para servidores simulados: 

- Stoplight Platform: plataforma colaborativa de diseño de API para diseñar, desarrollar y documentar API compatible con la tecnología de simulacros de la tecnología de Prism.
- Stoplight Studio: diseñador visual gratuito de OpenAPI que viene integrado con simulación con tecnología de Prism.

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.002.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.002.png)

<div id='self-hosted-prism'/>

### 2.2. Self-hosted Prism
Prism es un servidor HTTP de código abierto con el que se puede trabajar a partir de la línea de comandos. Proporciona simulación, validación de solicitudes y negociación de contenido. Se puede usar como herramienta independiente o en integración continua.

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.003.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.003.png)

<div id='instalacion'/>

## 3. Instalación
Dentro de Prism solo tendríamos que realizar la instalación cuando trabajamos con self-hosted Prism, ya que si trabajamos con stoplight ya viene definido para poder trabajar con él.

La instalación de Prism es muy sencilla, solo se tiene que ejecutar el siguiente comando en nuestra línea de comandos:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.004.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.004.png)

Primeramente, tendríamos que comprobar si tenemos instalado[ NodeJS](https://nodejs.org/es/), para poder utilizar npm.

<div id='pruebas'/>

## 4. Pruebas

<div id='http-mocking'/>

### 4.1. HTTP Mocking
Prism ayuda a crear un “mock”(simulacro falso) basado en un documento OpenAPI, lo que nos permite probar el funcionamiento de nuestra API incluso antes de que se construya. Para iniciar este “mock” tendremos que utilizar el siguiente comando:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.005.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.005.png)

El servidor mock HTTP de Prism simula una API web real proporcionando puntos finales y reglas de validación descritas en el documento de descripción de la API. Esto nos permite comenzar a escribir código para servicios frontend como aplicaciones web, móviles u otras aplicaciones de backend, mientras que los desarrolladores de API siguen escribiendo código. Esto ayuda a encontrar y resolver problemas desde el principio, antes de que se construya la API, porque cambiar todo ese código puede ser costoso.

Detectar problemas desde el principio mientras todavía se está modificando las descripciones de la API), significa que ayuda a evitar realizar cambios costosos en la API de producción y tener que realizar los servicios correspondientes en el backend.

Al trabajar con mensajes HTTP, tenemos su misma estructura de solicitudes y respuestas:

<div id='response'/>

#### 4.1.1. Response
Prism intentará devolver respuestas significativas en función de la información que tenga disponible, como ejemplos de respuestas, y utilizará varios mecanismos de respaldo en caso de que no se proporcionen ejemplos. Esto significa que se puede usar cualquier documento de descripción de OpenAPI sin trabajo adicional, pero cuanto más completo este el documento mejor pruebas se podrán realizar.

Lo primero que hay que entender es que Prism HTTP Server respeta la negociación de contenido. Si su API es una mezcla de JSON, XML y datos de formularios, puede usar **Accept** y **Content-Type** al igual que con una API real, y debería funcionar como se espera, o fallar si se solicitan tipos inexistentes.

Dentro de la [documentación oficial de Prism](https://docs.stoplight.io/docs/prism/83dbbd75532cf-http-mocking#response-generation) nos encontramos con el diagrama de decisiones del que se basan las respuestas de Prism.

Ahora veremos un ejemplo práctico a partir de los ejemplos definidos en una API. Si una respuesta tiene un ejemplo, se utilizará para esta respuesta. En la siguiente imagen nos encontramos una respuesta con un código 200 Ok:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.006.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.006.png)

Al llamar a la petición [*http://127.0.0.1:4010/pets/123](http://127.0.0.1:4010/pets/123)* nos dará:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.007.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.007.png)

Llamar a la misma URL con el *Prefer* encabezado por *example=dog* [*http://127.0.0.1:4010/pets/123](http://127.0.0.1:4010/pets/123)* producirá el otro ejemplo:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.008.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.008.png)

De forma predeterminada, Prism utiliza una estrategia de generación estática, pero también se puede habilitar la generación dinámica usando el indicador *-d* dentro de la línea de comandos. En la siguiente imagen observamos un ejemplo de cómo arrancar las dos formas:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.009.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.009.png)

#### *Generación de respuesta estática*
Si el objeto de esquema de OpenAPI proporciona un ejemplo de cuerpo de respuesta, se usa para proporcionar una respuesta. Pero si dentro de la API no se devuelve ejemplos, se creará un cuerpo de respuesta basado en el objeto *schema* para crear una respuesta falsa completa.
#### *Generación de respuesta dinámica*
De esta forma, se consigue generar un valor aleatorio para todas las propiedades según su tipo y otra información como *format* o incluso usando [Dynamic Reponse con Faker](https://docs.stoplight.io/docs/prism/9528b5a8272c0-dynamic-response-generation-with-faker).

Al probar las llamadas a la API, es útil tener respuestas generadas dinámicamente para así asegurarse de que puedan admitir varios casos de uso, en lugar de probar siempre con un mismo dato estático.  Para tener más facilidad a la hora de generar estas respuestas, Prism utiliza las bibliotecas **Faker** y **Json Schema Faker**.

A la hora de arrancar un servidor con prism habrá que comprobar que se ejecuta en modo dinámico, a partir de utilizar *-d* o usando el encabezado *Prefer* con la palabra clave *Dynamic* establecida en *True*.

Dentro de una especificación OpenApi, se puede pasar la palabra clave *x-faker* a una propiedad, lo que nos permite utilizar el método especifico de la API de Faker. Si un usuario pasa un método que no existe, Prism recurre a Json Schema Faker para conseguir generar unos valores aleatorios para esa propiedad. En la siguiente imagen vemos un ejemplo:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.010.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.010.png)

Al realizar la siguiente llamada [http://127.0.0.1:4010/pets/123 -h "Prefer: dynamic=true"](http://127.0.0.1:4010/pets/123%20-h%20%22Prefer:%20dynamic=true%22), dentro de la respuesta se generan valores aleatorios para *name* y *photoUrls*:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.011.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.011.png)

JSON Schema Faker tiene un conjunto de opciones de configuración predeterminadas. Dentro de una especificaion API, se puede un *x-json-schema-faker* donde configurar y cambiar alguna opción.

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.012.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.012.png)

<div id='request-validation'/>

#### 4.1.2. Request Validation
Prism puede hacer pruebas sobre todo tipo de reglas de validación para el cuerpo de la solicitud, encabezados, parámetros de consulta, usando palabras clave como, *type, format, maxLength*... También puede fallar devolviendo el código 401 si falta información de seguridad.
#### *Validacion de parámetros*
Se validarán las solicitudes que esperen un cuerpo de solicitud, un parámetro de consulta o un parámetro de ruta. Por ejemplo, haz un POST con un cuerpo JSON al que le falte el parámetro de nombre requerido.

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.013.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.013.png)

En este caso, Prism:

- Buscará una respuesta con código de estado 422 en la operación que estaba intentando ejecutar.
- Si no hay un 422 definido, buscará una respuesta con código de estado 400 en la operación que estabas intentando ejecutar.
- En caso de que no haya ni un 422 ni un 400 definido, Prism creará un código de respuesta 422 indicando los errores de validación que ha encontrado por el camino. Dicha respuesta tendrá una carga útil conforme a la especificación application/problem+json.

Dado que la operación no tiene definida ninguna respuesta de error, Prism generará una respuesta 422:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.014.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.014.png)

#### *Validación del servidor*
OpenAPI permite asociar toda la API, o determinadas operaciones, a servidores específicos. Para asegurarse de que la URL del servidor que se piensa utilizar es un servidor válido para la API, o para la operación concreta que está intentando realizar, se utiliza como parámetro de consulta *\_\_server*. A continuación, se ve un ejemplo:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.015.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.015.png)

Puede realizar una solicitud para hacer cumplir la validación del servidor:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.016.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.016.png)

Por otro lado, poniendo un servidor que no está definido en la especificación, conseguiremos que os muestre un mensaje de error 404 de que no ha encontrado dicho servidor.

<div id='validation-proxy'/>

### 4.2. Validation Proxy
Prism ayuda a verificar discreciones entre la implementación de su API y el documento de OpenApi que lo describe, lo que permite comprobar el **tráfico HTTP** a través del comando prism proxy.

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.017.png](../../../../assets/images/Aspose-3.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.017.png)

El proxy también se puede habilitar en el escenario o en cualquier otro entorno de preproducción, para garantizar que los documentos y el código de OpenAPI permanezcan sincronizados.

A diferencia de la simulación el proxy de validación espera que haya una API real ejecutándose en alguna parte. Esto podría ser un entorno de host local, un contenedor Docker…

La función proxy ayudara a identificar discrepancias o errores entre el documento OpenApi y cualquier otro servidor que se designe como destino. Esto puede ayudar a los desarrolladores **frontend** que se integran con su **API**, o a otros desarrolladores **backend**, que podrían querer canalizar sus solicitudes a través de Prism para ver si están realizando solicitudes válidas. El proxy también se puede habilitar en el escenario o en cualquier otro entorno de preproducción.

<div id='ayudar-integracion'/>

#### 4.2.1. Ayudar a la integración del consumidor de la API
Los consumidores de API pueden canalizar su tráfico de desarrollo a través de Prism ejecutándose como **Proxy** y luego retransmitir ese tráfico a la API en curso. Gracias a la validación por proxy conseguimos Informar de cualquier error que aparece en el camino, ya sea con las solicitudes que está enviando o las respuestas que regresan del servidor.

En este caso de uso, el equipo de API proporciona los documentos de OpenAPI, los distribuye a los consumidores de API y el **servidor Proxy** apunta al entorno de desarrollo. Además, se debe habilitar *–errors* para que Prism le avise si se detecta una discrepancia.

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.018.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.018.png)

<div id='pruebas-contrato'/>

#### 4.2.2. Pruebas de contrato extremo a extremo
Agregar pruebas de contrato a conjuntos de pruebas existentes ahora es fácil con Prism. Los equipos con suites de prueba de extremo a extremo existentes pueden colocar Prism en este entorno de prueba y cambiar algunas variables de entorno (o catálogo de servicios) para apuntar a **Prism Proxy**. Cada vez que la API A se comunica con la API B, o B con la C, pasará por C, por lo que, si alguna de las API realiza una solicitud no válida, todo el conjunto de pruebas puede fallar.

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.019.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.019.png)

Esto agrega pruebas de contrato a un conjunto de pruebas existentes, independientemente del idioma en el que estén escritas sus API, sin que se requieran cambios en las bases de código.

<div id='operaciones-no-implementadas'/>

#### 4.2.3. Las operaciones no implementadas serán simuladas
En caso de que el servidor responda con el código de estado 501 al realizar una petición, Prism intentará simular la llamada utilizando el documento OpenAPI provisto. Es decir, que simula una implementación de código a partir de lo que se especifica en la API.

<div id='operaciones-desuso'/>

#### 4.2.4. Operaciones en desuso
Si una operación está marcada como *deprecated: true*, Prism agrega como encabezado *Deprecation: true* a la respuesta, si la respuesta del servidor remoto aún no contiene ese encabezado.

<div id='mensajes-error'/>

## 5. Mensajes de error
Todos los errores que devuelve Prism se ajustan a RFC7807 - Detalles del problema para las API HTTP, lo que significa que siempre obtendrá un objeto JSON con las siguientes propiedades:

- type(cadena)
- title(cadena)
- status(número)
- detail(cadena)

<div id='errores-enrutamiento'/>

### 5.1. Errores de enrutamiento
Esta clase de errores se devuelven cuando Prism intenta identificar el recurso adecuado para responder a la solicitud HTTP proporcionada.

- NO\_BASE\_URL\_ERROR (400)
- NO\_RESOURCE\_PROVIDED\_ERROR (404)
- NO\_PATH\_MATCHED\_ERROR (404)
- NO\_SERVER\_MATCHED\_ERROR (404)
- NO\_METHOD\_MATCHED\_ERROR (405)
- NO\_SERVER\_CONFIGURATION\_PROVIDED\_ERROR (404)

<div id='errores-validacion'/>

### 5.2. Errores de validación
Esta clase de errores se devuelve cuando Prism valida la solicitud/respuesta con el archivo OpenAPI proporcionado.

- UNPROCESSABLE\_ENTITY (422)
- NOT\_ACCEPTABLE (406)
- NOT\_FOUND (404)
- VIOLATIONS (500)

<div id='errores-seguridad'/>

### 5.3. Errores de seguridad
Esta clase de errores se devuelve cuando la solicitud actual no cumple los requisitos de seguridad especificados en el recurso actual.

- UNAUTHORIZED (401)

<div id='errores-negociacion'/>

### 5.4. Errores de negociación
Esta clase de errores se devuelve cuando algo sale mal entre su solicitud válida y la devolución de una respuesta adecuada.

- NO\_COMPLEX\_OBJECT\_TEXT (500)
- NO\_RESPONSE\_DEFINED (500)
- INVALID\_CONTENT\_TYPE (415)

<div id='error-desconocido'/>

### 5.5. Error desconocido 
En caso de que obtenga un *UNKNOWN* error, probablemente significa que este caso extremo en particular no se maneja. Si encuentra uno de estos, abra un problema.

<div id='docker-compose'/>

## 6. Docker-compose
Una única instancia de Prism sirve un documento OpenAPI, pero es posible servir múltiples documentos ejecutando múltiples instancias de Prism en diferentes documentos, y luego entregando su contenido usando un Proxy inverso.

Puede utilizar cualquier proxy HTTP junto con una herramienta de gestión de procesos para lograrlo. El siguiente ejemplo explica cómo servir múltiples documentos OpenAPI usando Docker Compose.

En la siguiente imagen veremos un ejemplo de configuración de un archivo docker-compose.yaml:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.020.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.020.png)

Y el archivo Caddyfile correspondiente:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.021.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.021.png)

Estos dos archivos deberemos tenerlos en un mismo directorio para así poder ejecutarlos correctamente. Al tener la configuración de la url dentro del archivo caddyfile, se tienen dos puntos finales para poder probar las dos APIs configuradas. A partir de las siguientes URLs:

![Aspose.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.022.png](../../../../assets/images/Aspose-2.Words.8b59defa-4eeb-4ee0-974e-e4fa6ba78590.022.png)
