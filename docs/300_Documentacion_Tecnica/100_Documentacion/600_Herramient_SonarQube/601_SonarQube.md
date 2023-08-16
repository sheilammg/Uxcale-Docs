|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|16/03/2023|Axpe|Versión inicial|



# **SonarQube: Herramienta de revisión de código**

## Índice
---
[1. Introducción](#introducción)

- [1.1. ¿Escribiendo código limpio](#escribiendo-codigo-limpio)

[2. Características Principales](#caracteristicas-principales)

[3. Requisitos](#requisitos)

[4. Instalación](#instalacion)

[5. Métricas principales](#metricas-principales)

[6. Reglas](#reglas)

  - [6.1. Detalles de una regla](#detalles-regla)
  - [6.2. Crear regla personalizada](#crear-regla-personalizada)

[7. Perfiles de calidad (Quality Profiles)](#perfiles-calidad)

[8. Puertas de calidad](#puertas-calidad)

[9. SonarLint](#sonarlint)

  - [9.1. Instalación de Sonarlint](#instalacion-sonarlint)

<div id='introduccion'/>

## 1. Introducción
SonarQube es una herramienta de revisión de código automática y autoadministrada que lo ayuda sistemáticamente a entregar un código limpio. Como elemento central de nuestra solución Sonar, SonarQube se integra en su flujo de trabajo existente y detecta problemas en su código para ayudarlo a realizar inspecciones continuas del código de sus proyectos. La herramienta analiza más de 30 lenguajes de programación diferentes y se integra en su canal de CI y plataforma DevOps para garantizar que su código cumpla con los estándares de alta calidad. 

<div id='escribiendo-codigo-limpio'/>

### 1.1. Escribiendo código limpio
Escribir código limpio es esencial para mantener una base de código saludable. Definimos código limpio como código que cumple con un cierto estándar definido, es decir, código que es confiable, seguro, mantenible, legible y modular, además de tener otros atributos clave. Esto se aplica a todo el código: código fuente, código de prueba, infraestructura como código, código adhesivo, scripts, etc.

El enfoque Clean as You Code de Sonar elimina muchas de las dificultades que surgen al revisar el código en una etapa tardía del proceso de desarrollo. El enfoque Clean as You Code utiliza su puerta de calidad para alertarlo/informarle cuando hay algo que arreglar o revisar en su nuevo código (código que se agregó o cambió), lo que le permite mantener altos estándares y concentrarse en la calidad del código.

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.002.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.002.png)

La solución Sonar realiza comprobaciones en cada etapa del proceso de desarrollo:

- SonarLint proporciona comentarios inmediatos en su IDE a medida que escribe el código para que pueda encontrar y solucionar problemas antes de una confirmación.
- El análisis de relaciones públicas de SonarQube   encaja en sus flujos de trabajo de CI/CD con el análisis de relaciones públicas de SonarQube y el uso de controles de calidad.
- Las puertas de calidad evitan que el código con problemas se lance a producción, una herramienta clave para ayudarlo a incorporar la metodología Clean as You Code.
- El enfoque Clean as You Code lo ayuda a concentrarse en enviar código nuevo y limpio para producción, sabiendo que su código existente se mejorará con el tiempo.

<div id='caracteristicas-principales'/>

## 2. Caracteristicas Principales
Dentro de SonarQube nos encontramos con las siguientes características:

- Admite los lenguajes de programación más populares como Java, C / C ++, Objective-C, C #, PHP, Flex, Groovy, JavaScript, Python, PL / SQL, COBOL, etc.
- Realiza revisiones automáticas con análisis de código estático detectando problemas que afectan la calidad del código.
- Facilita informes ofreciendo información objetiva de la calidad actual de los proyectos utilizando métricas y gráficos de prueba de calidad avanzados. Esto incluye datos sobre código duplicado, estándares de codificación, pruebas unitarias, cobertura de código, complejidad del código, errores potenciales, comentarios, diseño y arquitectura.
- Se integra con toda la cadena de herramientas de DevOps ayudando al flujo de trabajo productivo, incluidos los sistemas de compilación, los motores de CI, utilizando webhooks y su RestAPI integral.
- Es ampliable con el uso de complementos.

<div id='requisitos'/>

## 3. Requisitos
Previamente se debe poner instalar Java (Oracle JRE u OpenJDK) en la maquina donde se planea ejecutar SonarQube. El servidor SonarQube requiere la versión 17 de Java y los escáneres SonarQube requieren la versión 11 o 17 de Java. SonarQube es capaz de analizar cualquier tipo de archivo fuente de Java, independientemente de la versión de Java que cumplan

El servidor SonarQube requiere al menos 2 GB de RAM para funcionar de manera eficiente y 1 GB de RAM libre para el sistema operativo. Si está instalando una instancia para un equipo grande o una empresa, se necesita al menos 8 núcleos, para permitir que la plataforma principal de SonarQube se ejecute con múltiples trabajadores, y 16 GB de RAM.

La cantidad de espacio en disco que necesitas dependerá de la cantidad de código que analices con SonarQube. SonarQube se recomienda instalarse en discos duros que tengan un buen rendimiento de lectura y escritura, debido a la gran cantidad de E/S que se realizaran cuando el servidor esté en funcionamiento. Por lo tanto, el rendimiento de lectura y escritura del disco duro tendrá un gran impacto en el rendimiento general del servidor SonarQube.

<div id='instalacion'/>

## 4. Instalación
A continuación, revisaremos los pasos para instalar una instancia local de SonarQube y analizar un proyecto. La instalación de una instancia local facilita su funcionamiento de forma muy rápida.

Para realizar la instalación de SonarQube nos encontramos con dos posibilidades. Por un lado, puedes usar SonarQube a través de una instalación tradicional con el archivo zip o a través de hacer girar un contenedor Docker.

- **Desde el archivo zip:**

Primero, descargar el archivo zip *SonarQube Community Edition* que nos encontramos en [la página oficial de Sonar](https://www.sonarsource.com/products/sonarqube/downloads/). Después se descomprime e la siguiente ruta *C: \ sonarqube o / opt / sonarqube.* Por último, iniciar el server:

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.003.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.003.png)

- **Desde la imagen de Docker:**

Primero, crearemos un fichero docker-compose.yml donde definiremos la configuración para levantar una imagen de sonarQube en Docker. En la siguiente imagen veremos dicha configuración:

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.004.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.004.png)

Después, deberemos de arrancar el fichero docker-compose.yml a partir del siguiente comando:

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.005.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.005.png)

Por último, habría que iniciar sesión en <http://localhost:9000> con las credenciales de administrador del sistema:

- inicio de sesión: admin
- contraseña: admin

Una vez iniciada la sesión en la instancia local de SonarQube, podemos comenzar a analizar un proyecto d forma local:

- Haz clic en el botón Crear nuevo proyecto.
- Asigna a tu proyecto una clave de proyecto y un nombre para mostrar y haz clic en el botón Configurar.
- En Proporcionar un token, selecciona Generar un token. Asigna un nombre a tu token, haz clic en el botón Generar y a continuación, haz clic en Continuar.
- Selecciona el idioma principal de tu proyecto en Ejecutar análisis en tu proyecto y sigue las instrucciones para analizar el proyecto. En este momento podrás descargar y ejecutar un escáner en tu código (si está utilizando Maven o Gradle, el escáner se descarga automáticamente).


<div id='metricas-principales'/>

## 5. Métricas Principales
Para llegar a comprender SonarQube debemos fijarnos en el funcionamiento de esta plataforma. SonarQube examina el código de nuestro proyecto y lo compara con una serie de reglas definidas, que están basadas en estándares o buenas prácticas. También podemos añadir reglas a parte de las que están ya definidas.

SonarQube divide las métricas en las siguientes categorías:

- Complejidad: La complejidad ciclomática depende del número de caminos independientes del código. El programador tratará de reducir este número al mínimo, pues la simpleza es sinónimo de calidad.
- Duplicados: SonarQube señala todas las líneas duplicadas, es decir, aquellas que aparecen más de una vez a lo largo del código fuente, con el fin de evitar que las mismas operaciones generen resultados distintos.
- Evidencias: Las evidencias son todos los fragmentos de código que se incorporaron recientemente e incumplen alguna de las reglas.
- Mantenibilidad: Por mantenibilidad se entiende la capacidad de un producto para evolucionar y ser modificado.
- Umbrales de calidad: SonarQube analiza el nivel de cumplimiento de los requisitos que debe superar el proyecto antes de lanzarse a producción, como un porcentaje mínimo de cobertura (la cantidad de código validado tras los test).
- Tamaño: Proporciona una cifra aproximada del volumen total del proyecto.
- Pruebas: La puesta en marcha de pruebas permite comprobar el funcionamiento y la integración de cada una de las unidades de código examinadas.

Sonarqube usa diversas herramientas de análisis estático como Checkstyle, PMD o FindBugs para obtener estas métricas que ayudan a mejorar la calidad.

||**Checkstyle**|**PDM**|**FindBugs**|
| - | :-: | :-: | :-: |
|**Propósito**|Verificar el cumplimiento de las reglas de codificación.|Identificación de problemas potenciales.|Encontrar errores.|
|**Tipos de verificación**|<p>- Convenciones de nombres</p><p>- Encabezados, importaciones</p><p>- Espacios en blanco, formateo</p><p>- Comentarios de Javadoc</p><p>- Buenas prácticas, convenciones de códigos</p><p>- Parámetros del método</p><p>- Complejidad ciclomática</p><p>- Expresiones regulares</p>|<p>- Posibles errores</p><p>- Código muerto</p><p>- Código duplicado</p><p>- Complejidad ciclomática</p><p>- Expresiones sobrecomplicadas</p>|<p>- Posibles errores</p><p>- Defectos de diseño</p><p>- Malas prácticas</p><p>- Corrección multiproceso</p><p>- Vulnerabilidades de código</p>|

En base a estas reglas de codificación definidas, SonarQube detecta:

- **Bugs**: errores que provocan un resultado que no es esperado.
- **Vulnerabilidades**: errores que podrían poner en peligro la seguridad de nuestro proyecto.
- **Code smells**: errores relacionados con las malas prácticas y la mantenibilidad en el código.

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.006.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.006.png)

Cuando seleccionamos un proyecto de los que tenemos añadidos nos encontramos:

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.007.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.007.png)

En esta imagen vemos que el proyecto seleccionado esta Passed ya que han pasado todas las condiciones que se encuentran configuradas dentro de SonarQube.

Una vez que SonarQube a revisado nuestro código y nos muestra los diferentes errores que tenemos, podemos ir al apartado **issues** dentro de la plataforma donde se puede observar más profundamente los errores del código.

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.008.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.008.png)

<div id='reglas'/>

## 6. Reglas
El [catálogo de Reglas de Sonar](https://rules.sonarsource.com/) es el punto de entrada donde puedes descubrir todas las reglas existentes o crear reglas nuevas basadas en las plantillas disponibles.

Por defecto, al seleccionar la opción Reglas del menú, verás todas las reglas disponibles instaladas en tu instancia de SonarQube. Tiene la capacidad de revisar y reducir la selección según los criterios de búsqueda en la barra lateral izquierda:

- **Idioma**: el idioma al que se aplica una regla.
- **Tipo**: bugs, vulnerabilidad, Code smells o reglas de puntos de acceso de seguridad.
- **Etiqueta**: es posible agregar etiquetas a las reglas para clasificarlas y ayudar a descubrirlas más fácilmente.
- **Repositorio**: el motor/analizador que aporta reglas a SonarQube.
- **Severidad predeterminada**: la severidad original de la regla, tal como la define SonarQube.
- **Estado**: las reglas pueden tener 3 estados diferentes:
  - **Beta**: la regla se implementó recientemente y aún no hemos recibido suficientes comentarios de los usuarios, por lo que puede haber falsos positivos o falsos negativos.
  - **En desuso**: la regla ya no debe usarse porque existe una regla similar, pero más poderosa y precisa.
  - **Listo**: la regla está lista para usarse en producción.
- **Disponible desde**: la fecha en que se añadió por primera vez una regla en SonarQube. Esto es útil para enumerar todas las reglas nuevas desde la última actualización de un complemento, por ejemplo.

**Plantilla**: muestra plantillas de reglas que le permiten crear reglas personalizadas.

- **Perfil de calidad**: inclusión o exclusión de un perfil específico.

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.009.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.009.png)

<div id='detalles-regla'/>

### 6.1. Detalle de una regla
Para ver los detalles de una regla, solo tendríamos que clicar en una de ellas. Junto con los datos básicos de la regla, también podrá ver en qué perfiles, si los hay, está activa la regla y cuántos problemas abiertos se han planteado con ella.

Las siguientes acciones están disponibles solo si tiene el nivel de permiso correcto:

- **Añadir/Quitar etiquetas:**

Es posible agregar etiquetas existentes en una regla o crear nuevas reglas; simplemente ingrese un nuevo nombre mientras escribe en el campo de texto.

Tenga en cuenta que algunas reglas tienen etiquetas integradas que no puede eliminar. Por ejemplo, las reglas las proporcionan los complementos que contribuyen a las reglas.

- **Ampliar descripción:**

Puede ampliar las descripciones de las reglas para que los usuarios sepan más información sobre una regla.

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.010.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.010.png)

<div id='crear-regla-personalizada'/>

### 6.2. Crear una regla personalizada
Dentro de reglas se proporcionan plantillas como base para que los usuarios definan sus propias reglas personalizadas en SonarQube. Para buscar plantillas, seleccione la opción *Mostrar solo plantillas* en el menú desplegable de los filtros:

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.011.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.011.png)

Para crear una regla personalizada a partir de una plantilla, seleccione Crear junto al encabezado Reglas personalizadas e ingrese la siguiente información:

- Nombre
- Clave (sugerida automáticamente)
- Tipo 
- Gravedad
- Estado
- Descripción (se admite el formato Markdown)
- Los parámetros especificados por la plantilla.

<div id='perfiles-calidad'/>

## 7. Perfiles de calidad (Quality Profiles)
Los perfiles de calidad son un componente central de SonarQube, ya que es donde se definen los conjuntos de reglas. Los perfiles de calidad se definen para diferentes lenguajes de programación individuales.

Para administrar perfiles de calidad, debemos entrar a la página **Perfiles de calidad (Quality Profiles)** donde se encuentran los perfiles de calidad agrupados por los diferentes lenguajes.

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.012.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.012.png)

Idealmente, todos sus proyectos se medirán con los mismos perfiles de calidad por defecto, pero eso no siempre es práctico. En algunos casos, puede encontrar que:

- Tiene diferentes requisitos técnicos de un proyecto a otro (pueden aplicarse diferentes reglas a una aplicación Java con hilos o sin hilos).
- Desea garantizar requisitos más estrictos para algunos de sus proyectos (marcos internos, por ejemplo).

Si bien se recomienda tener la menor cantidad posible de perfiles de calidad para garantizar la coherencia entre proyectos, puede definir tantos perfiles de calidad como sea necesario para satisfacer sus necesidades específicas.

Cada lenguaje debe tener un perfil de calidad predeterminado (marcado con la etiqueta DEFAULT). Los proyectos que no estén asignados explícitamente a perfiles de calidad específicos se analizarán utilizando los perfiles de calidad predeterminados. También hay al menos un perfil de calidad incorporado (el modo Sonar) por lenguaje. Estos perfiles de calidad están diseñados por SonarSource con reglas que son generalmente aplicables para la mayoría de los proyectos.

Los perfiles de calidad de Sonar Way son un buen punto de partida a medida que comienza a analizar el código, y comienzan como los perfiles de calidad predeterminados para cada idioma. Dicho esto, es recomendable a la hora de crear un perfil nuevo, el copiar los perfiles que estas por defecto y así, empezar a afinar los contenidos. Algunas características de los perfiles por defecto son:

- Los perfiles de calidad predeterminados no se pueden editar, por lo que no podrá personalizar la forma Sonar según sus necesidades.
- El camino de Sonar se convierte en una línea de base contra la cual puede rastrear sus propios perfiles de calidad.
- La forma de Sonar puede actualizarse con el tiempo para ajustar qué reglas se incluyen y ajustar la gravedad de las reglas.

Copiar los perfiles de calidad es muy sencillo ya que la herramienta nos da la facilidad de hacerlo a partir de un clic. Primeramente, debemos entra en u perfil de calidad, y darle al apartado de opciones como nos encontramos en la siguiente imagen.

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.013.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.013.png)

<div id='puertas-calidad'/>

## 8. Puertas de calidad
Una puerta de calidad es un indicador que le dice si su código cumple con el nivel mínimo de calidad requerido para su proyecto. Consiste en un conjunto de condiciones que se aplican a los resultados de cada análisis. Si los resultados del análisis cumplen o superan las condiciones de la puerta de calidad, muestra un estado Aprobado (Passed); de lo contrario, muestra un estado Fallido (Failed). En esta sección, nos centraremos en la puerta de calidad integrada, llamada “Sonar way”. Por defecto, este es el asignado a todos los proyectos nuevos.

La puerta de calidad "Sonar way" la proporciona SonarSource, está activada de forma predeterminada y se considera integrada y de solo lectura. Esta puerta de calidad se enfoca en el nuevo código que lo ayuda a implementar el enfoque Clean as You Code. Con cada lanzamiento de SonarQube, ajustamos automáticamente esta puerta de calidad predeterminada de acuerdo con las capacidades de SonarQube.

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.014.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.014.png)

Dentro de las condiciones, nos encontramos:

- Calificación de confiabilidad 
- Clasificación de seguridad
- Puntos de acceso de seguridad revisados
- Calificación de mantenibilidad
- Cobertura
- Líneas Duplicadas (%)

A la hora de poder crear una puerta de calidad personalizada, tendríamos que copiar la que viene por defecto y cambiar las condiciones con los valores que creamos convenientes para nuestro proyecto. Normalmente, se recomienda utilizar la que viene por defecto ya que se basa en estándares de código Clean Code y en la metodología Clean as You Code.

<div id='sonarlint'/>

## 9. SonarLint
SonarLint es una extensión IDE gratuita y open-source que identifica y te ayuda a solucionar los problemas de calidad y seguridad mientras escribes el código.

<div id='instalacion-sonarlint'/>

### 9.1. Instalación de SonarLint
A continuación, veremos como instalar SonarLint en nuestra plataforma de desarrollo Eclipse. La instalación es muy sencilla ya que solo tenemos que descargar la extensión correspondiente.

Primeramente, tendremos que entrar dentro de **Eclipse Marketplace**, que es donde se encuentran todos los puglins y herramientas externas de eclipse.

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.015.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.015.png)

Después, buscaremos el plugin correspondiente a SonarLint.

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.016.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.016.png)

Por último, para ver los diferentes errores de nuestro código, tendremos que abrir la ventana SonarLint On-The-Fly:

![Aspose.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.017.png](../../../../assets/images/Aspose-2.Words.8d4199d6-6250-4d51-894e-4a24b6dbf230.017.png)

