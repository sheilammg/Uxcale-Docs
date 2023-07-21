# ¿Qué es Spectral?

**[Spectral](https://stoplight.io/open-source/spectral)** es un linter JSON/YAML opensource, que permite crear, definir reglas, validar dichas reglas y aplicarlas para ficheros que contengan OAS versión3, Swagger versión 2 y AsyncAPI v2.

## Caracteristicas
Es una herramienta que nos facilita la validación de ficheros de tipo OpenAPI 2.X, 3.X. Por defecto ofrece un conjunto de reglas de validación básicas, pero además con Spectral se puede:

- Crear o definir nuevas reglas para aplicar a objetos dentro de ficheros JSON o YAML.
- Modificar las reglas por defecto.
- Usar JSON Path para definir en qué puntos de los ficheros JSON aplica una regla en concreto.
- Crear funciones personalizadas para casos de uso avanzados.
- Validar JSON contra Json Schemas

## Conceptos

Ante de integrar esta herramienta en el flujo de trabajo de diseño, previamente deberemos entender ciertos conceptos generales par aenter la funcionalidad: 

1. **Rulesets**: Son ficheros que contienen las reglas y funciones. Puede tener cualquier nombre, pero para integarlo e iniciar la revisión con Stoplight Studio debe existir al menos un fichero como nombre **.spectral.yml** para que inicie la validación.

    ```yaml
      formats: 
        - 'oas3'
      extends: 
        - 'spectral:oas'
        - 'spectral:asyncapi'
        - 'oas-rules-custom.yaml'
        - 'https://example.com/company-ruleset.yaml'
      rules:
        my-rule-name:
          description: Tags must have a description.
          given: $.tags[*]
          severity: error
          then:
            field: description
            function: truthy
    ```

2. **Rules**: Son [reglas](https://meta.stoplight.io/docs/spectral/01baf06bdd05a-rulesets), que se definen y que posteriormente se utilizarán para revisar y validar la especificación de la API.

    ```yaml
      formats: 
        - 'oas3'
      rules:
        my-rule-name:
          description: Tags must have a description.
          given: $.tags[*]
          severity: error
          then:
            field: description
            function: truthy
    ```

3. **Functions**: La *function* se asocia a una regla con el objetivo de verificar el cumplimiento de dicha regla. Se clasifican en predefinas o personalizadas que es código totalmente configurable. 

    En el caso de las *Reglas pesonalizadas* deben de estar definidas dentro de la ruta "**/functions**". Se escribiran en NodeJS y se tratará de aplicar buenas prácticas de código.


La **rule** contiene una propiedad llamada "**then**", dentro de ella existe otra propiedad que tiene como nombre "**function**" la cual será la asignada de relacionar la "rule" con la "function".

  Reglas predefinidas:
   - alphabetical
   - enumeration
   - falsy
   - length
   - pattern
   - casing
   - schema
   - schemaPath
   - truthy
   - undefined
   - unreferencedReusableObject
   - xor
   - typedEnum  
   
Para mayor compresión del funcionamiento de la esta funciones core ir al al apartado [**Core Funtions**](https://meta.stoplight.io/docs/spectral/docs/reference/functions.md) de  la documentación.

## Estructura de las Rules
Vamos a detallar la estructura de propiedades de las [rules](https://meta.stoplight.io/docs/spectral/e5b9616d6d50c-custom-rulesets):

```yaml
  rules:
    info-description-formatted:
      description: Tags must have a description.
      message: 'The {{error}} to the {{property}}'
      type: style
      severity: error
      recommended: true
      given: "$.info"                
      then:
        field: description
        function: truthy
      tags:
        - api
```

### Description
Campo que indica una breve descripción de la regla definida.

### Message
Propiedad se que se utiliza para retornar el error. Se pueden utilizar distinto funcionalidades pre-defininas dentro del mensaje de salida.
  -  {{error}} : Error devuelto por la función.
  -  {{description}} : Descripción general de la regla.
  -  {{path}} : Retorna la ruta donde se producio el error.
  -  {{property}} : Devuelve valor del campo de la especificación donde ocurrió el error.
  -  {{value}} : Retorna el valor devuelvo por la función.

### Type    (REVISAR)
Esta propiedad indica el tipo de la regla, puede ser de tipo "**style**", o "**validation**". 

### Severity
Propiedad que determina el tipo de severidad se quiere indicar, se puede clasificar en **error**, **warn**, **info** y **hint**. Por defecto es **warn**.

### Given
Es una propiedad obligatoria en cada definición de una *rule* y puede ser cualquier expresión JSONPath válida. Se puede utilizar esta herramienta [JSONPath Online Evaluator](https://jsonpath.com) para determinar la ruta que se desee.

| JSONPath  | Descripción                                  |
|-----------|----------------------------------------------|
| $         | El objeto/elemento root.                     |
| @         | El objeto/elemento actual.                   |
| *         | Wildcard, Relacionado a todos los elementos. |
| ?()       | Aplica filtro sobre la expresion.            |

### Then
La propiedad **then** indica que verificación hay que realizar cuando se cumple el **given**. 

Esta propiedad esta relacionada y contiene otras dos propiedades necesarias para su ejecución.
  - **field**: Especifíca el campo donde aplicará la *rule*. (Opcional)
  - **function**: Especifíca la función a utilizar en la rule y es un campo obligatorio. En este caso, se podría utilizar una *función Core* o una *personalizada*. Ej: **lenght**. 
  - **functionOptions**: Se indica los parámetros de entrada para dicha función, varía según la función que se utilice. (Requerido)


## Instalación
Existen dos formas de hacer uso de la heramienta, desde la línea de comandos y desde Stoplight, a continuación se detallan:

  - Instalación de Spectral desde línea de comandos
    Tener instalado NodeJS en el sistema operativo. [Descarga NodeJS](https://nodejs.org/es/download/).

    Ejecutar la siguiente comando en la consola de nuestro sistema operativo.    
    ```sh
    npm install -g @stoplight/spectral
    ```

  - Instalación de Spectral en Stoplight Studio:

    Como indicado previamente, Spectral viene ya integrado con Stoplight Studio, la opción para activarlo es la pestaña que se encuentra en la parte inferior derecha, con nombre **Issues**.

## ¿Como crear reglas?
Para la creación se deberá tener un archivo de nombre **.spectral.yaml**, en el cual servirá de almacén de todas la reglas.

  1. **Default rule**:

  ```yaml
    rules:
      info-description-formatted:
        description: Tags must have a description.
        message: 'The {{error}} to the {{property}}'
        type: style
        severity: error
        recommended: true
        given: "$.info"                
        then:
          field: description
          function: truthy
        tags:
          - api
  ```

  2. **Custom rule**:

  ```js
    module.exports = (targetVal) => {
      if (input !== "hello") {
        return [
          {
            message: 'Value must equal "hello".',
          },
        ];
      }
    };º
  ```


**RECOMENDACIÓN** 

**\*** Spectral tiene un conjunto de reglas [oas](https://meta.stoplight.io/docs/spectral/4dec24461f3af-open-api-rules) incorporado, con OAS siendo la abreviatura de la Especificación OpenAPI. 

**\*\*** Spectral tiene un conjunto de reglas [asyncapi](https://meta.stoplight.io/docs/spectral/1e63ffd0220f3-async-api-rules) incorporado para la especificación AsyncAPI. 
