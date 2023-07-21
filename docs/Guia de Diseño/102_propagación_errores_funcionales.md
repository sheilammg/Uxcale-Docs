# Propagación de errores funcionales
<!-- TOC -->

- [Propagación de errores funcionales](#propagaci%C3%B3n-de-errores-funcionales)
    - [1. Indice](#1-indice)
    - [2. Gestión de errores](#2-gesti%C3%B3n-de-errores)
    - [3. Tipos de errores y ejemplos](#3-tipos-de-errores-y-ejemplos)
        - [3.1. Errores asociados al cliente 4XX](#31-errores-asociados-al-cliente-4xx)
            - [3.1.1. Error 400](#311-error-400)
            - [3.1.2. Error 401](#312-error-401)
            - [3.1.3. Error 403](#313-error-403)
            - [3.1.4. Error 404](#314-error-404)
            - [3.1.5. Error 405](#315-error-405)
            - [3.1.6. Error 406](#316-error-406)
            - [3.1.7. Error 415](#317-error-415)
            - [3.1.8. Error 422](#318-error-422)
            - [3.1.9. Error 423](#319-error-423)
            - [3.1.10. Error 429](#3110-error-429)
        - [3.2. Errores asociados al servidor 5XX](#32-errores-asociados-al-servidor-5xx)
            - [3.2.1. Error 500](#321-error-500)
            - [3.2.2. Error 501](#322-error-501)
            - [3.2.3. Error 502](#323-error-502)
            - [3.2.4. Error 503](#324-error-503)

<!-- /TOC -->

## 1. Indice


## 2. Gestión de errores

El equipo de Gobierno API será el encargado de llevar a cabo la gestión de la correcta representación de los errores derivados por los servicios Backend. 

El objetivo de definir y aplicar un correcto uso de los errores desde la Oficina de Gobierno, y junto con los API Owner y desarrolladores, es mantener una claridad en el mensaje reportado por parte del producto API hacia la audiencia a la que va enfocado.

Se creará una la lista de los errores establecidos que serán almacenados 
en un repositorio único que será responsabilidad, en un primer inicio, por parte del equipo de la Oficina de Gobierno API.  Teniendo la intención de luego difundir su implementación en las herramientas del equipo correspondientes.

**Código de buenas prácticas**
- Las respuestas de las operaciones deben incluir todos los códigos posible de error que devuelva el sistema. Como mínimo, siempre contemplan los siguientes errores: 
  - **401 Unauthorized**, los errores de autorización, aunque esta esté delegada en un proxy superior.
  - **403 Forbidden** los errores de control de acceso.
  - **5XX** fallos internos del servidor.
  - Resto de codigos http aosciados a la funcionalidad y en función del tipo de recurso que se este definiendo.
- Los códigos devueltos deben indicar lo más específicos posibles, dentro del estándar HTTP.
  > Ejemplo: No hay que indicar un error 400 sï, en realidad podría ser un 401 (Unauthorized) porque las credenciales del usuario son incorrectas.
- No incluir aquellos códigos de error que nos se van a implementar.
- No incluir en la respuesta de error de la invocación el código HTTP numérico dentro del error. Este ya se contempla en la cabecera de la respuesta HTTP.
- La descripción ofrecida por el error debe ser la justa para comprender el error.
- En los errores 500, no hay que ser muy descriptivo, debe ser una descripción genénica y se delegará al log las trazas y el detalle completo del error. En ningún caso, se emitira información sensible, como queries de base de datos, ni información relativa a la implementación tecnológica y ni se indicara en la respuesta de la API.


## 3. Tipos de errores y ejemplos

En función del origen, los errores los contendremos en dos grupos, definidos por el código HTTP que se propagará, en base al estandar [RFC 7231](https://datatracker.ietf.org/doc/html/rfc7231#section-6.1).

### 3.1. Errores asociados al cliente (4XX)


#### 3.1.1. Error 400

**Caso de uso:** Petición erronea, los parámetros especificados en la invocación son incorrectos o se produce un error funcional.

**Implementación:** Todos los métodos, menos los GET de un documento.

```json
{
  "messages": [
    {
      "code": "badRequest",
      "message": "Request parameter does not meet the requirements.",
      "type": "ERROR",
      "description":  "The name must contain less than 50 characters."
    }
  ]
}
```

#### 3.1.2. Error 401

**Caso de uso:** Petición no autorizada, ya sea porque el token esta caducados o invalido.

**Implementación:** Todos los métodos.

```json
{
  "messages": [
    {
      "code": "unauthorized",
      "message": "Unauthorized to access the resource.",
      "type": "CRITICAL"
    }
  ]
}
```

#### 3.1.3. Error 403

**Caso de uso:** No tiene acceso o permisos para ejecutar la operación.

**Implementación:** Todos los métodos.

```json
{
  "messages": [
    {
      "code": "forbidden",
      "message": "Forbidden resource.",
      "type": "CRITICAL"
    }
  ]
}
```

#### 3.1.4. Error 404

**Caso de uso:** Recurso no encontrado, el identificador indicado no existe.

**Implementación:** Métodos GET, PUT, PATCH, DELETE Document.

```json
{
  "messages": [
    {
      "code": "notFound",
      "message": "Resource not found.",
      "type": "ERROR"
    }
  ]
}
```

#### 3.1.5. Error 405

**Caso de uso:** La petición no está permitido para el recurso al que se quiere acceder.

**Implementación:** Aquellos métodos que no tiene permisos a un recurso e intenta acceder.

```json
{
  "messages": [
    {
      "code": "methodNotAllowed",
      "message": "The requested resource does not support http method 'HEAD'.",
      "type": "ERROR"
    }
  ]
}
```

#### 3.1.6. Error 406

**Caso de uso:** Servidor no soporta el formato especificado en al cabecera "Accept" de la petición.

**Implementación:** Todos los métodos que necesitan que el payload de respuesta en un formato diferente al estandar y el serevidor no puede proporcionar.

```json
{
  "messages": [
    {
      "code": "notAcceptable",
      "message": "application/json is not supported.",
      "type": "ERROR"
    }
  ]
}
```

#### 3.1.7. Error 415

**Caso de uso:** El formato del cuerpo de la petición es incorrecto, el valor es diferente al indicado en la cabecera "Content-Type".

**Implementación:** Métodos POST, PUT, PATCH Document.

```json
{
  "messages": [
    {
      "code": "unsupportedMediaType",
      "message": "Only application/json is supported.",
      "type": "ERROR"
    }
  ]
}
```

#### 3.1.8. Error 422

**Caso de uso:** La estructura de la petición es valida, pero no semánticamente. La sitaxis es correcta pero no se puede procesar por el contenido, el valor de la solicitud.

**Implementación:** Todos los métodos.

```json
{
  "messages": [
    {
      "code": "unprocessableEntity",
      "message": "unprocessableEntity",
      "type": "ERROR"
    }
  ]
}
```

#### 3.1.9. Error 423

**Caso de uso:** Recurso de origen o destino de un método está bloqueado.

**Implementación:**  Todos los métodos.

```json
{
  "messages": [
    {
      "code": "locked",
      "message": "System blocked .",
      "type": "ERROR"
    }
  ]
}
```

#### 3.1.10. Error 429

**Caso de uso:** Se han invocado muchas peticiones en un periodo de tiempo y se ha excedido el límite.

**Implementación:** Todos los métodos que al realizar la solicitud se haya superado el límite de llamadas permitidas.


```json
{
  "messages": [
    {
      "code": "tooManyRequests",
      "message": "You exceeded the limit. Try again in an hour.",
      "type": "ERROR"
    }
  ]
}
```

### 3.2. Errores asociados al servidor (5XX)

En el caso de errores de la serie 5XX, se deben indicar descripciones genéricas y poco descriptivas, ya que se registrará en el log las trazas correspondiente y el detalle completo del posible error. En ningún caso, se debe informar de datos sentibles, como queries de BBDD, ni nada que dé información relativa a la implementación.

#### 3.2.1. Error 500

**Caso de uso:** Eror interno del servidor, es un error de tipo inesperado. El servidor no puede dar respuesta sobre la petición invocada. 

**Implementación:** Todos los métodos invocados que se genera una situación imprevista.

```json
{
  "messages": [
    {
      "code": "serviceError",
      "message": "Sorry, something has gone wrong.",
      "type": "ERROR"
    }
  ]
}
```

#### 3.2.2. Error 501

**Caso de uso:** El servidor no soporta la funcionalidad.

**Implementación:** Todos los métodos cuando se realiza una llamada pero que todavía no está disponible la implementación.

```json
{
  "messages": [
    {
      "code": "notImplemented",
      "message": "Server does not support the unctionality.",
      "type": "ERROR"
    }
  ]
}
```

#### 3.2.3. Error 502

**Caso de uso:** Servidor actúa como proxy o gateway y recibe de otro servidor una respuesta inválida, no pudiendo dar una respuesta coherente a la petición.

**Implementación:** Todos los métodos que el servidor origen no puede resolver y el servidor que actua como proxy propaga esta situación.

Ejemplo

```json
{
  "messages": [
    {
      "code": "badGateway",
      "message": "Service is not available.",
      "type": "ERROR"
    }
  ]
}
```

#### 3.2.4. Error 503

**Caso de uso:** Servidor no disponible debido a que está sobrecargado o se están realizando tareas de mantenimiento.

**Implementación:** En todos los métodos.

Ejemplo

```json
{
  "messages": [
    {
      "code": "serviceUnavailable",
      "message": "Server is currently unable to handle the request due to a temporary overload or scheduled maintenance. Please try again later",
      "type": "ERROR"
    }
  ]
}
```
