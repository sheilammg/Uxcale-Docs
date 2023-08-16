**Metodología y Responsabilidades de los Equipos y Roles** 

|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|23/02/2023|Axpe|Versión inicial.|
|**1.1**|23/05/2023|Axpe |Añadida Introducción, añadido el rol de AP Tester y API Designer a las tablas con las tareas. |
|**1.2**|28/07/2023|Axpe|Modificadas tareas de las tablas acorde al modelo de participación y añadidas las funciones del equipo de despliegue.|



## <a name="_toc127528008"></a><a name="_toc249631174"></a>Índice

[Índice	](#_toc249631174)

[1.	Introducción](#_toc1217459733)

[2. Fase de Diseño	](#_toc834266743)

[2.1. Planificación e Identificación	](#_toc73406775)

[2.2. Diseño y validación de la definición	](#_toc450866206)

[3. Fase de Desarrollo	](#_toc1885905864)

[3.1. Creación	](#_toc540526476)

[3.2. Implementación	](#_toc270687002)

[4. Fase de Gestión	](#_toc1688055636)

[4.1. Publicación	](#_toc1680791228)

[4.2. Monitorización y analíticas	](#_toc1741471437)

[4.3. Deprecación o retirada	](#_toc1163893268)




 # <a name="índice"></a><a name="_toc1217459733"></a>1. Introducción
En este documento se especifican las funciones, responsabilidades y roles de los equipos participantes en los procesos que se realizan en cada una de las fases del ciclo de vida API.

Es necesario aclarar que, aunque en este documento se insertan tablas detallando las funciones concretas de cada rol dentro de un equipo, dichas funciones y responsabilidades no siguen un esquema rígido. Es decir, **las responsabilidades y funciones que se asignan a cada rol pueden variar, dependiendo de las especificaciones y necesidades del equipo**. 

Por ejemplo, si un equipo de Oficina de Gobierno cuenta únicamente con una persona, por ejemplo, un API Architect, entonces dicho rol será el encargado de realizar todas las funciones correspondientes a la oficina. En cambio, si el equipo de Oficina de Gobierno cuenta con dos roles, un API Architect* y un API Designer, el API Architect podrá delegar tareas de validación y generación de plantillas en el API Designer. Las tareas asignadas al API Designer contarán con cierta flexibilidad y se ajustarán al criterio del equipo correspondiente. 

Sucederá lo mismo en el equipo API Owner o API Squad, en el que las tareas asignadas a los API Developer, API Designer y API Tester podrán variar según los requerimientos, y también dependerán de la coordinación con el equipo de Oficina de Gobierno. 

En el caso de que en una compañía no cuente con un equipo de Oficina de Gobierno, las tareas correspondientes se repartirán entre el resto de los equipos participantes. 

Por lo tanto, hay que tener en cuenta que las tablas de funciones en el presente documento se corresponden con un esquema orientativo y pueden adaptarse a las necesidades concretas de cada equipo, atendiendo a su dimensión, los roles presentes y el grado de experiencia de cada uno. 
# <a name="_toc834266743"></a>2. Fase de Diseño
Esta fase se compone de dos etapas: **Planificación e identificación** de la API, y **Diseño** y **validación** de la interfaz.
### <a name="_toc73406775"></a>2.1. Planificación e Identificación
El objetivo de esta fase es analizar las necesidades de negocio de uXcale para identificar un conjunto de APIs que aporten valor. Esto generará un listado de **APIs candidatas u objetivo** a definir, implementar, publicar, evolucionar y gestionar en el catálogo de servicios API del banco.

El primer paso es analizar las funcionalidades del proyecto, ver las necesidades y realizar una estimación a alto nivel. Para iniciar esta fase, el equipo de proyecto tendrá que realizar una **petición**. Para realizar y gestionar dicha petición, se utilizará la herramienta corporativa correspondiente, pudiendo ser el correo electrónico, Jira, etc. En la petición creada, el equipo de proyecto tendrá que indicar en un **listado las necesidades de negocio** y adjuntar la documentación necesaria asociada a los requerimientos. Como objetivo, el equipo de la Oficina de Gobierno ofrecerá una ***plantilla HLE*** en la que se definirán un listado de APIs a alto nivel que aporten valor. Además, durante esta fase se llevará a cabo la **catalogación funcional de las APIs**, con el apoyo del equipo de Negocio. 

**Recursos** 

- ***Herramienta de gestión corporativa***: Portal o herramienta correspondiente que utilice la compañía para la gestión de la API a lo largo de su ciclo de vida. Se utilizará la herramienta acordada para registrar y priorizar todas las APIs candidatas identificadas. 
- [***Plantilla HLE***:] Excel que se utiliza como plantilla para determinar una estimación de alto nivel.

**Participantes:**

<table><tr><th valign="top"><b>Equipo</b></th><th valign="top"><b>Rol</b></th><th valign="top"><b>Responsabilidad</b></th></tr>
<tr><td rowspan="2"><p></p><p>Oficina de Gobierno</p><p></p></td><td><p></p><p>API Architect </p><p></p></td><td>Garantizar soporte al equipo de desarrollo para analizar requisitos funcionales requeridos, intermediar entre las partes afectadas, y gestionar e identificar las nuevas APIs y su evolución. Encargado de aprobar la solicitud de participación de la OG y asegurar que se ha entregado toda la documentación necesaria y de manera correcta. </td></tr>
<tr>Oficina de Gobierno<td>API Govern Lead</td><td>Mediar entre negocio y desarrollo, y velar porque se cumplen los requerimientos de negocio. Encargado de aprobar la solicitud de participación de la OG y asegurar que se ha entregado toda la documentación. </td></tr>
<tr><td>API Squad</td><td>API Owner</td><td>Responsable de iniciar y gestionar los trámites necesarios para el identificación, análisis, creación o evolución de las APIs requeridas para la funcionalidad concreta. Es decir, será el responsable del roadmap de la API.</td></tr>
<tr><td rowspan="2">Equipo de Negocio </td><td>Experto de Negocio</td><td>Equipo responsable de analizar e identificar las nuevas funcionalidades del negocio. El objetivo es recopilar una lista de APIs que aporte valor a nuestra compañía. Son responsables de dar soporte y aportar el conocimiento funcional necesario para identificar y clasificar las APIs.</td></tr>
<tr><td>Analista funcional</td><td>Encargado de preparar la solicitud de participación de OG y aportar la documentación necesaria. </td></tr>
</table>
### <a name="_toc450866206"></a>2.2. Diseño y validación de la definición
El objetivo es definir y validar la especificación API identificadas: la interfaz de los recursos, identificando y definiendo el tipo operaciones, la estructura del cuerpo del mensaje de la solicitud y respuesta, formatos y códigos HTTP, etc., cubriendo toda la funcionalidad necesaria indicada por negocio.

El procedimiento consta de los siguientes pasos:

- Generar la definición API seguimiento el formato de las plantillas de Diseño.
- Revisión y validación de la definición de la API, a través de la plantilla excel de Diseño. 

**Participantes involucrados:**

<table><tr><th valign="bottom"><b>Equipo</b></th><th valign="bottom"><b>Rol</b></th><th valign="bottom"><b>Responsabilidad</b></th></tr>
<tr><td rowspan="2"><p>Oficina de Gobierno</p><p></p></td><td><p>API Architect</p><p></p></td><td>Indicar los repositorios donde se almacenarán las especificaciones API. Crear las nuevas entidades funcionales si se requieren. </td></tr>
<tr>Oficina de Gobierno<td><p>API Architect</p><p>API Designer</p></td><td>Revisar y validar las plantillas con la definición acordada y dar soporte al equipo de desarrollo.</td></tr>
<tr><td rowspan="2"><p>Equipo API Owner o API Squad</p><p></p></td><td>API Owner</td><td>Apoyo funcional a la hora de crear plantillas de diseño API. Apoyo funcional si se necesitan crear nuevas entidades funcionales.</td></tr>
<tr>Equipo API Owner<td>API Designer</td><td><p>Genera las plantillas con el apoyo del equipo Gobierno de API. Solicitud de revisión de la definición.</p><p></p></td></tr>
<tr><td>Equipo de Negocio</td><td>Experto de Negocio</td><td>Apoyo y aportar el detalle funcional.</td></tr>
</table>
## <a name="_toc1885905864"></a>3. Fase de Desarrollo 
### <a name="_toc540526476"></a>3.1. Creación
Validada la plantilla de diseño excel e identificadas las APIs que se van a necesitar, se inicia el proceso de escritura en un lenguaje de especificación de API ([OpenAPI 3).](https://spec.openapis.org/oas/v3.0.1.html) En esta especificación se deberán generar los métodos, parámetros y protocolos previamente identificados y validados en la fase de Diseño.

Dicho procedimiento consta de los siguientes pasos: 

- Generación de la especificación API en OpenAPI 3. Se recomienda el uso del IDE Stoplight Studio, siguiendo la guía de diseño de APIs definida por uXcale y revisando las validaciones del editor. En caso de no utilizar el Stoplight Studio, habrá que realizar un segundo paso y será pasar el conjunto de reglas de validación.
- Almacenamiento de la especificación de la API definida en el repositorio correspondiente, con un documento donde se reflejen los cambios y solicitud de revisión a la Oficina de Gobierno.
- Revisión y validación de la especificación de la API por parte de la OG.

**Participantes involucrados:**

|**Equipo**|**Rol**|**Responsabilidad**|
| :-: | :-: | :-: |
|Oficina de Gobierno|API Designer API Architect|Revisar y validar la especificación API, cumpliendo con la guía de diseño, estándares, buenas prácticas, etc. Encargado de aprobar la solicitud de publicación de la API en desarrollo, y podrá dar apoyo al proceso. |
|Equipo API Owner o API Squad|API Designer|Generación de la especificación API en lenguaje formal, almacenarlo en el repositorio indicado y generar una solicitud para su revisión. Solicitará la publicación de la API en desarrollo. |
||API Owner|Será informado del estado y evolución de la API.|
|Equipo de despliegue||Publicación de la especificación de la API en el entorno de desarrollo.|
### <a name="_toc270687002"></a>3.2. Implementación
En esta etapa se implementa la lógica de negocio que existe detrás de la API, partiendo de la especificación API generada previamente. También se promocionará entre los distintos entornos previos al productivo, generando las pruebas necesarias y mínimas para verificar su calidad. La fase de implementación cuenta con las siguientes partes:

- Desarrollo del microservicio asociado a la API y despliegue en el entorno de desarrollo para ensamblarlo con la API. 
- Desplegar la especificación en el API Manager, en el entorno de desarrollo, y establecer las configuraciones de los API Proxy y políticas.
- Realización de las pruebas técnicas y funcionales correspondientes.

**Participantes involucrados:**

<table><tr><th valign="bottom"><b>Equipo</b></th><th valign="bottom"><b>Rol</b></th><th valign="bottom"><b>Responsabilidad</b></th></tr>
<tr><td>Oficina de Gobierno</td><td>API Architect</td><td>Encargado de la generación de las SDK (a futuro automatizada) y facilitar su integración. Encargado de validar la implementación y las pruebas correspondientes.</td></tr>
<tr><td></td><td>API Developer</td><td>Encargado de validar la implementación de la API y las pruebas correspondientes.  </td></tr>
<tr><td rowspan="3"><p>Equipo API Owner o API Squad</p><p></p></td><td>API Developer</td><td>Desarrollar la API. Realizar pruebas mínimas que verifiquen el correcto funcionamiento de la implementación. Despliegue en el entorno de desarrollo. </td></tr>
<tr>Equipo API Owner<td>API Tester / QA</td><td>Realizar las pruebas técnicas y funcionales sobre la implementación de la API. </td></tr>
<tr><td>API Owner</td><td>Será informado del estado de la API. </td></tr>
</table>

**Nota:** En esta etapa se debe trabajar en paralelo, donde el equipo de QA podrá comenzar a realizar sus casos de pruebas y consumir la API pudiendo iniciar la verificación de los desarrollos.
## <a name="_toc1688055636"></a>4. Fase de Gestión
### <a name="_toc1680791228"></a>4.1. Publicación
Fase que se lleva a cargo la publicación de la API en el entorno productivo, poniéndose a disposición de los consumidores, para que empiecen a consumirla. Se utilizará el **API Manager** para la publicación y el **Portal de documentación para consumidores**, donde se recogerá toda la documentación útil de la API.

**Participantes involucrados:**

<table><tr><th valign="bottom"><b>Equipo</b></th><th valign="bottom"><b>Rol</b></th><th valign="bottom"><b>Responsabilidad</b></th></tr>
<tr><td rowspan="2">Oficina de Gobierno</td><td>API Architect</td><td>Aprueba la solicitud de publicación en cada entorno. Informador de la publicación y el encargado del mantenimiento del catálogo de APIs. Valida que la API se ha almacenado correctamente en el repositorio y que se ha añadido la documentación necesaria. </td></tr>
<tr>Oficina de Gobierno<td>API Designer</td><td>Apoyo a la publicación de la API en el entorno, en caso de que no haya equipo de despliegue. Valida que la API y su documentación se ha almacenado en el repositorio correspondiente.</td></tr>
<tr><td>Equipo API Owner o API Squad</td><td>API Owner</td><td>Es informado de la publicación de la API en cada entorno.</td></tr>
<tr><td></td><td>API Designer o API Developer</td><td>Solicita la publicación de la API en cada entorno. Ejecución de los pipelines para la gestión de la publicación o promoción del producto. Encargado de actualizar la documentación en el repositorio.</td></tr>
<tr><td>Equipo de despliegue</td><td></td><td>Encargado de publicar la API (especificación e implementación) en cada entorno una vez que la OG ha aprobado la solicitud de despliegue. </td></tr>
</table>

### <a name="_toc1741471437"></a>4.2. Monitorización y analíticas
En esta etapa se monitoriza y se analizan las estadísticas de la API en producción y definición de los puntos a medir. Se utilizará el **API Manager** para obtener las KPIs de las APIs.

**Participantes involucrados:**

|**Equipo**|**Rol**|**Responsabilidad**|
| :-: | :-: | :-: |
|Oficina de Gobierno|<p>API Architect</p><p>API Designer o API Developer</p>|Encargado de la plataforma y las APIs que están disponibles. Por otro lado, responsable de definir métricas técnicas, KPIs, avisos y alertas a nivel técnico.|
|Equipo API Owner|API Owner|Responsable de definir KPIs y métricas funcionales a nivel de negocio.|
### <a name="_toc1163893268"></a>4.3. Deprecación o retirada
En esta etapa se revisa el estado de la API y se decide deprecar o retirar la API.  Se utilizará el **API Manager** como herramienta para gestionar la deprecación o la retirada de la API.

El proceso detallado de deprecación de una API se detalla en el Procedimiento de participación de la Oficina de Gobierno.


**Participantes involucrados:**

|**Equipo**|**Rol**|**Responsabilidad**|
| :-: | :-: | :-: |
|Oficina de Gobierno|API Architect|<p>Verificar la revisión del impacto de la deprecación. Aprueba la solicitud de deprecación. Responsable de establecer los tiempos y los pasos a seguir, informar o alertar a los consumidores, monitorizar el consumo, autoriza y gestionar el ciclo completo de deprecación.</p><p></p>|
|Equipo API Owner|API Owner|Solicitar la retirada y definir junto con la Oficina de Gobierno los tiempos y los pasos a seguir. En período de producción, podrá alegar la detención del proceso con la justificación adecuada. |
|Equipo de despliegue||Añade la etiqueta de deprecación o retirada una vez que ha finalizado el tiempo de deprecación y la OG lo ha autorizado, o se ha confirmado que no existen consumidores.|
