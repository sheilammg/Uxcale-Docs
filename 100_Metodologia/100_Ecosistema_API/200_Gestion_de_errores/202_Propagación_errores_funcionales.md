

# **Propagación de errores funcionales**
|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|24/02/2023|Axpe|Versión inicial.|



# Índice
[1. Gestión de errores API](#Gestion_errores)

[2. Tipos de errores y ejemplos](#Tipos_errores)
  - [2.1. Errores de cliente (4XX)](#Errores_cliente)
      - [2.1.1. Error 400	](#Error_400)
      - [2.1.2. Error 401	](#Error_401)
      - [2.1.3. Error 403	](#Error_403)
      - [2.1.4. Error 404	](#Error_404)
      - [2.1.5. Error 405	](#Error_405)
      - [2.1.6. Error 406	](#Error_406)
      - [2.1.7. Error 407	](#Error_407)
      - [2.1.8. Error 408	](#Error_408)
      - [2.1.9. Error 409 ](#Error_409)
      - [2.1.10. Error 411](#Error_411)
      - [2.1.11. Error 412](#Error_412)
      - [2.1.12. Error 413](#Error_413)
      - [2.1.13. Error 414](#Error_414)
      - [2.1.14. Error 415](#Error_415)
      - [2.1.15. Error 416](#Error_416)
      - [2.1.16. Error 417](#Error_417)
      - [2.1.17. Error 422](#Error_422)
      - [2.1.18. Error 423](#Error_423)
      - [2.1.19. Error 426](#Error_426)
      - [2.1.20. Error 428](#Error_428)
      - [2.1.21. Error 429](#Error_429)
      - [2.1.22. Error 431](#Error_431)
  - [2.2 Errores de servidor (5XX)](#Errores_500)
      - [2.2.1. Error 500	](#Error_500)
      - [2.2.2. Error 501	](#Error_501)
      - [2.2.3. Error 502	](#Error_502)
      - [2.2.4. Error 503	](#Error_503)
      - [2.2.5. Error 504	](#Error_504)
      - [2.2.6. Error 505	](#Error_505)

[Anexo I: Filtros no encontrado](#AnexoI)

<a id="Gestion_errores"></a>
# 1. Gestión de errores API
El equipo de Gobierno API será el encargado de llevar a cabo la gestión de la correcta representación de los errores derivados por los servicios Backend dentro de la compañía.

El objetivo de definir y aplicar un correcto uso de los errores desde la Oficina de Gobierno, y junto con los API Owner y desarrolladores, es mantener una claridad en el mensaje reportado por parte del producto API hacia la audiencia a la que va enfocado.

Se creará una la lista de los errores establecidos que serán almacenados en un repositorio único que será responsabilidad, en un primer inicio, por parte del equipo de la Oficina de Gobierno API. Teniendo la intención de luego difundir su implementación en las herramientas del equipo correspondientes.

En todos los errores, se seguirá la estructura definida en documento de Definición de estructura de errores.

**Código de buenas prácticas** 

- Las respuestas de las operaciones deben incluir todos los códigos posibles de error que devuelva el sistema. Como mínimo, siempre contemplan los siguientes errores: 
  - **401 Unauthorized**, los errores de autorización, aunque esta esté delegada en un proxy superior.
  - **403 Forbidden** los errores de control de acceso. 
  - **5XX** fallos internos del servidor.
- Resto de códigos http asociados a la funcionalidad y en función del tipo de recurso que se esté definiendo. 
- Los códigos devueltos deben indicar lo más específicos posibles, dentro del estándar HTTP.

Ejemplo: No hay que indicar un error 400 sí, en realidad podría ser un 401 (Unauthorized) porque las credenciales del usuario son incorrectas.

- No incluir aquellos códigos de error que **no** se van a implementar.
- No incluir en la respuesta de error de la invocación el código HTTP numérico dentro del error. Este ya se contempla en la cabecera de la respuesta HTTP.
- La descripción ofrecida por el error debe ser la justa para comprender el error.
- En los errores 500, no hay que ser muy descriptivo, debe ser una descripción genérica y se delegará al log las trazas y el detalle completo del error. En ningún caso, se emitirá información sensible, como queries de base de datos, ni información relativa a la implementación tecnológica y ni se indicará en la respuesta de la API.

<a id="Tipos_errores"></a>
# 2. Tipos de errores y ejemplos
En función de su origen, los errores se pueden contener en dos grupos, definidos por el código HTTP que se propagará (en base al estándar RFC 7231). Para tener más información sobre la estructura de error se podrá acceder al documento de Definición de estructura de error.

<a id="Errores_cliente"></a>
## 2.1. Errores de cliente (4XX)
Los responses tipo 4xx que no incluyan información sensible deben tratar de ser específicos. Se aconseja devolver un array de objetos de error ('messages') para poder cubrir los diferentes errores de entrada de datos de una vez.

### <a id="Error_400"></a>2.1.1. Error 400
**Caso de uso** El código de estado 400 indica que el servidor no puede o no procesará la solicitud debido a que se percibe un error por parte del cliente, como puede ser una petición incorrecta (por ejemplo, una sintaxis de solicitud malformada o un enrutamiento engañoso de la solicitud) o un error funcional.

**Implementación** En todos los métodos menos GET de un documento.
```json
{
  "messages": [
    {
      "code": "BAD\_REQUEST",
      "message": "Bad Request",
      "type": "ERROR",
      "description":  "The request is incorrect because the selected parameters are wrong or a functional error has occurred."
    }
  ]
}
```
### <a id="Error_401"></a>2.1.2. Error 401
**Caso de uso** No autorizado. La petición incluye clave/token caducados o incorrectos.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "UNATHORIZED",
      "message": "Unathorized",
      "type": "ERROR",
      "description":  "The call needs some kind of authorization either or not  reported"
    }
  ]
}
```
### <a id="Error_403"></a>2.1.3. Error 403
**Caso de uso** El código de estado 403 indica que el servidor entendió la solicitud pero se niega a autorizarla debido a que no se tienen permisos para ejecutar esa operación.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "FORBIDDEN",
      "message": "Forbidden",
      "type": "FATAL",
      "description":  "You do not have permissions to operate with this         invocation."
    }
  ]
}
```
### <a id="Error_404"></a>2.1.4. Error 404
**Caso de uso** El código de estado 404 indica que el servidor de origen no encontró una representación actual para el recurso que se está buscando.

Actualmente lo utilizamos en los filtros que no devuelven dato. Indicar el código que se propone utilizar en ese caso.

**Implementación** En los métodos GET, PUT, PATCH, DELETE Document.
```json
{
  "messages": [
    {
      "code": "NOT\_FOUND",
      "message": "Not Found",
      "type": "FATAL",
      "description":  "Resource not found."
    }
  ]
}
```
### <a id="Error_405"></a>2.1.5. Error 405
**Caso de uso** El código 405 indica que el método de la petición no está permitido para el recurso al que se quiere acceder.

**Implementación** En todos los métodos si se intentan utilizar para hacer una petición a un recurso que no la permite.
```json
{
  "messages": [
    {
      "code": "METHOD\_NOT\_ALLOWED",
      "message": "Method not allowed",
      "type": "ERROR",
      "description":  " The request method is known by the server but is not supported by the target resource."
    }
  ]
}
```
### <a id="Error_406"></a>2.1.6. Error 406
**Caso de uso** El código de estado 406 indica que el servidor no puede devolver los resultados en el formato especificado en la cabecera "Accept" de la petición.

**Implementación** Con todos los métodos, que, al realizar una solicitud, requieren un payload de respuesta en un formato que el servidor no puede proporcionar.
```json
{
  "messages": [
    {
      "code": "NOT\_ACCEPTABLE",
      "message": "Not acceptable",
      "type": "ERROR",
      "description": "The format indicated in the "**Accept**" header of the request is not supported by the destination server."
    }
  ]
}
```
### <a id="Error_407"></a>2.1.7. Error 407
**Caso de uso** El código de estado 407 indica que el formato indicado en la cabecera "Accept" de la petición, no es soportado por el servidor de destino.

**Implementación** Todos los métodos.
```json
{
  "messages": [
    {
      "code": "PROXY\_AUTHENTICATION\_REQUIRED",
      "message": "Proxy authentication required",
      "type": "ERROR",
      "description":  " The format indicated in the "**Accept**" header of the request is not supported by the destination server."
    }
  ]
}
```
### <a id="Error_408"></a>2.1.8. Error 408
**Caso de uso** El código de estado 408 indica que el servidor no ha recibido un mensaje de solicitud completo en el tiempo de espera establecido.

**Implementación** En cualquier método.
```json
{
  "messages": [
    {
      "code": "REQUEST\_TIMEOUT",
      "message": "Request Timeout",
      "type": "ERROR",
      "description": " The server has not received the complete request message within the set timeout period."
    }
  ]
}
```
### <a id="Error_409"></a>2.1.9. Error 409
**Caso de uso** El código de estado 409 indica que no se pudo completar la solicitud debido a un conflicto con el estado actual del recurso solicitado.

**Implementación** En los métodos PUT y POST.
```json
{
  "messages": [
    {
      "code": "CONFLICT",
      "message": "Conflict",
      "type": "FATAL",
      "description": " The request has not been completed due to a conflict with the current status of the resource."
    }
  ]
}
```
### <a id="Error_411"></a>2.1.10. Error 411
**Caso de uso** El código de estado 411 indica que el servidor se niega a aceptar la petición sin una definición de Content-Length.

**Implementación** Operaciones donde el campo Content-Lenght es obligatorio.
```json
{
  "messages": [
    {
      "code": "LENGTH\_REQUIRED",
      "message": "Length Required",
      "type": "FATAL",
      "description": " The server does not accept the request without a Content-Length definition."
    }
  ]
}
```
### <a id="Error_412"></a>2.1.11. Error 412
**Caso de uso** El código de estado 412 indica que una o más condiciones en los campos de la cabecera de la petición han sido evaluados como FALSO cuando se han analizado en el servidor.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "PRECONDITION\_FAILED",
      "message": "Precondition Failed",
      "type": "ERROR",
      "description": "One or more conditions in the fields of the request header have been evaluated as FALSE. "
    }
  ]
}
```
### <a id="Error_413"></a> 2.1.12. Error 413
**Caso de uso** El código de estado 413 indica que el servidor no está procesando la petición porque el payload es más largo de lo que realmente puede procesar. El servidor puede cerrar la conexión para evitar que el cliente continúe con la petición.

**Implementación** En todos los métodos que lleven un payload.
```json
{
  "messages": [
    {
      "code": "PAYLOAD\_TOO\_LARGE",
      "message": "Payload Too Large",
      "type": "FATAL",
      "description": "The size of the client request has exceeded the server's file size limit."
    }
  ]
}
```
### <a id="Error_414"></a>2.1.13. Error 414
**Caso de uso** El código 414 indica que el servidor no está procesando la respuesta porque la URI es demasiado larga.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "URI\_TOO\_LONG",
      "message": "URI Too Long",
      "type": "FATAL",
      "description": "The size of the client request has exceeded the server's file size limit."
    }
  ]
}
```
### <a id="Error_415"></a>2.1.14. Error 415
**Caso de uso** El código de estado 415 indica que el servidor de origen se niega a atender la solicitud debido a que el formato del cuerpo de la petición es incorrecto, no corresponde con el identificado en la cabecera "Content-Type".

**Implementación** En los métodos POST, PUT, PATCH Document, el payload de la solicitud se envía en un formato que no corresponde con el indicado en la cabecera "Content-Type".
```json
{
  "messages": [
    {
      "code": "UNSUPPORTED\_MEDIA\_TYPE",
      "message": "Unsupported Media Type",
      "type": "FATAL",
      "description": "Incorrect format of the response, does not match the one indicated in the "**Content-Type**" header."
    }
  ]
}
```
### <a id="Error_416"></a>2.1.15. Error 416
**Caso de uso** El código de estado 416 indica que se tienen rangos inválidos debido a que ninguno de los rangos en la petición concuerda con la extensión actual del recurso seleccionado.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "REQUEST\_RANGE\_NOT\_SATISFIABLE",
      "message": "Request range not satisfiable",
      "type": "ERROR",
      "description": "Invalid ranges due to none of the ranges in the request matching the current extent of the selected resource."
    }
  ]
}
```
### <a id="Error_417"></a>2.1.16. Error 417
**Caso de uso** El código de estado 417 indica que la cabecera de la petición no concuerda con ninguno de los servidores internos.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "EXPECTATION\_FAILED",
      "message": "Expectation Failed",
      "type": "ERROR",
      "description": "The request header does not match any of the internal servers."
    }
  ]
}
```
### <a id="Error_422"></a>2.1.17. Error 422
**Caso de uso** El código de estado 422 indica que estructuralmente la petición es correcta, pero no semánticamente.

**Implementación** En todos los métodos, cuando la solicitud está en un formato aceptado, la sintaxis es correcta pero no se puede procesar por el contenido, el valor de la solicitud.
```json
{
  "messages": [
    {
      "code": "UNPROCESSABLE\_ENTITY",
      "message": "Unprocessable Entity",
      "type": "FATAL",
      "description": "The structure of the request is correct, but it is not semantically correct."
    }
  ]
}
```
### <a id="Error_423"></a>2.1.18. Error 423
**Caso de uso** El código de estado 423 indica que el recurso al que se está intentado acceder está bloqueado.

**Implementación** En todos los métodos, al realizar una solicitud cuyo recurso está bloqueado.
```json
{
  "messages": [
    {
      "code": "LOCKED",
      "message": "Locked",
      "type": "ERROR",
      "description": "The resource you are trying to access is blocked."
    }
  ]
}
```
### <a id="Error_426"></a>2.1.19. Error 426
**Caso de uso** El código de estado 426 indica que no se procesa la petición con el protocolo actual, pero en caso de que el cliente actualizase a un protocolo diferente podría funcionar.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "UPGRADE\_REQUIRED",
      "message": "Upgrade required",
      "type": "FATAL",
      "description": "The request cannot be processed with the current protocol."
    }
  ]
}
```
### <a id="Error_428"></a>2.1.20. Error 428
**Caso de uso** El código de estado 428 indica una respuesta de precondición requerida. Es decir, que el servidor requiere que la petición sea condicional, por lo que se debe incluir la cabecera "If-Match". Se recomienda su uso para flujos como el SCA o bien, para firmas previas antes de la operación.

**Implementación** En todos los métodos que al realizar una solicitud se requiera que previamente se haya cumplido una condición.
```json
{
  "messages": [
    {
      "code": "PRECONDITION\_REQUIRED",
      "message": " Precondition\_Required",
      "type": "ERROR",
      "description": "The request to the server must be a conditional request."
    }
  ]
}
```
### <a id="Error_429"></a>2.1.21. Error 429
**Caso de uso** El código de error 429 indica que se han realizado muchas peticiones en un periodo de tiempo y se ha excedido el límite.

**Implementación** En todos los métodos que al realizar la solicitud se haya superado el límite de llamadas permitidas.
```json
{
  "messages": [
    {
      "code": "TOO\_MANY\_REQUESTS",
      "message": "Too Many Requests",
      "type": "ERROR",
      "description": "Too many requests in a given period of time and limit has been exceeded."
    }
  ]
}
```
### <a id="Error_431"></a>2.1.22. Error 431
**Caso de uso** El código de estado 431 indica que los campos de cabecera son demasiado largos, es decir, que la petición HTTP que el navegador está haciendo al servidor es demasiado grande.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "REQUEST\_HEADER\_FIELDS\_TOO\_LARGE",
      "message": "Request header fields too large",
      "type": "FATAL",
      "description": "The HTTP request being made to the server is too large."
    }
  ]
}
```
## <a id="Errores_500"></a>2.2 Errores de servidor (5XX)
En el caso de errores 5xx, no deben ser muy descriptivos, ya que se registrará en el log las trazas y el detalle completo del error. Nunca deben emitirse queries de BBDD, ni nada que dé información relativa a la implementación tecnológica subyacente.
### <a id="Error_500"></a>2.2.1. Error 500
**Caso de uso** El código de estado 500 indica que se ha producido un error inesperado, y el servidor no es capaz de dar respuesta sobre la petición realizada.  Es una respuesta genérica que no ha podido ser cubierta con otro código 5xx.

**Implementación** En todos los métodos cuando se lanza la solicitud y se genera una situación inesperada.
```json
{
  "messages": [
    {
      "code": "INTERNAL\_SERVER\_ERROR",
      "message": "Internal server error",
      "type": "FATAL",
      "description": "Unexpected error from the server, it has no way to respond to the invocation."
    }
  ]
}
```
### <a id="Error_501"></a>2.2.2. Error 501
**Caso de uso** El código de estado 501 indica que el servidor no soporta la funcionalidad que se requiere para dar respuesta a la petición.

**Implementación** En todos los métodos cuando se realiza una solicitud para la que todavía no está disponible la implementación que da la respuesta.
```json
{
  "messages": [
    {
      "code": "NOT\_IMPLEMENTED",
      "message": "Not Implemented",
      "type": "ERROR",
      "description": "The functionality is not supported by the service."
    }
  ]
}
```
### <a id="Error_502"></a>2.2.3. Error 502
**Caso de uso** El código de estado 502 indica que el servidor actúa como proxy o gateway y recibe de otro servidor una respuesta inválida, no pudiendo dar una respuesta coherente a la petición.

**Implementación** En todos los métodos que al realizar una solicitud, el servidor origen no puede resolver y el servidor que actúa como proxy propaga esta situación.
```json
{
  "messages": [
    {
      "code": "BAD\_GATEWAY",
      "message": "Bad Gateway",
      "type": "ERROR",
      "description": "Indicates that the server, while acting as a gateway or proxy, received an invalid response from an inbound service that it accessed while attempting to fulfill the request."
    }
  ]
}
```
### <a id="Error_503"></a>2.2.4. Error 503
**Caso de uso** El código de estado 503 indica que el servidor no está disponible para realizar la petición debido a que está sobrecargado o se están realizando tareas de mantenimiento.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "SERVICE\_UNAVAILABLE",
      "message": "Service unavailable",
      "type": "ERROR",
      "description": "Indicates that the server is unavailable to perform the request because it is overloaded or maintenance is being performed, and that it will probably be relieved after some time."
    }
  ]
}
```
### <a id="Error_504"></a>2.2.5. Error 504
**Caso de uso** El código de estado 504 indica que el servidor, mientras actuaba como puerta de enlace o proxy, no recibió una respuesta oportuna desde un servidor ascendente al que necesitaba acceder para completar la solicitud.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "GATEWAY\_TIMEOUT",
      "message": "Gateway timeout",
      "type": "ERROR",
      "description": "Indicates that the server, while acting as a gateway or proxy, did not receive a timely response from an upstream server it needed to access to complete the request."
    }
  ]
}
```
### <a id="Error_505"></a>2.2.6. Error 505
**Caso de uso** El código de estado 505 indica que el servidor no soporta la versión HTTP que se ha usado en la petición.

**Implementación** En todos los métodos.
```json
{
  "messages": [
    {
      "code": "NOT\_SUPPORTED",
      "message": "Not Supported",
      "type": "ERROR",
      "description": "The server does not support the HTTP version used in the request."
    }
  ]
}
```

# <a id="AnexoI"></a>Anexo I: Filtros no encontrados

En los casos en los que se realice un filtrado sobre un recurso concreto y dentro de ese recurso no haya ningún resultado con dicho filtro, se podrá devolver un código 200 vacío, ya que no se está encontrando el filtro que se está aplicando, pero el recurso en sí, sí que existe.

No es recomendable devolver un 404 debido a que el recurso si existe, y dicho código de error 404 se devuelve en los casos en los que no se encuentre el recurso que se está buscando, en este caso lo que no se está encontrado son las condiciones aplicadas al recurso, pero la petición en sí es correcta.

