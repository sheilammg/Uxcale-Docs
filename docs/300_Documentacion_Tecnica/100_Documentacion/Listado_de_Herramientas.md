|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|12/02/2023|Axpe|Versión inicial|


# **Listado de Herramientas** 

## Índice
---
[1. Introducción](#introducción)

[2. Ventajas y desventajas de las diferentes herramientas](#ventajas-desventajas)

  - [2.1. Stoplight Studio 3](#stoplight-studio)
  - [2.2. Visual Studio Code 4](#visual-studio-code)
  - [2.3. Insomnia 4](#insomnia)
  - [2.4. Swagger Editor 5](#swagger)

<div id='introduccion'/>

## 1. Introducción

Este documento se realiza con el objetivo de mostrar las diferentes herramientas que se pueden utilizar en el proceso de desarrollo de APIs y microservicios.

<div id='ventajas-desventajas'/>

## 2. Ventajas y desventajas de las diferentes herramientas


<div id='stoplight-studio'/>

### 2.1. Stoplight Studio 3 
|**IDE Stopligth Studio**|**Ventajas**|**Desventajas**|
| :-: | :-: | :-: |
||Buena visualización de los elementos de la especificación API.||
||Permite generar el diseño de una API desde un formulario.||
||Permite de manera sencilla la integración con spectral.||
||Permite definir o modificar reglas de Spectral en la propia herramienta.||
||Genera informe de error de la especificación, indicando la ubicación y una descripción del problema.||
||Buena documentación para el manejo de la herramienta.||
||Buena documentación para el manejo de Spectral dentro de la herramienta.||
||Permite generar mocks.||

<div id='visual-studio-code'/>

### 2.2. Visual Studio Code 4 

|**Visual Studio Code**|**Ventajas**|**Desventajas**|
| :-: | :-: | :-: |
||Permite la instalación de OpenAPI con un plugin.|Es necesario la instalación de diferentes plugin, para aumentar la funcionalidad de la herramienta.|
||Permite la instalación de Spectral con un plugin.|Visualización poco intuitiva y desordenada de los diferentes elementos de una especificación API.|
||Genera informe de error de la especificación, indicando la ubicación y una descripción del problema.|Da problemas la integración con Spectral dado que se queda bloqueado en sucesivas ocasiones.|

<div id='insomnia'/>

### 2.3. Insomnia 4

|**Insomnia**|**Ventajas**|**Desventajas**|
| :-: | :-: | :-: |
||Buena visualización de los elementos de la especificación API|No permite trabajar dentro de la herramienta con spectral.|
||Permite usar un .spectral personalizado añadiéndolo al repositorio raíz del git.|No permite generar mocks.|
||Genera informe de error de la especificación, indicando la ubicación y una descripción del problema.||
||Permite generar solicitudes y respuestas de depuración en la propia herramienta.||
||Permite probar las APIs mediante test.||

<div id='swagger'/>

### 2.4. Swagger Editor 5


|**Swagger Editor**|**Ventajas** |**Desventajas**|
| :- | :- | :- |
||Buena visualización de los elementos de la especificación API.|No permite incluir reglas de spectral personalizadas.|
||Genera informe de error de la especificación, indicando la ubicación y una descripción del problema.|No permite generar mocks.|
