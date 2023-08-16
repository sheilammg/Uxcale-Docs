|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|11/04/2023|Axpe|Versión inicial|

# **Documentación técnica: Karate**

## Índice
---
[1. Introducción](#introducción)

[2. Instalación](#instalacion)

  - [2.1. Instalación de Karate a partir de línea de comandos](#instalacion-karate-linea-comandos)

  - [2.2. Instalación de Karate en Eclipse con Spring Boot](#instalacion-karate-eclipse-spring-boot)

  - [2.3. Instalación de Karate a partir de Visual Studio Code](#instalacion-karate-visual-studio)

[3. Estructura de un archivo ".feature"](#estructura-archivo)
  - [3.1. Feature](#feature)
  - [3.2. Background](#background)
  - [3.3. Scenarios](#scenarios)
    - [3.3.1. Scenarios outline](#scenarios-outline)

[4. Estructura de carpetas](#estructura-carpetas)

[5. Palabras clave principales](#palabras-clave-principales)

[6. Variables](#variables)

[7. Acciones](#acciones)

[8. Anotaciones](#anotaciones)

[9. Informe de las pruebas](#informe-pruebas)

[10. ¿Cómo crear scenarios?](#como-crear-scenarios)

<div id='introduccion'/>

## 1. Introducción
Karate es una herramienta Open-Source que combina automatización de pruebas de API, mocks, pruebas de rendimiento e incluso automatización de la interfaz de usuario en un solo marco unificado.

Características principales:

- Su sintaxis es compatible de forma nativa con JSON, XML, YAML y CSV.
- La sintaxis de las pruebas es muy legible, ya que los datos del escenario se pueden expresar en línea, en tablas JSON, XML, o Cucumber Scenario Outline, todos formatos Human-readable.
- Posee un depurador con todas las funciones, que puede retroceder e incluso volver a reproducir un paso mientras lo edita.
- Los scripts pueden llamar a otros scripts lo que permite modularizar nuestro código de testing.
- Cuenta con un motor de Javascript incorporado que le permite crear una biblioteca de funciones reutilizables que se adaptan al entorno u organización específicos.
- Su estructura sigue el estándar Java/Maven, además de contar con integración perfecta o seamless en pipelines CI/CD, aparte de soporte para JUnit 5.
- Permite ejecución paralela mediante multi-threading.
- Genera reportes en formato HTTP, que incluyen logs de los request y responses, lo que facilita la depuración y detección de errores.
- Tiene soporte para la gestión de cabeceras y sistemas de autenticación.
- Está basado en las tecnologías de Cucumber y GherKin para la automatización de pruebas de API.
- **Cucumber**: es una herramienta de prueba que admite el desarrollo impulsado por el comportamiento (BDD). Ofrece una forma de escribir pruebas que cualquiera puede entender, independientemente de sus conocimientos técnicos.
- **GherKin**: es un Lenguaje DSL (Domain-Specific Language), es decir, que fue creado para resolver un problema muy específico. Está compuesto por un conjunto de elementos que se pueden apreciar en la siguiente imagen:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.002.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.002.png)

<div id='instalacion'/>

## 2. Instalación
Dentro de Karate tenemos tres formas de poder utilizar la herramienta, desde eclipse a partir del Framework Spring Boot, desde una extensión de Visual Studio Code y, por último, a partir de la línea de comandos.

<div id='instalacion-karate-linea-comandos'/>

### 2.1. Instalación de Karate a partir de línea de comandos
La instalación para ejecutar Karate directamente desde línea de comando es sencilla, ya que solo tendríamos que ir a la página oficial de Karate y descargar de allí el archivo *.jar.* Después tendríamos solo que ejecutar dicho archivo.

Para llevar a cabo esta instalación tendríamos que revisar sus requisitos mínimos que serian los siguientes: tener instalado Java (Java 11 mínimo) y alrededor de 60 MB libres en disco.

<div id='instalacion-karate-eclipse-spring-boot'/>

### 2.2. Instalación de Karate en Eclipse con Spring Boot
Para la integración con SpringBoot, nos serviremos de la herramienta de gestión de proyectos Maven. En el .pom de nuestro proyecto, añadiremos la siguiente dependecia:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.003.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.003.png)

Una vez añadida la dependencia, instalaremos el plugin de Cucumber en nuestro IDE de Eclipse. Podremos hacer esto fácilmente mediante la Eclipse Marketplace.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.004.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.004.png)

A partir de estos dos pasos ya conseguiríamos tener instalado e integrado Karate en nuestro proyecto con Spring Boot.

<div id='instalacion-karate-visual-studio-code'/>

### 2.3. Instalación de Karate a partir de Visual Studio Code
El editor de código fuente Visual Studio Code nos permite instalar Karate de forma sencilla a partir de la extensión oficial de Karate. Para realizar su instalación tendríamos que ir al apartado de extensiones de Visual Studio Code y buscar la extensión de Karate, en la que nos fijaremos que es la oficial desarrollada por Karate Labs. En la siguiente imagen se muestra cual es detalladamente:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.005.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.005.png)

<div id='estructura-archivo'/>

## 3. Estructura de un archivo ".feature"
Un archivo “.feature” consiste en el archivo donde definiremos los diferentes scenarios que queremos probar, y a su vez es el que nos permitirá arrancar estos scenarios a la vez o uno a uno dependiendo de lo que nos interese.

El formato de este archivo está basado técnicamente en formato GherKin, por lo que todo lo que se necesita para probar servicios web son las tres secciones: **Feature**, **Background** y **Scenario**. De estas secciones la que es opcional es Background.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.006.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.006.png)

También hay una variante de Scenario llamada **Scenario Outline** junto con **Examples**, útil para pruebas basadas en datos.

<div id='feature'/>

### 3.1. Feature
Esta etiqueta agrupará a la **feature** completa, es decir una colección de Scenarios con su respectivo Background.

<div id='background'/>

### 3.2. Background
El **Background** es el campo donde se definirán todas las variables, que podrán ser utilizados en todos los scenarios de esta Feature. Este campo es opcional. 

Las variables pueden tener diversos formatos, como def, assert, print, header, url... La lista completa de formatos será explicada posteriormente más profundamente. 

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.007.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.007.png)

También, podemos utilizar una función de Javascript para generar un identificador aleatorio para cada uno de los scenarios. En el siguiente ejemplo, asignamos al header Request-Id un valor aleatorio entre el 0 y el 1000 generados desde el fichero Javascript request-id.js para identificar cada request.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.008.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.008.png)

<div id='scenarios'/>

### 3.3. Scenarios
Los **Scenarios** son aquellas situaciones que queremos testear contra nuestra API. Dentro de realizar pruebas de servicios web se requiere acceso a aspectos de bajo nivel, como encabezados HTTP, rutas de URL, parámetros de consulta, cargas útiles JSON o XML complejas y códigos de respuesta. Y Karate te da control sobre estos aspectos con el pequeño conjunto de palabras clave enfocadas en HTTP como url, path, param…

Están formados por tres partes principales:

- **Given**. Nos indica sobre qué recurso vamos a realizar el test. Normalmente se pone la url del servicio al que queremos realizar la prueba. *headers* que tiene nuestro servicio, o diferentes condiciones que queramos definir.
- **When**. Señala las condiciones que se deben cumplir para que se lance el Scenario. Un uso muy común es indicar el método para el que queremos lanzar nuestro test.
- **Then**. Son las condiciones que se deben cumplir para que el resultado de la prueba de nuestro Scenario sea exitoso.

Dentro de cada parte podemos utilizar **And** para extender la funcionalidad. Estos serían algún ejemplo: 

- Given – cabeceras
- When – request body de un POST
- Then – validación de los datos obtenidos en la respuesta

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.009.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.009.png)

<div id='scenarios-outline'/>

#### 3.3.1. Scenarios outline
Dentro de Karate también podremos utilizar este tipo de scenario para lograr hacer pruebas basadas en datos. Se debe definir una tabla con datos de ejemplo y usarlos en el scenario a partir de la palabra clave definida en el tabla. En la siguiente imagen se ve un ejemplo:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.010.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.010.png)

<div id='estructura-carpetas'/>

## 4. Estructura de carpetas
Los archivos “.feature” que utiliza Karate para definir los diferentes scenarios, se pueden organizar libremente utilizando los estándares de los paquetes Java. Dentro de estos estándares lo común es tener archivos fuente que no sean de java en una estructura de carpetas separadas(“src/test/resources”), pero dentro de Karate se recomienda que los archivos “.feature” se mantengan junto con los archivos java, que estos se encuentran en el directorio “src/test/java”.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.011.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.011.png)

Normalmente, cuando nos encontramos con un proyecto grande vamos a tener otros archivos de datos (.js, .json), por lo que es mas conveniente tener los archivos “.java” y “.feature” juntos.

<div id='palabras-clave-principales'/>

## 5. Palabras clave principales
Dentro de Karate ya vienen definidas algunas palabras clave, que las mas importantes son: url, path, request, method y status.

- **Url**: se utiliza para definir la url donde se quiere hacer la prueba. Una Url permanece constante hasta que se vuelve a utilizar en un scenario diferente. Por otro lado, para crear direcciones URL dinámicas podremos utilizar la palabra clave **param** para añadir parámetros de consulta.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.012.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.012.png)

- **Path**: se utiliza para definir los parámetros de ruta de estilo REST. Se admiten valores delimitados por comas, lo que puede ser más conveniente y se ocupa de la codificación de URL y de agregar '/' entre los segmentos de la ruta según sea necesario.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.013.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.013.png)

- **Request**: se utiliza para enviar, por ejemplo, un cuerpo en la petición (request body).

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.014.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.014.png)

- **Method**: con esta operación conseguimos definir los métodos HTTP. Para definir estos métodos se utiliza los verbos HTTP: get, post, put, delete, patch, options, head, connect, trace.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.015.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.015.png)

- **Status**: en esta operación se establece el código de respuesta HTTP esperado para la petición realizada.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.016.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.016.png)

Y esta afirmación hará que la prueba falle si el código de respuesta HTTP es diferente. También, si queremos realizar una comprobación mas compleja contra el código de estado HTTP, podemos utilizar **responseStatus**.

<div id='variables'/>

## 6. Variables

- **Def**: se puede definir variables a partir de la palabra clave def directamente en el archivo. La estructura debe ser primero la palabra clave def seguida de un nombre de variable y un valor. Es como definir variables en cualquier lenguaje de programación. Un dato importante es que si se define una variable con el mismo nombre se sobrescribe el valor anterior.

- **Text**: no se utiliza comúnmente, pero en algunos casos se necesita para mostrar expresiones en varias líneas o cadenas, sin utilizar JSON ni XML. En la siguiente imagen vemos un ejemplo con scenario outline:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.017.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.017.png)

- **Table**: se utiliza para formar matrices JSON de forma sencilla, como si fuera una tabla de datos. Un ejemplo sería el siguiente:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.018.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.018.png)

- **Match**: se usa para abordar requisitos de aserción complejos para abordar requisitos de aserción complejos para cargas útiles de respuesta JSON y XML. En resumen, se utiliza para implementar la coincidencia entre dos campos.

Esta técnica no solo es compatible con la coincidencia aproximada, sino que también se puede usar en caso de coincidencia absoluta (==), para verificar si un campo o campos concretos no deberían coincidir (!=), la presencia de las claves deseadas utilizando “contains”( only/any/deep/!contains), iterar sobre cada elemento presente dentro de una matriz(match each) e incluso coincidir con la cabecera de la respuesta(match header).

Dentro de la [documentación oficial de Karate](https://github.com/karatelabs/karate#match) nos encontraremos una amplia gama de coincidencias como match ==, match !=, match contains, match contains only, match contains any, match contains Deep, match !contains, match each, match header.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.019.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.019.png)

Normalmente para una mejor practica nos centraremos solo en usar def para definir variables, a no ser que en algunos casos debamos utilizar otra. Por lo tanto, se tienen diferentes marcadores de tipo para llevar a cabo una conversión de los datos dependiendo de lo que necesitemos. 

- **string**- convertir JSON o cualquier otro tipo de datos (excepto XML) a una cadena.
- **json**- convertir XML, un objeto similar a un mapa o una lista, una cadena o incluso un objeto Java en JSON.
- **xml**- convertir JSON, un objeto similar a un mapa, una cadena o incluso un objeto Java en XML
- **xmlstring**- específicamente para convertir la representación interna de Karate similar a un mapa de XML en una cadena.
- **csv**- convertir una cadena CSV en JSON.
- **yaml**- convertir una cadena YAML en JSON.
- **bytes**- convertir a una matriz de bytes, útil para cargas binarias o comparaciones.
- **copy**- para clonar una referencia de variable de carga útil (JSON, XML, Map o List)

<div id='acciones'/>

## 7. Acciones
- **Assert**: se utiliza para afirmar si una expresión devuelve un valor booleano, que este puede ser afirmativo o negativo dependiendo de la expresión. En la siguiente imagen vemos un ejemplo:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.020.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.020.png)

- **Print**: se utiliza para mostrar variables o diferentes expresiones por la pantalla de la consola. En resumen, consiste en una expresión que muestra datos. Este sería un ejemplo:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.021.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.021.png)

- **Replace**: se utiliza para sustituir marcadores o datos, pero principalmente para tratar cadenas sin formato. En algunos casos también sería conveniente utilizar replace para un JSON anidado y complejo.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.022.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.022.png)

- **Remove**: se utiliza para eliminar claves o elementos de datos de instancias JSON o XML. También se puede utilizar para eliminar matrices JSON entreras por índice. 

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.023.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.023.png)

- **Configure**: se utilizar para configurar los ajustes de configuración de un cliente Http utilizado por Karate. La estructura que se utiliza es similar a la def pero en vez de una variable con nombre, se utiliza las palabras clave de configuración.

La más utilizada es headers, ya que es con la que conseguimos definir los diferentes headers necesarios para el cliente Http. Las demás claves de configuración se pueden observar en la documentación oficial de Karate.

- **Call**: se utiliza para llamar a otros archivos “.feature”, para poder reutilizar datos o funciones de ese “.feature” que estamos llamando. Aquí hay un ejemplo del uso de la call, cargado con la función read:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.024.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.024.png)

También existe la función **Callonce** que tiene la misma funcionalidad que **Call** pero este garantiza que se ejecutara solo una vez.

- **Listen**: se utiliza para esperar hasta que ocurra ese evento. La variable **listenResult** es la encargada de contener el valor pasado por la llamada **Karate.signal()**. En la siguiente imagen vemos un ejemplo.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.025.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.025.png)

- **Doc**: Karate contiene un motor de plantillas incorporado que se usa para insertar HTML personalizado adicional dentro de los informes de los diferentes scenarios. Con doc conseguimos cargar dichos archivos HTML, a partir también de la función read.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.026.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.026.png)

- **Read()**: se utiliza para la reutilización de datos de forma sencilla, a partir de leer y recuperar los datos de otros archivos. De forma predeterminada, se espera que los archivos que quereos leer se encuentren en la misma carpeta que el archivo “.feature”. Pero se puede anteponer el nombre, a partir de **classpath**: que consiste en la carpeta raíz. En la siguiente imagen veremos diferentes ejemplos:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.027.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.027.png)

<div id='anotaciones'/>

## 8. Anotaciones

|**Anotación** |**Descripción** |
| :- | :- |
|**@ignore**|Cualquier Scenario con esta etiqueta se omitirá cuando este se ejecute. |
|**@parallel**|Esta etiqueta se utiliza cuando no se desea que se ejecute en pararlelo algún Scenario, a partir de esta anotación **@parallel=false**|
|**@report**|Se utiliza cuando queremos mostrar o ocultar algun Scenario en el informe HTML. Por defecto se muestra, pero si queremos ocultarla es a partir de la siguiente anotación **@report=false**|
|**@setup**|Se utiliza en los casos en los que la fuente de datos necesite varios pasos, por ejemplo, si se necesita llamar a una API para obtener una matriz JSON, para "configurar" estos datos|
|<p>**@env**</p><p>` `**@envnot**</p>|Estas dos etiquetas permiten “seleccionar” o “deseleccionar” algún Scenario. Esto puede ser realmente conveniente, por ejemplo, para nunca ejecutar algunas pruebas en un determinado entorno|

<div id='informe-pruebas'/>

## 9. Informe de las pruebas
Karate tiene una herramienta que nos muestra informes HTML con el resultado de las pruebas. Para abrir estos informes, tendremos que dirigirnos a la carpeta *target*, donde nos encontramos dicho archivo. También, cuando arranquemos nuestras pruebas, dentro de la consola nos mostrara un enlace con el que podremos ir directamente a este informe.

Dentro de este informe podremos observar los distintos scenarios de test que hemos realizado y el resultado de cada uno de los test, así como mediciones de tiempos, etc.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.028.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.028.png)

<div id='como-crear-scenarios'/>

## 10. ¿Cómo crear scenarios?
Primeramente se creara un archivo “.feature”, donde nos encontraremos con la siguiente estructura explicada anteriormente:

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.029.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.029.png)

Dentro de Feature definiremos la descripción de las diferentes pruebas que queremos hacer. En el background se definen las variables o elementos que se van a reutilizar en varios scenarios para evitar redundancia en estos. La funcionalidad principal de background es la reutilización en scenarios.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.030.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.030.png)

Por último, definiremos el Scenario que es donde se crean los parámetros para realizar la prueba. Dentro del Scenario, primero definimos la Url (se puede definir en el background) en GIVEN, después el método HTTP en WHEN, y por último, el código de estado que devuelve en THEN.

![Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.031.png](../../../../assets/images/Aspose.Words.67669d70-b96a-449e-98d6-cae1079b3dba.031.png)

Así crearemos los diferentes Scenarios, donde también podremos realizar todas las comprobaciones que veamos conveniente.

La forma más sencilla de arrancar las pruebas es pulsando *Run* >> que se encuentra encima del apartado “Feature”, que nos mostrara por consola si se ha realizado con éxito o no. Encima de cada Scenario también nos encontramos un *Run >>*, este nos facilita el probar el Scenario en solitario, en vez de probar todos a la vez.
