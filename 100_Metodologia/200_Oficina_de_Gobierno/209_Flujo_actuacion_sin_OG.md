

# FLUJO DE ACTUACIÓN SIN OFICINA DE GOBIERNO 


|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|10/07/2023|Axpe|Versión inicial.|

# Contenido
[Introducción	](#_toc139963000)

[Flujo de actuación sin Oficina de Gobierno	](#_toc139963001)

[Monitorización	](#_toc139963002)

[Deprecación de una API	](#_toc139963003)

[Flujo de deprecación de una API	](#_toc139963004)

[Deprecación en entornos pre-productivos	](#_toc139963005)

[Deprecación en entorno de producción	](#_toc139963006)




# <a name="_toc139963000"></a>Introducción

En este documento se recoge la propuesta para la compañia del flujo de actuación a seguir cuando surge un nuevo proyecto o iniciativa que requiera el uso de las APIs. Los pasos que se describen a continuación no abarcan el proyecto global, sino sólo aquellas áreas donde intervengan las APIs y haya que realizar tareas de gestión, organización, diseño e implementación. Este procedimiento abarca todo el ciclo de vida de dichas APIs. 

En el caso de la compañía, al carecer de una Oficina de Gobierno que gestione y gobierne este proceso, se presenta esta propuesta con los pasos a seguir por el equipo responsable del diseño y desarrollo de las APIs (API Squad), para conseguir la máxima efectividad y orden a la hora de participar en este tipo de proyectos. 

Los roles y los tiempos que están amarillo a lo largo del documento,  se pueden personalizar o modificar en función de lo que se necesite.


# <a name="_toc139963001"></a>Flujo de actuación sin Oficina de Gobierno


<div align="center">  <img src="images/diagrama.png" alt="Diagrama del flujo de actuacion sin Oficina de Gobierno"  width="70%"/></div>


1. Llega una solicitud de participación del API Squad en un nuevo proyecto o iniciativa que requiere del uso de APIs. La solicitud llegará al equipo a través de la vía comunicativa que se haya establecido en compañía, como el correo electrónico o el Jira. En dicha solicitud se aportará la documentación funcional necesaria para analizar los requisitos. El solicitante podrá ser el API Owner, el responsable de proyecto, o el experto del área de negocio en el cuál se ha generado la necesidad. 
1. Se organizará una reunión inicial para organizar el proyecto y analizar los requisitos y las necesidades de negocio, para lo cual se hará uso de la documentación funcional aportada. En dicha reunión se recomienda la participación de los siguientes roles:
   1. API Desginer y/o API Developer
   1. Backend Designer y/o Developer
   1. Frontend Designer y/o Developer
   1. Analista funcional (de manera optativa) 
   1. Responsable de proyecto 
1. Después de la reunión de inicio, el API Designer/Developer encargado de realizar la API deberá analizar exhaustivamente las necesidades de negocio, y revisar las APIs existentes para confirmar si ya existe una API en la organización que cubra las funcionalidades requeridas. Esto puede dar lugar a dos escenarios:
   1. **No existe una API** que cubra las necesidades de negocio: en ese caso, se trata de un nuevo desarrollo y se creará una API nueva. Los pasos a seguir para la creación de una nueva API se detallan en el Procedimiento de creación y modificación de APIs.
   1. **Ya existe una API** que cubre las necesidades de negocio.
      1. **La API necesita modificaciones o cambios**, se requiere hacer una evolución de una API existente. El proceso de modificación se detalla en el flujo de Creación y modificación de APIs. 
      1. ` `**La API** cubre por completo las necesidades de negocio y **se puede reutilizar de forma directa**. En este caso, habrá que comprobar si el consumidor/cliente tiene acceso a dicha API. En el caso de que no lo tenga, el API Owner gestionará la suscripción para que se pueda consumir la API.  
1. El siguiente paso consistirá en crear una o varias APIs desde cero que cubran las necesidades de negocio, o bien modificar/actualizar alguna de las APIs existentes que ya cubre parte de las necesidades. Tanto el proceso de creación como el de modificación de una API sin participación de la Oficina de Gobierno se recogen en el documento de Procedimiento de creación y modificación de APIs. 
1. Una vez creada la especificación API, se procede a su publicación. Será el API Designer y/o API Developer quien solicite al equipo de despliegue la publicación:
- **Entorno de desarrollo**
  - Especificación API: después de obtener la validación automática con las reglas de Spectral, se publica la especificación API en el entorno de desarrollo.
  - Implementación API: se publica en desarrollo después de la especificación, ya que el desarrollo de la implementación empieza una vez que la especificación está publicada en desarrollo. Cuando la implementación ha pasado la validación automática y las pruebas correspondientes, se publica en el entorno de desarrollo.
- **Entorno de preproducción**

La especificación y la implementación van a la par. Se realizan las pruebas correspondientes que se especifican en el Procedimiento de creación y modificación de APIs. Estas pruebas engloban todas las pruebas de la fase anterior y a mayores las pruebas UAT, de carga o de regresión. 

- **Entorno de producción**

La especificación y la implementación van a la par. Se realizan las pruebas correspondientes que se especifican en el Procedimiento de creación y modificación de APIs. Estas pruebas engloban todas las pruebas de la fase anterior y a mayores las pruebas UAT, de carga o de regresión.

El flujo de despliegue en desarrollo y en entornos superiores se describe con detalle en el documento de Proceso de creación y modificación de las APIs.

1. Una vez que se ha completado la publicación de la API, el API Designer y/o Developer será el encargado de almacenarla en el repositorio correspondiente, adjuntando los siguientes ficheros:
   1. Documentación de la API
   1. Especificación YAML/JSON
   1. Ficheros de la implementación API 
   1. Informes de pruebas de la implementación

**\*Nota:** es conveniente que el almacenado se realice al publicar la API en el entorno de desarrollo, actualizando de forma posterior los ficheros necesarios. 
#
# <a name="_toc139963002"></a>Monitorización

El API Owner se encargará de la monitorización de sus APIs publicadas, debido a que es un proceso importante para garantizar su correcto funcionamiento y disponibilidad. 

La monitorización se lleva a cabo definiendo sondas, endpoints de health, observando si el Gateway está disponible, además de ver si la API está funcionando correctamente y levantada.

Se realiza una sonda para cada API, y para cada uno de los consumidores, de forma que se tiene como objetivo tener todo el flujo completo monitorizado, desde la suscripción de los consumidores, hasta la implementación API.

Se desarrollarán una serie de dashboard donde se monitorizará el consumo de APIs para poder observar su comportamiento, es decir, quien consume la API, el número de solicitudes que se   realizan, si el consumo es excesivo o no, y se generarán una serie de gráficas que reflejen toda esta información.


# <a name="_toc139963003"></a>Deprecación de una API 


<div align="center">  <img src="images/ciclo-de-vida.png" alt="Deprecacion de una API"  width="70%"/></div>

¿Qué es el deprecado de una API? 

El deprecado de una API consiste en **deshabilitarla o descatalogarla**, de manera que ya no se recomienda su uso a los consumidores.  

Cuando una API se depreca, deja de tener soporte activo (mantenimiento). Normalmente, una API pasa a estado deprecado principalmente debido a que se publica una nueva versión. En este caso, se recomienda a los consumidores que migren a la nueva versión, o que utilicen otra alternativa de consumo.  

¿Qué es la retirada de una API? 

Consiste en eliminar o dar de baja la API de forma definitiva, y se corresponde con la última etapa dentro del proceso global de deprecación. Una API se puede retirar completamente cuando: 

- No existen consumidores.  
- Cuando la versión de la API todavía no se ha desplegado, o se ha desplegado parcialmente, y ya existe publicada una nueva versión. En este caso la versión antigua queda obsoleta y se podrá eliminar definitivamente.    
## <a name="_toc139884174"></a><a name="_toc139884233"></a><a name="_toc139963004"></a>Flujo de deprecación de una API
<div align="center">  <img src="images/deprecado.png" alt="Deprecacion de una API"  width="70%"/></div>


El proceso de deprecación debe ejecutarse de manera eficiente para generar el menor impacto posible y para evitar afectar de forma drástica a los consumidores. Resulta de vital importancia establecer un período de deprecación que permita la adaptación de los consumidores a la nueva versión API o a otra alternativa. 

El proceso de deprecación de una API se puede iniciar debido a que el API Owner, en el proceso de monitorización de la API, observa que ya no hay consumidores de dicha API. En ese caso, el API Owner podrá iniciar la deprecación de la API. El inicio del proceso también se puede deber a la existencia de una nueva versión *major,* u otras razones justificadas que se han explicado anteriormente. 

A continuación, el API Owner establecerá un **rango de** **tiempo de deprecación de la API y los pasos a seguir**. De manera estándar, este tiempo será de 3 meses, aunque dependerá del caso concreto. También se determinará **si el paso final del proceso será la deprecación o la retirada** total de la API. 
## <a name="_toc139884175"></a><a name="_toc139884234"></a><a name="_toc139963005"></a>Deprecación en entornos pre-productivos

1. El API Owner **avisa a todos los consumidores** de la API de su deprecación, para que comiencen a migrar a la nueva versión o se adapten a una alternativa de consumo y dejen de utilizar la versión antigua. 
1. Se **bloquean las nuevas suscripciones** a la API. 
1. Se realiza el **seguimiento o monitorización (trazas)** de la API, para mantener un seguimiento tanto de los consumidores y del tráfico, como de su funcionamiento interno.** Los datos resultantes de la monitorización se almacenarán en un informe. Dependiendo de la volumetría, se darán dos casuísticas:   
   1. **Si la volumetría es alta**: el seguimiento deberá ser constante y el tiempo de monitorización se dividirá rangos más cortos. Por ejemplo, los 60 días estándares se pueden dividir en 8 semanas. Cada semana se hará un seguimiento de las peticiones y las llamadas a la API para confirmar el descenso del tráfico.  
   1. **Si la volumetría es baja**, a los 40 días de monitorización se recogerán los datos y se analizarán. 

En esta fase se tendrá en cuenta aquellos procesos que verifican el funcionamiento de las APIs, como el uso de sondas (o healthcheck), ya que darían lugar a falsos positivos. El tiempo de monitorización se establecerá un periodo estándar de 60 días.

1. Si a los 40 días sigue habiendo consumidores, se puede mandar un segundo aviso a los consumidores. 
1. Finalizado el tiempo de monitorización, se procede a la deprecación de la API en el entorno por parte del operador correspondiente dentro del equipo de despliegue, añadiendo la **etiqueta de deprecado** a la API. Si se ha determinado que el estado final de la API sea su retirada, entonces se añadirá la **etiqueta de retirada**. En los entornos pre-productivos, se puede adelantar el tiempo de deprecación si se confirma la ausencia de consumo de la API. 
## <a name="_toc139884176"></a><a name="_toc139884235"></a><a name="_toc139963006"></a>Deprecación en entorno de producción
Se recomienda que empiece 30 días después del inicio del proceso en entornos pre-productivos. 

1. El API Owner **avisa a todos los consumidores** de la API de su deprecación.
1. Se **bloquean las nuevas suscripciones** a la API. 
1. Se realiza el **seguimiento o monitorización (trazas)** de la API. Las dos casuísticas son las mismas que en los entornos pre-productivos.   
1. A los 40 días se establece un **punto de control en el tiempo de monitorización**, en el que se mandará una alerta en caso de que siga habiendo y a mayores se **abrirá una incidencia** para revisar el caso, y se podrá decidir detener o bloquear el proceso si se considera necesario. 
1. Finalizado el período de monitorización, se depreca la API en el entorno por parte del operador correspondiente dentro del equipo de despliegue, añadiendo la **etiqueta de deprecado** a la API. Siempre se esperará a que termine el período establecido, sin adelantar el proceso de deprecado. Si se ha determinado que el estado final de la API sea su retirada, entonces se añadirá la **etiqueta de retirada**.

En este **momento finalizaría el proceso completo de deprecación de la API**. 

**\*Nota:** se han establecido unos tiempos estándares recomendados, pero estos tiempos pueden modificarse en cada caso.  

