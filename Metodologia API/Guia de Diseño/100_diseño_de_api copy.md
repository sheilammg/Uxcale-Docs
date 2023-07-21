---
marp: true
author: Axpe Consulting
theme: gaia 
---


**Diseño de APIs**
## Índice
---
## 1. Introducción

El presente documento tiene como objetivo detallar una serie de Código de Buenas Practicas en torno al diseño de las APIs dentro de la compañia **Axpe Consulting**. El objetivo principal de dicho documento es homogeneizar y estandarizar su estructura para:

- Simplificar el consumo tanto por equipos internos de la compañía como proveedores externos.
- Facilitar la toma de decisiones en torno al diseño.
- Acelerar los proyectos de los diferentes equipos al hablar un lenguaje común.
---
### 1.1. ¿Qué es una API? 

Una API es una interfaz expuesta por un sistema para establecer una forma técnica y funcional de interacción con múltiples sistemas. Es un contrato y una vía de acceso que permite la interoperabilidad entre sistemas. Cumpliento las siguientes caracteristicas:

- Toda API debe tener expuesta una versión mock. Se trata de una versión de la API que se comporta como la real, pero carece de muchas características funcionales y no-funcionales, limitándose a responder con un conjunto de datos estáticos que simulan el comportamiento de la API real.
---
- Debe ser definida como un servicio REST, siempre que sea posible.
- Las APIs deben tener una correcta visualización (API Portal)
- Deben estar correctamente [versionadas](./101_versionado.md).
- El consumo de la misma debe estar manejado mediante permisos de las aplicaciones, planes de consumo y visibilidad de la misma.
- Debe estar definida utilizando un estándar: OpenApi 3.
- La definición debe estar desacoplada de la implementación.
- Diseño e implementación deben estar en inglés. 
- Documentación de la API pueden estar en español.
- Debe estar bien documentada y debe poderse consumir en base a su documentación.
---


## 2. Destinatarios

Equipos que contengan perfiles técincos y funcionales, con conocimientos a la hora de diseñar y especificaciones APIs, que hagan uso de una alguna plataforma API Management, como por ejemplo: Google APIGEE, Mulesoft Platform, Azure API Mangement, etc.





---
## 3. Pautas Generales

### 3.1. Estructura del documento
Un documento de OpenAPI pude estar formado por un solo documento o dividirse en varias partes conectadas a discreción del autor. En este último caso, se utilizan palabras clave Reference Objects y .Schema Object $ref

Se recomienda que el documento raíz de OpenAPI se llame: openapi.yaml.

---
### 3.2. Especificación

La especificación de una API indica un conjunto de prácticas, protocolos de comunicación y estructuras que definirán el contrato. Debido a que es un estándar, nos basaremos en la especificación OpenAPI.
La versión de OpenAPI debe ser la misma para todos las APIs en nuestro caso siempre se hará uso de la versión 3.X.

---
### 3.3. Idioma

Se establece el **inglés** como idioma para definir nuestras especificaciones APIs, es decir, todos los componentes necesarios desde la definición de URL, objetos, atributos hasta documentación asociada a los mismos (descripciones, ejemplos, etc).


---
### 3.4. Ejemplos

En la especificación API, se recomienda definir ejemplos en la request y la response, si tuvieran body, de cada operación y sólo a este nivel.
Ya que si cualquiera de los objetos que los componen, se modificase, sólo habría que actualizar estos ejemplos. Y no habría que acordarse tambien de los ejemplos de cada obejto y atributo donde se hubieran indentificado.

Por tanto, a nivel de especificación completa, no se recomienda identificar ejemplos a nivel de objeto completo, definido en la sección de "schemas". Ni a nivel de cada atributo que compone cada uno de los schemas. En caso de tratarse de un campo, en el que el ejemplo ayuda a entenderlo mejor, éste se deberá reflejar en la propia descripición del atributo.

Recomendado:

```yaml
paths:
  '/accounts/{accounttId}':
    parameters:
      - $ref: '#/components/parameters/AcceptLanguageHeader'
      - $ref: '#/components/parameters/XRequestIdHeader'
    get:
      parameters:
        - $ref: '#/components/parameters/AccountIdPathParam'
      tags:
        - Account
      description: Retrieve account information by id.
      operationId: getAccountsAccountId
      responses:
        '200':
          description: OK
          headers:
            X-Request-ID:
              $ref: '#/components/headers/XRequestIdHeader'
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/AccountResponse'
          examples:
            account-response:
              data:
                accounttId: a0001
                participants:
                  - userId: usr0001
                    name: John
                    surname: Doe
                    identification:
                      value: 31820431T
                      type: NIF
                balance:
                  amount: 15.45
                  currency: EUR
                iban: ES7921000813610123456789
        '400':
          $ref: '#/components/responses/BadRequest'
        '401':
          $ref: '#/components/responses/Unauthorized'
        '403':
          $ref: '#/components/responses/Forbidden'
        '404':
          $ref: '#/components/responses/NotFound'
        '500':
          $ref: '#/components/responses/InternalServerError'
```

No recomendado:

```yaml
components:
  schemas:
    Balance:
      title: Balance
      type: object
      description: Transaction amount.
      properties:
        amount:
          type: number
          description: Transaction amount.
          format: float
          x-faker: finance.amount
        currency:
          type: string
          description: String based on ISO 4217 to specify the transaction currency.
          x-faker: finance.currencyCode
      required:
        - amount
        - currency
      x-examples:
        example-balance:
          amount: 15.45
          currency: EUR
```

No recomendado:

```yaml
properties:
  amount:
    type: number
    description: Transaction amount.
    format: float
    x-faker: finance.amount
    example: 15.45
```

Recomendado:

```yaml
properties:
  amount:
    type: number
    description: Transaction amount. Example of value 15.45 .
    format: float
    x-faker: finance.amount
```

### 3.5. Extensión de Atributos
Aunque la estructura de la especificación está ya definida, si se requiere puede extenderse. Para ello, los atributos empezarán con “X-”.

> ejemplo: X-Api-Key

### 3.6. Estructura Objetos definidos
Así mismo, es necesario definir el atributo **title** para cada uno de los objetos definidos en la especificación, con el objetivo de que los validadores (Spectral) puedan reconocer dicho objeto y debe ser igual al objeto. A continuación se muestra un ejemplo de la definición completa de un objeto.

```yaml
Balance:
  title: Balance
  type: object
  description: Transaction amount.
  properties:
    amount:
      type: number
      description: Transaction amount.
      format: float
      x-faker: finance.amount
    currency:
      type: string
      description: String based on ISO 4217 to specify the transaction currency.
      x-faker: finance.currencyCode
  required:
    - amount
    - currency
  x-examples:
    example-balance:
      amount: 15.45
      currency: EUR
```

Este validador también revisará que exista una descripicón (**descripction**) y un resumen (**summary**) a nivel de operación y no a nivel de path.


### 3.7. Versionado

**Necesidad de versionado**

En la mayoría de las ocasiones, excepto en pocos casos y muy simples, una API tiende evolucionar a medida que cambian las necesidades de negocio, por ejemplo se agregan nuevas funcionales o nuevas operaciones sobre un recurso o modifican las existentes, la composición de los recursos pueden cambiar y la estructura del contenido en los recursos puede ser modificada.

Actualización de una API para gestionar requisitos nuevos o diferentes es un proceso relativamente fácil. El problema se centra, que aunque el desarrollador que diseña e implementa una API tiene control total de los recursos que se exponen, no tiene el mismo control en las aplicaciones consumidoras que pueden ser creadas por organizaciones de terceros.

Por tanto, el objetivo es permitir que las aplicaciones existentes sigan funcionando, y las nuevas aplicaciones aprovechen las nuevas características y recursos sin alterar el consumo de las aplicaciones previamente al los cambios. 

En el documento [_versionado_](./101_versionado.md) se detalla las mejores prácticas para el versionado de los servicios y muestra algunas consideraciones claves en el diseño, desarrollo, actualización y mejora de los servicios para facilitar la evolución compatible y resalta algunos enfoques para realizar el versionado de los mismos, para apoyar y hacer esta evolución y su complejidad más manejable.

## 4. Diseño

### 4.1. Definición de URIs
Las API REST utilizan identificadores de recursos uniformes (URI) para abordar los recursos. Los diseños de URIs realizados adecuadamente facilita el entendimiento de la funcionalidad del recurso de la API, tal como:

http://api.axpe.es/francia/paris/louvre/leonardo-da-vinci/mona-lisa

Un recurso diseñado incorrectamente, complicaría y sería muy difícil enterder su objetivo, como:

http://api.axpe.es/68dd0-a9d3-11e0-9f1c-0800200c9a66

### 4.2. Partes de la URL
Las normativas presentadas en esta sección pertenecen al formato estándar de una URI. [**RFC 6570**](https://datatracker.ietf.org/doc/html/rfc6570) (RFC 3986) define la sintaxis URI genérica como se muestra a continuación:

Esquema: 
    
> URI = scheme ": //" BaseURI "/" BasePath [ "?" query ] [ "#" fragment ]

Ejemplo de endpoint con el estándar URI:

![Estructura URL](./_images/scheme_url.png)

- **Scheme**: El esquema identifica el protocolo a usar para acceder a los recursos, puede ser HTTP (sin SSL) o HTTPS (con SSL).
    
- **BaseURI**: Formado por el hostname y el puerto. Así:
    - Hostname: Contiene el nombre del servidor.
    -	Puerto: Si no se informa se utilizará el por defecto para HTTP (80) y HTTPS (443). 

- **BasePath**: Prefijo de la URL para todos los paths relativos a la raíz del host. Formado por un contexto o path, la Major Version de la API, un resource y elementos pathParam que será el identificador asociados a la API.
    - *Major Version*: Llevará siempre un numérico, no decimal, a continuación a la letra v en minúscula
    - *Recurso*:  Nombre del recurso o recursos sobre el que se está operando. En caso de ser nombre compuesto, el formato será **kebab-case** y el plural no lo llevará nunca el primer sustantivo sino los siguientes a este ya que el primer sustantivo será complementario a los siguientes. Además, el nombre de este recurso ha de ser único, no puede coincidir con ningún otro ya que provoca un error en tiempo de despliegue.
      >Ej: /order-supplies, /product-prices, /product-stocks, /order-returns 

    -	*Path*: Es la ruta que identifica el recurso especifico en el host el cual el cliente consumidor quiere acceder, separando la estructura jerarquica de recursos con un barra (“/”).
    -	*Contexto*: En la jerarquia lógica de los recursos este sería el recurso padre.
    - *Versión*: Versión MAJOR. Parte del versionado semántico.
    - *Resource*: Es un recurso hijo, relacionado directamente con un recurso padre.
- **QueryString**: Es un componente opcional, se incluye a continuación del path y posee una estructura no jerárquica. Para identificar este elemento se utiliza el signo de interrogación (“?”). Proporciona una cadena de información que el recurso puede usar para algún propósito. Por ejemplo, parámetros de búsqueda o datos a ser procesados. 

  La query suele ser una cadena de pares de clave-valor(“key=argument”)separados uno del otro por un ampersand (“&”).

  Respecto la URL especifica para cada tipo y nivel de API tendríamos la siguiente estructura común:

  > https://{DNS}/{API_NAME}/v1/{RECURSO}

  **Nota:** Revisar la [Catalogación de las APIs](../../Oficina/catalogaci%C3%B3n_APIs.md) para ver cómo debe ser la nomenclatura de las mismas.


### 4.3. Modelado de los recursos

El componente path de la URI transmite un modelo de recursos de la API REST, cada segmento del path separado por barra inclinada (“/”) corresponde a un recurso único dentro del modelo de jerarquía. Por ejemplo, este diseño de URI:

>http://api.axpe.com/users/{userId}/adresses/{adressId}

Indica que cada una de estas URIs debería también identificar un recurso accesible

> http://api.axpe.com/users/{userId}/adresses/{adressId}

> http://api.axpe.com/users/{userId}

> http://api.axpe.com/users

> http://api.axpe.es

El modelado de recursos es un ejercicio que establece los conceptos clave de la API. Este proceso es similar al modelado de datos para un esquema de base de datos relacional o el modelado de un sistema orientado a objetos. 

- Los nombres de los recursos deben estar alineados con los nombres utilizados por negocio para los mismos. Utilizando como base la [ISO 20022](https://www.iso20022.org/standardsrepository).

- Los identificadores de los recursos son únicos para cada recurso.

- Los nombres de los recursos pueden tener varios niveles. Estas agrupaciones se deben asociar con cuidado, intentando no tener más de 2 o 3 niveles, y agrupando solo las relaciones de recursos “fuertes”.
  
  Incorrecto:
  ```
  /users/1244/addresses/123/country/5/city/555/population/5568
  ```
  Correcto:
  ```
  /users/1244/addresses
  ```
- Se debe utilizar siempre un sustantivo plural para recopilar y almacenar nombres de recursos 
  
- Los recursos deben ser nombres, no verbos. Los recursos son entidades sobre las que actuamos, la acción ya viene definida por el verbo HTTP utilizado.

  Incorrecto:
  ```
  /users/v1/get-users
  ```
  Correcto:
  ```
  /users/v1/users
  ```

- No utilizar mayúsculas, las url son case sensitive.
- Utilizar, preferiblemente, kebab-case

  ```
  https://api.axpe-consulting.com/my-profile/v1/users
  ```

- No mencionar a herramientas o referencias tecnologicas como bases de datos o plataformas a la hora de nombrar el recurso.

  Incorrecto:

  ```
  /users/v1/users-db
  /users/v1/users-mongo-db
  ```

- Intentar nombrar los recursos con nombres concretos, explicativos y cortos. Por ejemplo, un coche de alquiler podría ser “/renting-car” en vez de “/cars”. Esto hará que sean más fácil de recordar y utilizar por el usuario.

- No terminar un recurso con "/". Si se hace esto y tenemos definidos:

  Incorrecto:
  ```
  /users/{userId}/
  ```
Al hacer una petición sobre el recurso /users/{userId}/addresses también cumpliríamos el patrón del recurso superior y se ejecutarán ambos.

- Las extensiones de los archivos no deben estar presentes en la URI.
  Incorrecto:
  ```
  /v1/product-prices.json
  ```

- Cuando sea necesario el versionado de la API, el número de versión debe incluirse en la URI como prefijo. Una API se versiona sólo cuando el cambio no es compatible hacia atrás.

- El versionado basado en URL se utiliza para simplificar el uso de los consumidores de API, en comparación con los enfoques más complejos basados en campos de cabecera.
- En general, un número de versión que sigue el concepto de versión semántica tiene la estructura: **vMajor**
  >Plantilla de URI: /v{Major}/
  ```
  Ejemplo: POST /v1/product-prices/stores/3455/product
  ```
- La misma operación utilizando la versión 2 de la API
  ```
  Ejemplo: POST /v2/product-prices/stores/3455/product
  ```

### 4.4. Path Params

Un path param es un identificador único del recurso. Por ejemplo:

```
/users/{userId}
```

Pueden ponerse varios path param en caso de existir una ruta lógica de recursos dependientes entre sí.

```
/users/{userId}/documents/{documentId}
```

#### 4.4.1. Código de Buenas Prácticas

- No se pueden concatenarse path params. Un path param debe ir precedido del recurso que representa. Si hiciésemos esto la URL quedaría incomprensible:

  Incorrecto:
  ```
  /users/{userId}/{documentId}
  /users/13225365/647658
  ```

  Correcto:
  ```
  /users/{userId}/documents/{documentId}
  ```

- El atributo debe ser identificativo en si mismo, no es suficiente con un "{id}". La razón radica en que si este recurso se “amplía” en el futuro e incluye otros identificadores, no sabríamos a cuál de las entidades se refiere el parámetro {id}. Por ejemplo:

  Incorrecto:

  ```text
  /users/{id}/documents/{id}
  ```

  Correcto:

  ```text
  /users/{userId}/documents/{documentId}
  ```

- Se aconseja que el identificador tenga una morfología similar a la entidad correspondiente.Por ejemplo, “xxxxId”, siendo xxx el nombre de la entidad a la que referencia:

  ```
  /users/{userId}
  /accounts/{accounttId}
  /vehicles/{vehicletId}
  /users/{userId}/vehicles/{vehicletId}
  ```

- Cuidado con crear ambigüedades en las URI a la hora de definir paths. Por ejemplo, si la entidad "user" puede identificarse por dos identificadores únicos y crearemos dos URI

  ```
  /users/{userId}
  /users/{nif}
  ```

  al invocar a nuestra API se elegiría una de las opciones y no podríamos distinguir cual se ha elegido.

- Las APIs no deben utilizar los números de secuencia generados por la base de datos como identificadores de recursos.

- Los valores enumerados pueden utilizarse como identificadores de recursos.



### 4.5. Parámetros de consulta (Query Params)

Los parámetros de consulta son pares de clave-valor que se especifican después de la sección de ruta de una URI, tal como se define en [RFC 3986](https://datatracker.ietf.org/doc/html/rfc3986) y sirven para filtrar, ordenar y paginar.
Se preceden de "?" y se pueden concatenar con "&".

```
/users?name=juan&surname=perez
```

#### 4.5.1. Código de Buenas Prácticas

- **Obligatoriedad**

  - En general suelen ser atributos opcionales, aunque en ocasiones pueden ser obligatorios.
  - Relacionado con lo anterior: a veces se necesita que al menos uno o varios parámetros de búsqueda sean obligatorios por una cuestión de eficiencia de la consulta o por el tipo de consulta en sí. En este caso se indicará en la description del propio método GET y se controlará que esos datos se envian. Si no se cumple habrá que devolver un error 400 desde el backend.
  - Únicamente se utilizaran en los mensajes de solicitud GET o HEAD. Para los recursos en los que la respuesta del servidor a una solicitud POST soporta la paginación, los parámetros de consulta de paginación pueden ser proporcionados con solicitudes POST

- **Definición**

  - En notación camelCase.
  - Incluir una "description" que indique el significado del parámetro
  - Incluir un "example" que indique un valor real que podría utilizarse.
  - Cada parámetro debe estar escrito igual que el objeto del modelo buscado. Ejemplos:

  Petición:

  ```text
  GET /users?name=Juan&surname=Perez&birthDate=1987-11-17
  ```

  Respuesta:

  ```json
  {
    "data": [
      {
        "id": "1234",
        "name": "Juan",
        "surname": "Perez",
        "birthDate": "1987-11-17"
      }
    ]
  }
  ```

- **Tipos de datos**
  - Es recomendable que los parámetros tengan el tipo más específico posible. Por ejemplo, usar enumerados cuando sea posible, o format=date en caso de fechas.

- **Limitadores**

  - Cuidado con los tipos string. Ponerlos obligatorios no implica que no puedan enviarse como una cadena vacía. Poner un minLength: 1 si en realidad son obligatorios y no pueden incluirse vacíos.
  - También se debe especificar un maxLength si lo tiene el modelo que consumimos para ser mas restrictivos.

  ```yaml
  schema:
    type: string
    minLength: 1
    maxLength: 20
  ```

  - Si un atributo string es obligatorio no tiene sentido poner un minLength: 0.
  - Si un número no puede ser negativo incluir un minimum: 0.

  ```yaml
  in: query
      name: age
      description: user age
      required: false
      schema:
          type: integer
          format: int32
          minimum: 0
          example: 18
  ```

- **Valores por defecto**

  - Si tenemos un comportamiento en que un valor es obligatorio (por ejemplo un paginado), podemos hacer que el atributo sea opcional y tener un valor por defecto establecido. Así se aligera el API y se hace “obligatorio” un campo.

    ```yaml
    in: query
    name: limit
    description: The number of items to return.
    required: false
    schema:
      type: integer
      minimum: 1
      maximum: 100
      default: 20
    ```

  - Un path param con un valor default no tiene sentido que sea required: true.
  - Su uso debe usarse solo con el propósito de restringir una búsqueda o filtrado de un recurso.


- **Clasificacion Filtros** (REVISAR)

QueryString | Descripción
---------|----------
fields  | Permite seleccionar los campos que se desean recuperar del recurso. Campos separados por el carácter ‘,’, https://api.axpe.com/v1/namespace/resource/{resource_id}?fields=field1,field2
expand  | Este campo permite al usuario solicitar información sobre las  sub-entidades que desea expandir Sub-entidades separadas por el carácter ‘,’.  https://api.axpe.com/v1/namespace/resource/{resource_id}?expand=sub-entity1. <br><br>Por razones de complejidad, solo se recomienda el uso con sub-entidades de primer nivel.|
isDescription | Estos parámetros deben ser opcionales, debe reportarse como boolenos. El campo se utilizará cuando la operación deba devolver los datos como códigos en lugar de descripciones traducidas.|
sort | Permite ordenar los resultados obtenidos, ascendente "+" o descendente "-" por los criterios definidos por API Designer.<br><br>Ejemplo: GET /customers/ {customer_id}?_sort=+last_name. Los campos estarán separados por el carácter ",". <br><br>**NOTA**: Por motivos de complejidad, solo es válido para entidades.|
\<attribute> | En algunos casos los identificador del URI puede tener múltiples valores, se agrega un parámetro a QueryString con el nombre del campo del identificador que informa el tipo de datos que se utilizará.https://api.axpe.com/v1/namespace/resource/{resource_id}?resource_type=value|
query | Son aquellos casos en los que se desea permitir un número elevado de campos \<attribute>, este permitimos agruparlos en un único, que contendrán el json codificado en Base64 que contendrá todos.<br><br>Por ejemplo, para una petición GET https://api.axpe.com/v1/namespace/resource/{resource_id}?resource_type1=value1&resource_type2=value2&resource_type3=value3. <br><br>Se codificaría el json:<br> <pre><br>{<br>“resource_type1”: “value1”,<br>“resource_type2”: “value2”,<br>“resource_type3”: “value3”<br>} <br> ewogICDigJxyZXNvdXJjZV90eXBlMeKAnTog4oCcdmFsdWUx4oCdLAogIOKAnHJlc291cmNlX3R5cGUy4oCdOiDigJx2YWx1ZTLigJ0sCiAg4oCccmVzb3VyY2VfdHlwZTPigJ06IOKAnHZhbHVlM+KAnQp9Cg==</pre> Pudiendo hacer la llamada GET: <br>https://api.Axpe.com/v1/namespace/resource/{resource_id}?query= ewogICDigJxyZXNvdXJjZV90eXBlMeKAnTog4oCcdmFsdWUx4oCdLAogIOKAnHJlc291cmNlX3R5cGUy4oCdOiDigJx2YWx1ZTLigJ0sCiAg4oCccmVzb3VyY2VfdHlwZTPigJ06IOKAnHZhbHVlM+KAnQp9Cg== <br><br>Existiran casos en lo que seguir este esquema pueda violar límites en cuanto a longitud de URL, consultar con el Área de Arquitectura para acometer el problema con otras técnicas.
format | Permite informar el formato de la respuesta de la API.<br>Solo debe ser utilizado para HATEOAS.Permite informar el formato de la respuesta de la API.Solo debe ser utilizado para HATEOAS. <br> <br> **NOTA**: Ver más detalles en la sección "Diseño de encabezado HTTP". <br>Ejemplo: GET /clientes?format=pdf <br> <br> **NOTA**: Ver más detalles en la sección "Diseño de encabezado HTTP". <br> Ejemplo: GET /clientes?_formato=pdf|

### 4.6. Nomenclatura

Otro de los aspectos a establecer dentro de la nomenclatura de las APIs es el nombre y formato de los campos de entrada y salida de las peticiones HTTP.


#### 4.6.1. Formatos

- Todas las menciones de JSON son una referencia al formato [JSON](https://datatracker.ietf.org/doc/html/rfc7159).
- Las cadenas de formato de fecha (sólo fecha, fecha y hora y timestamp) deben cumplimentar el estandar ISO 8601 tal como se indica en la [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3339).
- Las campo que hagan referencias a código de tipo moneda se expresarna como indica el estandar (3 dígitos), [ISO-4217](https://es.wikipedia.org/wiki/ISO_4217)
-Los atributos asociados al código de país se expresaran como indica el estandar, con un código de 2 dígitos, [ISO-3166-1](https://es.wikipedia.org/wiki/ISO_3166-1#C%C3%B3digos_ISO_3166-1).
- Código de lenguajes, [ISO 639-1](https://www.iso.org/iso-639-language-codes.html)

#### 4.6.2. Estructura del cuerpo del mensaje

Por defecto, se define, que el formato debe ser [JSON](https://datatracker.ietf.org/doc/html/rfc7159). Aunque en algunos casos es posible que sea necesario definir otros formatos o mediaTypes según la funcionalidad del recurso.

Debe usarse un capa denotado como "data" en la salidas de los JSON:

- Pertenecen a verbos GET, pues es facil que incluyan o puedan incluir paginación.

- Que necesiten información adicional no relacionada con el propio objeto (por ejemplo, metadatos de negocio).

- El uso de este envoltorio, facilita la agrupación y estructuración de la información de respuesta y facilita la distinción la información de negocio y la de paginación.

- No debe utilizarse a la entrada de las peticiones.
  
  **Estructura de la petición**:
    ```json
    {
        ... atributos del recurso ...
    }
    ```
  **Estructura de la respuesta**:
  ```json
  {
      "data": {
           ... atributos del recurso ...
      },
      "pagination" :{
          ... atributos paginación ...
      },
      "metadatos":{
           ... atributos metadatos ...
      }
  }
  ```


#### 4.6.3. Atributos

- Los atributos tal y como se ha especificado en el documento deben ir en **inglés** y en notación **lowerCamelCase**.

- El nombre seleccionado debe ser lo más explícito posible, debe ser legible y autoexplicativo de forma que simplemente viendo el JSON sea comprensible sin tener que recurrir a la documentación. Utilizando como base la [ISO 20022](https://www.iso20022.org/standardsrepository). 
  >Ejemplo: Entre number y phoneNumber, phoneNumber es mucho más explícito.

- El valor de los atributos **enumerados** también debe ser legibles y autoexplicativos. Se recomienda establecer un formato único, para que sean fácilmente identificables en el JSON. Deberán ir en inglés y siempre en mayúscula. 
  > Ejemplo un campo status:<br>- status: 0,1,2 No está bien definido, no se sabe a qué equivalen esos valores.<br>- status: OK, FAILURE, PROCESSING Sí está bien definido, los valores son legibles y no es necesario recurrir a la documentación.

- El nombre de los atributos **booleanos** debe indicar claramente a qué hace referencia, tener preguntas de sí/no como nombre, cuuando su valor es true o false
  >Ejemplo sería: **isFinished**.
  <br>Y por tanto aquellos atributos que correspondan con una respuesta _**"S"**_, _**"N"**_, deben modelarse como un boleano, así de esta forma el desarrollador sin ver el tipo de campo puede saber qué se trata de un tipo booleano.

- Se debe especificar y ser restrictivo lo máximo posible a la hora de definir el tipo del campo.
  > Ejemplo, un atributo que representa una fecha debe ser un tipo [date](https://datatracker.ietf.org/doc/html/rfc3339).

- Los nombres de los atributos que sean identificadores únicios se acompañará en nombre con la palabra **Id** y no code.
  
  Incorrecto:

  ```json
  {
    "id": "number",
    "code": "integer"
  }
  ```

  Correcto:

  ```json
  {
    "userId": "number",
    "documentId": "integer"
  }
  ```

- Todos los campos de tipos de arrays deben ser nombrados como sustantivos plurales, por lo tanto, los tipos de objetos deben ser nombrados como sustantivos singulares.


#### 4.6.4. Coherencia en el diseño del recurso

El recurso debe verse como un todo o una caja negra, en la que en función del método HTTP nos comunicamos de una forma u otra, pero la información que se maneja dentro de dicha caja es siempre idéntica y con la misma estructura.

De esta forma a la hora de diseñar el recurso para que sea **coherente** se debe tener en cuenta lo siguiente:

- Independientemente del método HTTP utilizado los atributos simples que se refieren al mismo concepto deben llamarse igual. En el caso de objetos y arrays deben tener la misma estructura de información y obligatoriedades.

- Es posible que la respuesta del GET de un detalle (document) contenga más información que el GET de una lista (collection). Al revés no es posible, si un atributo existe en el listado debe existir en el detalle y contener la misma información y estructura.

- Es posible que los atributos necesarios para crear un recurso (POST) sean menos que los que forman parte del recurso (GET), ya que algunos se calculan o autogeneran.

- En caso de devolver la información de un recurso, independientemente del método, se envían todos los atributos del recurso.
 

### 4.7. Cabeceras 

Cabecera | Descripción 
---------|----------
Accept-Language (deseable) |	El consumidor solicita la lista de idiomas por orden de preferencia.
Content-Language (deseable)|	El servidor responde con el idioma de la respuesta
Authorization| Campo para enviar el token de acceso al API (OAuth, JWT)
If-None-Match (en caso de necesidad) |	Obtiene los datos cacheados siempre que le ETag no hayan cambiado
If-Match (en caso de necesidad) |	Utilizado para solicitudes de modificación de servicios. Permite realizar cambios solo si ningún otro cliente ha realizado ningún otro cambio durante la ejecución.
ETag (en caso de necesidad)|	Campo utilizado en el proceso de acceso/modificación de recursos cacheados
Accept (deseable)	| El consumidor solicita el formato de datos de la respuesta.
Content-Type |	El servidor responde con el formato de los datos de respuesta
Location |	El servidor devuelve tras un POST la URL del recurso recién creado.
X-Request-ID **\*** | Identificador único de mesaje. La especificación de este UUID segurirá el formato de la norma [RFC-4122](https://www.ietf.org/rfc/rfc4122.txt)


**\*** Para facilitar la búsqueda y filtrado de las solicitudes en los sistemas de logs, como kibana, se recomienda definir o usar un prefijo de no más de cuatro caracteres **“XXXX”** donde se indique el tipo y el significado de la petición. Además, todas las respuestas deberán informar dicho campo de cara a poder tener una trazabilidad completa de petición-respuesta. 

Este prefijo deberá estar informado a nivel de Operation ID.

Por ejemplo:

  - Cambio o modificación de precio de venta “URRP” Update Recommended Retail Price.

  - Borrado de precio de venta “DRRP” Delete Recommended Retail Price.

  - Consulta de albarán de entrega “RDN” Read Delivery Note
  
  - Creación de un albarán de entrega “CDN” Create Delivery Note

> Ejemplo: RDN-732d6a23-816-4042-b2e3-ba15b7d8f490

### 4.8. Métodos 

La mayoría de las funcionalidades de negocio pueden caer dentro de las acciones CRUD estándar (Crear, Leer, Actualizar, Eliminar) y su mapeo a los métodos estándar y extendidos de HTTP.

Los métodos HTTP son los siguientes:

Método HTTP | Descripción
----------- | -----------
**GET** |  Recupera la representación de un recurso (único o colección).
**POST**|  Puede crear un recurso o ejecutar una acción completa y arbitraría en un recurso.
**PUT** |   Crea (si no existe) o edita (si existe) totalmente un recurso.
**DELETE**|   Eliminar un recurso único o los recursos contenidos en una colección (nunca la propia colección).
**PATCH** |   Actualización parcial de un recurso o colección de recursos.
**HEAD** |   Recupera los meta-datos (cabeceras) asociados a un recurso, su comportamiento es similar a GET, excepto que no se devuelve ningún contenido en el body.
**OPTIONS** |   Recupera la información sobre los métodos HTTP permitidos para un recurso.
**TRACE** |   Utilizado para debuggear.

El uso de estos métodos debe ser consistente con la semántica, para ello se aplica la sección [4.3 de la RFC-7231](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3) y la [RFC-5789](https://datatracker.ietf.org/doc/html/rfc5789).


#### 4.8.1. Idempotencia y método seguro

- **Idempotencia**
    Un método HTTP es *idempotente* si, tras invocarlas varias veces sobre un mismo recurso, el estado de ese recurso no cambia en el servido, aunque ela respuesta del mismo podrá ser diferente.

    Ejemplo con el método DELETE. Si hacemos una operación DELETE sobre un recurso

    `DELETE /users/79897987`<br> Se borrar la entidad indicada y nos devolvera un respuesta 204 (Not content) indicando que se ha borrado satisfactoriamente. Si volvemos a invocar esta operación, en este caso se devolvera un código HTTP 404. Como podemos ver, la respuesta diferente, pero el recurso queda en el mismo estado (no existe).

  **NOTA**: *Todas* las operaciones GET, PUT y DELETE siempre se comportaran de forma idempotente. Si existen efectos secundarios, esto nos indicara que se esta gestionando una mala implementación de nuestras APIS.
  
  Para ello se seguirá la sección [4.2.2 de la RFC-7231](https://datatracker.ietf.org/doc/html/rfc7231#section-4.2.2) donde se define el concepto de idempotencia. 

- **Método seguro**

  Los métodos seguros son aquellos que en su semántica definda, principalmente los de lectura, no producen efectos o cambios sobre el recurso en el destino.  En cualquier caso, se aplica la definición de *Método Seguro* de la sección [4.2.1 de la RFC-7231](https://datatracker.ietf.org/doc/html/rfc7231#section-4.2.1).

-  **RESUMEN** 

    | **Operación** | **Uso**                     | **Idempotente** | **Seguro** |
    | ------------- | --------------------------- | --------------- | ---------- |
    | GET           | Consulta recurso            | Si              | Si         |
    | GET           | Consulta colección recursos | Si              | Si         |
    | POST          | Crear                       | No              | No         |
    | POST          | Operación                   | No              | No         |
    | PUT           | Actualizaciones completas   | Si              | No         |
    | PATCH         | Actualizaciones parciales   | Si              | No         |
    | DELETE        | Borrar                      | Si              | No         |
    | OPTIONS       | Info de método              | Si              | No         |
    | HEAD          | Info de recurso             | Si              | Si         |
    | TRACE         | Debug                       | Si              | No         |


#### 4.8.2. Arquetipos REST

Al modelar los recursos de una API, se puede tomar como base algunos arquetipos de recursos básicos. Al igual que los patrones de diseño, los arquetipos de recursos nos ayudan a comunicar las estructuras y comportamientos que se encuentran comúnmente en los diseños de una API REST. Se componen de cuatro arquetipos de recursos distintos: **Document**, **Collection**, **Store** y **Controller**.

Para Comunicar un modelo de recursos claro y limpio a los clientes, una API REST debe clasificar cada recurso con solo uno de estos arquetipos, para lograr uniformidad lo deseable es evitar diseñar recursos híbridos de más de un arquetipo. En su lugar se debe priorizar en lo posible el diseño de diferentes recursos que estén relaciones jerárquicamente.

A continuación se describen los diferentes arquetipos:

- **Document**:

  Un recurso de tipo document es un concepto similar a una instancia de objeto o registro de base de datos. La representación de estado de un documento normalmente incluye ambos campos con valores y enlaces a otros recursos relacionados. Con su campo fundamental y su estructura basada en enlaces, el tipo document es el arquetipo base de los otros arquetipos de recursos (collection, store y controller).

  En otras palabras, los otros tres arquetipos de recursos pueden verse como especializaciones del arquetipo document.

  Cada siguiente URI de ejemplo identifica en negrita un recurso del tipo document:
  
  > GET http://api.axpe.es/ligas/**inglesa** <br>
  > GET http://api.axpe.es/ligas/**inglesa**/equipos/**liverpool** <br>
  > GET http://api.axpe.es/ligas/**inglesa**/equipos/**liverpool**/jugadores/**georginio**
  
    
  Un recurso del tipo documento puede tener recursos hijo que representan sus conceptos subordinados específicos. Con su capacidad de reunir muchos tipos de recursos diferentes en un solo padre, un documento es un candidato lógico para ser un recurso raíz.

- **Collection**:

  Un recurso de tipo Collection es un directorio (listas) de recursos administrado por el servidor. Los clientes pueden proponer nuevos recursos para ser agregados a una colección, sin embargo, depende de la colección elegir crear el nuevo recurso o no. 

  Un recurso de colección elige lo que quiere contener y también decide los URIs de cada recurso contenido.

  Cada siguiente URI a continuación identifica negrita un recurso del tipo collection:
 
  > GET http://api.axpe.es/**ligas** <br>
  > GET http://api.axpe.es/**ligas**/inglesa/**equipos** <br>
  > GET http://api.axpe.es/ligas/inglesa/equipos/liverpool/jugadores
  
- **Store**:

  Una store es un repositorio de recursos administrado por el cliente. Un recurso de tipo store permite a un cliente guardar recursos en una API, sacarlos de nuevo, y decidir cuándo eliminarlos. Por su cuenta, las store no crean nuevos recursos; por lo tanto una store nunca genera nuevas URIs.

  En su lugar, cada recurso almacenado tiene una URI que fue elegido por un cliente cuando se colocó inicialmente en la store.

  La siguiente interacción de ejemplo muestra a un usuario (con ID 1234) de cliente usando una API REST de fútbol, para insertar un recurso de tipo document llamado alonso en su store de favoritos:

  > PUT  /usuarios/1234/**favoritos**/alonso

  Este otro ejemplo muestra una inserción de una publicación (con el ID 2233) del tipo documento en la store de publicaciones

  > PUT  /**publicaciones**/2233

- **Controller**:

  Los recursos de tipo controller son como funciones ejecutables, con parámetros y valores de retorno; entradas y salidas. Al igual que el uso de formularios HTML en una aplicación web tradicional, una API REST  usa un recurso del tipo controller para realizar acciones específicas de la aplicación que no pueden asignarse lógicamente uno de los métodos estándar CRUD (create, replace, update y delete).

  Los controller suelen aparecer como el último segmento en una ruta URI, sin recursos hijos para seguirles en la jerarquía. El siguiente ejemplo muestra en negrita un recurso controller que permite a un cliente reenviar una alerta a un usuario:

  > POST  /alertas/245743/**resend**
    
  Este otro ejemplo muestra a un cliente ejecutando la acción de checkout en un carrito de compras:

  > POST  /carrito-de-compras/3378/**checkout**

#### 4.8.3. GET

**Escenarios:**

Verbo asociado a la consultar, ya sea de un recurso o colección de recursos.
Se identifican dos tipos de llamadas:

- Tipo Document, un único recurso:

  > GET /users/{userId}

- Tipo "Collection o Store", un conjunto de recursos. Estas pueden tener asociados query parameters (filtros).

  > GET /users <br> 
  > GET /users?name=Juan&surname=Castaño
  

**¿Qué retorna?**
1. Un  GET de tipo document,es decir, un único recurso: devolverá un recurso específico, correspondiente al identificador deseado. <br><br>Ejemplo de solicitud correcta:

    |             | **Solicitud**       | **Respuesta**    |
    | ----------- | ---------------     | -----------------|
    | **Recurso** | GET /users/23452345 |                  |
    | **Header**  |                     | 200 OK           |
    | **Payload** |                     | { <br>&nbsp;&nbsp;&nbsp;&nbsp;"data": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "23452345",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"surname": "Castaño",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"secondSurname": "Castaño"<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |

- Si existe el recurso, devolverá la información asociada en el payload y en la cabecera un código HTTP 200 de petición "exitosa".

- Si no existe (userId) indicado en la llamada, devolverá un 404 indicando que el objeto no fue encontrado.

- **RECOMENDACIÓN**: Se sugire devolver solamete información de un recurso, sin metainformación, a no ser que sea esencial.


2. Un GET de un conjunto de recursos (“collection o store”) devolverá una lista de resultados. Por ejemplo:

|             | **Solicitud** | **Respuesta**  |
| ----------- | -----------   | ------------- |
| **Recurso** | GET /users    |               |
| **Header**  |               | 200 OK        |
| **Payload** |               | {<br>&nbsp;&nbsp;&nbsp;&nbsp;"data": [<br>&nbsp;&nbsp;&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "245345235234",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"surname": "Castaño"<br>&nbsp;&nbsp;&nbsp;&nbsp;},<br>&nbsp;&nbsp;&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "566434444460",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name": "david",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"surname": "Perez"<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;]<br>} |

- Si la llamada devuelve información, devolverá un código 200 y la información en un listado en el cuerpo del mensaje.

- Si la llamada no devuelve datos, con o sin filtros (query params), la búsqueda devolverá un 200, indicando un listado vacío.

- **RECOMENDACIÓN**: Se podrá devolver información adicional, como la paginación u ordenación si la consulta permitía dicha funcionalidad.

**Código de Buenas Prácticas**

Las diferentes llamdas deben enfocarse en torno a un mismo recurso,Ses decir, se debe fomentar la reutilización. No se debe duplicar o crear nuevos metodos para obtener información sobre misma identidad, para ello, ya se dispone los query string (filtros) para obtener la información deseada.


Ejemplo incorrecto:<br>
`GET /users` <br>
`GET /usersByDepartment`<br>
`GET /usersByName`

Para distinguir las diferentes consultas utilizaremos query params

`GET /users?department=xxx&name=xxx`

#### 4.8.4. POST

**Escenarios:**

Existen dos posibles situaciones para utilizar POST: 

1. Para crear un recurso (document) en una colección:

```json
POST /users
{
  "name": "Juan",
  "surname": "Castaño"
}
```

2. Cuando se necesita representar una funcionalidad concreta que no podemos asociar a ningún métodos estándar CRUD (controller).

Se deben intentar evitar este tipo de invocación en la medida de lo posible y debería reducirse a lo mínimo pensando en modificar el diseño para que se ajuste a otro tipo de recurso que no sea un controller.

Ejemplo, caso que se lanza un proceso batch que actualiza los usuarios a un nuevo estado. `POST /users/v1/promote`

Debido a su naturaleza, este tipo de aciones, están sujetas a otras reglas especificas respecto al de operaciones:

- Se identifican con un **verbo en la url** debajo de la entidad sobre la que realizan la acción.
- LA documentación debe ser más completa e incluir todos los ejemplos implicados y necesarios para su cumpliento para todos los casos que pueda abordar.

**¿Qué retorna?**

1. Creación de un nuevo recurso (**document**) en una colección. Si la creación se ha realizado con éxito::

   - Código HTTP 201 (created).
   - En la cabecera, se hace uso del campo Location al recurso con el id creado. De esta forma el usuario ya dispone del nuevo identificador del recurso.

     `Location: /users/2253345234523`

   - Y en el cuerpo (payload) irá vacío. 
   
   Ejemplo:

    |             | **Solicitud**      | **Respuesta**           |
    | ----------- | ---------------- | ---------------------- |
    | **Recurso** | POST /users      |                        |
    | **Headers**  |                  | 201 Created   <br> Location /users/144444        | 
    | **Payload** |                  |{<br>&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;"surname": "Castaño"<br>} |                        |

- Existe la posibilidad de puede devolver en el payload de respuesta el propio recurso creado. Este recurso tendrá que devolver al recurso con todos sus campos, tal como se devolvería en un GET. Se tendrá en cuena que este objeto de salida seguramente sea diferente al utilizado en el payload de entrada, esto es debido a los atributos autocalculados o autogenerados a la hora de la creación de la nueva entidad.
- Se recomendación es evitar devolver datos en cuerpo de la invocación siempre que se pueda, simplemente devolver la **cabecera Location** con el código HTTP 201.

|             | **Solicitud** | **Respuesta**  |
| ----------- | ------------- | -------------- |
| **Recurso** | POST /users   |                |
| **Header**  |               | 201 Created<br>Location /users/1231231234123    |
| **Payload** |               | { <br>&nbsp;&nbsp;&nbsp;&nbsp;"data":<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "1231231234123",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"surname": "Castaño", <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"status": "CREATED",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"timeStamp": "1653991582",<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |

2. Caso de uso de un **controller**, el comportamiento será el siguente:

- La invocación ha sido satisfactoria se retorna:un código HTTP 200 (OK) y si fuera el caso se podrá retorna información en el cuerpo de respuesta. 


|             | **Solicitud**               | **Respuesta**     |
| ----------- | --------------------------- | ----------------- |
| **Recurso** | POST /users/cancel          |                   |
| **Header**  |                             | 200 Ok            |
| **Payload** | JSON de la petición         | JSON de respuesta |


- Caso en que la operación se finaliza satisfactoriamente y no es necesario devolver información en el cuerpo de la llamada, entonces se retornará un código HTTP 204 (No content) y el cuerpo irá vación

|             | **Solicitud**       | **Respuesta**  |
| ----------- | ------------------- | -------------- |
| **Recurso** | POST /users/cancel  |                |
| **Header**  |                     | 204 No content |
| **Payload** | JSON de la petición | N/A            |

**Código de Buenas Prácticas**

En muchos casos a la hora de la creación de un objeto es posible que el objeto de entrada tenga menos campos que el objeto final, presente en GET y en la respuesta del POST si se retorna cuerpo. 

Por ejemplo, los campos autocalculados por el sistema siempre estarán delegados y será el sistema el encargado de indicar el valor, ejemplo un ID o la fecha de creación de la identidad o el estado en el que se cuentra.


| **Entrada**    | **Salida**    |
| -------------- | ------------- |
| {<br>&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;"surname": "munoz"<br>} | {<br>&nbsp;&nbsp;&nbsp;&nbsp;"id": "234523452345234",<br>&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;"surname": "munoz",<br>&nbsp;&nbsp;&nbsp;&nbsp;"status": "PENDING",<br>&nbsp;&nbsp;&nbsp;&nbsp;"timestamp": "15646465465"<br>}|

#### 4.8.5. PUT

**Escenarios:**

- Se utiliza en aquellos casos que se pretenga realizar una modificación completa de un recurso existente. La actualizacion es completa y será necesario enviar el objeto **completo**, incluyento todos los atributos en el cuerpo de la solicitud a excepción del identificador (ID) que ya va informada en la url:

  ```json
  PUT /users/14444
  {
    "name": "Juan",
    "surname": "Castaño hernandez"
  }
  ```

- En otras ocasiones también se puede aplicar a la hora de crear el recurso. **Siempre** cuando el consumidor que invoca a la llamda conozca previamente el identificador con el que se va a crear. Esto caso no suele ser habitual, ya que normalmente es el servidor el quien que autogenera el identificador. Si se desconoce el identificador y lo autogenera el servidor, este método no deber utilizarse para creación y si el POST.

**¿Qué retorna?**

- Caso de haber **creado un recurso**, se devuelve un código HTTP 201 (Created) y la cabecera Location con la url de acceso al recurso creado y su identificador. 

- Caso de haber **modificado un recurso**, es decir realizar un actualización del objeto completo, se devolverá un código HTTP 204 y el payload irá vacío.


|             | **Solicitud**     | **Respuesta**       |
| ----------- | ----------------- | ------------------- |
| **Recurso** | PUT /users/1244   |                     |
| **Header**  |                   | Opción 1: Se creó recurso: 201 Created <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Location: /users/1244<br>Opción 2: Se modifica recurso: 204 No content |
| **Payload** | {<br>&nbsp;&nbsp;&nbsp;&nbsp;"name": "david",<br>&nbsp;&nbsp;&nbsp;&nbsp;"surname": "munoz",<br>&nbsp;} |                                        |

**Código de Buenas Prácticas**

Cuando se invoque al método PUT, se debe informar con todos los campos que pertenecen al recurso, sean editables o no. 

#### 4.8.6. PATCH

**Escenarios:**

Aquellos casos en que se busca modificar un recurso de forma parcial (sólo parte de sus campos).

**CUIDADO**: Este método es más complejo de implementar, ya que es requisito obligatorio mantener la coherencia y sus obligatoriedades del recursos. En los casos que no se tenga claro es preferible usar el método PUT verificando los campos modificables y los que no lo son.

La correcta forma de utilizarlo es:

- Se enviarán aquellos campos en el cuerpode la solicituda que solo se desean modificar y los atributos no enviados en el cuerpo de solicitud se mantendrar  inalterados.
- El procedimiento para la actualizacion de los campos será el siguiente:
  - La petición del patch contiene atributos que no contiene el target, se añaden.
  - Contiene el atributo indicado en el cuerpo de la petición, su valor es reemplazado.
    - Atributos  de tipo string, number y boolean, se sustituye por el valor.
    - Los atributos tipo array:
      - No contien atributos con ID, el array es sustituido completamente.
      - Contienen atributos con ID, se sustituye o cambian los datos de ese objeto a través de su identificador.
    - Atributos tipo objeto, se definen las mismas normas de manera recursiva.
  - Atributo lleva como valor null en el cuerpo de la petición, este es eliminado.

A continuacion se refleja varios escenarios y funcionamiento óptimo de este método sobre la entidad (users) siguiente:

```json
{
  "id": "987654321",
  "name": "Juan",
  "surname": "martín",
  "permissions": ["write"]
}
```

- Si enviamos un atributo que no existía, se añadirá.

|             | **Solicitud**           | **Respuesta**                  |
| ----------- | ----------------------- | ------------------------------ |
| **Recurso** | PATCH /users/987654321  |                                |
| **Header**  |                         | - 204 (No content) sin cuerpo de respuesta o <br> - 200 (OK) con el cuerpo|
| **Payload** | {<br>&nbsp;"email": "juanmarting@axpecom"<br>&nbsp;} | { <br>&nbsp;&nbsp;&nbsp;&nbsp;"data": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "987654321",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"surname": "martín", <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"permissions": ["read"],<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"email": "juanmarting@axpe.com"<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |

- Envío de un atributo existen, se actualiza o modifica el valor.

|             | **Solicitud**           | **Respuesta**       |
| ----------- | ------------------------|-------------------- |
| **Recurso** | PATCH /users/987654321  |                     |
| **Header**  |                         | - 204 No content sin cuerpo de respuesta <br>- 200 OK con el cuerpo                                                     |
| **Payload** | {<br>&nbsp;"surname": "Perez"<br>&nbsp;} | { <br>&nbsp;&nbsp;&nbsp;&nbsp;"data": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "987654321",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"surname": "Perez", <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"permissions": ["read"]<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |

- Se envía un array y sin identificadores de cada uno de los items que lo compone, se manda el array completo y será para reemplarlo en su totalidad. 

|             | **Solicitud**            | **Respuesta**              |
| ----------- |------------------------- |--------------------------- |
| **Recurso** | PATCH /users/987654321   |                            |
| **Header**  |                          | - 204 No content sin cuerpo de respuesta <br>- 200 OK con el cuerpo|
| **Payload** | {<br>&nbsp;"permissions": ["admin"]<br>&nbsp;} | { <br>&nbsp;&nbsp;&nbsp;&nbsp;"data": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "987654321",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"surname": "Perez", <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"permissions": ["admin"]<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |

- Otro caso, si  se envía un array y este contine en cada uno de sus items  contiene identificadores, el comportamiento es diferente. Este caso se manda solo aquellos items del array que se quieren actualizar, con los datos correspondiente de cada item enviado:

Ejemplo: La entidad user tiene los siguientes atributos o valores:

```json
{
  "id": "987654321",
  "name": "Juan",
  "surname": "Castaño",
  "permissions": [
    {
      "id": "1",
      "description": "read"
    }
  ]
}
```

- Para añadir un item nuevo:

|             | **Solictud**           | **Respuesta**      |
| ----------- | ---------------------- | ------------------ | 
| **Recurso** | PATCH /users/987654321 |                    |
| **Header**  |                        | 204 No content sin cuerpo de respuesta <br>o 200 OK con el objeto entero en cuerpo   |
| **Payload** | {<br>&nbsp;&nbsp;&nbsp;&nbsp;"permissions": [<br>&nbsp;&nbsp;&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "2",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"description": "admin"<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;]<br>} | { <br>&nbsp;&nbsp;&nbsp;&nbsp;"data": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "987654321",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"surname": "Perez", <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"permissions":[<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "2",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"description": "admin"<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;},<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "1",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"description": "read"<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |     |


- En el caso de actualizar un item existente, se indica el ID del item a actualizar y los atributos que se van a modificar por el nuevo valor:

|             | **Solicitud**          | **Respuesta**     |
| ----------- | -----------------------| ----------------- |
| **Recurso** | PATCH /users/987654321 |
| **Header**  |                        | 204 (No content) sin cuerpo de respuesta <br>o 200 (OK)con el cuerpo    |
| **Payload** | {<br>&nbsp;&nbsp;&nbsp;&nbsp;"permissions": [<br>&nbsp;&nbsp;&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "50",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"description": "admin"<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;]<br>} | { <br>&nbsp;&nbsp;&nbsp;&nbsp;"data": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "987654321",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"surname": "Perez", <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"permissions":[<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "50",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"description": "admin"<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;]<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |     |

- Caso en el que se quiera borrar un atributo hay que indicarlo explicitamente, para ello utilizaremos el valor **null** para indicar esta acción.

|             | **Solicitud**          | **Respuesta**     |
| ----------- | ---------------------- | ----------------- |
| **Recurso** | PATCH /users/987654321 |                   |
| **Header**  |                        | 204 (No content) sin cuerpo de respuesta <br>o 200 (OK)con el cuerpo |
| **Payload** | {<br>&nbsp;"permissions": null<br>&nbsp;} | { <br>&nbsp;&nbsp;&nbsp;&nbsp;"data": {<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"id": "123",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"name": "Juan",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"surename": "Martín"<br>&nbsp;&nbsp;&nbsp;&nbsp;}<br>} |

**¿Qué retorna?**

Con este verbo puede ocurrir **dos casos**:
- Primer caso, la respuesta se devuelve un código 204 y el payload vacío. Se recomienda utilizar lo más posible esta opción para su optimización.
- Segundo caso, en la respuesta se devuelve el objeto modificado con todos sus atributos modificados o no, tal y como este definido.

Referencia [JSON Merge Patch](<https://tools.ietf.org/html/rfc7386>)

**Código de Buenas Prácticas**

- Esta operación debe ser atómica. Todos las modificaciones deben aplicarse o en caso contrario se debe emitir un error y no modificar ninguno.
- El PATCH debe ser idempotente. Aunque existe una RFC que permite que no sea idempotente su gestión es tan compleja a la hora de implementar el servicio que hay que evitar su uso.

#### 4.8.7. DELETE

**Escenarios:**

Se pueden especificar dos tipos de endpoints para borrado:

- Borrar un objeto concreto (document): 
<br> ` DELETE /users/{userId}`

- Borrar todos los objetos (collection):
<br>`DELETE /users`

**¿Qué retorna?**

- En caso del borrado de un objeto único (o varios) con éxito, se retorna un 204.
- En caso del borrado de un objeto único que no se encuentra, se retorna un 404 (no encontrado)

|             | **Solicitud**        | **Respuesta**   |
| ----------- | -------------------- | --------------  |
| **Recurso** | DELETE /users/1244   |                 |
| **Header**  |                      | 204 No content  |
| **Payload** |                      | N/A             |


#### 4.8.8. OPTIONS

**Escenarios:**

Este operación es utilizada para recuperar un header con la información relacionada y disponible al recurso por el que se pide información.

**¿Qué retorna?**

- Los posibles métodos relacionados con el recurso, dentro de la etiqueta **Allow**.
- Los **Content-type** admitidos.
- Metainformación que requiera el cunsumidor.

|             | **Solicitud**       |  **Respuesta** |
| ----------- | ------------------- | ---------------|
| **Recurso** | OPTIONS /users      |                |
| **Headers** |                     | HTTP/1.1 200 OK<br>*Allow*: GET,HEAD,POST,OPTIONS,TRACE<br>*Content-Type*: text/html; charset=UTF-8<br>Date: Wed, 08 May 2020 10:24:43 GMT<br>Content-Length: 0 |

#### 4.8.9. HEAD

**Escenarios:**

Este método es similar a realizar una petición GET, la diferencia radica en que solo se retornan las cabeceras, sin respuesta en el cuerpo. Así sabemos que información tiene asociada el recurso.

**¿Qué retorna?**

Al realizar esta petición devolvera las siguiente opciones:

- Status code devuelto (si el recurso existe).
- Información sobre content-type.
- Caché.
- Última modificación del recurso.

|             | **Solicitud**      | **Respuesta**   |
| ----------- | ------------------ | ----------------|
| **Recurso** | HEAD /users/1244   |                 |
| **Headers** |                    | HTTP/1.1 200 OK<br>Content-Type: text/html; charset=UTF-8 Date: Wed, 08 May 2013 10:<br>12:29 GMT<br>ETag: "780602-4f6-4db31b2978ec0"<br>Last-Modified: Wed, 01 June 2022 16:13:23 GMT<br>Content-Length: 2452 |

Para ello se recomienda aplicar la referencia [RFC-7231](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.2).

#### 4.8.10. RESUMEN OPERACIONES HTTP


| **Operación** | **Empleo**                         | **Idempotente** | **Seguro** | **Query Params** | **Path Params** | **Request Body** | **Response Body**               |
| ------------- | ---------------------------------- | --------------- | ---------- | ---------------- | --------------- | ---------------- | ------------------------------- |
| **GET**       | Consulta recurso                   | Si              | Si         | No               | Si              | No               | Si                              |
| **GET**       | Consulta colección recursos        | Si              | Si         | Si               | No              | No               | Si                              |
| **POST**      | Crear recurso                      | No              | No         | No               | No              | No               | Si                              |
| **POST**      | Operación controller               | Puede           | Puede      | No               | No              | Si               | Puede                           |
| **PUT**       | Actualización completa del recurso | Si              | No         | No               | Si              | Si               | Puede. Se aconseja no informalo.|
| **PATCH**     | Actualización parcial del recurso  | Si              | No         | No               | Si              | Si               | Puede. Se aconseja no informalo.|
| **DELETE**    | Borrado del recurso                | Si              | No         | No               | Puede           | No               | No                              |
| **HEAD**      | Información del recurso            | Si              | Si         | No               | Puede           | No               | No                              |
| **OPTIONS**   | Información del método             | Si              | Si         | Si               | No              | No               | No                              |


### 4.9. Códigos de estado HTTP


El comportamiento del uso de los códigos HTTP queda defindo en la sección [6 de la RFC-7231](https://datatracker.ietf.org/doc/html/rfc7231#section-6).

A continuación se especifica la sintaxis. Donde el primer dígito del código de respuesta indica uno de los 5 tipos de respuesta:

- 1XX (Informational) Respuestas informativas,proceso continuo.
- 2XX (Successful) Peticiones correctas
- 3XX (Redirecction) Redirecciones, se deben tomar medidas adiccionales para completar la solicitud.
- 4XX (Client Error) Errores del cliente. La solicitud contine una sintaxis incorrecta o no se puede complir.
- 5XX (Server Error) Errores de servidor. El servidor no completo una solicitud que aparentamente es correcta.

> La información más detallada sobre los códigos de respuesta, se puede consultar en estandar[ RFC-7231 en la sección 6.1](https://tools.ietf.org/html/rfc7231#section-6.1)

A continuación se muestra los códigos HTTP mas usados:

| **Código HTTP** | **¿Cuándo usarlo?**       | **¿Dónde usarlo?**               |
| --------------- | ------------------------- | -------------------------------- |
| **200**         | Respuesta exitosa y devuelve información del recurso       | GET Collection <br>GET, PUT, PATCH (no se recomienda) Document.<br>PUT Store<br> POST Controller |
| **201**         | Respuesta exitosa y devuelve el recurso creado                    | POST Document                |
|**202**| Indica que la petición ha sido recibida pero que todavía no se ha actuado al respecto| GET<BR>POST Controller|
| **204**         | Respuesta es exitosa y no se devuelve el contenido en la respuestaecurso | DELETE Collection<br>PUT, PATCH, DELETE Document<br>PUT Store                                                             |
| **400**         | Petición incorrecta: <br> los parámetros seleccionados erroneos  o se produce un error funcional | Todos, menos GET de un documento  |
| **401**         | Autorización incorrecta. La llamada necesita algún tipo de autorización, ya sea que este caducada o no se haya informado.   | Todos                            |
| **403**         | No se tienen permisos para operar con esta invocación.            | Todos |
| **404**         | Recurso no encontrado. | GET, PUT, PATCH, DELETE Document |
| **405**         | La petición no está permitido para el recurso al que se quiere invocar.| Todos                            |
| **406**         | El formato indicado en al cabecera "Accept" de la petición, no es soportado por el servidor destino.| Todos |
| **415**         | Formato incorrecto de la respuesta, no concuerda con el indicado en la cabecera "Content-Type".| POST, PUT, PATCH Document        |
| **422**         | Estructuralmente la petición es correcta, pero no semánticamente | Todos|
| **429**         | Muchas peticiones en un periodo de tiempo determinado y se ha excedido el límite| Todos                            |
| **500**         | Eror inesperado por parte del servidor, no tiene forma de responder a la invocación. <br> Normalmente, es una respuesta global cuando no se puede cubrir con otro código o se busca enmascarar el error. | Todos              |
| **501**         | Funcionalidad no soportada por el servido. | Todos|
| **502**         | Indica que el servidor, aunque actuando como puerta de enlace o proxy, recibió una respuesta no válida de un servidor de entrada al que accedió mientras intentaba cumplir con la solicitud. | Todos              |
| **503**         | Indica que el servidor no está disponible para realizar la petición debido a que está sobrecargado o se están realizando tareas de mantenimiento, y que probablemente se aliviará después de un tiempo.| Todos              |
| **504**         | Indica que el servidor, mientras actuaba como puerta de enlace o proxy, no recibió una respuesta oportuna desde un servidor ascendente al que necesitaba acceder para completar el solicitud.| Todos              |


> Podrán agregarse más códigos de estado HTTP siempre y cuando esten en el protocolo estándar y sean justificados

Mapeo entre los distintos métodos y los código de estado más usados:


**Estado Código** | **200 Success** |	**201 Created**	| **202 Accepted** | **204 No Content**	| **400 Bad Request**|	**404 Not Found**	|**422 Unprocessable Entity**| **500 Internal Server Error**|
----------|----|----|----|----|----|----|----|----|
GET 	    | X  |		|    |X   |X   |   X|   X|   X|
GET 	 (Async)   |   |		|  X  |   |X   |   X|   X|   X|
POST  (Controller)    | X  | 	|X   |    |X   |   X|   X|   X|
POST     |   |X 	|   |    |X   |   X|   X|   X
PUT	      | X  |X		|X   |X   |X   |   X|   X|   X|
PATCH     | X  |		|    |X   |X   |   X|   X|   X|
DELETE    | X  |		|    |X   |X   |   X|   X|   X|
HEAD 	    | X  |		|    |X   |X   |   X|   X|   X|
OPTIONS 	| X  |		|    |X   |X   |   X|   X|   X|


### 4.10. Filtros 
Existen mecanismos de filtrado para ayudar a obtener los resultados esperados restringiendo el subconjunto de elementos obtenidos mediante la declaración de condiciones.

Se usarán 3 tipos de filtros para las APIs en la compañía:

- Filtros simples
- Filtros complejos
- Filtros complejos demasiado extensos

#### 4.10.1. Filtros simples

Los filtros simples son los más habituales, usan directamente los nombres de los campos de la entidad para las búsquedas en colecciones o stores de documentos a través de query parameters. La estructura del filtrado tiene la siguiente composición:

```
?[campo][operador][valor]
```

- donde el **campo** es el nombre del atributo de la entidad a buscar.
- el **operador** es el operador utilizado para realizar el tipo de comparativa para hacer el filtrado. 
- y el **valor** del atributo que cumple el operador.

A continuación se indica cómo se debe usar el filtrado según latipología del dato por el que se busca: un texto, un número o una fecha y el tipo de operación:

| **Operación**     | **Textos**                    | **Números**                         | **Fechas**                                                 |
| ----------------- | ----------------------------- | ----------------------------------- | ---------------------------------------------------------- |
| **Igual**         | GET .../?name=Juan            | GET .../?amount=807.24              | GET .../?executionDate=2018-30-05                          |
| **Comparación**   | GET .../?name=Juan&name=pedro | GET .../?amount=807.24&amount=25.65 | GET .../?executionDate=2018-30-05&executionDate=2018-29-05 |
| **Mayor o igual** | N/A                           | GET .../?**from**Amount=807.24      | GET.../?**from**ExecutionDate=2018-30-05                   |
| **Menor o igual** | N/A                           | GET .../?**to**Amount=807.24        | GET.../?**to**ExecutionDate=2018-30-05                     |
| **Contiene**      | GET .../?name=~Juan           | N/A                                 | N/A                                                        |

##### 4.10.1.1. Reglas adicionales:

- El operador & es evaluado como un OR para los valores de un mismo nombre de atributo y un AND entre atributos distintos.
- Para las operaciones sobre campos numérico, fecha ó enumerados se permitirá usar los prefijos “from” y “to” que actuará como comparadores de “mayor ó igual que” y “menor o igual que”.

##### 4.10.1.2. Ejemplos:

- **Igualdad**
  Para buscar los users con nombre "david" y apellido "munoz":

  ```js
  GET /users?name=david&surname=munoz
  ```

  También podemos buscar por varios valores incluyendo el parámetro varias veces:

  ```js 
  GET /users?name=david&name=Juan
  ```

- **Inclusión**
  Si tenemos ya un filtro que busca por "igualdad" y queremos dotarlo de la posibilidad de buscar por "inclusión", debemos incluir el carácter "~". Esta nomenclatura no es un estándar y no se usa de forma habitual.

  ```js
  GET /users?name=dav //Busca el nombre exacto "dav"
  GET /users?name=~dav //Busca nombres que incluyan "dav"
  ```

- **Mayor que / menor que**
  Crearemos un nuevo atributo y haremos que le preceda un "from" y un "to"

  ```js
  GET /users?fromCreatrionDate=2019-01-01T00:00:00 //Busca usuarios con creationDate mayor que 2019
  GET /users?toCreatrionDate=2019-11-31T23:59:59 //Busca usuarios con creationDate menor que 2020
  GET /users?fromCreatrionDate=2019-01-01T00:00:00&toCreatrionDate=2019-11-31T23:59:59 //Busca usuarios creados este año (entre 2019 y 2020)
  ```

Las **ventajas** del uso de este tipo de filtrado son:

- Es fácil de usar en el servidor y en cliente
- No tiene problemas con filtros combinacionales con el mismo campo
- Las URIs son mucho más entendibles

#### 4.10.2. Filtros complejos

Esta definición de filtros está más enfocada a definiciones de servicios más técnicos. La sintaxis para utilizar un filtro complejo en los recursos de tipo collection en las APIs está basada en la definición de [RSQL](https://github.com/jirutka/rsql-parser#grammar-and-semantic).

RSQL tiene parsers implementados para JavaCC, Java, Python y otros lenguajes. Para filtrar un collection utilizando filtros complejos, se deberá enviar un parámetro _q_ dentro de la query con la expresión RSQL a evaluar.

> ejemplo: http://axpe.com/users?q=name=="Juan Perez" and birthYear>2003

Nota: Todos los ejemplos asumen que el query se codificará debidamente para viajar en la URI antes de enviarse al servidor.

#### 4.10.3. Filtros extensos

Aunque serán poco frecuente los filtros para consultas cuyo tamaño supera potencialmente las capacidades del stack tecnológico disponible, y que no pueden ser enviados en la URL, se ofrece la siguiente alternativa:

Para filtrar el recurso usuarios de tipo collection (GET /users) se creará un recurso de tipo controller (ver sección sobre controllers) llamado **search** bajo el recurso de tipo collection, **POST /users/search** y se enviará en el payload del mensaje los campos necesarios para su búsqueda siguiendo la misma estructura del recurso principal (users).


### 4.11. Paginación

La mayoría de las operacións GET sobre una colección podría soportar o se recomienda tener algún tipo de paginación. Devolver todos los recursos de la colección a la vez puede ser pesado y podría requerir demasiado tiempo y consumo.

El código **200 OK** será el utilizado para indicar que no se está devolviendo todo el contenido, en tal caso se acompañará de un nodo con los datos necesarios de paginación que nos permitirá movernos por la colección.

Existen varios métodos de paginación y en muchas ocasiones es complicado adaptarse si se van a exponer servicios que ya están implementados y tienen un tipo de paginación ya establecido.

Se definen **dos métodos de paginación** que cubren casi todo el espectro de necesidades y que deberán utilizar los equipos de desarrollo:


#### 4.11.1. Paginación offset-limit

Es el método mas común y simple para realizar una paginación. Limit/Offset se hizo popular entre las aplicaciones que utilizan bases de datos SQL que ya tienen LIMIT y OFFSET como parte de la sintaxis de SQL SELECT. Es muy fácil de implementar, ya que se requiere muy poca lógica de negocios para implementar dicha paginación.

- **limit:**
  - Número de registros que se devuelven por página 
    >Ejemplo, con limit=10 se devolverán 10 registros en una consulta.
  
  - Se recomienda establecer un limite por defecto, para que en caso de que este campo no se indique en la petición se retorne un número limitado de resultados en la respuesta. Además será necesario indicar este valor por defecto en el contrato de definición de la API.
 
  - Valor **no obligatorio** de indicar, sí se no indica a la entrada se usa el valor por defecto definido en el servicio, que habrá que documentar en la descripción del campo.

- **offset:** 
  
  - Parámetro en el que se indica el siguiente registro a devolver por el Backend.  
  
  - Si el servicio es implementado siguiendo esta paginación, desde el primer momento, el offset es el número de registro a partir del cual se quiere recibir el numero de registros indicado en el limit.
    > Ejemplo, offset=30 devolverá los registros de 31 en adelante. 
  
  - Si el servicio ya está implementado previamente, este offset debe utilizarse como la clave por la cual el backend es capaz de identificar la pagina a retornar, puede ser el numero de registro como el caso anterior, puede ser un timestamp, un identificador de la pagina, etc. Este valor dependerá del tipo de implementación de la paginación que tenga el servicio.

  - En la primera llamada no es necesario indicar el campo, ya que su valor por inicial sería 0, el resto de llamadas sería obligatorio indicarlo.

A continuación se muestran algunos casos:

- Primera llamada, y que devuelva la primera página:

  ```js
  GET /users?limit=10 //Devuelve los registros del 1 al 10 con un tamaño de página de 10
  ```

- Para la consulta de otra página:

  ```js
  GET /users?offset=30&limit=10 //Devolverá los registros del 31 al 40 con un tamaño de página de 10
  ```

La estructura de la **RESPUESTA** será siguiente:

- Esta estructura es obligatoria si hay resultados en la búsqueda, y se encontrara dentro de la estructura raíz "data".
- La información necesaria para paginación estará englobada en un nodo llamado **"pagination"**. Esta estructura es obligatoria si hay resultados en la búsqueda.
- Links de navegación a las páginas: actual(obligatorio) con "self", anterior (si existe) con "prev", y siguiente (si existe) con "next".
- Opcionalmente: "first" (primera página), "last" (última página).

| Atributo       | Obligatorio | Descripción|
| -------------- | ----------- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| offset  | Si          |   Número de registro a partir del cual se quiere recibir el numero de registros indicado en el limit. Si es indicado a la entrada, será el valor de la consulta. Si no es indicado a la entrada, al ser la consulta de la primera página su valor será 0 |
| limit | Si          | Número de registros que se devuelven por página. Si es indicado a la entrada, será el valor de la consulta, si no será el valor establecido por defecto por el servicio|
| pageNumber     | No          | Número de página en la que nos encontramos|
| totalPages     | No          | Número de páginas para el limit indicado|
| totalElements  | No          | Número total de elementos en el listado|
| links          | Si          | Lista de links de navegación a diferentes páginas|
| links.self     | Si          | Uri absoluta a la propia página que se ha devuelto.|
| links.first    | No          | Uri absoluta a la primera página de resultados.|
| links.last     | No          | Uri absoluta a la última página de resultados.|
| links.prev     | No          | Uri absoluta a la página previa de resultados.|
| links.next     | Si **\***        | Uri absoluta a la página siguiente.|

(**\***) Campo obligatorio siempre que haya siguiente página. Sí es la última página de la colección, no se rellena dicho campo.

##### 4.11.1.1. Condiciones de uso

- Para consumir las URIs devueltas en “first”, “last”, "self", “prev” y “next” para estos enlaces siempre será GET.
- Obtener la siguiente página sería un GET del contenido en "next".
- Las URIs de los links son absolutas, nunca relativas.
- Los objetos "pagination" y "links" deben ser referencias a objetos concretos dentro de la definición del API.
- Se deben mantener los queryParams (filtros, ordenación etc..) que pudieran venir en la Request en todos los links de salida acorde a la entrada.
- Si el limit no viene definido por el consumieor, el backend debe utilizar un valor por defecto.
- En los casos que la petición venga vacia, no devuelva información, se devolverá un **204 Not Content**.

  ```json
  {
    "data": [
      {
        "id": "20923481234",
        "name": "juan",
        "surname": "Castaño"
      }
    ],
    "pagination": {
      "offset": 20,
      "limit": 10,
      "pageNumber": 3,
      "totalPages": 7,
      "totalElements": 65,
      "links": {
        "first": "http://www.api.axpe.com/users?limit=10",
        "prev": "http://www.api.axpe.com/users?offset=10&limit=10",
        "self": "http://www.api.axpe.com/users?offset=20&limit=10",
        "next": "http://www.api.axpe.com/users?offset=30&limit=10",
        "last": "http://www.api.axpe.com/users?offset=60&limit=10"
      }
    }
  }
  ```

#### 4.11.2. Paginación por cursor

- Esta tipo de paginación se basa en devolver en la respuesta de paginación un puntero concreto que apunta al siguiente dato a consultar dentro del dataset.

- Es especialmente útil cuando hay inserciones y borrados constantes en los datos a consultar, pues con **_offset-limit_** podríamos devolver respuestas inconsistentes.

- Solo se permite avanzar hacia delante o hacia atrás durante la paginación debido a que son posiciones relativas respecto a la anterior consulta.

La consulta de la con paginación en un metodo GET se van a utilizar con dos query parameters en la **ENTRADA**:

- **pageSize:**

  - Número de registros que se devuelven. Se aconseja tener un _pageSize_ por defecto. En los caso de que este campo no se indique en la petición, se deberá retornar un número limitado en la respuesta. Por otro lado, será necesario indicar este valor por defecto en el contrato de definición de la API.

- **paginationKey:**

  - Parámetro que identifica la posición de los registros a devolver.
  
  - Si el cursor apunta a la página siguiente: el cursor será un token que contenga la información del último registro que devolvió en la anterior consulta e indicará el sentido "avanzar".
  
  - Si el cursor apunta a la página anterior: el cursor será un token que contenga la información del primer registro que devolvió la anterior consultar e indicará el sentido "retroceder".
  
  - En la primera llamada a la página no es necesario indicar este campo.

- Para la consulta de la primera página:

  ```js
  GET /users/v1/users?pageSize=10 //Devolverá los registros del 1 al 10
  ```

- Para la consulta de la siguiente página:

  ```js
  GET /users/v1/users?pageSize=10&paginationKey=134523SWEDRTGS //Devolverá los 10 siguientes registros a partir del cursor indicado.
  ```

  A continuación se detalla la estructura de **RESPUESTA**:

- Esta estructura es obligatoria siempre que haya resultados en la búsqueda. 

- La paginación ira dentro de un nodo llamado "pagination".

- Esta estructura esta consitituada por el nodo llamado  "Links" de navegación a las páginas, compuesto: actual(obligatorio) con "self", anterior (si existe) con "prev", y siguiente (si existe) con "next".

- Opcionalmente: "first" (primera página), "last" (última página).



| Atributo       | Obligatorio | Descripción                                                                                                                                                                                                                                                  |
| -------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| paginationKey  		 | Si          | Campo (cursor) generado por el servicio, el cual indica la posición a recuperar.|
| pageSize 		 | Si          | Número de registros que se devuelven por página. Si es indicado a la entrada, será el valor de la consulta, si no será el valor establecido por defecto por el servicio.                                                                                      |
| pageNumber     | No          | Indica el número de página en la que se situa.                                                                                                                                                                                                                   |
| totalPages     | No          | Indica el número total de páginas para el pageSize.                                                                                                                                                                                                                     |
| totalElements  | No          | Número total de elementos en el listado.                                                                                                                                                                                                                      |
| links          | Si          | Conjunto de links de navegación a diferentes. Compuesta dichos enlaces son URIs absolutas, no relativas. páginas.                                                                                                                                                                                                       |
| links.self     | Si          | Enlace a la propia página que se ha devuelto. Incluye los parámetros de consulta 'paginationKey' y 'pageSize'.                                                                                                                                                                                                     |
| links.first    | No          | Enlace a la primera página de resultados. Incluye de manera opcional el parámetro de consulta 'pageSize'.                                                                                                                                                                                                                 |
| links.last     | No          | Enlace a la última página de resultados.  Incluye los parámetros de consulta 'paginationKey' y 'pageSize'.                                                                                                                                                                                                             |
| links.prev     | No          | Enlace a la página previa de resultados. Incluye los parámetros de consulta 'paginationKey' y 'pageSize'.                                                                                                                                                                                                              |
| links.next     | Si **\***        | Enlace a la página siguiente. Incluye los parámetros de consulta 'paginationKey' y 'pageSize'.   

(**\***)Obligatorio, siempre que haya siguiente página. Este campo, si es la última página de la colección, no se enviará.

```json
  {
    "data": [
    {
      "id": "ASDFA352345",
      "name": "Juan",
      "surname": "Perez"
    }
    ],
    "pagination": {
      "pageSize": 10,
      "pageNumber": 3,
      "totalPages": 7,
      "totalElements": 65,
      "links": {
        "first": "http://www.api.axpe.com/users?pageSize=10",
        "prev": "http://www.api.axpe.com/users?paginationKey=aca4834xyz&pageSize=10",
        "self": "http://www.api.axpe.com/users?paginationKey=abc1234xyz&pageSize=10",
        "next": "http://www.api.axpe.com/users?paginationKey=def5678xyz&pageSize=10",
        "last": "http://www.api.axpe.com/users?paginationKey=ghi9012xyz&pageSize=10"
      }
    }
  }
```

##### 4.11.2.1. Condiciones de uso

- Se sobreentiende que el verbo a utilizar para consumir las URIs devueltas en “first”, “last”, "self", “prev” y “next” para estos enlaces siempre será GET.

- Obtener la siguiente página sería un GET del contenido en "next".

- Las URIs de los links son absolutas, nunca relativas.

- Los objetos "pagination" y "link" deben ser referencias a objetos concretos dentro de la definición del API.

- Se deben mantener los queryParams (filtros, ordenación etc..) que pudieran venir en la Request en todos los links de salida acorde a la entrada.

- Si el consumidor no indica el pageSize el backend debe utilizar un valor por defecto. El servicio decide si puede cumplir con este valor o retorna un número de resultados diferente.

- Para un caso en el que la petición no devuelva información se devolverá un 204 Not Content.

### 4.12. Ordenación
- El parámetro **sortBy** indicado en la URI de servicio, establece al sistema qué valores se utilizan para ordenar el resultado. Sólo se admite cuando la ruta del recurso identifica una colección de entradas y el servicio final permite la ordenación

- Por norma general, las consultas realizadas vendrán, por defecto vendran ordenadas por uno de los atributos.

- En algunos casos, si se quisiera ampliar esta necesidad y permitir ordenar por otros atributos, se incluirá el query param "sortBy" acompañado de los nombres de atributo por los que queremos ordenar, precedidos por - (descendente) o + (ascentente).

- Si no se indica + o -, por defecto será + (ascendente).

  ```js
  GET /users?sortBy=+name // Ascendente
  GET /users?sortBy=-name // Descendente
  GET /users?sortBy=name // Ascendente (por defecto)
  GET /users?sortBy=name,-surname // Se ordena por name, luego por surname descendente
  ```

#### 4.12.1. Cuando y Condiciones de uso

- Los posibles valores por los que ordenar deben estar especificados en el description de sortBy o en un valor enumerado.

- Sería conveniente poner un criterio de ordenación por defecto si se incluye el atributo sortBy.

- En el caso de enviarse un atributo con un formato inadecuado (Ej: sortBy=\*name) o un atributo por el cual no podemos ordenar, el servicio deberá devolver un error de tipo 400 indicando el motivo del fallo.

- Es una sintaxis sencilla de escribir y leer y tiene sentido en muchos lenguajes de programación, en lugar de especificar en otro parámetro de entrada el orden (ascendente o descendente)

- Para implentar esta funcionaliadad en la capa API, el servicio backend debe soportar esta funcionalidad, en caso de no estar soportado en origen se recomienda **no desarrollar** esta característica en la capa API.

### 4.13. Obtención de recursos

En determinadas situaciones el consumidor o solo quiere recuperar algunos campos del servicio (Recursos Paraciales) o requiere mas información (Recursos Extendidos), y gustaría obtener información de los subrecursos asociados, por lo que nos vemos obligados a hacer consultas a otro endpoint.

#### 4.13.1. Recursos parciales

Situaciones en las que el consumidor no necesita obtener todos los atributos de un recurso, y se require solamente un subconjunto de estos.

- Para estos casos, se ofrece el parametro **fields** para que puedan realizar una selección de aquellos atributos del recurso que desea recibir.

- Se puede aplicar a la mayoria de los recursos, ya sean únicos como a colecciones.

- Para seleccionar aquellos atributos de segundo nivel y posteriores se usará el ‘.’ como elemento separador, haciendo uso de su código "%2E" como carácter de escapado.

- Esta opción, optimiza el uso del ancho de banda del canal ,los posibles recursos técnicos de nuestros backends, como mejorar latencias y repercutir en una mejor experiencia de usuario.


**Implementación**

- Este campo se especifican los atributos que se requieran obtener separados por coma.

  ```js
  GET /users?fields=id,name
  ```

  Del ejemplo indicado previamente, del objeto users se indico devolver los atributos “id” y “name”, ignorando el resto de atributos.

  ```json
  {
    "data": [
      {
        "id": "213432143",
        "name": "Maria"
      }
    ]
  }
  ```

- También, se puede aplicar a recursos determinados.

  ```js
  GET /users/v1/users/4564321?fields=id,name
  ```

  Si ampliamos esta capacidad y queremos filtrar por atributos que están anidados, se seguirá la estructura ofrecida por json, separando las estructuras por "."

  ```js
  GET /users/v1/users?fields=id,name,addresses.city
  ```
  ```json
  {
    "data": [
      {
      "id": "213432143",
      "name": "Maria",
      "addresses": {
        "city": "Madrid"
      }
      }
    ]
  }
  ```

#### 4.13.2. Obtención de recursos extendidos

En determinadas situaciones, la consulta de un recurso no ofrece suficiente información o se requiere obtener más información de otros recursos asociados, por lo que nos vemos obligados a hacer consultas a otro endpoint.

- Para realizar este tipo de consultas se hace el uso del query parameter llamado **expand**.

- Es un mecanismo que permite obtener los recursos relacionados en una sola llamada. <br>
Por ejemplo:

  ```js
  GET /users/213432143
  ```
  ```json
  {
    "data": {
      "id": "213432143",
      "name": "Juan"
    }
  }
  ```

  y después consultamos la información de sus vehículos:

  ```js
  GET /users/213432143/vehicles
  ```
  ```json
  {
    "data": [
      {
      "id": "3422",
      "type": "MOTO"
      }
    ]
  }
  ```

  En vez de realizar varias llamadas, se podría habilitar en el API un query param “expand”, que admitiese el ampliar la información, añadiendo la de los vehicles de la siguiente forma:

  ```js
  GET /users/v1/users/213432143?expand=vehicles
  ```
  ```json
  {
    "data": {
      "id": "213432143",
      "name": "Juan",
      "vehicles": [{
        "id": "3422",
        "type": "MOTO"
        }
      ]
    }
  }
  ```

  De este modo, utilizando el atributo “expand” nos ahorra varias llamadas.

**Implementación**

- Obligatorio que el recurso principal, como los subrecursos asociados que se expandan, deben exponer su método GET correspondiente.

- Es necesario que el usuario tenga permisos para consultar los subrecursos expandidos, es decir, tenga acceso al método GET correspondiente.

- El valor del de los atributos del expand debe ser el mismo nombre del recurso que se quiere expandir. 
> Por ejemplo si tenemos los recursos: /users/{userId}/vecicles y /users/{userId}/addresses se podría hacer en una única llamada la siguiente consulta:

  ```js
  GET /users/{userId}?expand=vehicles,addresses
  ```

- El recurso expandido se introducirá en el JSON de salida dentro de una estructura llamada como el del subrecurso expandido en camelCase (vehicles y addresses):

  ```json
  {
    "data": {
      "id": "213432143",
      "name": "Juan",
      "vehicles": [
        {
          "id": "3422",
          "type": "MOTO"
        }
      ],
      "address": {
        "city": "Salamanca",
        "line": "Calle Toro, 76"
      }
    }
  }
  ```

- Da la posibilidad de combinar con otros filtros para filtrar los recursos a recuperar.

  ```js
  GET /users?name=MAria&expand=vehicle,addresses
  ```
  ```js
  GET /users/123?expand=vehicle&fields=name,vehicle.type
  ```
  ```json
  {
    "data": {
      "name": "Juan",
      "vehicles": [{
        "type": "MOTO"
        }
      ] 
    }
  }
  ```

  Hay que tener cuidado con este tipo combinación pues puede dificultar el desarrollo.

- No se permite el uso de expand sobre subrecursos que tienen paginación, debido a que esto generaría una respuesta del servicio muy compleja.

### 4.14. Mime-types

- Información unica, a parte de las URLs, visible desde el exterior son las representaciones de los recursos, por lo que conviene que la misma sea homogénea y multiformato (JSON, XML, HTML, etc).

- Es en este punto donde entra en juego los Mime-types que sirven para tipificar el contenido que se envía en el cuerpo del mensaje de una petición o respuesta HTTP [RFC-6838](https://datatracker.ietf.org/doc/html/rfc6838).

- Los diferentes tipos de media types pueden consultarse en [RFC-1700](https://datatracker.ietf.org/doc/html/rfc1700),página 95 y 96, siendo los mas utilizados:

  - **application/json** [RFC-4627](https://datatracker.ietf.org/doc/html/RFC4627) Para el manejo de datos.
  - **application/octet-stream** [RFC-2046](https://datatracker.ietf.org/doc/html/RFC2046) Para datos binarios arbitrarios, es decir, sin ningún tipo de formato preestablecido.
  - **application/x-www-form-urlencoded** [RFC-1686](https://datatracker.ietf.org/doc/html/RFC1686) Para datos enviados form url encoded, es el valor por defecto cuando se envían datos de un form html
  - **application/pdf** [RFC-8118](https://datatracker.ietf.org/doc/html/RFC8118) Para documentos PDF application/xml, text/xml. [RFC-3026 ](https://www.rfc-editor.org/rfc/rfc3026 ) Para ficheros en formato XML. Además se recomienda el uso del parámetro charset.
  - **text/html** [RFC-2854](https://datatracker.ietf.org/doc/html/RFC2854) Para ficheros en formato HTML. Se recomienda el uso del parámetro charset.

## 5. Gestión de Errores API

Para la evolución y mantenimiento de los servicios, se debe desarrollar una buena gestión de errores, de forma que se provea un mensaje de error útil, en un formato conocido y facilmente consumible.

El servicio ddebera devolver códigos de status HTTP prácticos. Los errores del servicio generalmente caen dentro de 2 tipos: la serie de códigos 4XX para problemas en el cliente y la serie de códigos 5XX para problemas asociados en el servidor. 

La representación de un error debería no ser diferente a la representación de cualquier recurso, con su propio conjunto de campos. Como mínimo, el servicio debería normalizar todos los errores de las serie 4XX y 5XX. En la mayoría de los casos, en lo relativo a la devolución de errores funcionales en los servicios, debido a su complejidad, los códigos HTTP suelen cubrir todas las casuísticas posibles.

La composición de este mensaje de error, es la siguiente:
  - Un **código de error único (code)**, que pueda ser buscado para más detalles en la documentación. Este campo debe ser legible (*human readable*), por tanto no debería ser un código numérico, sino alfanumérico. Campo obligatorio.
  - Un **mensaje de error útil (message)**, que describa el error. Como recomendación y por seguridad se considera que el contenido de este atributo no debe contener valores de datos internos. Campo obligatorio. 
  - Un **nivel de error (type)**, que defina los diferentes niveles de gravedad de los errores. Campo obligatorio cuyos valores serán los siguiente: 

    **Nivel**	| **Descripción**                                                            |
    ----------|----------------------------------------------------------------------------|
    CRITICAL  | Indica un error que impide el funcionamiento de la aplicación completa.    | 
    FATAL	    | Errores muy graves que presumiblemente harán abortar la ejecución.         |
    ERROR	    | Errores que aún podrían permitir que la aplicación continuase ejecutándose.|
    WARNING   |	Situaciones potencialmente dañinas                                         |
    INFO      | Mensajes informativos que resalten el progreso de la aplicación            |

  -	Una **descripción detallada (description)**. Campo opcional.

A continuación se muestra la estructura de error JSON definida:

```json
{
  "messages": [
    {
      "code": "invalidParameters",
      "message": "There are invalid parameters in the request.",
      "type": "ERROR",
      "description": "Address is not valid. Invalid character: '@'"
    }
  ]
}
```

Para más información sobre la propagación de errores, cuándo y para qué métodos usarlos, seguir leyendo [Propagación de Errores Funcionales](./102_propagaci%C3%B3n_errores_funcionales.md)

## 6. Seguridad

La seguridad de las API definidas dependerá completamente de la arquitectura en la que se implementen, es necesario la revisión del documento de definición de [Arquitectura Técnica Seguridad](./103_arquitectura_tecnica_seguridad) donde se indica un detalle completo de la seguridad definida. 

### 6.1. Principios de Seguridad

Para establecer la arquitectura de seguridad de APIS, se establecen unos principios en los cuales confiamos para implementar la seguridad:

Principio | Descripción                                                |
----------|------------------------------------------------------------|
**Seguridad end-to-end** | Primer principio, significa que tenemos una seguridad definida e implementada desde el principio hasta el final del proceso, que nos permite garantizar la seguridad de los servicios desde su exposición como API (protegidas vía JWT) hasta el consumo de servicios de back-end, como por ejemplo de SAP (protegidos vía usuario y contraseña).|
**Basado en la Configuración**|	El segundo principio, significa que tenemos establecido una implementación de la seguridad basada en la configuración, lo que nos permite aislar desarrollos de seguridad.<br>Así la protección de las APIs es vía configuración, indicando qué políticas aplicar (ejemplo JWT) sin necesidad de implementar lógica específica en la API. Así, los desarrolladores no necesitan conocer ninguna característica de implementación de la seguridad, estarán aislados de ella y, por tanto, no pueden comprometerla.|
**Seguridad Integrada** |	El tercer principio,es la seguridad que está integrada en la arquitectura de APIs (formada por API Gateway + IdP) lo que nos permite reducir la exposición ante ataques.<br>No habrá componentes fuera de la arquitectura que proporcionen seguridad: la arquitectura contendrá todos los controles de seguridad, evitando la aparición de vulnerabilidades que ocurren cuando son los desarrolladores de las APIs los que desarrollan piezas a medida con niveles de seguridad inadecuados.|
**Servicios Externos de Seguridad** |	Con el cuarto principio, se establece que la arquitectura tiene la flexibilidad de integrarse con los servicios de seguridad externos que nos permite no tener dependencias con los proveedores.<br> Así, el IdP (IdentityServer) está desacoplado del API Gateway, de tal manera que fácilmente se pueda eliminar un vendor de la arquitectura.|
**Seguridad centrada en APIs** | Como quinto principio, aplicamos la seguridad centrada en la API para la protección de amenazas. La arquitectura logra esta protección a través de una arquitectura con componentes que garantizan la seguridad de las APIs, incluyendo tanto protecciones anti hacking como controles de autorización.|
**Dominios de usuario**	| El sexto principio(User Realms), establece una importante funcionalidad dentro de la evolución de la arquitectura y es que las mismas APIs pueden ser consumidas independientemente de qué proveedor de identidad es el que ha realizado el login. <br> Por ejemplo, las mismas API pueden usarse para aplicaciones usadas por usuarios que han iniciado sesión en aplicaciones internas de Axpe, o cualquier otro dominio de usuario, ya que diferentes dominios son soportados en la misma implementación.

### 6.2. Políticas


Tipo de Política 	|  Política    | Descripción  |
------------------|--------------|--------------|
Anti-hacking      |	IP Blacklist | 	Se utiliza para definir un conjunto de IPs de las que no se van a aceptar peticiones,  ya sea de manera permanente o de manera puntual ante un ataque.|
|                 |IP Whitelist  | Se utiliza para definir un conjunto de IPs que van a ser desde las únicas desde las que se van a aceptar peticiones, por ejemplo para garantizar que todo el tráfico entrante solo llega desde la máquina del WAF|
|                 | JSON Thread Protection |	Sirve para controlar que una API no es atacada por un tercero que intente por ejemplo enviar un mensaje JSON con un tamaño de cientos de megas, o por ejemplo un mensaje JSON con cientos de miles de nodos anidados recursivamente.|
|                 | CORS	       | Sirve para permitir que una web app acabe lanzando llamadas de APIs a pesar de haber sido descargada de un dominio diferente al del API Gateway
Seguridad       	| JWT	         | Se utiliza para validar que todas las peticiones entrantes llevan un token JWT el cual se debe haber obtenido previamente de un IdP|
|                 | Client ID	   | Se utiliza para validar que el client ID (API Key) está presente como cabecera. Habitualmente las políticas JWT también ofrecen esta capacidad.|
Control consumo   |	Rate limit	 | Se utiliza para limitar el número de veces que una determinada API se ejecuta por segundo, minuto u hora.

### 6.3. Buenas prácticas
Resumen de las recomendaciones de [OWASP API Security](https://owasp.org/www-project-api-security/).

- No utilizar identificadores que se puedan adivinar (mejor usar UUIDs), implementar controles de seguridad que aseguren que el usuario que está llamando a un servicio sea el dueño de los datos que está obteniendo y no exponer IDs internos sino usar otros que no se puedan adivinar y luego mapearlos internamente podrían ayudarnos a estar protegidos ante esta amenaza.
- Restringir los permisos de un token, fomentando el uso de scopes.
- Las APIs deberían filtrar los datos que exponen, no limitándose a exponer todos los posibles.
- Limitar el uso de las APIs para evitar ataques de denegación de servicio. Estas limitaciones pueden ser a nivel de usuario, API, recurso o método.
- No mezclar en el mismo API tareas que deban ser ejecutadas por distintos roles. Por ejemplo, no mezclar tareas destinadas a ser usadas por usuarios y administradores.
- Tratar de evitar vincular los modelos de datos existentes con los datos enviados por el consumidor del API.
- Tener en cuenta la seguridad de los elementos usados en las implementaciones de las APIs, y mantenerlas actualizadas y con parches de seguridad correctos.
- Usar la validación de entradas como método de prevención de ataques de inyección de código.
- Mantener una gestión de APIs correctas, manteniendo un control correcto de las piezas que se securizan y cómo, documentación correcta, control de versionado y automatizaciones donde sea posible.
- Mantener un registro y monitorización que permita reaccionar rápidamente ante brechas de seguridad, al ser posible con alarmas que avisen de situaciones anómalas. Además, estos logs deben estar a su vez con la suficiente seguridad.

## 7. Modelo de datos

Con un enfoque al modelo Data-Centric cuyo objetivo principal es que está detrás de una API se debe especificar las propiedades o atributos asociado a esos recursos modificables por dicha API de una forma abstracta (es decir, independiente de la implementación). 

En esta sección se define el procedimiento donde se definen los tipos de recursos comunes como, estructura común de [errores](../../errors.json), [cabeceras](../../headers.json) comunes, reutilizables para cumplir con estándares. También se definen las entidades (o recursos) de negocio, sobre las cuales se diseñarán las estructuras de payloads que contendrán las API. Para mas detalles de las estructuras más comunes ir al fichero [commons](../../common.json)

Una práctica muy útil es la definición de una plantilla OpenAPI que contenga las estructuras comunes, los esquemas de seguridad, respuestas de cada verbo, etc, en base a los estándares definidos. El DDD y entidades de negocio son recursos complementarios a las plantillas que, en conjunto, generan la base para el diseño de las API.

## 8. Estandares

[RFC-3986](https://tools.ietf.org/html/rfc3986)
Estandar que se utiliza para definir la sintaxis genérica de la URI .

[RFC-7231](https://tools.ietf.org/html/rfc7231)
Protocolo de transferencia de hipertexto: HTTP/1.1 .

[RFC-6838](https://tools.ietf.org/html/rfc6838)
Especificaciones del tipo de medio y procedimientos de registro.

[RFC-6749](https://tools.ietf.org/html/rfc6749)
Marco de autorización de OAuth 2.0

[RFC-7519](https://tools.ietf.org/html/rfc7519)
Definición del Token web JSON (JWT) 

[RFC-7523](https://tools.ietf.org/html/rfc7523)
Perfil de token web JSON (JWT) para la autenticación y autorización del cliente OAuth 2.0
 
[RFC 3339](https://tools.ietf.org/html/rfc3339)
Este documento especifica un protocolo de seguimiento de estándares de Internet para la comunidad de Internet, en cual se define un formato de fecha y hora para uso en protocolos de Internet que es un perfil del estándar ISO 8601 para la representación de fechas y horas usando el calendario gregoriano.


[ISO 639-1](https://www.iso.org/iso-639-language-codes.html)
Códigos de idiomas 
- [BCP47](https://tools.ietf.org/html/bcp47): etiquetas para identificar idiomas.


[ISO 3166-1](https://www.iso.org/iso-3166-country-codes.html)
Códigos de países 

[ISO 4217](https://www.iso.org/iso-4217-currency-codes.html)
Códigos de moneda 

[ISO 60559:2011](https://www.iso.org/standard/57469.html)
Esta norma especifica formatos y métodos para la aritmética de coma flotante en sistemas informáticos: funciones estándar y extendidas con precisión simple, doble, extendida y extensible y recomienda formatos para el intercambio de datos.

- [IEEE 754-2008](https://standards.ieee.org/standard/754-2008.html)
Estándar para aritmética de punto flotante.


## 9. Glosario

**API-First**
COMPLETAR

**API**

API es un conjunto de funcionalidades utilizadas por cualquier otra persona, que abarca un conjunto de funcionalidades implementadas y gestionadas como servicios REST.

**API INTERNAS**

APIs para aplicaciones de la compañía (internet o intranet).

**API EXTERNAS**

APIs para aplicaciones no que no pertenecen a la compañia (partners).

**GESTIÓN DE API / API MANAGEMENT**

- Es el proceso de creación y publicación de APIs, haciendo cumplir sus políticas de uso,controlar el acceso, nutrir a la comunidad de suscriptores, recopilar y analizar el uso estadísticas e informes sobre el rendimiento.
- Implica la catalogación de la API para su consumo (publicación), exposición (impulsar), controlar, monitorear (supervisar) y ejecutar de manera segura, confiable y entorno escalable.

**ADMINISTRADOR DE API / API MANAGER**

- Es para definir y desarrollar APIs.
- Es para gestionar el entorno de la API
- Unifica la visión de la API.

**PUERTA DE ENLACE API / API GATEWAY**

  - Es donde se procesan "físicamente" las transacciones de las APIs.
  - Permite diferentes modelos de consumo relacionados con las entidades lógicas. 
  - Se considera única por entidad y caso de consumo.
  - Sus características incluyen funciones tales como:
    - Autenticación.
    - Aplicación de la política de seguridad.
    - Balanceo de carga.
    - Gestión de caché.
    - Resolución de dependencia.
    - Gestión de contratos y acuerdos de nivel de servicio (SLA).

**PORTAL PARA DESARROLLADORES DE API / API DEVELOPER PORTAL**

  - Visibiliza y gestiona a las APIs producidas desde la Organización Productora.
  - Sus principales características:
    - Suscripción de API
    - Socialización.
    - Descubrimiento.
    - Retroalimentación.
    - Foros.
    - Gestión de Organización de Consumidores.

**JWT (TOKEN WEB JSON)**

Prootocolo de autenticación estándar que le permite la creación de tokens de seguridad con información, como Issuer, Audience, Expiration tiem, kid, etc. 

**AUDIENCIA**

Identificar el destinatario del token JWT al que pertenece.

**SWAGER**

Es una especificación abierta para la definición de Rest APIs, definición de estructura, etc que genera automáticamente una documentación API simple e interactiva.

**YAML**

Es uno de los formatos de serialización de datos utilizados por la especificación Swagger.


**KEBAB CASE**

Estilo de escritura donde se usa el guión bajo para separar palabras. Se usa para definir la URL, exceptuando los pathparameters que debera ir en camelCase al igual que su atributo.

**CAMEL CASE**

Estilo de escritura donde la primera letra de cada palabra debe ir en mayúsculas. Se debe aplicar a todos los atributos exceptuando en el nombre de los recurso. 


**OAUTH 2.0**

Es un protocolo de autorización estándar. Se basa en la sencillez para el cliente-desarrollador.

**SCOPE**

Es el parámetro de entrada en la solicitud de un token Oauth, que gestiona el consentimiento sobre las operaciones de una API.

**OPERACIÓN IDEMPOTENTE**

Una operación idempotente implica que el estado del recurso será igual al estado devuelto por la primera invocación, independientemente del número de llamadas realizadas posteriormente.

**OPERACIÓN SEGURA**

Las operaciones seguras no implica peligro alguno en su ejecución, es decir, el estado de cualquier recurso no será alterado o se generará uno nuevo.

**OPERACIÓN INSEGURA**

Las operaciones inseguras implican cierto grado de criticidad en su ejecución (generación de recurso nuevo, alteración de recurso existente...)

**TIPO DE DATOS FORMATOS RECOMENDADOS**

- [RFC 3339](https://datatracker.ietf.org/doc/html/rfc3986) para formatos de fecha/hora.
- [ISO 20022](https://www.iso20022.org/standardsrepository/) para importes con doble tipo de dato (16 dígitos con 5 obligatorios y fijos)
- Códigos de país [ISO 3166-1](https://www.iso.org/iso-3166-country-codes.html) alpha2.
- Código de idioma [ISO 639-1](https://www.iso.org/iso-639-language-codes.html).
- [BCP-47](https://tools.ietf.org/html/bcp47) (basado en ISO 639-1) para variantes lingüísticas.
- Códigos de moneda [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html ).
- entero > int32 > entero entre -231 y 230.
- entero > int64 > entero entre -263 y 262.
- entero > bigint > número entero con signo arbitrariamente grande.
- número > float > IEEE 754-2008/ISO 60559:2011 binary64 número decimal.
- número > doble > IEEE 754-2008/ISO 60559:2011 binary128 número decimal.
- número > decimal > número decimal con signo arbitrariamente preciso.
- Los datos de descripciones documentados deben estar alineados con ejemplos documentados en swagger.