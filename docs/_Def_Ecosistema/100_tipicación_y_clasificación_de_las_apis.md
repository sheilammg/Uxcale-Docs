# Tipificación y clasificación de las APIs

Con el objetivo de mantener una adecuada organización en los dominios funcionales de la compañia y pretendiendo exponer APIs como servicios, se ha decidido generar una clasificación y tipificación en los modelos de las APIs. Teniendo en cuenta la plataforma de desarrollo e implementación donde las APIs se ejecutarán se ha generado los tres siguiente tipos:

1. API de Sistema
2. API de BaaS/Producto
3. API de Experiencia

El presente documento indica el alcance de cada uno de estos tipos de APIs, así como los principios y normalizaciones que deberán asegurar su buen uso dentro del ecosistema API. Podiendo contar con esquemas de seguridad adecuados, políticas o bien restricciones, distintos dependiendo del ámbito de la arquitectura donde se vayan a ejecutar.

## Antecedentes.

**REVISAR SI AÑADIMOS ESTE PUNTO.**

Actualmente los servicios que otorga el Backend están orientados a funcionar para el canal que los consume, lo que lleva a un acoplamiento especifico, tacito en ocasiones, donde el servicio de Backend se acopla a la pantalla de la aplicación Frontend en la que se representan los datos. Este acoplamiento ocurre en varias aplicaciones internas de la compañía.

Podemos ver otro tipo de implementación de los servicios de Backend para el canal digital, donde se ha preparado un componente de Software que se encarga de mediar entre las aplicaciones del Canal Digital y los servicios de Backend. La motivación de este componente Software es utilizar los mismos servicios de Backend que sirven al canal de Sucursales. Sin embargo, debido a las necesidades del canal digital, se han tenido que duplicar, en algunos casos los servicios de Backend para dar soporte a ambos canales.

Dentro de esta tesitura en la duplicación de los servicios Mainframe, tenemos los casos en que los servicios no solo han sído acoplados al canal, sino también a la aplicación del canal, teniendo como resultado servicios clonados, a los que (en su mayoría) se les añade alguna estructura de datos más no propia del dominio que le facilita la implementación a la aplicación del canal. Derivado de esta acción de clonación, se tienen servicios activos que podrían ya estar deprecados.

En resumen, hemos identificado los siguientes escenarios en la implementación del Backend:

-
-
-
-

Por otro lado, en las implementaciones frontales, actualmente hemos identificado los siguientes escenarios:

-
-
-
-

Conforme se vaya avanzando en la identificación de equipos participantes en el ecosistema API, es probable que se identifiquen más escenarios a comprender y normalizar para el uso estandarizado de las APIs bajo las guías de uso explicadas más adelante.

Durante la preparación de las guías de diseño de las APIs de sistema se podrán detallar estos casos de uso identificados, teniendo tendencia a crecer en las distintos escenarios posibles. Por tanto será imprescindible establecer, en conjunto con el equipo de desarrollo, los medios de adaptación con el objetivo de mantener crear diseños agnósticos al canal y con entradas y salidas de esquemas de datos globales, facilitando así el uso e integración con los servicios bancarios orientados a dominios funcionales de negocio.

## Categorización de APIs

Antes de a entrar a definir la propuesta de tipificación de APIs, se tendra la siguiente distinción:

1. **API funcionales**. Orientadas a soportar funciones de negocio.
2. **API no funcionales**. Dan soporte a las funciones de negocio, son de uso tranversal a los dominios de negocio.
3. **¿ALGUNA MAS?**
3. **API Técnicas**. 

Teniendo en cuenta esta categorización, ahora se identificarán los tipos de API con su orientación y principios que las regirán.

## Tipos de API

Dada la situación actual, se llevará a cabo un esfuerzo para llegar a un adecuado ecosistema de APIs que permita mantener una organización óptima para el definición, diseño, implementación y uso de las APIs. 

Como ya sabemos, en ocasiones se han generado servicios duplicados que recuperan información adicional para facilitar la implementación en los aplicativos, para estos casos se plantea la estrategia de consumo entre APIs de producto pertenecientes a diferentes dominios funcionales. Un ejemplo, en una entidad financiera existirán los múdulos de _Personas_ y de _Cuentas_, que son productos transversales a la mayoría de los servicios de Backend; teniendo la identificación del cliente final, y la autorización de este cliente sobre los recursos, respectivamente.

El siguiente diagrama muestra en alto nivel los tipos de API en una vista de capas, la cual representa los principales colindantes con el ecosistema en un alto nivel.

---

![Diagrama de capas por tipo de API](../_images/diagrama-tipo-api.png)

El diagrama previo muestra el modelo de tipos de API en una vista vertical, donde las APIs de experiencia están por éncima de las de recurso, representando esto que las aplicaciones de los distintos canales harán el consumo de servicios bancarioas a través de la exposición de los productos de API con orientación a la experiencia del consumidor. Luego las APIs de recurso tendrán a su disposición el acceso a las APIs de menor nivel y más cercanas a las funciones de negocio programadas en el Backend.

A continuación se hace una definición más detallada de cada tipo de API y se explican algunos de los principios y normas que los regirán durante la etapa de diseño del API.

### API de sistema

#### Funcional

Este tipo de API es la más cercana a los sistemas de información.Representan las interfaces de mayor granularidad dentro del dominio de negocio, deberán de contener las operaciones esenciales/atómicas en cuanto al manejo de los datos. Estas API tengan una relación directa con un servicios de Backend que exponga las operaciones del (sub)sistema que representan, debiendo ser _agnósticos_ a la aplicación que los consuma.

Los modelos de datos de este tipo de API deberán de ser la base sobre el que se sustentarán los servicios de negocio, por lo que debe de tenerse en cuenta el uso de esquemas de datos propios al dominio, pretendiendo minimizar el uso de modelos pertenecientes a otros dominios o bien contar con modelos compuestos. En el caso de que sea indispensable la composición de modelos en este tipo de API para la ejecución de los servicio de Backend, se deberá plantear un patrón que aplique al mayor número de servicios a implementar.

#### No Funcional

También conociadas como API de Soporte, se utilizan como medio de acceso a funciones que no son propias del dominio de negocio, sino que son un complemento o incluso pueden ser un enriquecedor de los modelos de datos propios del dominio de negocio.

> **Ejemplo**: Un caso representativo de este tipo de API es la generación de un documento, donde el API puede exponer su operación de generación de documento y habilitar parámetros para indicar el formato en que se necesita dicho documento; de esta forma cualquir dominio funcional que requiera de esta necesidad de creación de documentos, que no es una actividad propia del dominio, podrá usar esta API.

#### Técnica

Se pretende usarlas para que los equipos técnicos las utilicen y se les facilite la generación e integración de componentes de Software e Infraestructura durante el ciclo de vida de desarrollo.

> **Ejemplo**: Dada una specificación para la generación de infraestructura a través de uno de los ciclos de operaciones de desarrollo (devOps) para proveer de infraestructura requerida para la puesta en ejecución de una instancia de servicio. Se pretende trabajar de la mano con ambos equipos en la generación y adopción del API técnica.

Hasta el momento, en las definiciones que hemos indicado, solo se ha estado realizando a cabo la categorización y tipificación de APIs en el modo síncrono, bajo un estilo de arquitectura RESTFul, donde cada llamada a la API es llevada a cabo mediante una solicitud (request) y se espera una respuesta (response) bajo el protocolo correspondiente. No obstante, bajo un modelo arquitectónico enfocado a eventos, este estilo puede complicar la definición e implementación de las operaciones que no son síncronas, por consiguiete, se necesitará una guía de especifica de diseño para el uso de APIs asíncronas.

#### Asíncrona

Dada la naturaleza de este tipo de API, el uso de la misma se limitará para establecer comunicaciones de sucesos dentro de una arquitectura manejada por eventos. Su especificación se basará en la iniciativa _AsyncAPI 2.4_ a diferencia del resto que se diseñarán la especificación openAPI 3.X.


> **Ejemplo**: AÑADIR

### API de Producto (BaaS)

En esta capa se exponen los recursos del dominio de negocio a través de servicios (BaaS), representan operaciones compuestas, que agrupan una logica de negocio soportadas por las APIs de sistema. Este tipo de API, tiene como principal responsabilidad el componer la información a través de la ejecución de distintas operaciones de Backend expuestas a través de las APIs de sistema.

Este tipo de API sigue siendo agnóstico a la aplicación, de tal forma que la aplicación raíz no implique la implementación de lógica especializada o este acompañada por un modelo de datos acorde. Se debe evitar el acoplamiento a la aplicación a hora del diseño de la propia API como a las operaciones y esquemas contenidos en la especificación.

En cuanto a los modelos de datos contenidos en estas API, deberán de ser generados en base a los esquemas provistos por las API de sistema, de tal mandera que un esquema a nivel de API tenga los mismos o un menor número de elementos de datos respecto al esquema del API de sistema del que se obtiene la información.

En este nivel se fomenta la composición de modelos vinculados al dominio funcional de negocio, siempre respetando la jerarquía y organización natural de los elementos de dominio, así como sus reglas y validaciones por cada elemento.

> **Ejemplo**: En una entidad bancaría este tipo de API puede ser el de Pagos SEPA (Single Euro Payments Area o Zona Única de Pagos en Euros), donde vemos un enriquecimiento en las operaciones de Backend a través de servicios bancarios como puede ser el uso de pagos periódicos y la programación de pagos. De igual forma, los modelos de datos son enriquecidos con los modelos de otros dominios como lo son el de personas y el de cuentas.

### API de experiencia

En esta capa se agrupa, todas aquellas APIs que concentran un grupo de servicios expuestos a través de las API de recurso y las exponen a las aplicaciones para su consumo, estando limitadas a:

- _Operaciones de orquestación_: Casos en que una operación requerida en el producto requiera a varias invocacione de una operación de negocio, lo que supondrá realizar una orquestación invocando a las llamadas a las APIs de recurso correspondiente. Otro caso, dentro del ambito de la transformación en el tipo de contenidos de entrada/salida de los datos, ejemplo las llamadas que se envie un documento en formato XML y sea fundamental transformar a un documento JSON para llevar a cabo la invocación.

- _Composición de esquemas_: Como resultado de esta orquestación es probable que tengamos que componer y comprobar un modelo de datos que represente ambas operaciones.

- _Enriquecimiento de esquemas_:En el caso de monitorización cuando se requiere de un identificador que permita dar seguimiento del flujo íntegro de la transacción, operación o bien para notificar causas técnicas, tanto a los siguientes niveles inferiores de API como a los consumidores. Generalmente esta vinculado al enriquecimiento de información dentro de ciclo de ejecución del proceso de negocio. Otros casos serían aquellos que necesiten información adiccional propia de la aplicación a los esquemas de datos del negocio, sin que esto represente una lógica distinta al servicio funcional de negocio dado.

- _Resolución de los modelos de seguridad_: APIs expuestas para los consumidores aplicativos, punto en el que se deberá  tener consideración que los modelos de seguridad deberá deternminar. En este punto se debe resolver la propagación de los identificadores de seguridad (tokens) hacia los siguientes niveles de API.

- _Homologación de mensajes_: Las responsabilidad de asegurar un mensaje con un modelo común de datos al cliente final: errores, advertencias y/o información.

Como objetivo se parte del principio de diseño que este tipo de APIs esten desvinculadas a la aplicación o a un producto de Software en enconcreto o particular, teniendo en cuenta que de otra forma es sensible este tipo de API termine comportándose como un **patron "Backend for Frontend"**. Como consecuencia se limitara el uso unicamente para esta aplicación, donde cualquier cambio en la pantalla podría implicar un cambio en el API.

> Para evitar el uso de este patrón, se pretende fomentar en fases posteriores, de un API única expuesta a través de GraphQL para el consumo de los aplicativos frontales. Debido a la complejidad subyacente a la implementación de este modelo de exposición donde se pone sobre la balanza el consumo de APIs de sistema versus la capa de presentación, queda fuera de alcance en esta etapa.

## Invocación entre las API

El flujo de comunicación entre los diferentes niveles de API debe estar supeditado a su naturales de obtención y transmición de la información. Por tanto, si ubicamos los tipos de API en la plataforma en una vista horizontal, podemos ver su representación de la siguiente forma:

![invocación-apis](../_images/flujo-invocacion-apis.png)

De esta froma podemos resumir en la siguiente tabla los medios de invocación entre los diferentes niveles de API.

**APIs de experiencia**

- :negative_squared_cross_mark: Otra API de Experienca
- :white_check_mark: API de BaaS
- :negative_squared_cross_mark: API de Sistema

**APIs de BaaS**

- :negative_squared_cross_mark: Otra API de Experienca
- :negative_squared_cross_mark: API de BaaS
- :white_check_mark: API de Sistema

**APIs de sistema**

- :negative_squared_cross_mark: Otra API de Experienca
- :negative_squared_cross_mark: API de BaaS
- :white_check_mark: API de sistema, ya sea de soporte o bien, preferentemente del mismo dominio

Dentro de este principio de clasificación, ordenamientos y tipificación de API, es importante recalacar las condiciones y normas a la hora de definri la especificación indicada en las guías de diseño, pero sin perder la flexibilidad al diseñar un servicio o API de experiencia. En ocasiones, habrá que establecer patrones y mecanismos de recuperación de información a partir del como estarán implementadas las operaciones de negocio en el Backend, de tal forma que no se rompan las estructuras actuales que conlleven a la regeneración de los dominios de negocio.
