

#  **Patrones de diseño**
|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|24/03/2023|Axpe|Versión inicial.|

# Índice
- [1. Introducción	](#_toc1689117939)

- [2. Tipos de patrones de diseño	](#_toc439664740)

- [3. Patrones de diseño recomendados ](#_toc1043760565)

  - [3.1. Patrón Composite	](#_toc456211337)

  - [3.2. Patrón Proxy	](#_toc1699599255)

  - [3.3. Patrón Backend for Frontend (BFF)	](#_toc1840314773)

  - [3.4. Circuit Breaker o Patrón Disruptor	](#_toc676984127)

  - [3.5. Patrón API Gateway	](#_toc2065311893)



# <a name="_toc129769265"></a><a name="_toc1689117939"></a>1. Introducción
Los patrones de diseño son una solución general, reutilizable y aplicable a diferentes problemas de diseño de software. Se trata de plantillas que identifican problemas en el sistema y proporcionan soluciones apropiadas a problemas generales a los que se han enfrentado los desarrolladores durante un largo periodo de tiempo, a través de prueba y error.

Dentro de la definición de patrón de diseño se incluyen distintos tipos de patrones, de los cuales destacaremos los patrones de diseño y los arquitectónicos. Estos tipos están estrechamente relacionados y son muy similares, sin embargo no son el mismo concepto dado que un patrón arquitectónico tiene un enfoque más abstracto, más general.
# <a name="tipos-de-patrones-de-diseño"></a><a name="_toc129769266"></a><a name="_toc439664740"></a>2. Tipos de patrones de diseño
Los patrones de diseño se pueden clasificar según el área donde ayuden a resolver problemas. Las áreas son muy diversas y variadas, sin embargo nos centraremos en dos áreas en concreto, el **área del software** y el **desarrollo en la nube.** Dentro de cada área hay distintas categorías donde se encapsula cada patrón aún más, permitiendo así caracterizar al patrón con mayor facilidad.
# <a name="patrones-de-diseño-recomendados-para-ren"></a><a name="_toc129769267"></a><a name="_toc1043760565"></a>3. Patrones de diseño recomendados 
En este apartado se explicarán en profundidad los patrones de diseño seleccionados y recomendados para la compañia, que son los siguientes:

- **Patrones de diseño de software:**
  - Composite
  - Proxy
- **Patrones de diseño en la nube:**
  - Backends for Frontends (para el diseño y la implementación)
  - Circuit Breaker (para la disponibilidad y la resiliencia)
  - API Gateway (para la gestión y el seguimiento, sobre todo)
## <a name="patrón-composite"></a><a name="_toc129769268"></a><a name="_toc456211337"></a>3.1. Patrón Composite
Este es un tipo de patrón de diseño estructual que permite componer objetos en estructuras de árbol para representar jerarquías de parte-todo. Este patrón permite a los clientes tratar las estructuras como si fuesen objetos individuales y a las composiciones de manera uniforme.

El patrón Composite se puede utilizar cuando: 

- Haya que implementar una estructura de objetos con forma de árbol. Sólo tiene sentido aplicarlo si el modelo central de la aplicación se puede representar en forma de árbol. 
- Cuando el código cliente trate elementos simples y complejos de la misma manera.

![DiagramaComposite](images/Composite.png)


El uso del patrón Composite sólo tiene sentido cuando el modelo central de la aplicación se puede representar en forma de árbol. Por ejemplo, tenemos un primer objeto, que será Productos y otro segundo objeto que será Cajas. Una caja puede contener varios productos, pero también puede contener cajas mas pequeñas, a su vez estas cajas pequeñas pueden contener más productos o incluso más cajas, y así sucesivamente. Si se decide crear un sistema de pedidos y queremos saber el precio total del pedido.

Se puede intentar la solución directa que es desenvolver todas las cajas, contar todos los productos y calcular el total, esto sería viable en el mundo real pero en un programa no es tan fácil, ya que hay que conocer de antemano las clases que hay que iterar tanto de Producto Como de Caja, el nivel de anidación de las cajas etc. Esto hace que la solución sea bastante complicada.

La mejor solución es aplicar el patrón Composite, el cual dice que se defina una interfaz unificada (Component) para los objetos parciales (Leaf) y objetos completos (Composite). Los Leaf son objetos individuales que implementar la interfaz unificada Component directamente, y los objetos completos (Composite) envían solicitudes a sus componentes secundarios. Esto permite a los clientes trabajar a través de la interfaz unificada Component, para poder tratar de manera uniforme los objetos individuales (Leaf) y completos (Composite). Los objetos individuales son los que realizan la solicitud directamente, mientras que los objetos completos son aquellos son los que reenvían la solicitud a sus componentes secundarios de forma recursiva hacia abajo en la estructura del árbol. Esto hace que las clases de cliente sean más fáciles de implementar, cambiar, probar, y reutilizar.

La gran ventaja de esta solución es que no hay que preocuparse por las clases concretas de los objetos que componen el árbol. No se tiene por que saber si un objeto es individual o completo. Se pueden tratar todos por igual a través de la interfaz común. Cuando se invoca a un método, los propios objetos pasan la solicitud a lo largo del árbol.

Algunos problemas y consideraciones que hay que tener en cuenta a la hora de implementar este patrón:

- Se puede trabajar con estructuras de árbol complejas con mayor comodidad utilizando el polimorfismo y la repercusión a nuestro favor.
- Se aplica el principio abierto/cerrado, ya que se puede introducir nuevos tipos de elementos en la aplicación sin descomponer el código existente, que ahora funciona con el árbol de objetos.
- En algunas ocasiones podrá resultar complicado proporcionar una interfaz común para clases cuya funcionalidad difiere demasiado. En esos casos, habrá que generalizar en exceso la interfaz que unifica los objetos (Component), provocando que sea más difícil de comprender.
## <a name="patrón-proxy"></a><a name="_toc129769269"></a><a name="_toc1699599255"></a>3.2. Patrón Proxy
Proxy es un patrón de diseño estructural que funciona como intermediario o sustituto de un objeto original, para controlar y administrar el acceso al mismo. Por lo tanto, el Proxy es una capa que separa al cliente del objeto destino, y contiene la misma interfaz que el objeto al que representa. El Proxy puede cumplir la función de redirigir al objeto original, pero también puede añadir nuevas funcionalidades.

Este patrón se utiliza para: 

- Retrasar la inicialización de un objeto muy pesado, que utiliza muchos recursos del sistema.
- Controlar el acceso al objeto de servicio cuando es una parte fundamental del sistema operativo. 
- Objetos ubicados en un servidor remoto a los que hay que acceder a través de la red, de manera que el proxy pase la petición y se encargue de gestionar los detalles.
- Mantener un historial de solicitudes al objeto original, que queden registradas en el Proxy. - Guardar en la memoria caché resultados de solicitudes previas para que, en las que sean recurrentes, se puedan utilizar los mismos resultados. 
- Desechar un objeto cuando ya no haya clientes que lo utilicen, y liberar los recursos subyacentes del sistema.
- Retrasar la replicación de un objeto grande y complejo. El Proxy rastrea cuándo se ha modificado el objeto, y éste no se copia de nuevo a menos que hayan realizado cambios.
- Garantizar la seguridad.

![DiagramaProxy](images/Proxy.png)



El patrón Proxy se utiliza sobre todo para objetos grandes y complejos que consumen muchos recursos del sistema, y queremos evitar que estén siempre en funcionamiento, sino sólo cuando se necesita.

También se utiliza este patrón cuando queremos restringir el acceso de ciertos clientes al objeto original. Por ejemplo, supongamos que queremos acceder a Internet a través de una aplicación. Si queremos restringir el acceso a ciertas páginas web y lo hacemos directamente sobre la clase Internet, ningún usuario tendrá nunca acceso a estos sitios.

El Proxy también se utiliza en casos en los que una aplicación tiene que cargar o mostrar imágenes y vídeos que son muy pesados, y esto puede ser un problema cuando la app tiene recursos limitados o conectividad a Internet de bajo ancho de banda. Por ejemplo, imaginemos un objeto servicio de descarga de vídeos. Supongamos que este servicio coge el nombre del vídeo solicitado, va a youtube, lo busca, lo descarga y te devuelve los metadatos y la localización de la descarga. Cada vez que un usuario necesita un vídeo particular, este se vuelve a descargar, independientemente de si ya se ha descartado previamente.

Al implementar el patrón de diseño Proxy, lo que se hace es desarrollar una nueva clase que tiene la misma interfaz que el objeto original, de manera que es indistinguible y el cliente puede ignorar que está interactuando con un Proxy. El Proxy puede implementar la inicialización diferida en el caso de objetos que consumen muchos recursos, de manera que este objeto se construye sólo cuando es necesario, y no se encuentra en funcionamiento todo el tiempo. En el caso de restringir el acceso a ciertas páginas web, en vez de hacerlo directamente sobre la clase Internet, la solución es crear una clase proxy que puede verificar la solicitud de acceso del usuario en una lista de páginas prohibidas, y denegar el acceso cuando sea necesario.

Además, el Proxy también puede añadir nuevas funcionalidades, como la de una memoria caché que guarde la información relacionada con los vídeos o imágenes que ya se han descargado, para así evitar descargarlos de nuevo. Delegará todo el trabajo en el servidor original, pero mantendrá un seguimiento de los vídeos o las imágenes y devolverá los datos de la memoria caché si estos ya se han descargado en una solicitud previa.

Tenemos diferentes tipos de patrón Proxy:

- **Proxy remoto**: representante local de un objeto remoto, que se encuentra en otro servidor. El Proxy pasa la solicitud por la red y gestiona las inconveniencias de acceder al objeto real.
- **Proxy virtual**: da una respuesta por defecto e instantánea, ya que el objeto original puede tardar un poco en procesar los resultados. Inicia la operación al objeto real y cuando éste procesa la solicitud, da la información real al cliente.
- **Proxy de protección**: controla las aplicaciones que tienen acceso al objeto.
- **Proxy de referencia inteligente**: proporciona una capa adicional de seguridad que requiere ciertas operaciones para acceder al objeto.

Se deben considerar los siguientes puntos a la hora de decidir cómo implementar este patrón:

- El patrón agrega otra capa de abstracción, de manera que algunos clientes acceden al Proxy, y otros al objeto real, lo que puede dar lugar a un comportamiento dispar.
- El código puede complicarse, pues se introducen muchas clases nuevas.
- La respuesta del servicio puede retrasarse.

## <a name="_toc1840314773"></a>3.3. Patrón Backend for Frontend (BFF)
Este patrón crea servicios independientes del backend para que diferentes aplicaciones de frontend o interfaces los puedan usar. Este patrón es útil cuando se desea evitar personalizar un único backend para varias interfaces. 

El BFF se puede usar cuando: - Un servicio back-end de uso general o compartido deba mantenerse con una sobrecarga de desarrollo importante. - Se desee optimizar el back-end para los requisitos de interfaces de clientes específicos. - Cuando las personalizaciones se realizan en un back-end de uso general para dar cabida a varias interfaces. - Un lenguaje alternativo es más adecuado para el back-end de una interfaz de usuarios diferentes. 

Debe evitarse su uso cuando:

- Las interfaces realizan las mismas solicitudes, o muy similares, al back-end. 
- Sólo se usa una interfaz para interactuar con el back-end.

![DiagramaBFF](images/BFF.png)


Inicialmente se puede destinar una aplicación a una interfaz de usuario web de escritorio. Normalmente, un servicio de back-end se desarrolla en paralelo y proporciona las características necesarias para esa interfaz de usuario. A medida que crece la base de usuarios de la aplicación, se desarrolla una aplicación que debe interactuar con el mismo back-end. El servicio back-end se convierte en un back-end de uso general que atiende los requisitos de la interfaz tanto de escritorio como de móvil. Es importante destacar que las funcionalidades de un dispositivo móvil difieren significativamente de las funcionalidades de las de un explorador de escritorio, en términos de pantalla, rendimiento, y limitaciones de pantalla. En consecuencia, los requisitos para un back-end de aplicación móvil difieren de los de la interfaz de usuario web de escritorio. 

Estas diferencias pueden dar lugar a requisitos contrapuestos para el back-end. El back-end requiere cambios significativos y regulares para atender tanto la interfaz de usuario web de escritorio como la aplicación móvil. 

A menudo, hay equipos independientes de la interfaz que funcionan en cada front-end y hacen que el back-end se convierta en un cuello de botella en el proceso de desarrollo. Los requisitos de actualización conflictivos y la necesidad de mantener el servicio en funcionamiento para ambos front-ends puede suponer dedicar un gran esfuerzo a un único recurso que se puede implementar. Como la actividad de desarrollo se centra en el back-end, se puede crear un equipo independiente para administrar y mantener el back-end. 

Cuando un equipo de la interfaz requiere cambios en el back-end, esos cambios se deben validar con otros equipos de la interfaz antes de que se puedan integrar en el back-end. 

La solución que se obtiene es crear un back-end por cada interfaz de usuario. De manera que hay que ajustar el comportamiento y el rendimiento de cada back-end para que se adapte mejor a las necesidades del entorno de front-end, sin preocuparse de que pueda afectar a otras experiencias front-end. 

Como cada back-end es especifico de una interfaz, se puede optimizar para esa interfaz. En consecuencia, será más pequeño, menos complejo, y es probable que más rápido que un back-end genérico que intenta satisfacer los requisitos de todas las interfaces. Cada equipo de la interfaz tiene autonomía para controlar su propio back-end y no se apoya en un equipo de desarrollo de back-end centralizado. Esto proporciona flexibilidad al equipo de la interfaz en la selección del lenguaje, el ritmo de lanzamiento, la priorización de la carga de trabajo y la integración de características en el back-end. 

Hay que tener en consideración los siguientes puntos: 

- Hay que tener en cuenta el número de servidores back-end que se van a implementar. 
- Si diferentes interfaces (por ejemplo los clientes móviles) van a hacer las mismas solicitudes, hay que calcular si es necesario implementar un back-end para cada interfaz o si será suficiente con un back-end único. 
- Es probable que al implementar este patrón se produzca una duplicación de código en los servicios. 
- Los servicios back-end que estén centrados en front-end solo deben contener una lógica y un comportamiento específicos del cliente. La lógica de negocios general y otras características globales se deben administrar en otra parte de la aplicación. 
- Hay que pensar en cómo se puede reflejar este patrón en las responsabilidades de un equipo de desarrollo. 
- Se debe tener en cuenta el tiempo que tardará en implementar este patrón.

## <a name="_toc676984127"></a>3.4. Circuit Breaker o Patrón Disruptor 
Este patrón se utiliza para controlar errores que pueden tardar una gran cantidad de tiempo durante la conexión a un servicio o recurso remoto. Es decir, evita que la aplicación intenta una operación que tiene probabilidades de fallar de forma reiterada. Por lo tanto, permite que la aplicación continúe con su ejecución sin malgastar recursos mientras el problema no está resuelto. Sirve para mejorar la estabilidad y la resistencia de una aplicación. 

El Circuit Breaker se usa para: 

- Evitar que una aplicación intente invocar un servicio remoto o acceda a un recurso compartido, cuando es muy probable que esta operación produzca un error. 

Se debe evitar su uso: 

- Para el control de acceso a recursos locales privados en una app. En este caso, el uso de un disyuntor agregaría sobrecarga al sistema.
- Como sustituto para controlar las excepciones en la lógica empresarial de las apps. 

Este patrón resulta útil cuando, en un entorno distribuido, las llamadas a los servicios y los recursos remotos pueden producir un error debido a errores transitorios, como son las conexiones de red lentas, el agotamiento de los tiempos de espera o los recursos que se sobrecargan o no están disponibles temporalmente. Estos errores suelen corregirse por sí mismos tras un breve período de tiempo y una aplicación sólida en la nube debe estar preparada para controlarlos mediante una estrategia como la del patrón Retry (reintento). Sin embargo, también puede haber situaciones en las que los errores se deban a eventos que no están anticipados y cuya corrección puede tardar mucho más tiempo. La gravedad de estos errores puede abarcar desde una pérdida parcial de la conectividad hasta la total detención de un servicio. 

En estas situaciones, es posible que no tenga sentido para una aplicación volver a intentar continuamente una operación que no es probable que pueda funcionar de modo correcto y, en su lugar, deba admitir este hecho con rapidez y tratar este error en consecuencia. Además, si un servicio está muy ocupado, el error en una sola parte del sistema podría provocar errores en cascada. Por ejemplo, una operación que invoca un servicio puede configurarse para implementar un tiempo de espera y responder con un mensaje de error si el servicio no responde dentro de este período. 

Sin embargo, esta estrategia puede desencadenar muchas solicitudes simultáneas a la misma operación para que se bloquee hasta que expire el período de tiempo de espera. Estas solicitudes bloqueadas pueden contener recursos críticos del sistema, tales como memoria, subprocesos o conexiones de base de datos, entre otros. Por lo tanto, estos recursos podrían agotarse y provocar errores de otras partes posiblemente no relacionadas del sistema que tenga que usar los mismos recursos. 

En estas situaciones, podría ser preferible para la operación dejar de funcionar de inmediato y solo intentar invocar el servicio, si es posible que pueda ejecutarse correctamente. Hay que tener en cuenta que establecer un tiempo de espera menor podría ayudar a resolver este problema, pero no debería ser tan corto como para que la operación de error en la mayoría de los casos, incluso aunque la solicitud al servicio finalmente pudiera realizarse correctamente.

![DiagramaCircuitBreaker](images/Circuit_Breaker.png)



El patrón Circuit Breaker puede impedir que una aplicación intente repetidamente ejecutar una operación que tenga probabilidad de dar error. Esto le permite continuar sin esperar a corregir el error ni desperdiciar ciclos de CPU mientras se determina si el error continuará durante mucho tiempo. El patrón Circuit Breaker también permite a una aplicación detectar si el error se ha resuelto. Si el problema parece haberse corregido, la aplicación puede intentar invocar la operación. 

Un Circuit Breaker (disyuntor) actúa como un proxy para las operaciones que podrían producir errores. El proxy debe supervisar el número de errores recientes que se han producido y utilizar esta información para decidir si permite que continue la operación o simplemente devuelve de inmediato una excepción. 

El proxy se puede implementar como una máquina con los siguientes estados que imitan la función de un disyuntor eléctrico: 

- **Closed (cerrado):** la solicitud de la aplicación se enruta a la operación. El proxy mantiene un recuento del número de errores recientes, y si la llamada a la operación se realiza correctamente, el proxy incrementa este recuento. Si el número de errores supera un umbral en un periodo de tiempo determinado, el proxy cambia el estado a Open (abierto). En este momento, el proxy inicia un temporizador de tiempo de espera y, cuando este temporizador expira , se coloca en el estado Half-open(semiabierto). 
- **Open (abierto):** la solicitud de la aplicación produce un error inmediatamente y se devuelve una excepción a la aplicación. 
- **Half-open (semiabierto):** se permite pasar un número limitado de solicitudes de la aplicación e invocar la operación. Si estas solicitudes se realizan de forma correcta, se supone que la causa del error se ha corregido y el disyuntor cambia el estado a Closed (cerrado) y el número de errores se restablece. Si alguna solicitud da error, el disyuntor supone que el anterior error no se solucionó y vuelve al estado Open (abierto) y reinicia el temporizador de tiempo de espera para dar al sistema más tiempo para recuperarse. 

El estado de Half-open es útil para impedir que un servicio de recuperación se colapse de repente con solicitudes. A medida que un servicio se recupera, podría ser capaz de admitir un número limitado de solicitudes hasta que la recuperación se completa, pero mientras está en curso, una saturación de trabajo puede hacer que el servicio agote el tiempo de espera o dé un error nuevo. 

En resumen, el patrón Circuit Breaker proporciona estabilidad mientras el sistema se recupera de un error y minimiza el impacto en el rendimiento. Puede ayudar a mantener el tiempo de respuesta del sistema al rechazar rápidamente una solicitud para una operación que es probable que dé error, en lugar de esperar a que agote el tiempo de espera o no termine nunca. Si el disyuntor genera un evento cada vez que cambia el estado, esta información puede utilizarse para supervisar el estado de la parte del sistema protegida por el disyuntor o para alertar a un administrador cuando un disyuntor se active en el estado Open (abierto). 

Es importante mencionar que el patrón es personalizable y puede adaptarse según el tipo de errores posibles. 

Algunos problemas y consideraciones a tener en cuenta: 

- Control de excepciones: Una aplicación que invoca una operación a través de un disyuntor debe estar preparada para controlar las excepciones que se produzcan si la operación no está disponible. La forma en que se controlan las excepciones será la especificación de la aplicación. 
- Tipos de excepciones: Una solicitud podría producir un error por diversos motivos, algunos de ellos podrían indicar un tipo de error más grave que otras. Un disyuntor puede examinar los tipos de excepciones que se producen y ajustar su estrategia en función de la naturaleza de esas excepciones. 
- Registro: Un disyuntor debe registrar todas las solicitudes con error (y, posiblemente correctas) para permitir que un administrador supervise el estado de la operación. 
- Capacidad de recuperación: Debe configurar el disyuntor para que coincida con el modelo de recuperación más probable de la operación que se protege. 
- Prueba de las operaciones con error: En el estado Open en lugar de usar un temporizador para determinar cuándo cambiar al estado Half-open, un disyuntor puede en cambio hacer ping periódicamente al servicio remoto o al recurso para determinar si tiene que estar disponible de nuevo. 
- Invalidación manual: En un sistema en el que el tiempo de recuperación de una operación que da error es muy variable, es conveniente proporcionar una opción de restablecimiento manual que permita a un administrador cerrar el disyuntor y así poder restablecer el contador de errores. De manera similar, un administrador podría forzar que un disyuntor pase al estado Open y reiniciar así el temporizador de tiempo de espera, en caso de que la operación protegida por el disyuntor no esté disponible temporalmente. 
- Simultaneidad: El mismo disyuntor puede tener acceso a un gran número de instancias simultáneas de una aplicación. La implementación no debe bloquear las solicitudes ni agregar una sobrecarga excesiva a cada llamada a una operación. 
- Diferenciación de recursos: Hay que tener cuidado cuando se use un único disyuntor para un tipo de recurso si puede haber varios proveedores independientes subyacentes. Ya que en caso de que se combinen las respuestas de error por ejemplo una aplicación podría intentar acceder a algunas peticiones incluso cuando fuese muy probable que se produjera un error. 
- Disyuntor acelerado: A veces, una respuesta de error puede contener suficiente información para que el disyuntor se active inmediatamente y permanezca de esta manera una cantidad mínima de tiempo. 
- Respuestas de las solicitudes con error: En el estado Open, en lugar de generar un error rápidamente, un disyuntor también puede registrar los detalles de cada solicitud en un diario y hacer que estas solicitudes se reproduzcan cuando el servicio o el recurso remoto estén disponibles. 
- Tiempos de espera inadecuados en servicios externos: Un disyuntor podría no ser capaz de proteger completamente las aplicaciones, de las operaciones que generan errores en los servicios externos configurados con un período prolongado de tiempo de espera. Si el tiempo de espera es demasiado largo, un subproceso que ejecuta un disyuntor podría bloquearse durante un largo período antes de que este indique que la operación ha fracasado. En este momento, muchas otras instancias de aplicaciones también podrían intentar invocar el servicio a través del disyuntor y ocupar un número significativo de subprocesos antes de que todos den error.

## <a name="_toc2065311893"></a>3.5. Patrón API Gateway 
El patrón API Gateway proporciona un punto de entrada único para ciertos grupos de microservicios. Utiliza un sistema distribuido. Es una variación del patrón BFF, que utilizaría una puerta de enlace independiente para cada tipo de cliente.  

![DiagramaAPIGateway](images/API_Gateway.png)


Este patrón se usa cuando:

- Se quiera evitar problemas de seguridad, ya que sin una puerta de enlace, todos los microservicios estarían expuestos. 
- Para evitar excesivas llamadas entre cliente y servidor, ya que esto genera una latencia significativa. La agregación manejada a un nivel intermedio podría mejorar el rendimiento y la experiencia del usuario para la aplicación cliente. 
- Para que no se acoplen las aplicaciones del cliente a los microservicios internos. 

A menudo la granularidad de las APIs proporcionadas por los microservicios suele ser diferente a lo que necesita un cliente, lo que significa que los clientes necesitan interactuar con varios servicios. Además, los clientes necesitarán diferentes datos, por ejemplo: la versión del navegador de escritorio de la página web suele ser más elaborada que la de la versión móvil. 

Otro de los problemas es que el rendimiento de la red es diferente en los distintos clientes, por ejemplo, una red móvil suele ser mucho más lenta y tiene una latencia mucho más alta que en una no móvil. Y por supuesto, cualquier WAN es mucho más lenta que una LAN, esto significa que un cliente móvil nativo utiliza una red que tiene características de rendimiento muy diferentes a las de una LAN utilizada por una aplicación web del lado del servidor. 

Otra peculiaridad es que el número de instancias de servicio y sus ubicaciones (host+puerto) cambia dinámicamente. 

La mejor solución a los problemas que se han comentado anteriormente es implementar un API Gateway que sea el único punto de entrada para todos los clientes. La puerta de enlace API maneja las solicitudes de dos maneras, la primera es que algunas solicitudes simplemente se envían/enrutan al servicio apropiado, y la segunda es que se manejan otras solicitudes desplegándose en múltiples servicios. Hay que tener cuidado al implementar este patrón, ya que por lo general no suele ser buena idea tener una puerta de enlace API única que agregue todos los microservicios internos de su aplicación. Si lo hace, actúa como un agregador u orquestador monolítico y viola la autonomía de los microservicios al acoplar todos los microservicios. Por lo tanto, las puertas de enlace deben segregarse en función de los límites comerciales y las aplicaciones del cliente y no actuar como un agregador único para todos los microservicios internos. 

Algunos problemas y consideraciones a la hora de implementarlo:  

- El inconveniente más importante es que cuando se implementa un API Gateway, se está acoplando ese nivel con el de los microservicios internos. Un acoplamiento como este podría presentar serias dificultades para su aplicación.  
- El uso de una puerta de enlace API de un microservicio crea un posible punto único adicional de falla.  
- Una puerta de enlace API puede introducir un mayor tiempo de respuesta debido a la llamada de red adicional. Sin embargo, esta llamada adicional generalmente tiene menos impacto que tener una interfaz de cliente que haga demasiadas llamadas a los microservicios internos. 
- Si no se escalan adecuadamente, la puerta de enlace API puede convertirse en un cuello de botella. 
- Este patrón requiere unos costes de desarrollo adicionales y en caso de que haya agregación de datos y lógica personalizada un mantenimiento futuro. Los desarrolladores deben actualizar el API Gateway para exponer los puntos finales de cada microservicio. Además, los cambios de la implementación en los microservicios internos pueden provocar cambios de código en el nivel de API Gateway. 
- Si la puerta de enlace API, es desarrollada por un solo equipo puede haber un cuello de botella en el desarrollo, esta es una de las razones por las que se considera que es mejor tener varias puertas de enlace API detalladas que respondan a las diferentes necesidades de los clientes.


