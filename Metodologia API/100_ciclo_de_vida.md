# **Ciclo de vida del API**

## Índice

- [1. Fase de diseño](#1-fase-de-dise%C3%B1o)
   - [1.1. Planificación](#11-planificaci%C3%B3n)
   - [1.2. Diseño de la definición](#12-dise%C3%B1o-de-la-definici%C3%B3n)
   - [1.3. Validación de la definición](#13-validaci%C3%B3n-de-la-definici%C3%B3n)
- [2. Fase de implementación](#2-fase-de-implementaci%C3%B3n)
   - [2.1. Creación](#21-creaci%C3%B3n)
      - [2.1.1. Objetivos](#211-objetivos)
      - [2.1.2. Productos de entrada](#212-productos-de-entrada)
      - [2.1.3. Productos generados](#213-productos-generados)
      - [2.1.4. Herramientas](#214-herramientas)
      - [2.1.5. Audiencia](#215-audiencia)
      - [2.1.6. Actores](#216-actores)
   - [2.2. Implementación](#22-implementaci%C3%B3n)
      - [2.2.1. Objetivos](#221-objetivos)
      - [2.2.2. Productos de entrada](#222-productos-de-entrada)
      - [2.2.3. Productos generados](#223-productos-generados)
      - [2.2.4. Herramientas](#224-herramientas)
      - [2.2.4.1. Audiencia](#2241-audiencia)
      - [2.2.5. Actores](#225-actores)
- [3. Fase de gestión](#3-fase-de-gesti%C3%B3n)
   - [3.1. Publicación](#31-publicaci%C3%B3n)
   - [3.2. Monitorización y analíticas](#32-monitorizaci%C3%B3n-y-anal%C3%ADticas)
   - [3.3. Retirada](#33-retirada)


![Ciclo de vida del API](/Ciclo%20de%20Vida/Guia%20de%20Dise%C3%B1o/_images/diagrama-ciclo-vida.png)

---


## 1. Fase de diseño

Fase que compuesta por las estapas de planificación de la API, su objetivo funcional, diseño y validiación de la interfaz.

### 1.1. Planificación e identificación

En la fase de planificación se enfoca en las necesidades del negoción para obtener un conjunto de APIS que aporte valor. Para ello nos deberemos de hacer la siguiente pregunta: ¿Realmente necesito un API?, es decir lo que nos están pidiendo es realmente un API y que no es otro tipo de solución de software, ya que muchas veces pensamos que todo se tiene que resolver creando un API. La idea de crear un API es la de exponer una funcionalidad clara de negocio, bien sea para ser consumida de forma interna por la organización o bien consumida por una entidad externa y en este caso, incluso monetizarla.

En definitiva esta fase se encarga de analizar las necesidades del negocio para obtener un conjunto de APIs que aporten valor, dando como resultado un listado de APIs candidatas a ser construidas y publicadas en el catálogo de servicios de la organización.

El proceso de planificación se puede enfocar de las siguientes formas:

- **Top-down**: iniciado desde negocio como una planificación reactiva.
- **Bottom-up**: planificación proactiva desde tecnología.

Desde el equipo de gobierno tendrán los siguientes objetivos:

- Guiar a los responsables de negocio para definir APIs que aporten valor y aterrizar los requisitos funcionales.
- Soporte a los equipos en la estructuración y definición de las APIs objetivo.
- Mantener un catálogo de APIs, versionadas, que sirva de referencia.
- Fortalecer el modelo API First en la organización.

### 1.2. Diseño de la definición

El objetivo es definir la interfaz de los recursos de las distintatas APIs, se identifican operaciones, la estructura de los cuerpos de entrada/salida, formatos de la respuesta y códigos HTTP implicados.
En esta fase, se define la funcionalidad de negocio en la que se enfoca la esta API, a quien va dirigida y los objetivos, dando como resultado el diseño completo de la interfez en un documento de análisis.

El equipo de API tiene el objetivo de crear y mantener a una base de conocimiento, preparada por los expertos de negocio y los equipos de análisis en conjunto con el propio equipo, para su uso posterior en subsecuentes diseños.


### 1.3. Validación de la definición

En esta fase, desde el equipo de gobierno, se supervisará el diseño, verificando el complimiento de la nomenclatura establecida y asegurando que las APIs definidas aportarán valor al catálogo.
Se hará una revisión global previa a la escritura de la API con el fin de asegurar el cumplimiento de las guías de diseño y normalizaciones por el tipo de API correspondiente.

Una parte fundamental, que comparten ambas fases (Diseño y Validación), es en este punto del **versionado**, ya que normalmente la API irá evolucionando a medida que se agregan nuevas funcionalidades del negocio. Para el versionado de nuestras APIs seguiremos un estilo de [versionamiento semántico](https://semver.org/), donde:

1. El formato de la versión indicada en el documento de especificación de la API: `[MAJOR].[MINOR].[PATCH]`:
   1. `[MAJOR]` Cambios que hacen a la API incompatible con los desarrollos anteriores.
   1. `[MINOR]` Agregar nuevas funcionalidades, sin afectar a las anteriores.
   1. `[PATCH]` Corrección de errores (bugs) sobre la versión.
      > ejemplo: version 1.2.5
2. El versionado mayor irá indicado en la url del recurso, y solo se tienen en cuenta los cambios mayores, ya que son estos los que indican incompatibilidades entre las versiones, y por tanto los que afectan directamente a los consumidores (obligando a actualizar sus desarrollos para adaptarse a los nuevos requisitos de esta versión).
   > ejemplo: 'https://www.axpe.com/contexto/v2/recurso'

## 2. Fase de implementación

Una vez finalizado el diseño y validado el resultado por el equipo de API, pasaremos a la construcción de la API. En esta se escribe la especificación de la API usando como base la plantilla correspondiente y aplicando las guías de diseño, teniendo como referencia para la construcción el análisis funcional. Una vez escrita la especificación, se procede a la publicación para los equipos de desarrollo que llevarán a cabo las tareas de implementación y al grupo de consumidores que integrarán en sus aplicaciones las llamadas al API correspondientes. En paralelo, el equipo de API se encargará de llevar a cabo la configuración de políticas de seguridad, cuota y consumo.

### 2.1. Creación

Una vez analizada y documentada la interfaz de la API correctamente, se procede a escribirla en un lenguaje y generar la de especificación API(Swagger/Raml). En esta especificación se generar los métodos, parámetros y protocolos involucrados y previamente planificados y validados en la fase de previa (Diseño).

Se desarrollara la especificación API aplicando unas buenas prácticas y guiado por el documento de [Diseño](./100_dise%C3%B1o_de_api.md). Los métodos identificados, con sus respectivos parámetros de entrada aplicando buenas prácticas, orientando a que el nombre de la operación sea lo suficientemente legible, claro y conciso para que cualquier usuario pueda entender la funcionalidad de dicha operación. 

La estructura de los esquema de entrada y salida de los distintos métodos, se crearán o se reutilizarán dependiendo de la necesidad. Se tedrá que revisar el repositorio de modelos, donde se encuentra un listado de esquemas (modelos). También se deberá tener en cuenta los esquemas para los diferentes tipos de errores que retorne la API ya sea errores funcionales o técnicos y dependiendo de que nivel sea la API se retornará mayor o menor información.

En cuanto a la seguridad definida en la API, se procederá según los estándares de autenticación y autorización predefinidos por la compañia Axpe, estas acciones deberan ser supervisada y validadas con las áreas correspondientes.

Finalizada la creación de la especificación API, se deberá validar con el equipo de gobierno la definición aportada y comprobar que cumple con lo definido en la fase de diseño.  Se verificará  que se ha palicado las reglas  indicadas en la guía de diseño, estándares API, buenas prácticas, y que se esté aplicando las reglas base predefinidas con la herramienta Spectral y que está suficientemente documentada y con los ejemplos de al menos un caso de uso por operación.

En el caso que se genere esquemas de datos, se debe actualizar el listado de esquemas ya sea modificando el existente o agrengándolo.

#### 2.1.1. Objetivos

Los objetivos principales a tener en cuenta son los siguientes:

- Creación de la especificación de la API en OpenAPI v3.
- Validación de la especificación de la API en OpenAPI V3.
- Creación y validación de los mecanismos de seguridad en los recursos expuestos.

#### 2.1.2. Productos de entrada

- Listado de modelos o esquemas de datos a utilizar.
- Documento para diseñar la API - [Guia Diseño de APIs](100_dise%C3%B1o_de_api.md).

#### 2.1.3. Productos generados

- Especificación de la API en OpenApi v3.

#### 2.1.4. Herramientas

- Stoplight Studio/ Visual Studio Code
- Spectral
- Guía de diseño.
- Repositorio único de esquemas de datos. 

#### 2.1.5. Audiencia

| Audiencia          | Responsabilidad                                                                                                       |
| ------------------ | --------------------------------------------------------------------------------------------------------------------- |
| Diseñador API      | Responsable de llevar a cabo la generación de la especificación API                                                   |
| Evangelista API    | Validar que la especificación generada cumpla con la guía de diseño, estándares, buenas prácticas y reglas Spectral.  |
| Equipo de gobierno | Validar que la especificación creada cumpla con lo definido en la fase de diseño y reglas Spectral.                   |

#### 2.1.6. Actores

| Actor            | Afectación                     |
| ---------------- | ------------------------------ |
| Equipo funcional | Análisis de los requerimientos |

### 2.2. Implementación

En esta fase se implementa la lógica de negocio que existe por debajo de la API, partiendo siempre como base de la especificación API creada en el estaodo previo. Esta desarrollo consite en los mapeos de los campos como en el proceso de ensamblado con el backend. El cómo se lleve a cabo la implementación tanto del cliente que consumirá la API como el backend de lógica de negocio, estará fuera del ámbito de esta fase.

El equipo encargado del desarrollo tendrá que notificar al equipo de gobierno cuando se tenga publicado el servicio que implementa la especificación para que se haga la integración del servicio. 

Por último, se tendrá encuanta y paso importante a la hora del desarrollo,como al finalizar, debemos de asegurarnos que la API pueda ser consumida en modo MOCK mediante la herramienta mocking en local **PRISM**.
Esta plantaforma de Sandbox local deberán permitir al desarrollador realizar pruebas simples a la API sin necesidad de llevar a cabo integraciones complejas que dificulte su adopción.

#### 2.2.1. Objetivos

- Desarrollar de la lógica de negocio.

#### 2.2.2. Productos de entrada

- Especificación de la API.

#### 2.2.3. Productos generados

- SDK back/front.

#### 2.2.4. Herramientas

- Generadores de SDK.
- Stoplight con PRIMS.

##### 2.2.4.1. Audiencia

| Audiencia            | Responsabilidad                                                                     |
| -------------------- | ----------------------------------------------------------------------------------- |
| Equipo de Gobierno   | Encargado de facilitar su integración y la generación de la documentación adecuada. |
| Equipo de Desarrollo | Equipo encargado de la desarrollar los microservicios de la API.                    |

#### 2.2.5. Actores

N/A

## 3. Fase de gestión

Se incluyen todas las tareas requeridas para la monitorización, analítica, evolución y mantenimiento de la APIs.

### 3.1. Publicación

En esta fase se encarga de lleva a cabo la publicación en el catálogo de APIs. Se podrán a disposición de la comunidad de desarrolladores, para que asi comience a utilizarla. Es recomendable y necesario que la API esté bien documentada para favorecer su utilización y la libertad de uso entre los desarrolladores, para ello se deberá estar correctamente catalogada a través de etiquetas que faciliten su búsqueda e identificación dentro del grupo de APIs.

El equipo de gobierno se encargará de revisar las siguientes tareas:

- Publicación de las API.
- Definir los canales de comunicación entre los distintos participatnes (gobierno, negocio y tecnología).
- Apoyar a la comunidad de desarrolladores, obtenido y valorando el feedback de su uso y funcionalidad.
- Fomentar la reutilización de las APIs previamente publicadas.

### 3.2. Monitorización y analíticas

En esta estapa se buscar definir y identifiar los indicadores que ofrezcan mayor información a la hora de monitorización y analíticas de las APIs observadas. Para ello se tendrán los siguiente criterios:

- Buscar y crear la confianza en un modelo de API.
- Entender los beneficios y las necesidades de los usuarios asociados ecosistema.
- Gestionar los servicios y las versiones de las APIs.
- Entender y cuándo se pueden retirar los servicios.
- Preveer y adelantarse al crecimiento del tráfico producido.

Se incluiran los KPIs necesarios que permitan identificar y analizar oportunidades de negocio, dotando de información en tiempo real a los equipos de Marketing y Operaciones.

En el aspecto técnico, se tendrán y proveerán elementos de medición del rendimiento de la API, tiempos de ejecución, retrasos o latencia en las comunicaciones y demás elementos técnicos que doten de información para mejorar la infraestructura en el que transitan las API.

### 3.3. Retirada

Esta fase se compone en definir los medios y herramientas encargados de identificar cuando un API llega al período de decomisión. El principal objetivo y más común, es que salgan nuevas versiones de este API o nuevos API que ofrecen una funcionalidad extendida y no sea retrocompatible.

Se establecerán los instrumentos de notificación arpopiados a los consumidores suscritos a este API, dando un tiempo considerable de adaptación y no se vean impactadas por el proceso de decomisión.
