**Equipos y roles en el ciclo de vida API**


|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|22/02/2023|Axpe|Versión inicial.|
|**1.1**|07/03/2023|Axpe|<p>Se añaden las funciones de Service Management al rol de Arquitecto. </p><p>Ampliada la descripción de API Designer del Equipo de API Owner. </p>|
|**1.2.**|23/05/2023|Axpe|Actualizados los anexos I y II y revisión del documento. |



# <a name="_toc1935921834"></a>**Índice**

[Índice	](#_toc1935921834)

[1. Oficina de Gobierno de Arquitectura	](#_toc315664423)

[1.1. Diseñador API / API Designer	](#_toc1303564591)

[1.2. Arquitecto API / API Architect	](#_toc1306176856)

[1.3. API Evangelista / API Evangelist	](#_toc1986843455)

[2. Equipo API Owner / Equipo de Proyecto	](#_toc1055109104)

[2.1. API Owner	](#_toc351857355)

[2.2. API Designer	](#_toc1722622588)

[2.3. API Developer	](#_toc511671067)

[2.4. Tester / QA	](#_toc1869134427)

[3. Equipo de negocio	](#_toc18142774)

[3.1. Experto de negocio	](#_toc1319406065)

[Anexo I. Ejemplo de situación actual](#_toc947066225)

[Anexo II. Ejemplo de dimensión del equipo 	](#_toc188647213)




En este documento se detallan todos los equipos presentes en el ciclo de vida de las APIs y los roles que desempeñarán durante el mismo.

Todos aquellos involucrados durante el ciclo de vida API se denominan **actores** o **contributors**. Este término engloba a todos aquellos que interactúan durante el ciclo de vida API, pudiendo pertenecer a cualquiera de los tres equipos que se definen a continuación:
# <a name="_toc315664423"></a>1. Oficina de Gobierno
El equipo que forma la Oficina de Gobierno se encuentra presente en todas las fases del ciclo de vida del API, y está compuesto por las personas que tienen un cierto grado de "expertis" en el área de Apificación, y que se encargan de validar la definición y la implementación de las APIs, su mantenimiento y su correcta gestión y ejecución.

Sus funciones principales serán:

- Fomentar y consolidar el modelo API First en la organización.
- Mediar entre los equipos de Negocio y API Owner para asegurar un catálogo de APIs que aporten valor. Dar apoyo cuando sea necesario a ambos equipos, tanto en la parte funcional como en la parte de desarrollo. 
- Establecer los estándares, las buenas prácticas, la metodología y el marco de actuación a seguir a la hora del diseño de APIs. 
- Validar el diseño y la implementación de las APIs, asegurando que siguen los estándares de calidad, las buenas prácticas de diseño y la metodología definida. 
- Definir y gestionar adecuadamente las políticas necesarias para el correcto funcionamiento de cada API.
- Monitorización y análisis de las APIs.
- Encargados de la publicación en el catálogo y despliegue en gateway, en el caso de que no exista un equipo de despliegue. 
- Mantener y administrar un catálogo de APIs versionadas que sirva de referencia para la creación y decomisión de operaciones de negocio.

Este equipo está compuesto por los siguientes roles:
## <a name="diseñador-de-api-api-designer"></a><a name="_toc127359185"></a><a name="_toc1303564591"></a>1.1. Diseñador API / API Designer
Los diseñadores de APIs trabajaban juntamente con el equipo de proyecto en todo el ciclo de vida API. Son los encargados de ayudar a definir y de validar las interfaces y verificar que la definición cumple con el documento de diseño definido por el banco. Por otro lado, revisarán y garantizarán que la documentación aportada a la hora de definir APIs sigue los estándares de calidad y nomenclatura establecidos. También podrá apoyar al API Architect en sus funciones. 
## <a name="arquitecto-api-api-architect"></a><a name="_toc127359186"></a><a name="_toc1306176856"></a>1.2. Arquitecto API / API Architect
Es la persona que se ocupa de gestionar y liderar la estrategia de "Apificación" implantada, y es responsable de su cumplimiento. Por otro lado, será el encargado de validar los diseños de definiciones antes de que comience su desarrollo y también una vez que estén implementados. 

Además, el arquitecto también realizará las funciones de Service Management cuando no haya un equipo de despliegue. Es decir, todas las funciones relacionadas con la gestión y administración de las APIs y su ciclo de vida (exposición, consumo, políticas, estadísticas, etc.) utilizando el API Manager que considere el banco. Por lo tanto, será el encargado de gestionar correctamente el ciclo de vida de las credenciales OAuth para los consumidores de APIs de la compañía. Se encargará de realizar el alta y la baja de las credenciales OAuth cuando un consumidor desee acceder a recursos propios, o finalizar su relación con el banco. En el caso de que exista un equipo de despliegue en la organización, el API Architect se encargará de dar apoyo y ayudar en sus funciones. 

También será el encargado del mantenimiento del catálogo de APIs, publicándolas, desplegándolas en el gateway y retirándolas del catálogo cuando dejen de aportar valor al negocio.
## <a name="api-evangelista-api-evangelist"></a><a name="_toc127359187"></a><a name="_toc1986843455"></a>1.3. API Evangelista / API Evangelist
Experto que ha definido la metodología de gobierno, las buenas prácticas, normativa de diseño y las guías de diseño API, siguiendo los estándares y gobiernos de las APIs. Ayuda al API designer en la toma de decisiones y valida el diseño de las APIs, garantizando la vitalidad y viabilidad de las soluciones en el tiempo y asegurando que las APIs aporten valor. El API Evangelist puede ejercer el rol de Responsable de Oficina de Gobierno, coordinando al equipo y llevando las tareas de gestión. 
## 1\.4. Responsable de Oficina de Gobierno / API Govern Lead
Este rol puede ser asumido por el API Architect. El API Govern Lead suele ser un perfil más funcional, centrado en la gestión de equipos y organización de tareas. Además, este rol normalmente tiene conocimiento de negocio y cumple el papel de mediador entre negocio y desarrollo.  Al final, es un responsable de equipo, un líder que asegura la buena organización y coordinación entre los diferentes miembros, así como el cumplimiento de los objetivos de la OG.
# <a name="equipo-api-owner-equipo-de-proyecto"></a><a name="_toc127359188"></a><a name="_toc1055109104"></a>2. Equipo API Owner / API Squad
El equipo del API Owner, también llamado API Squad, se encuentra presente en todas las fases del ciclo de vida de la API, y está compuesto por el responsable de la API y las personas que se encargan de su definición, su mantenimiento y su correcta ejecución.

Este equipo está compuesto por los siguientes roles:
## <a name="api-owner"></a><a name="_toc127359189"></a><a name="_toc351857355"></a>2.1. API Owner
Es la persona que asume la propiedad de la API, gestionando su plan de producto y estableciendo los objetivos que se persiguen con su implementación. Es decir, define la API en cuanto a prestaciones, segmento de negocio y funcionalidad. Actúa de enlace entre tecnología y negocio. Hace de enlace entre el equipo tecnológico/técnico y las áreas de negocio y podrá ayudar a identificar las APIs candidatas en los proyectos en los que esté participando.
## <a name="api-designer"></a><a name="_toc127359190"></a><a name="_toc1722622588"></a>2.2. API Designer
El equipo API Owner también puede tener uno o varios API Designers, que tienen la misma función que los que pertenecen a la Oficina de Gobierno en cuanto al diseño de las interfaces, aunque más enfocados a las necesidades de negocio, en este caso. La diferencia entre ambos es que el API Designer del equipo API Owner diseñará las interfaces siguiendo la metodología aportada por la Oficina de Gobierno, y siguiendo los estándares y nomenclatura definidos, mientras que no ayudará a definir ni validar, ni tampoco revisarán la documentación, ya que de eso se encarga la Oficina de Gobierno. 
## <a name="api-developer"></a><a name="_toc127359191"></a><a name="_toc511671067"></a>2.3. API Developer
Desarrollador de software que se encargará de implementar el backend que tiene la lógica de negocio que se expone en la API, y principalmente estará presente en la fase de desarrollo en el ciclo de vida de la API. Este rol, dependiendo de la complejidad del servicio a "*Apificar*", podrá tener una estructura simple o compleja y se podrán encontrar otros más específicos como Technical Lead o Arquitecto.
## <a name="_toc127359192"></a><a name="_toc1869134427"></a>2.4. Tester / QA
Encargado de controlar y administrar la calidad del software entregado por el equipo, a nivel funcional. Como en el caso anterior, se pueden encontrar roles más específicos dentro de este grupo, como Technical lead o Analista.

# <a name="equipo-de-negocio"></a><a name="_toc127359193"></a><a name="_toc18142774"></a>3. Equipo de negocio
Compuesto por aquellas personas que tienen un conocimiento profundo y detallado del área de negocio y de la funcionalidad que quieren exponer vía API. Principalmente, estos actores estarán involucrados en la fase de planificación y de diseño, donde identificarán las necesidades del negocio con el objetivo de obtener un conjunto de APIs candidatas que aporten valor al negocio. Son fundamentales para dar soporte y aportar todo el conocimiento funcional necesario.
## <a name="experto-de-negocio"></a><a name="_toc127359194"></a><a name="_toc1319406065"></a>3.1. Experto de negocio
Persona con conocimiento de negocio que ayuda a la comunidad (Oficina de Gobierno y Equipo API Owner) a entender la funcionalidad que se persigue con la API. Trabaja codo con codo con el API Owner para definir los requisitos de la API.
# 3\. Equipo de despliegue o equipo API Platform
Este equipo no siempre constituye una unidad separada, sino que a menudo sus tareas son asumidas por la Oficina de Gobierno o el equipo API. Sin embargo, sí que se recomienda cuando el equipo crece en tamaño. 

El equipo de despliegue se encarga de subir las APIs a la plataforma de API correspondiente. Se encarga de la gestión de las APIs, de su publicación en el API Portal, su mantenimiento y monitorización. 
# <a name="_toc947066225"></a>Anexo I. Ejemplo de situación actual
En este anexo se describirá la situación actual de los equipos en un banco y los roles con los que cuentan: 

- **Equipo de Oficina de Gobierno** –** No existe actualmente
- **API Squad**
  - API Owner
  - API Designer
  - API Developer
- **Equipo de Negocio** – No cuentan con un equipo de negocio diferenciado, sino que se encuentra integrado con el equipo API Owner. 
- **Equipo de Despliegue -** No cuentan con un equipo de despliegue diferenciado, sino que se encuentra integrado con el equipo API Owner.
# <a name="_toc188647213"></a>Anexo II. Ejemplo de dimensión del equipo

En este anexo se adaptarán los equipos y roles que intervienen en el ciclo de vida API a la situación actual de la compañía.

Se propone establecer un equipo de Oficina de Gobierno, siguiendo inicialmente un **modelo centralizado** en la compañía, formado por: 

- **Equipo de Oficina de Gobierno** 
  - API Evangelist o Responsable de OG (perfiles internos del cliente)
  - API Govern Lead (perfiles internos del cliente)
  - API Designers/Governors (perfiles externos – uXcale)

Se propone un equipo de Oficina de Gobierno al menos formado por 5 perfiles. Estos roles podrán variar, pero para la Oficina de Gobierno, se proponen los siguientes roles:

- 1 API Govern Lead 
- 1 Responsable de OG con funciones de API Evangelist
- 2 o 3 API Designers/Governors

Si la carga de trabajo es elevada, entonces se podrá aumentar el número de API Desginers/Developers pertenecientes a la Oficina de Gobierno para cumplir las necesidades.  

- **Equipo API Squad (Owner) y Equipo de Negocio**
  - API Owner
  - API Designer 
  - API Developer 

En cuanto al API Squad o equipo API Owner, seguirá contando con el rol de API Owner, y también con los roles de API Designer y API Developer. Hay que tener en cuenta que el equipo API Owner no siempre es el mismo, por lo tanto, estos roles pueden variar dependiendo de si el equipo es más o menos amplio. 

El Equipo de Negocio en el caso del banco no constituye una unidad separada, sino que las funciones de asesoramiento y soporte que corresponden a este equipo son asumidas por el API Squad, que son también los que conocen a fondo todo el área de negocio y las funcionalidades de la API. 

Si la compañía tampoco contiene un equipo de despliegue independiente, que se encargue de todas las tareas relacionadas con el API Platform, estas tareas serán asumidas por el equipo de Oficina de Gobierno. 

