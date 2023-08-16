
# PROCESO DE PARTICIPACIÓN DE LA OFICINA DE GOBIERNO


|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|08/06/2023|Axpe|Versión inicial.|
|**1.1**|09/06/2023|Axpe|Modificación de algunos puntos en el flujo de participación y modificación del diagrama.|
|**2.0**|10/07/2023|Axpe|Actualización del flujo y del diagrama de participación. Se añade el punto de deprecación.  |
# **Contenido**
[Introducción](#_toc139961711)

[Proceso de participación de la OG](#_toc139961712)

[Creación de una API nueva](#_toc139961713)

[Modificación de una API existente](#_toc139961714)

[Monitorización](#_toc139961715)

[Deprecación de una API	](#_toc139961716)

[Flujo de deprecación de una API	](#_toc139961717)

[Deprecación en entornos pre-productivos	](#_toc139961718)

[Deprecación en entorno de producción	](#_toc139961719)






# <a name="_toc139884169"></a><a name="_toc139961711"></a>Introducción
Cuando surge una nueva iniciativa o proyecto en el que se requiera el uso de APIs, la Oficina de Gobierno participará en el área de dicho proyecto donde intervengan las APIs, para ejercer las tareas de gobernanza y de gestión, y acompañando durante todo el ciclo de vida de dichas APIs.

El ámbito de responsabilidad de la Oficina de Gobierno se limita a las áreas del proyecto en las que se requiere el uso de las APIs. Con el fin de llevar a cabo estas acciones, es necesario recibir una solicitud de trabajo por parte de los **responsables del proyecto** o el **analista funcional**, en la cual se especifique la necesidad de realizar cualquier acción relacionada con una API.

Como hemos enfatizado anteriormente, la responsabilidad de la Oficina de Gobierno se limita a programar reuniones, revisar documentación funcional y llevar a cabo los trabajos exclusivamente relacionados con las APIs requeridas. El resto de las tareas de gestión serán responsabilidad de los encargados de los proyectos o de la estructura establecida por la compañía, y no serán competencia de la Oficina de Gobierno.

A continuación, se detalla paso a paso el proceso de participación de la OG en un nuevo proyecto en el que se requieran sus competencias. 


# Proceso de participación de la OG

<div align="center">  <img src="images/002.png" alt="Diagrama del proceso de participacion de la OG"  width="100%"/></div>

## Solicitud de participación de la OG

El primer paso consiste en la **solicitud de la participación de la Oficina de Gobierno** en un nuevo proyecto o iniciativa. La solicitud la recibirán el **API Govern Lead** y/o el **Responsable de la Oficina de Gobierno.** Las tareas del ciclo se ejecutarán por parte de los **API Designers/Governors**, según se decida en la organización interna del equipo de Oficina de Gobierno. 

Para crear la solicitud (Analista funcional o responsable de proyecto) se utiliza la herramienta **Jira,** debido a que permite crear multitud de tareas para cada proyecto y además permite interactuar con las mismas, asignando la tarea correspondiente a un equipo u otro. Este método ofrece más flexibilidad y dinamismo que otras herramientas.  No se aceptarán solicitudes a través del correo electrónico u otras herramientas corporativas. 

Las peticiones de la participación de la Oficina de Gobierno pueden venir de 3 tipos de solicitantes: 

- **API Owner:** el responsable o dueño del servicio que expone la API. 
- **Consumidor:** el responsable del sistema que requiera consumir el API.
- **Analista funcional y/o Responsable de proyecto**: dentro de un proyecto concreto, es aquel que se responsabiliza de dicho proyecto.  

A continuación, se muestra la plantilla de la tarea en Jira con toda la documentación necesaria que debe adjuntarse:

<div align="center">  <img src="images/004.png" alt="Plantilla - Solicitud intervención OG"  width="70%"/></div>

- <a name="_toc139884133"></a><a name="_toc139884171"></a>[Plantilla – Solicitud de intervención OG]

## Aprobación / Rechazo de la solicitud de participación por parte de la OG

Una vez que se asigna la tarea con la solicitud a la Oficina de Gobierno, esta revisará la documentación aportada, y podrá emitir:

- **Aprobación de la solicitud**
  - La OG verificará que se ha aportado toda la documentación necesaria: funcional, planificación de proyecto, [plantilla HLE](https://github.com/axpecloud/modernapps-api-methodology/blob/feature/dise%C3%B1orRest/300_Documentacion_Tecnica/200_Artefactos/Plantilla_HLE.xlsx) (presupuesto), solución propuesta y la catalogación funcional. 
- **Rechazo de la solicitud**
  - La OG podrá rechazar la solicitud de participación en caso de que el área del proyecto no se corresponda con la responsabilidad de la OG o la solicitud no proceda por alguna otra razón justificada, como que la documentación no esté completa. En este caso, la OG emitirá un informe con las razones del rechazo de la solicitud y los puntos a incluir, y notificará dicho rechazo. De esta manera, con el informe emitido, el solicitante puede volver a preparar la solicitud. 

## Análisis de APIs solicitadas

Aceptada la solicitud de participación, La OG convocará una reunión inicial para analizar las necesidades y las APIs solicitadas, con los siguientes roles:

- API Govern Lead 
- API Designer/Developer
- Backend Designer/Developer
- Frontend Designer/Developer 
- Analista funcional (de manera opcional)

El objetivo de esta reunión es obtener de forma definitiva los requisitos de negocio. Tras la reunión inicial, la OG terminará de analizar las necesidades exhaustivamente. En el supuesto de que persistan incertidumbres relativas a las APIs solicitadas o a las necesidades de negocio, la OG procederá a convocar una nueva reunión con el propósito de realizar un análisis adicional de los requisitos, a fin de asegurar su comprensión precisa y definitiva. 

Una vez que se han analizado con éxito las necesidades y se han obtenido los requisitos, se revisarán las APIs existentes para confirmar si ya existe una API en la organización que cubra las funciones que se necesitan. Esto puede dar lugar a dos escenarios:

- **No existe una API** que cubra las necesidades de negocio: en ese caso, se trata de un nuevo desarrollo y se creará una API nueva. Los pasos a seguir para la creación de una nueva API se detallan en el Procedimiento de creación y diseño de APIs.
- **Ya existe una API** que cubre las necesidades de negocio.
  - **La API necesita modificaciones o cambios**, se requiere hacer una evolución de una API existente. El proceso de modificación se detalla en el flujo de Creación y modificación de APIs. 
  - ` `**La API** cubre por completo las necesidades de negocio y **se puede reutilizar de forma directa**. En este caso, habrá que comprobar si el consumidor/cliente tiene acceso a dicha API. En el caso de que no lo tenga, la OG gestionará la suscripción para que se pueda consumir la API. 

## Creación de la nueva API o Modificación de la API existente

El siguiente paso consistirá en crear una o varias APIs desde cero que cubran las necesidades de negocio, o bien modificar/actualizar alguna de las APIs existentes que ya cubre parte de las necesidades. En caso de que se cuente con una API actualizada con la funcionalidad que se está buscando, no serán necesarios ninguno de estos pasos. 
### <a name="_toc139884172"></a><a name="_toc139961713"></a>Creación de una API nueva
El responsable de Proyecto dará de alta **una épica en el Jira por cada API** que se vaya a realizar, a través de la solicitud que se muestra en la imagen. Dentro de la épica de la API, se crean todas las historias de usuario asociadas a su proceso de diseño y validación. Estas tareas se asignarán a cada equipo o rol que correspondiente. Por ejemplo, la tarea de Validación de la especificación API se asignará a la Oficina de Gobierno, y la tarea de Creación de la especificación se asignará al API Designer.

<div align="center">  <img src="images/008.png" alt="Solicitud validación API"  width="70%"/></div>

- Plantilla – Solicitud API
- Esta plantilla será la misma tanto en el caso de creación de una nueva API como en el caso de modificación de una existente. 

Dentro de las historias de usuario de Validación de la especificación API y Validación de la implementación se crearán subtareas que reflejen cada paso: 

<div align="center">  <img src="images/009.png" alt="Validación de la especificación API"  width="70%"/></div>

**Nota**: La oficina de Gobierno hace un trabajo de validación, no dice, por ejemplo, qué seguridad hay que aplicar en el API.

La creación de una API desde cero, así como su implementación, se detalla paso a paso en el Proceso de creación y modificación de APIs, y esto no es competencia de la Oficina de Gobierno.
## <a name="_toc139884173"></a><a name="_toc139961714"></a>Modificación de una API existente
En el caso de tener que modificar una o varias APIs, de nuevo el responsable de Proyecto dará de alta **una épica en el Jira por cada API** que se vaya a realizar, a través de la tarea [Plantilla – Solicitud validación API] que es la misma que en el caso de creación de una API nueva. 

A la hora de modificar una API existente, es importante identificar si:

- **Se trata de un cambio *minor* en la versión.** En este caso, no impactaría al funcionamiento de la API. De todas maneras, se debe informar de los cambios introducidos, y se debe comprobar que el software sigue funcionando correctamente y que efectivamente, no se genera ningún impacto. 
- **Se trata de un cambio *major* en la versión*.*** En este caso, es necesario publicar una versión nueva y deprecar la anterior, por lo tanto, hay que avisar al resto del equipo y a los consumidores del impacto en la consumición de la API. 

El proceso de modificación de la API se detalla en el Proceso de creación y modificación de las APIs. 

## Publicación de la API

Cuando la API ha pasado todas las validaciones, se procede a su publicación. Es el diseñador/desarrollador API quien realizará la solicitud de publicación en cada entorno, siendo la OG quien apruebe dicha solicitud. Es el equipo de despliegue quien procede a la publicación:

- **Entorno de desarrollo**
  - Especificación API: después de haber pasado la validación de la OG y haber obtenido un Scoring de 100% en las reglas de Spectral, se publica la especificación API en el entorno de desarrollo.
  - Implementación API: se publica en desarrollo después de la especificación, ya que el desarrollo de la implementación empieza una vez que la especificación está publicada en desarrollo. Cuando la implementación ha pasado la validación de la OG y las pruebas correspondientes, se publica en el entorno de desarrollo.
- **Entorno de preproducción**

La especificación y la implementación van a la par. Se realizan las pruebas correspondientes que se especifican en el Procedimiento de Creación de una API. Estas pruebas engloban todas las pruebas de la fase anterior y a mayores las pruebas UAT, de carga o de regresión. La OG valida que se han pasado las pruebas. 

- **Entorno de producción**

La especificación y la implementación van a la par. Se realizan las pruebas correspondientes que se especifican en el Procedimiento de creación y modificación de las APIs. Estas pruebas engloban todas las pruebas de la fase anterior y a mayores las pruebas UAT, de carga o de regresión.

Una vez publicada en el entorno de producción, la OG validará que se ha almacenado en el repositorio correspondiente, junto con toda la documentación necesaria. 

El flujo de despliegue en desarrollo y en entornos superiores se describe con detalle en el documento de Proceso de creación y modificación de las APIs.

# <a name="_toc139961715"></a>Monitorización 
La Oficina de Gobierno llevará a cabo la monitorización de las APIs que se han publicado, debido a que es un proceso importante para garantizar su correcto funcionamiento y disponibilidad.

La monitorización se lleva a cabo definiendo sondas, endpoints de health, observando si el Gateway está disponible, además de ver si la API está funcionando correctamente y levantada.

Se realiza una sonda para cada API, y para cada uno de los consumidores, de forma que se tiene como objetivo tener todo el flujo completo monitorizado, desde la suscripción de los consumidores, hasta la implementación API.

Se desarrollarán una serie de dashboard donde se monitorizará el consumo de APIs para poder observar su comportamiento, es decir, quien consume la API, el número de solicitudes que se   realizan, si el consumo es excesivo o no, y se generarán una serie de gráficas que reflejen toda esta información.

Todo este proceso de monitorización lo realizará el rol de la OG que se encuentre más ligado a monitorización y testing, es decir, el API Govern/Designer que esté más especializado en esta tarea. 




# <a name="_toc139961716"></a>Deprecación de una API 

<div align="center">  <img src="images/011.png" alt="Deprecación de una API"  width="70%"/></div>

¿Qué es el deprecado de una API? 

El deprecado de una API consiste en **deshabilitarla o descatalogarla**, de manera que ya no se recomienda su uso a los consumidores.  

Cuando una API se depreca, deja de tener soporte activo (mantenimiento). Normalmente, una API pasa a estado deprecado principalmente debido a que se publica una nueva versión. En este caso, se recomienda a los consumidores que migren a la nueva versión, o que utilicen otra alternativa de consumo.  

¿Qué es la retirada de una API? 

Consiste en eliminar o dar de baja la API de forma definitiva, y se corresponde con la última etapa dentro del proceso global de deprecación. Una API se puede retirar completamente cuando: 

- No existen consumidores.  
- Cuando la versión de la API todavía no se ha desplegado, o se ha desplegado parcialmente, y ya existe publicada una nueva versión. En este caso la versión antigua queda obsoleta y se podrá eliminar definitivamente.    

## <a name="_toc139884174"></a><a name="_toc139961717"></a>Flujo de deprecación de una API
<div align="center">  <img src="images/012.png" alt="Flujo de deprecación de una API"  width="70%"/></div>
El proceso de deprecación debe ejecutarse de manera eficiente para generar el menor impacto posible y para evitar afectar de forma drástica a los consumidores. Resulta de vital importancia establecer un período de deprecación que permita la adaptación de los consumidores a la nueva versión API o a otra alternativa. 

El proceso de deprecación de una API se puede iniciar de dos maneras:

- **En forma de solicitud manual**: la solicitud la inicia el API Owner, a través de una tarea en Jira. Normalmente es debido a una nueva versión *major,* pero puede ser debido a otras razones. En esta solicitud deberá indicarse el motivo de la deprecación. 


<div align="center">  <img src="images/013.png" alt="Validación de la especificación API"  width="70%"/></div>      
  
- Plantilla de Solicitud deprecación de API

- **De forma automática por parte de la OG**: debido a que, en el proceso de monitorización de la API, la OG observa que ya no hay consumidores de dicha API. En este caso, podrá iniciar la deprecación de la API, aunque no exista una solicitud manual. 

A continuación, se seguirán los siguientes pasos:

- La OG **aprueba de la solicitud** (en caso de que haya) e informa al API Owner de que se va a iniciar el proceso de deprecación. 
- La OG establecerá un **rango de** **tiempo de deprecación de la API y los pasos a seguir**. De manera estándar, este tiempo será de 3 meses, aunque dependerá del caso concreto. También se determinará (en conjunto con el API Owner, si es necesario) **si el paso final del proceso será la deprecación o la retirada** total de la API. 
- La OG informará al API Owner del rango de tiempo de deprecación, el estado final de la API y los detalles que se consideren necesarios.
## <a name="_toc139884175"></a><a name="_toc139961718"></a>Deprecación en entornos pre-productivos

1. La OG **avisa a todos los consumidores** de la API de su deprecación, para que comiencen a migrar a la nueva versión o se adapten a una alternativa de consumo y dejen de utilizar la versión antigua. 
1. La OG **bloquea las nuevas suscripciones** a la API. 
1. La OG realiza el **seguimiento o monitorización (trazas)** de la API, para mantener un seguimiento tanto de los consumidores y del tráfico, como de su funcionamiento interno.** Los datos resultantes de la monitorización se almacenarán en la tarea de Jira, en un informe. Dependiendo de la volumetría, se darán dos casuísticas:   
   1. **Si la volumetría es alta**: el seguimiento deberá ser constante y el tiempo de monitorización se dividirá rangos más cortos. Por ejemplo, los 60 días estándares se pueden dividir en 8 semanas. Cada semana se hará un seguimiento de las peticiones y las llamadas a la API para confirmar el descenso del tráfico.  
   1. **Si la volumetría es baja**, a los 40 días de monitorización se recogerán los datos y se analizarán. 

En esta fase se tendrá en cuenta aquellos procesos que verifican el funcionamiento de las APIs, como el uso de sondas (o healthcheck), ya que darían lugar a falsos positivos. El tiempo de monitorización se establecerá un periodo estándar de 60 días.

1. Si a los 40 días sigue habiendo consumidores, la OG mandará un segundo aviso de la retirada de la API. Además, llegado este punto de control, se actualizará al API Owner el estado de la deprecación de la API. 
1. Finalizados los 60 días de monitorización, la OG autoriza la retirada de la API. En entornos pre-productivos, se podría autorizar la retirada de la API antes de finalizar los 60 días de monitorización, si se confirma la ausencia de consumo de la API. 
1. Deprecación de la API en el entorno por parte del operador correspondiente dentro del equipo de despliegue, añadiendo la **etiqueta de deprecado** a la API. Si se ha determinado que el estado final de la API sea su retirada, entonces se añadirá la **etiqueta de retirada**. 
## <a name="_toc139884176"></a><a name="_toc139961719"></a>Deprecación en entorno de producción
Se recomienda que empiece 30 días después del inicio del proceso en entornos pre-productivos. 

1. La OG **avisa a todos los consumidores** de la API de su deprecación.
1. La OG **bloquea las nuevas suscripciones** a la API. 
1. La OG realiza el **seguimiento o monitorización (trazas)** de la API. Las dos casuísticas son las mismas que en los entornos pre-productivos.   
1. A los 40 días se establece un **punto de control en el tiempo de monitorización** en el que se actualizará al API Owner el estado de la deprecación de la API. Además, si sigue habiendo consumidores, se mandará una alerta y a mayores se **abrirá una incidencia** para revisar el caso (se puede abrir una incidencia nueva o utilizar la tarea del Jira existente, cambiando la criticad a ALTA). 
1. Finalizados los 60 días de monitorización, la OG abre un plazo de tiempo para que el API Owner pueda hacer alegaciones en la tarea Jira. En caso de que se produzcan alegaciones claras e irrefutables, se podrá revisar el proceso y tomar la decisión correspondiente (por ejemplo, bloquear o detener la deprecación). Se recomienda que este período de gracia tenga una duración de unos 4 o 5 días. 
1. Finalizado el período de monitorización y de alegaciones, se depreca la API en el entorno por parte del operador correspondiente dentro del equipo de despliegue, añadiendo la **etiqueta de deprecado** a la API. Siempre se esperará a que termine el período establecido, sin adelantar el proceso de deprecado. Si se ha determinado que el estado final de la API sea su retirada, entonces se añadirá la **etiqueta de retirada**.

En este **momento finalizaría el proceso completo de deprecación de la API**. 

**\*Nota:** se han establecido unos tiempos estándares recomendados, pero estos tiempos pueden modificarse en cada caso.  

**\*\*Nota:** los entornos preproductivos engloban el entorno de desarrollo y el resto de los entornos de pre-producción. 







