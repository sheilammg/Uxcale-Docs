|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|26/05/2023|Axpe|Versión inicial|

# **Documentación técnica: Postman** 

## Índice
---
[1. Introducción](#introducción)

  - [1.1. ¿Qué es Postman](#que-es-postman)

  - [1.2. Características](#caracteristicas)

  - [1.3. Ventajas](#ventajas)

[ 2. Instalación](#instalacion)
  - [2.1. Versión web](#version-web)

  - [2.2. Aplicación de escritorio para Windows](#aplicacion-de-escritorio-para-windows)

  - [2.3. Aplicación de escritorio para Mac](#aplicacion-de-escritorio-para-mac)

  - [2.4. Aplicación de escritorio para Linux](#aplicacion-de-escritorio-para-linux)

[3. Casos de uso](#casos-de-uso)

<div id='introduccion' />

## 1. Introducción

<div id='que-es-postman' />

### 1.1. ¿Qué es Postman? 
Postman es una plataforma de API que permite crear APIs y también gestionar su uso de manera más sencilla y rápida. Postman te permite gestionar cada paso del ciclo de vida API, así como hacer pruebas y comprobar el correcto funcionamiento de las APIs. 

Inicialmente nació como una extensión del navegador Chrome de Google, pero actualmente ya existe como aplicación de escritorio con mayores funcionalidades de prueba, y dispone de herramientas nativas para diferentes sistemas operativos. 

Postman se puede utilizar de manera gratuita, aunque también ofrece versiones de pago más completas. 

<div id='caracteristicas' />

### 1.2. Características 
Postman es una herramienta que ofrece muchas ventajas y funcionalidades a la hora de gestionar el ciclo de vida API. Algunas de las más importantes son las siguientes: 

#### Integración con otras herramientas 

Postman puede integrarse con herramientas de desarrollo de software como Github, Jenkins, OpenAPI, etc. y también con AWS y Azure. 
#### Ofrece servicios de Gobierno de APIS

Esta función de Postman permite educar a los equipos de desarrolladores y comunicarles las reglas de diseño de API. También permite implementar la seguridad en una fase más temprana en el ciclo de vida API y ofrece pautas y políticas a los equipos para que implementen APIs más seguras. Postman también ofrece informes sobre las API y tableros que ayudan a identificar qué APIs no están documentadas, probadas o mantenidas, lo que mejora su gestión operativa y ayuda a comprender cómo usar los recursos del equipo de manera más efectiva. El resultado de todas estas funciones de Gobierno son APIs de mejor calidad y fomentar una mejor colaboración entre el equipo de desarrollo y el equipo de diseño de API. 
#### Ofrece espacios de trabajo

Postman ofrece diferentes espacios de trabajo para organizar el trabajo con las APIs y la colaboración, ya sea a nivel de organización o incluso a nivel público. Hay **espacios de trabajo personales**, para trabajo individual y centrado; **espacios de equipo** para colaborar en el trabajo API; **espacios de socios** que permiten a las organizaciones invitar a sus socios a trabajar en la creación de productos y servicios API y **espacios públicos**, que permiten compartir la API públicamente con todos los usuarios. 

#### Ofrece Repositorio de APIs

Postman ofrece un repositorio centralizado, basado en la nube y controlado por versiones para todos los productos API a lo largo de todo el ciclo de vida. Este repositorio garantiza una única fuente de información para las API. Con el repositorio, los equipos y organizaciones pueden recopilar métricas y discernir información gracias también al servicio de Gobierno de Postman. Con este repositorio se puede simplificar, organizar y escalar mejor todo el ciclo de vida de la API. El repositorio ofrece una Red API privada, para equipos, y también una Red Pública, siendo esta el centro de API público más grande del mundo. 
#### Otras herramientas

Todas las herramientas que ofrece Postman se conectan con el repositorio. Algunos ejemplos son:
- **API client**, que permite explorar, depurar y probar las APIs fácilmente y organizar las solicitudes en *Postman Collections* para su reutilización. 
- **Diseño de API**, que permite diseñar la especificación de la API usando OpenAPI, RAML, GraphQL o SOAP. 
- **Documentación de APIs**, que permite crear toda la documentación de las APIs. 
- **API testing**, que permite construir y ejecutar tests (integración, funcionales, regresión, etc.) directamente en Postman. 
- **Servidores Mock**, que te permiten saben cómo va a funcionar exactamente tu API antes de que se encuentra en producción.
- **Monitores**, que te ayudan a estar actualizado acerca de la salud y la actividad de las APIs.
- **Detección de APIs** con *Postman Interceptor* o *proxy de Postman*, que permiten capturar solicitudes y cookies del navegador de Postman para acelerar el fujo de trabajo.  

<div id='ventajas' />

### 1.3. Ventajas

En este apartado destacaremos algunas de las ventajas de utilizar Postman y también sus funcionalidades más utilizadas y destacables: 
- Tiene una interfaz muy sencilla e intuitiva de usar. 
- Puede integrarse con otras herramientas de desarrollo de software y permite sincronizar con varias aplicaciones. 
- Permite trabajar en espacios colaborativos para todo el equipo. 
- Permite trabajar con colecciones y mantenerlas actualizadas. 
- Permite testear colecciones y catálogos de APIs, tanto para backend como para frontend, automatizar y crear rutinas de pruebas. 
- Puede organizar en carpetas, funcionalidades y módulos los servicios web. 
- Permite gestionar el ciclo de vida de nuestra API (conceptualización y definición, desarrollo, monitoreo y mantenimiento). 
- Permite generar documentación de las APIs.
- Permite almacenar datos para su uso en otras pruebas. 
- Posee convertidor JSON en varios lenguajes. 

<div id='instalacion' />

## 2. Instalación 

<div id='version-web' />

### 2.1. Versión web 
Para utilizar la versión  web de Postman, no tenemos más que acudir a la [página oficial de Postman](https://web.postman.co/) y darle al botón de "Ejecutar Postman" o "Launch Postman". Una vez hecho esto, nos podremos registrar de forma gratuita con el correo para poder acceder a las funcionalidades de la versión web.  

![Postmanweb.png](../../../../assets/images/Postmanweb-2.png)


<div id='aplicacion-de-escritorio-para-windows' />

### 2.2. Aplicación de escritorio para Windows

La aplicación de escritorio se puede descargar en la [página de descargas de la web oficial de Postman.](https://www.postman.com/downloads/) 

![postmandesktop.png](../../../../assets/images/postmandesktop-2.png)

Una vez descargado, cuando se ejecuta la aplicación se abrirá la página de inicio de sesión. Ahí podremos crear una nueva cuenta gratuita o iniciar sesión en caso de que ya se esté registrado. Hecho esto, ya se podrá empezar a utilizar Postman de escritorio. 

![postmandesktop2.png](../../../../assets/images/postmandesktop2-2.png)


<div id='aplicacion-de-escritorio-para-mac' />

### 2.3. Aplicación de escritorio para Mac

En la propia [página de descargas de la web oficial de Postman](https://www.postman.com/downloads/) encontramos las opciones de descargar la herramienta para Mac y para Linux. En el caso de Mac, dependiendo de si el procesador es Intel o Apple, se elegirá la opción *Intel Chip* o *Apple Chip* y se procederá a la descarga. 

![postmandesktop4.png](../../../../assets/images/postmandesktop4-2.png)


El proceso es igual que en Windows. Una vez descargado, se abrirá el programa y nos saltarán dos avisos: uno para asegurar que queremos abrir una aplicación descargada de internet, y el segundo para moverlo a la carpeta de aplicaciones y aparecerá la página de inicio de sesión, igual que en windows. Una vez registrados o habiendo hecho *log in*, se podrá utilizar la herramienta. 

![postmandesktop3.png](../../../../assets/images/postmandesktop3-2.png)


### 2.4. Aplicación de escritorio para Linux

Tenemos tres posibles formas de instalar Postman para Linux: a través de Snap, Ubuntu Software o desde un archivo comprimido tar.gz. De todas maneras, hay que tener en cuenta que Postman es compatible con las siguientes distribuciones:
- Ubuntu (desde versión 14.04)
- Fedora 24
- Debian (desde versión 8)


**Descargar Postman con Snap**: habrá que acceder a la terminal y escribir el comando: 
>   sudo snap install postman 
Habrá que introducir la contraseña del usuario de Linux. A continuación se descargará el programa, y para abrirlo, se escribirá en la terminal: 
> postman 
Se abrirá la página de inicio que ya hemos visto con anterioridad. 

**Descargar Postman con Ubuntu Software**: Abrimos las aplicaciones de Ubuntu y buscamos Ubuntu Software. Abrimos el programa y una vez dentro, buscamos en la lupa el programa Postman. Pinchamos en el icono y se nos abrirá una nueva ventana. Al lado del icono de Postman, vendrá el botón de instalar. Una vez instalado, simplemente iremos a la lista de aplicaciones, buscaremos Postman y lo ejecutaremos.

![postmandesktop5.png](../../../../assets/images/postmandesktop5-2.png)


**Descargar Postman con tar.gz**: en la [página de descargas oficial de Postman](https://www.postman.com/downloads/) nos viene la opción de descargar para Linux: x64 o o arm64, la versión que sea más indicada en cada caso. Una vez descargado, pinchamos en el archivo con el botón derecho y hacemos click en "extraer aquí". Se creará una carpeta nueva que ya no estará comprimida y se podrá abrir con normalidad. Al abrir esta carpeta, se encontrarán dos archivos, siendo uno de ellos una carpeta llamada "app" y un archivo ejecutable del programa, llamado "Postman". Haga clic en el ejecutable "Postman" para ejecutar el programa. Al finalizar la instalación, aparecerá la misma página de inicio de sesión que en los casos anteriores.

![postmandesktop6.png](../../../../assets/images/postmandesktop6-2.png)

![postmandesktop7.png](../../../../assets/images/postmandesktop7-2.png)


## 3. Testing manual de APIs 
En el siguiente apartado se mostrará un ejemplo sobre cómo probar las APIs de forma manual con la herramienta de Postman.

Para ello, utilizaremos la API interna **Buscador de fondos y valores de Renta4.** Esta API nos permite buscar fondos de inversión y filtrar por multitud de campos para obtener los fondos que mejor se adaptan al cliente. 

En primer lugar, crearemos una **Collection** para nuestra API Buscador, para poder ir almacenando en dicha colección la lista de peticiones.

![postmanr41.png](../../../../assets/images/postmanr41-3.png)

En nuestro caso, hemos llamado Buscador a la colección, como se puede ver en la siguiente imagen. Dentro de la colección hay dos carpetas para separar los **fondos** de los **valores**. 

![postmanr42.png](../../../../assets/images/postmanr42-4.png)


### 3.1. Método HTTP POST

Siguiendo la especificación de la API, en primer lugar crearemos dentro de la colección tres peticiones POST. 
En la imagen se muestra como crear una petición dentro de una colección o de una carpeta (en este caso la carpeta de valores) de forma manual:

![postmanr44.png](../../../../assets/images/postmanr44-2.png)

En el caso de esta API de Búsqueda de Renta4, el método POST se utiliza como filtro complejo, para poder filtrar por multitud de campos los fondos de inversión o los valores. 
En este caso nos fijaremos en la request **POST /valores/avanzado**, que nos permite realizar una búsqueda avanzada de los valores disponibles en los canales digitales de Renta4. 

![postmanr45.png](../../../../assets/images/postmanr45-2.png)

Si nos fijamos en el **Body**, se pasará un formato JSON con los filtros que se quieran aplicar para la búsqueda. Al enviar la request pulsando SEND (botón azul, derecha) obtenemos un único elemento con los campos isin y nombLargo, ya que se ha filtrado por el número de isin, mercado y tipo de producto, y se ha indicado que únicamente se muestren esas dos columnas. En la respuesta podemos ver el Status 200 OK, o también podríamos obtener un 201, Created. 

### 3.2. Método HTTP GET
Para el método GET, el procedimiento será el mismo que para el POST, en el caso anterior. En la API de Búsqueda de R4 nos encontramos primero el POST y luego el GET, por eso hemos de seguir este orden en Postman. 
Creamos de forma manual la petición GET y nos aparecerá como se muestra en la imagen: 

![postmanr49.png](../../../../assets/images/postmanr49-2.png)


![postmanr411.png](../../../../assets/images/postmanr411-3.png)

En este caso tenemos dos métodos GET. El de la primera imagen (valores/opciones/tipos/) nos devuelve los tipos de opciones, y el de la segunda (valores/opciones/{codTipo}/valores) nos devolvería los valores asociados a un tipo de opción concreta. En ambos casos al lanzar la petición nos devuelve un listado, y el Status de la respuesta es un 200 Ok. 

### 3.4. Método HTTP PUT

Para mostrar los siguientes métodos HTTP (PUT, PATCH Y DELETE) utilizaremos una API diferente, ya que estos métodos no se encuentran en la mayoría de las APIs de Renta4. Para ello hemos utilizado la **API de Postman**, que es una API que nos permite acceder a los datos almacenados en nuestro workspace de Postman. 

El método PUT sirve para actualizar al completo la información de un recurso, en este caso de una de nuestras colecciones del workspace. La petición PUT se crea del mismo modo que que el POST o el GET. Una vez creada la petición dentro de la colección, necesitamos el **valor Id del recurso** que queremos actualizar. Para obtener dicho valor, primero haremos un GET de todas nuestras colecciones:

![postman429.png](../../../../assets/images/postman429-2.png)

En este caso cogeremos el id de la segunda colección que aparece, cuyo nombre es BuscadorTres. Vamos a actualizar el nombre a BuscadorCuatro con el método PUT:

![postman430.png](../../../../assets/images/postman430-2.png)

Como podemos ver en la imagen, arriba en los Path Params tenemos puesta una variable llamada **collection Id**, que contiene el valor de la colección que queremos modificar. En el Body también tenemos dos variables definidas: **collection Name** y **collectionSchemaUrl**. Esta última variable contiene todo el esquema del recurso, para no tener que introducir cada valor manualmente.
En la respuesta se puede ver que hemos utilizado el PUT para modificar el nombre de la colección, que se ha actualizado a Buscador Cuatro. El status de la respuesta es un 200 Ok y nos devuelve el recurso actualizado. 

Los valores de estas variables se podrían introducir de forma manual en cada método, aunque en este caso lo que hemos hecho ha sido crear un environment llamado POSTMAN API ENV, en el cuál vamos actualizando el valor de nuestras variables cuando sea necesario. Para trabajar dentro de este environment, debemos seleccionarlo arriba a la derecha. 

![postman431.png](../../../../assets/images/postman431-2.png)

En la imagen se puede ver que hemos modificado el valor de collectionId con el valor de la colección que queríamos modificar. También se ve cómo hemos cambiado el nombre de collectionName a BuscadorCuatro. Le damos a guardar y de esta manera, cuando hagamos el PUT, los valores que introduzcamos en el Body y que hayamos guardado en las variables, se actualizarán, como hemos visto. 

### 3.5. Método HTTP PATCH

Para crear el método PATCH el procedimiento es el mismo que para el método PUT. Este método nos va a permitir actualizar el recurso parcialmente.
De nuevo, modificaremos el valor de las variables que queramos modificar. Vamos a utilizar el mismo valor id que para el PUT. Esta vez vamos a modificar el nombre de la colección y también actualizaremos la descripción de la misma:

![postmanr432.png](../../../../assets/images/postmanr432-2.png)

En la imagen podemos ver el Body de la Request, en el que introduciremos en formato JSON los campos que queremos modificar, en este caso, el nombre del cliente y la descripción. Ambas son variables, lo que significa que las vamos a modificar a nivel de environment:

![postmanr433.png](../../../../assets/images/postmanr433-2.png)

Al enviar la petición, obtenemos un código de estado 200 Ok y nos devuelve el recurso modificado. También podemos obtener una respuesta 204 No Content, dependiendo de cómo esté definida la API. 

### 3.6. Método HTTP DELETE

Para el método HTTP Delete utilizaremos la misma API. El procedimiento es el mismo de los métodos anteriores. En este caso no es necesario ningún Body, sólo tendremos que cambiar el valor de la variable **collectionId** en el environment para asegurarnos de que eliminamos la colección que queremos. 

![postmanr434.png](../../../../assets/images/postmanr434-2.png)

De nuevo el Status de la respuesta nos devolverá un código 200, aunque lo normal es que devuelva un 204 No Content. Esto significa que el recurso se ha eliminado con éxito. 

### 3.6. Cabeceras y autorización  

Según la especificación de la API, para ejecutar algunos métodos HTTP, o incluso todos, será necesaria una autorización. En caso de que sea necesaria dicha autorización, la información necesaria se enviará, normalmente, a través de las cabeceras.   

![postmanr413.png](../../../../assets/images/postmanr413-3.png)

Dentro de cualquier método HTTP, como en este caso el POST /valores/avanzado, podemos ver las cabeceras para dicho método tal y como se muestra en la imagen. Las primeras 8 cabeceras en este caso han sido generadas automáticamente por Postman (este tipo de cabeceras normalmente aparecen ocultas). 

La última cabecera es la de autenticazión. Se pueden definir diferentes métodos de autenticazión, pero en nuestro ejemplo tenemos una seguridad tipo Bearer token, tal y como se ve en la imagen. Además, el token está dentro de la variable {{access_token}}. 
Será necesario añadir esta cabecera en todos los métodos HTTP que requieran este tipo de autorización con token. En caso de no introducir el token o de que haya caducado, la respuesta nos devolverá un error 401. 

Como se ha mencionado, el valor del token se puede **guardar dentro de una variable**, en nuestro caso llamada access_token. Si definimos esta variable a nivel de la colección Buscador, el valor del token se guardará automáticamente para todas las requests que hayamos creado y en las que esté definida la cabecera de Authorization. Si queremos modificar o cambiar el token, sólo tenemos que hacerlo a nivel de la variable en Buscador, en lugar de cambiarlo manualmente en todas las requests. 

![postmanr412.png](../../../../assets/images/postmanr412-2.png)

### 3.7. Pre-Request Script 
Para cada request creada, Postman nos ofrece la posibilidad de validar los parámetros de entrada. Para esto utilizamos el Pre-Request Script dentro de cada método HTTP. 
Esta opción nos permite definir tests para validar parámetros **antes de lanzar la petición**. Es decir, con el Pre-Request Script podemos validar el Request Body, las cabeceras, etc. 

![postmanr48.png](../../../../assets/images/postmanr48-2.png)

En la imagen se pueden ver algunos tests, por ejemplo, para validar el schema del Request Body o para asegurar que la cabecera Content-Type se encuentra presente en la petición.

### 3.8. Tests 
Postman también nos permite definir todo tipo de tests para validar nuestras requests: 

![postmanr47.png](../../../../assets/images/postmanr47-2.png)

Dentro de la pestaña de Test, podemos definir en Javascript todo tipo de tests, desde tests unitarios más simples, hasta tests funcionales o de rendimiento. Con este tipo de tests normalmente validaremos las respuestas de la petición, es decir, después de lanzar la request, a diferencia del Pre-Request Script, que sirve para validar los parámetros antes de haber lanzado la petición. 

En la imagen vemos ejemplos de **test unitarios** que se han creado para la respuesta (en orden de aparición): 
- Para confirmar que el código de respuesta es un 200.
- Para confirmar que el código de respuesta es un Ok.
- Para confirmar que la respuesta tiene un Body.
- Para confirmar que el Body de la respuesta tiene un formato JSON.
Una vez definidos los test unitarios, al lanzar la petición nos fijaremos en la pestaña de Test Results, para ver si la API ha pasado todos nuestros tests. En la imagen se puede ver que efectivamente, se cumple que la respuesta para esta petición es un 200 Ok, con un Body en formato JSON. 

- AÑADIR MÁS EJEMPLOS DE PRUEBAS UNITARIAS Y FUNCIONALES

En cuanto a las **pruebas de rendimiento**, no se realizarán con la herramienta Postman sino con Jmeter, por lo que dichos tests se describirán en el documento correspondiente (REFERENCIAR). 

## 4. Testing automático de APIs

En el apartado anterior hemos visto cómo probar una API de forma manual. Sin embargo, Postman también ofrece la ventaja de realizar este proceso de forma automática, de manera que si se producen cambios en la API, no tendremos que crear de cero todo el flujo de trabajo de testing. En lugar de introducir manualmente los tests en cada request, podemos recurrir a la automatización con el **Collection Runner**, que nos permite ejecutar la colección completa. 

Si pinchamos abajo a la derecha, en el botón de "Runner", se nos abrirá en Postman la pestaña correspondiente. También se puede acceder a esta opción directamente desde la colección, tal y como se muestra a continuación: 

![postmanr415.png](../../../../assets/images/postmanr415-3.png)

Una vez hecho esto, se nos abrirá la colección en la ventana del Runner, de manera que podremos ver en qué orden se van a ejecutar las peticiones. También podremos activar o desactivar las peticiones que nos interesen. 

![postmanr416.png](../../../../assets/images/postmanr416-2.png)

![postmanr416.5.png](../../../../assets/images/postmanr416-2.5.png)

En este caso vamos a ejecutar la carpeta de **valores**, que es con la que hemos estado trabajando. Por ello, deseleccionamos las peticiones de **fondos**. Si pinchamos en Run Buscador, se ejecutará toda la carpeta de valores: 

![postmanr421.png](../../../../assets/images/postmanr421-2.png)

![postmanr422.png](../../../../assets/images/postmanr422-2.png)

En la imagen podemos ver que Postman nos devuelve todos los resultados de las peticiones, de manera que podemos ver todos los tests que se han pasado con éxito y también los que se han fallado, petición a petición. También nos ofrece una visualización resumen, si pinchamos en la derecha:

![postmanr423.png](../../../../assets/images/postmanr423-2.png)

Otra forma de automatizar con Postman es a través de los **Monitores**. Podemos crear un monitor para nuestra colección, de manera que no tenemos que estar pendientes de iniciar las pruebas manualmente. En el monitor podemos establecer cuándo y cuántas veces queremos ejecutar la colección, de manera que Postman lo hará automáticamente, sin que nosotros tengamos que pinchar en el botón de "Run". 

En nuestro caso hemos creado una nueva colección únicamente con la carpeta de **valores** para poder crear un monitor sólo para estas peticiones: 

![postman427.png](../../../../assets/images/postman427-2.png)

En la imagen se muestran los pasos para crear un Monitor para nuestra colección de Valores de Renta4. Según los parámetros que hemos introducido, esta API se ejecutará todos los días a las 8:00 AM. Postman notifica automáticamente por correo electrónico si algo ha fallado en los tests. También se puede ejecutar de forma manual en el momento, con el botón de "Run": 

![postman428.png](../../../../assets/images/postman428-2.png)

![postmanr450.png](../../../../assets/images/postmanr450.png)


### 4.1. Automatización con Newman 
Newman es una de las herramientas más útiles a la hora de automatizar los tests de colecciones. Newman nos permite ejecutar colecciones con línea de comandos y además, genera al final un informe con todos los datos de las pruebas. Además, Newman se puede integrar con servidores de integración continua (CI) y sistemas de compilación. 

Para poder utilizar Newman de forma local en el ordenador, primero tenemos que instalar [Node.js](https://nodejs.org/es/download). Una vez que tenemos instalado Node.js, abrimos la terminal y escribimos el siguiente comando para instalar Newman:

> npm install -g newman

![newman1.png](../../../../assets/images/newman1-2.png)

A continuación, para ver si se ha instalado correctamente, podemos escribir el comando: 

> newman --version

Una vez confirmado que tenemos Newman correctamente instalado, pasamos a ejecutar nuestra colección. En este caso, usaremos de nuevo la colección de **Postman API**. Para ello, primero tenemos que exportar nuestra colección de Postman como un archivo JSON, la versión v2.1 (recomendada):

![newman2.png](../../../../assets/images/newman2-3.png)

Una vez exportada la colección, nos movemos a la carpeta correspondiente en la terminal de Node.js (usando el comando cd) y ejecutamos la colección con el siguiente comando:
> newman run *"nombre del archivo.json"*

![newman5.png](../../../../assets/images/newman5-3.png)

En nuestro caso nos hemos movido a Downloads y una vez ahí hemos ejectuado la colección *ejemplo_API.postman_collection.json*. 

![newman6.png](../../../../assets/images/newman6-2.png)

Newman ofrece la posibilidad de generar informes, como el informe HTML, que resultará muy útil a la hora de avergiuar qué tests han fallado y por qué, ya que contiene una gran cantidad de información. 
Para instalar el generador de informes, utilizaremos el siguiente comando: 
> npm install -g newman-reporter-htmlextra

![newman4.png](../../../../assets/images/newman4-2.png)

Una vez instalado, el comando para generar el informe HTML de una colección es el siguiente:

> newman run *"nombre del archivo".json* -r htmlextra

![newman11.png](../../../../assets/images/newman11-2.png)

El informe se genera dentro de la carpeta donde se encuentra el archivo de nuestra colección, en una nueva carpeta llamada **newman**. En este caso, la carpeta se ha generado dentro de "Descargas": 

![newman7.png](../../../../assets/images/newman7-2.png)

El informe nos ofrece una visión general de las peticiones, las respuestas, y todo lo que ha pasado al ejecutar nuestra colección. Podemos ver un resumen general, el total de los tests ejecutados, los tests que se han pasado con éxito, los que han fallado y los que no se han ejecutado:

![newman8.png](../../../../assets/images/newman8-2.png)

![newman9.png](../../../../assets/images/newman9-2.png)

![newman10.png](../../../../assets/images/newman10-2.png)

Este informe HTML es un documento muy completo que también nos permite ver con detalle qué ha sucedido al lanzar cada petición, y por lo tanto resulta una herramienta muy útil. 


