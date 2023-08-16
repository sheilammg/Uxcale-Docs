|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|11/04/2023|Axpe|Versión inicial|

# **Guía de uso Karate**

## Índice
---
[1. Introducción](#introducción)

[2. Karate en Eclipse con Spring Boot](#karate-eclipse-spring-boot)

[3. Karate en Visual Studio Code](#karate-visual-studio-code)

[4. Karate stand-alone](#karate-stand-alone)

<div id='introduccion'/>

## 1. Introducción
En este documento se detalle los pasos a realizar para realizar las diferentes pruebas con Karate. Karate es una herramienta Open-Source que combina automatización de pruebas de API, simulacros, pruebas de rendimiento e incluso automatización de la interfaz de usuario en un solo marco unificado.

Existen tres formas para poder utilizar esta herramienta y así poder realizar las diferentes pruebas que implementaremos.


<div id='karate-eclipse-spring-boot'/>

## 2. Karate en Eclipse con Spring Boot
Para la integración con SpringBoot, nos serviremos de la herramienta de gestión de proyectos Maven. En el .pom de nuestro proyecto, añadiremos la siguiente dependecia:

![Aspose.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.002.png](../../../../assets/images/Aspose-2.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.002.png)

Una vez añadida la dependencia, instalaremos el plugin de Cucumber en nuestro IDE de Eclipse. Podremos hacer esto fácilmente mediante la Eclipse Marketplace.

![Aspose.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.003.png](../../../../assets/images/Aspose-2.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.003.png)

Tras haber instalado el plugin correctamente, crearemos nuestro fichero de testing “.feature” donde se introducirán los diferentes escenarios que queremos probar.

Para ejecutarlo y arrancar el fichero definido, simplemente tendremos que seleccionar "Run As" en las opciones de ejecución y elegir "Cucumber Feature".

![Aspose.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.004.png](../../../../assets/images/Aspose-2.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.004.png)

<div id='karate-visual-studio-code'/>

## 3. Karate en Visual Studio Code
La herramienta Visual Studio Code, cuenta con una extensión oficial de “Karate”. Su instalación, se realiza al igual que el resto de las extensiones de Visual Studio Code. Primeramente, nos dirigimos a la pestaña de extensiones en nuestro IDE o podemos pulsar Ctrl + Shift + X.

![Aspose.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.005.png](../../../../assets/images/Aspose-2.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.005.png)

Una vez ahí, buscamos “Karate” y seleccionamos la primera opción. Es importante asegurase de que instalamos correctamente el plugin oficial, desarrollado por Karate Labs.

![Aspose.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.006.png](../../../../assets/images/Aspose-2.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.006.png)

Una vez instalado, ya podemos crear nuestro fichero .feature para empezar a desarrollar nuestros test. Un aspectos destacable de la integración con Visual Studio Code, es que nos permitirá ejecutar todos los test del documento a la vez o uno a uno, además de generar la salida en la consola, donde nos mostrara diferentest logs, junto con el link al reporte en formato HTML.

![Aspose.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.007.png](../../../../assets/images/Aspose-2.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.007.png)

<div id='karate-stand-alone'/>

## 4. Karate en stand-alone
También existe la opción de ejecutar Karate directamente desde línea de comandos. Para ello, descargaremos el archivo *.jar* de la [página oficial de Karate](https://github.com/karatelabs/karate/releases), en el apartado de Assets.

Los requisitos de instalación son muy simples: tener instalado Java (Java 11 mínimo) y alrededor de 60 MB libres en disco. Al ser un archivo *.jar*, es compatible con cualquier sistema operativo.

Una vez descargado, solo tendremos que ejecutar las diferentes operaciones desde nuestro terminal. Por ejemplo, desde el terminal, para lanzar un test usaremos el siguiente comando: 

![Aspose.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.008.png](../../../../assets/images/Aspose-2.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.008.png)

Este comando seria para arrancar todos los escenarios implementados, pero si queremos solo probar un escenario tendríamos que usar el siguiente comando, donde definimos el escenario que queremos:

![Aspose.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.009.png](../../../../assets/images/Aspose-2.Words.f88d5154-62d2-48d8-80eb-9df046f586d8.009.png)

Esta herramienta nos permitirá realizar muchas otras acciones, como iniciar un servidor mock, cambiar entre diferentes entornos, ejecutar varios features de manera paralela, generar diferentes tipos de salidas...

Esta seria la forma más sencilla de arrancar las diferentes pruebas implementadas en el .feature, pero podemos encontrar más funcionalidades en el apartado **standalone** de la  [página oficial de Karate](https://github.com/karatelabs/karate/tree/master/karate-netty#standalone-jar).
