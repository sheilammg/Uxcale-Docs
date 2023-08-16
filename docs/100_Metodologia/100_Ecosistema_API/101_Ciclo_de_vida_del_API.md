

# **Ciclo de vida del API**
|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|24/02/2023|Axpe|Versión inicial|
|**1.1**|15/03/2023|Axpe|<p>Se han puesto herramientas de ejemplo y se han especificado en mayor detalle las herramientas nombradas para poder comprender mejor su función.</p>|









# Índice
- [1. Fase de diseño](#Fase_diseño)

   - [1.1. Planificación e identificación	](#Planificacion_identificacion)

   - [1.2. Diseño de la definición	](#Diseño_definicion)

   - [1.3. Validación de la definición](#Validacion)

- [2. Fase de desarrollo	](#Fase_desarrollo)

   -  [2.1. Creación	](#Creacion)

      -  [2.1.1. Objetivos	](#Objetivos_creacion)

      -  [2.1.2. Productos de entrada](#Productos_entrada_cre)

      -  [2.1.3. Productos generados](#Productos_generados_cre)

      -  [2.1.4. Herramientas	](#Herramientas_cre)

      -  [2.1.5. Audiencia	](#Audiencia_cre)

      -  [2.1.6. Actores	](#Actores_cre)

   -  [2.2. Implementación	](#Implementacion)

      -  [2.2.1. Objetivos](#Objetivos_implementacion)

      -  [2.2.2. Productos de entrada](#Productos_entrada_imp)

      -  [2.2.3. Productos generados](#Productos_generados_imp)

      -  [2.2.4. Herramientas	](#Herramientas_imp)

      -  [2.2.5. Audiencia	](#Audiencia_imp)

      -  [2.2.6. Actores](#Audiencia_imp)

- [3. Fase de gestión](#Fase_gestion)

   -  [3.1. Publicación	](#Publicacion)

   -  [3.2. Monitorización y analíticas](#Monitorizacion)

   -  [3.3. Retirada](#Retirada)

   -  [3.4 Actores](#Actores)




# Ciclo de vida
La definición de un ciclo de vida para el API es un factor clave para la gestión de las mismas. A través de este, se pretenden determinar y gestionar los distintos estados en la vida de una API, desde su identificación hasta su de comisión.

![Ciclo de vida](images/Ciclo_de_vida.png)



# <a id="Fase_diseño"></a>1. Fase de diseño
Fase que está compuesta por las etapas de planificación de la API, y cuyo objetivo funcional es el diseño y validación de la interfaz.
## <a id="Planificacion_identificacion"></a> 1.1. Planificación e identificación
La fase de planificación se enfoca en las necesidades del negocio para obtener un conjunto de APIS que aporten valor. Para ello debemos hacernos la siguiente pregunta: ¿Realmente necesito un API? Es decir, lo que nos están pidiendo, ¿es realmente un API y no otro tipo de solución de software? Ya que, muchas veces, pensamos que todo se tiene que resolver creando un API. La idea de crear un API es la de exponer una funcionalidad clara de negocio, bien sea para ser consumida de forma interna por la organización, o bien consumida por una entidad externa y, en este caso, incluso monetizarla.

En definitiva, esta fase se encarga de analizar las necesidades del negocio para obtener un conjunto de APIs que aporten valor, dando como resultado un listado de APIs candidatas a ser construidas y publicadas en el catálogo de servicios de la organización.

El proceso de planificación se puede enfocar de las siguientes formas:

- **Top-down**: iniciado desde negocio como una planificación reactiva.
- **Bottom-up**: planificación proactiva desde tecnología.

Desde el equipo de gobierno tendrán los siguientes objetivos:

- Guiar a los responsables de negocio para definir APIs que aporten valor y aterrizar los requisitos funcionales.
- Dar soporte a los equipos en la estructuración y definición de las APIs objetivo.
- Mantener un catálogo de APIs, versionadas, que sirva de referencia.
- Fortalecer el modelo API First en la organización.
## <a id="Diseño_definicion"></a>1.2. Diseño de la definición
El objetivo es definir la interfaz de los recursos de las distintas APIs. También se identifican operaciones, la estructura de los cuerpos de entrada/salida, formatos de la respuesta y códigos HTTP implicados.  En esta fase se define la funcionalidad de negocio en la que se enfoca la API, a quién va dirigida y los objetivos, dando como resultado el diseño completo de la interfaz en un documento de análisis.

El equipo de API tiene el objetivo de crear y mantener una base de conocimiento, preparada por los expertos de negocio y los equipos de análisis en conjunto con el propio equipo, para su uso posterior en subsecuentes diseños.
## <a id="Validacion"></a>1.3. Validación de la definición
En esta fase, desde el equipo de gobierno se supervisará el diseño, verificando el cumplimiento de la nomenclatura establecida y asegurando que las APIs definidas aportarán valor al catálogo. Se hará una revisión global previa a la escritura de la API con el fin de asegurar el cumplimiento de las guías de diseño y normalizaciones por el tipo de API correspondiente.

Una parte fundamental, que comparten ambas fases (Diseño y Validación), es el punto del **versionado**, ya que normalmente la API irá evolucionando a medida que se agregan nuevas funcionalidades del negocio. Para el versionado de nuestras APIs seguiremos un estilo de [versionamiento semántico](https://semver.org/), donde:

1. El formato de la versión indicada en el documento de especificación de la API: [MAJOR].[MINOR].[PATCH]:
1. [MAJOR] Cambios que hacen a la API incompatible con los desarrollos anteriores.
1. [MINOR] Agregar nuevas funcionalidades, sin afectar a las anteriores.
1. [PATCH] Corrección de errores (bugs) sobre la versión.

   Ejemplo: versión 1.2.5
1. El versionado mayor irá indicado en la url del recurso, y solo se tienen en cuenta los cambios mayores, ya que estos son los que indican incompatibilidades entre las versiones, y por tanto los que afectan directamente a los consumidores (obligando a actualizar sus desarrollos para adaptarse a los nuevos requisitos de esta versión).

Ejemplo: https://www.axpe.com/contexto/v2/recurso
# <a id="Fase_desarrollo"></a>2. Fase de desarrollo
Una vez finalizado el diseño y validado el resultado por el equipo de Oficina de Gobierno, pasaremos a la construcción de la misma. En esta fase se escribe la especificación de la API usando como base la plantilla correspondiente y aplicando las guías de diseño, teniéndolas como referencia para la construcción con el análisis funcional. Una vez escrita la especificación, se procede a la publicación para los equipos de desarrollo, que llevarán a cabo las tareas de implementación; y para el grupo de consumidores, que integrarán en sus aplicaciones las llamadas al API correspondientes. En paralelo, el equipo de API se encargará de llevar a cabo la configuración de políticas de seguridad, cuota y consumo.
## <a id="Creacion"></a>2.1. Creación
Una vez analizada y documentada la interfaz de la API correctamente, se procede a escribirla en un lenguaje y generar la especificación API como por ejemplo pueden ser: Swagger, OpenApi, Raml  , etc; donde Swagger es un conjunto de herramientas de código abierto para poder diseñar, construir, documentar y utilizar servicios web RESTful, OpenApi es la evolución de Swagger y Raml es un lenguaje de modelado para definir APIs RESTful con una sintaxis sencilla y fácil de comprender.

En esta especificación se generan los métodos, parámetros y protocolos involucrados y previamente planificados y validados en la fase de diseño.

Se desarrollará la especificación API aplicando unas buenas prácticas y guiado por el documento de Diseño. Los métodos identificados deben tener sus respectivos parámetros de entrada aplicando buenas prácticas, es decir, orientando a que el nombre de la operación sea lo suficientemente legible, claro y conciso para que cualquier usuario pueda entender la funcionalidad de dicha operación.

La estructura de los esquemas de entrada y salida de los distintos métodos se crearán o se reutilizarán dependiendo de la necesidad. Se tendrá que revisar el repositorio de modelos, donde se encuentra un listado de esquemas (modelos) que podrán ser reutilizados en cualquier momento. También se deberán tener en cuenta los esquemas para los diferentes tipos de errores que retorne la API, ya sean errores funcionales o técnicos y, dependiendo de que nivel sea, la API se retornará mayor o menor información. Se tendrá un documento específico que detalle toda la información sobre la estructura de los esquemas de entrada y salida.

En cuanto a la seguridad definida en la API, se procederá según los estándares de autenticación y autorización predefinidos por la compañia. Estas acciones deberán ser supervisadas y validadas con las áreas correspondientes.

Finalizada la creación de la especificación API, se deberá validar con el equipo de gobierno la definición aportada y comprobar que cumple con lo definido en la fase de diseño. Se verificará que se han aplicado las reglas indicadas en la guía de diseño, estándares API, buenas prácticas, y que se esté aplicando las reglas base predefinidas con la herramienta Spectral y que está suficientemente documentada y con los ejemplos de al menos un caso de uso por operación.

En el caso que se generen esquemas de datos, se debe actualizar el listado de esquemas, ya sea modificando el existente o agregándolo.
### <a id="Objetivos_creacion"></a>2.1.1. Objetivos
Los objetivos principales a tener en cuenta son los siguientes:

- Creación de la especificación de la API en OpenAPI v3.
- Validación de la especificación de la API en OpenAPI v3.
- Creación y validación de los mecanismos de seguridad en los recursos expuestos.
### <a id="Productos_entrada_cre"></a>2.1.2. Productos de entrada
- Listado de modelos o esquemas de datos a utilizar.
- Documento para diseñar la API - Guía Diseño de APIs.
### <a id="`Productos_generados_cre"></a>2.1.3. Productos generados
- Especificación de la API en OpenAPI 3.
### <a id="Herramientas_cre"></a>2.1.4. Herramientas
- Stoplight Studio/ Visual Studio Code.
- Spectral.
- Guía de diseño.
- Repositorio único de esquemas de datos.
### <a id="Audiencia_cre"></a>2.1.5. Audiencia

|Audiencia|Responsabilidad|
| - | - |
|Diseñador API|Responsable de llevar a cabo la generación de la especificación API|
|Evangelista API|Validar que la especificación generada cumpla con la guía de diseño, estándares, buenas prácticas y reglas Spectral.|
|Equipo de gobierno|Validar que la especificación creada cumpla con lo definido en la fase de diseño y reglas Spectral.|
### <a id="Actores_cre"></a>2.1.6. Actores

|Actor|Afectación|
| - | - |
|Equipo funcional|Análisis de los requerimientos|
## <a id="Implementacion"></a>2.2. Implementación
En esta fase se implementa la lógica de negocio que existe por debajo de la API, partiendo siempre como base de la especificación API creada en el estado previo. Este desarrollo consiste tanto en los mapeos de los campos como en el proceso de ensamblado con el backend. El cómo se lleve a cabo la implementación tanto del cliente que consumirá la API como el backend de lógica de negocio, estará fuera del ámbito de esta fase.

El equipo encargado del desarrollo tendrá que notificar al equipo de gobierno cuando se tenga publicado el servicio que implementa la especificación, para que se haga la integración del servicio.

Por último, un paso importante tanto a la hora del desarrollo como al finalizar es que debemos de asegurarnos que la API pueda ser consumida en modo MOCK mediante alguna herramienta  de mocking en local como puede ser por ejemplo **PRISM**. Esta plataforma de Sandbox local deberá permitir al desarrollador realizar pruebas simples a la API sin necesidad de llevar a cabo integraciones complejas que dificulten su adopción.
### <a id="Objetivos_implementacion"></a>2.2.1. Objetivos
- Desarrollar la lógica de negocio.

### <a id="Productos_entrada_imp"></a>2.2.2. Productos de entrada
- Especificación de la API.

### <a id="Productos_generados_imp"></a>2.2.3. Productos generados
- SDK back/front.

### <a id="Herramientas_imp"></a>2.2.4. Herramientas
- Generadores de SDK.
- Stoplight con PRISM.

### <a id="Audiencia_imp"></a>2.2.5. Audiencia

|Audiencia|Responsabilidad|
| - | - |
|Equipo de Gobierno|Encargado de facilitar su integración y la generación de la documentación adecuada.|
|Equipo de Desarrollo|Equipo encargado de desarrollar los microservicios de la API.|
|<p></p><p></p><p></p><p></p>||
### <a id="Actores_imp"></a>2.2.6. Actores

|<a name="fase-de-gestión"></a><a name="_toc127433550"></a><a name="_toc127531403"></a>Actor|Afectación|
| - | - |
|Equipo de Gobierno|Encargado de facilitar su integración y la generación de la documentación adecuada.|
|Equipo de Desarrollo|Equipo encargado de desarrollar los microservicios de la API.|
# <a id="Fase_gestion"></a>3. Fase de gestión
Se incluyen todas las tareas requeridas para la monitorización, analítica, evolución y mantenimiento de la APIs.
## <a id="Publicacion"></a>3.1. Publicación
En esta se lleva a cabo la publicación en el catálogo de APIs. Se podrán a disposición de la comunidad de desarrolladores, para que así comience a utilizarla. Es recomendable y necesario que la API esté bien documentada para favorecer su utilización y la libertad de uso entre los desarrolladores. Para ello, deberá estar correctamente catalogada a través de etiquetas que faciliten su búsqueda e identificación dentro del grupo de APIs.

El equipo de gobierno se encargará de revisar las siguientes tareas:

- Publicación de las API.
- Definir los canales de comunicación entre los distintos participantes (gobierno, negocio y tecnología).
- Apoyar a la comunidad de desarrolladores, obteniendo y valorando el comentario de su uso y funcionalidad.
- Fomentar la reutilización de las APIs previamente publicadas.
## <a id="Monitorizacion"></a>3.2. Monitorización y analíticas
En esta etapa se buscar definir e identificar los indicadores que ofrezcan más información a la hora de monitorización y analíticas de las APIs observadas. Para ello se tendrán los siguientes criterios:

- Buscar y crear la confianza en un modelo de API.
- Entender los beneficios y las necesidades de los usuarios asociados ecosistema.
- Gestionar los servicios y las versiones de las APIs.
- Entender cuándo se pueden retirar los servicios.
- Prever y adelantarse al crecimiento del tráfico producido.

Se incluirán los KPIs necesarios que permitan identificar y analizar oportunidades de negocio, dotando de información en tiempo real a los equipos de Marketing y Operaciones.

En el aspecto técnico, se tendrán y proveerán elementos de medición del rendimiento de la API, tiempos de ejecución, retrasos o latencia en las comunicaciones y demás elementos técnicos que doten de información para mejorar la infraestructura en la que transitan las API.
## <a id="Retirada"></a>3.3. Retirada
Esta fase se basa en definir los medios y herramientas encargados de identificar cuando un API llega al período de comisión. El principal objetivo y más común, es que salgan nuevas versiones de este API o nuevos API que ofrecen una funcionalidad extendida y no sea retro compatible.

Se establecerán los instrumentos de notificación apropiados a los consumidores suscritos a este API,y  dando un tiempo considerable de adaptación, además es un proceso que debe ejecutarse de manera eficiente para generar el mennor impacto posible y para evitar afectar de forma drástica a los consumidores.

## <a id="A"></a>3.4 Actores


|Actor|Afectación|
| - | - |
|Equipo de Gobierno|Encargado de la gestión de las APIs, además de verificar el control|
|Equipo de Técnico|Encargado de verificar el mantenimiento, publicación, etc.|






