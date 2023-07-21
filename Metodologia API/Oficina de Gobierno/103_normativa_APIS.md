
# Normativa APIs v0.0

Índice
<!-- TOC -->

- [Normativa APIs v0.0](#normativa-apis-v00)
    - [1. Introducción](#1-introducci%C3%B3n)
    - [2. Definición de la Estructura de las reglas](#2-definici%C3%B3n-de-la-estructura-de-las-reglas)
    - [3. Prerrequisitos de validación](#3-prerrequisitos-de-validaci%C3%B3n)
    - [4. Normativa /Reglas](#4-normativa-reglas)
        - [4.1. Sección GENERAL](#41-secci%C3%B3n-general)
            - [4.1.1. Subsección GENERAL](#411-subsecci%C3%B3n-general)
        - [4.2. Sección INFO](#42-secci%C3%B3n-info)
            - [4.2.1. Subsección INFO](#421-subsecci%C3%B3n-info)
        - [4.3. Sección BASEPATH](#43-secci%C3%B3n-basepath)
            - [4.3.1. Subsección BASEPATH](#431-subsecci%C3%B3n-basepath)
        - [4.4. Sección PATHS](#44-secci%C3%B3n-paths)
            - [4.4.1. Subsección PATHS](#441-subsecci%C3%B3n-paths)
            - [4.4.2. Subsección PARAMETERS](#442-subsecci%C3%B3n-parameters)

<!-- /TOC -->



## 1. Introducción

Este documento tiene como objetivo recopilar el conjunto de reglas, de obligado cumplimiento, que aplica a todas las APIs que se desarrollen para Axpe Consulting.

Dado que una API se establece como un elemento atómico  y no divisible para su utilización, la modificación de alguna de las partes de una API existente o creación de nueva API, implicará que la API completa cumpla con la normativa vigente indicada en este documento.

## 2. Definición de la Estructura de las reglas

Para facilitar el entendimiento y localización de las reglas, cada una de ellas tiene sintaxis que nos indica código de referencia. 

Este código se compone de la siguiente secciones:

- **G**-X-XXX-XXX. La primera sección corresponde con el nombre de la sección del yaml a la que hace referecia la regla.

  Sección  | Referencia|
  ---------|-----------|
  General  | G         |
  Info     | I         |
  BasePath | B         |
  Paths    | P         |
- X-**1**-XXX-XXX La siguiente sección corresponde con la severidad de la regla:


  Severidad     | Valor   |
  --------------|---------|
  Crítica       | 1       |
  Leve          | 2       |
  Recomendación | 3       |
 
- X-X-**GEN**-XXX La tercera sección se corresponden con el nombre de la subsección del yaml a la que hace referencia la regla. 
  Subsección    | Valor   |
  --------------|---------|
  General       | GEN     |
  Info          | INF     |
  BasePath      | BAS     |
  Paths         | PAT     |
  Parameters    | PAR     |

- X-X-XXX-**001** La última sección corresponden con un número ordinal, unico que identificará la regla que este fallando asignado dentro de la sección o subsección de la regla.

## 3. Prerrequisitos de validación

Antes de comenzar con la validación de la especificación API, la Oficina de Gobierno comprobará que se cumplen el requisito principal; La herramienta validador debe devolver **0 erores**. Si no se cumple este prerrequisito, no se iniciadara la validación y verificación por parte de la Oficina de Gobierno. 

| Código          | Descripción   | Ejemplo   | Información adicional | Spectral |
| --------------- | ------------- | --------- | --------------------- | -------- |
|P-1-PRE-001  | El resultado del validador debe ser 0 errores. |  | Modelo de participación OGA | 

## 4. Normativa / Reglas

En este apartado se detalla cada una de las reglas que compone la Normativa de APIs para Axpe Consulting.

### 4.1. Sección GENERAL

#### 4.1.1. Subsección GENERAL

| Código          | Descripción   | Ejemplo   | Información adicional | Spectral |
| --------------- | ------------- | --------- | --------------------- | -------- |
| *G-1-GEN-001*   | El nombre del fichero debe ser openapi. | openapi.yaml | [Guia de diseño](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md)|  TBD|
| *G-1-GEN-002*   | El nombre del fichero debe estar formado en minúsculas. | openapi.yaml | [Guia de diseño](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md) | TBD|
| *G-1-GEN-003*   | La extensión del fichero debe ser .yaml | openapi.yaml | [Guia de diseño](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md) | TBD|
| *G-1-GEN-004*   | En caso de extender la especificación, los atributos añadidos deben comenzar con “X-”. | X-Request-Id | [Guia de diseño](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md) | TBD|
| *G-1-GEN-005*   | La versión indicada en el campo openapi debe ser 3.0.0 o superior. | openapi: 3.0.1 | [Guia de diseño](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md) | TBD|

### 4.2. Sección INFO

#### 4.2.1. Subsección INFO

| Código          | Descripción   | Ejemplo   | Información adicional | Spectral |
| --------------- | ------------- | --------- | --------------------- | -------- |
| *I-1-INF-001* | El campo title es obligatorio. | title: Sales Product  | [Guia de diseño: 3.1 Estructura del documento.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#31-estructura-del-documento) |TBD
| *I-1-INF-002* | El campo title debe empezar por mayúscula y debe contener un espacio entre cada palabra, en caso de existir varias palabras. | title: Sales Product  | [Guia de diseño: 3.6. Estructura Objetos definidos.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#36-estructura-objetos-definidos) |TBD| 
| *I-1-INF-003* | El campo title debe estar cumplimentado en inglés. | title: Sales Product  | [Guia de diseño: 3.3. Idioma.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#33-idioma) |TBD| 
| *I-1-INF-004* | El campo version es obligatorio. | version: 1.0.0 | [Guia de diseño: 3.7 Versionado.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#37-versionado) |TBD| 
| *I-1-INF-005* | La versión indicada en el campo version debe seguir un estilo de versionado semántico, con el formato: [MAJOR].[MINOR].[PATCH]. | version: 1.0.0 | [Guia de diseño: 3.7 Versionado.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#37-versionado) |TBD| 
| *I-1-INF-006* | La primera versión indicada en el campo version debe ser la 1.0.0. | version: 1.0.0 | [Guia de diseño: 3.7 Versionado.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#37-versionado) |TBD| 
| *I-1-INF-007* | Debe subirse versión siempre que exista una modificación en el documento. | version: 1.0.1 | [Guia de diseño: 3.7 Versionado.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#37-versionado) |TBD| 
| *I-1-INF-008* | En el campo version se incrementará [PATCH] cuando se trate de corrección de errores (bugs) sobre la versión actual. | version: 1.0.1 | [Guia de diseño: 3.7 Versionado.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#37-versionado) |TBD| 
| *I-1-INF-009* | En el campo version se incrementará [MINOR] cuando el evolutivo incluya cambios compatibles con la versión actual. | version: 1.1.0 | [Guia de diseño: 3.7 Versionado.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#37-versionado) |TBD| 
| *I-1-INF-010* | En el campo version se incrementará [MAJOR] cuando el evolutivo incluya cambios incompatibles con la versión actual | version: 2.0.0 | [Guia de diseño: 3.7 Versionado.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#37-versionado) |TBD| 
| *I-1-INF-011* | El campo description es obligatorio. | description: This API Capture, track, resolve and report on card related transactional disputes, handling all the dispute resolution messages between the Issuer, the Card Network and the Acquirer. | -- |
| *I-1-INF-012* | El campo description debe estar cumplimentado en inglés. | description: This API Capture, track, resolve and report on card related transactional disputes, handling all the dispute resolution messages between the Issuer, the Card Network and the Acquirer. | [Guia de diseño: 3.3. Idioma.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#33-idioma) |TBD| 
| *I-1-INF-013* | El objecto contact.name es obligatorio definirlo en la especificación API. | contact.name: CoE Apificación	 | -- |TBD| 
| *I-1-INF-014* | El campo contact.name debe contener el nombre y apellidos del API Owner . | contact.name: CoE Apificación | -- |TBD| 
| *I-1-INF-015* | El campo contact.email es obligatorio. | contact.email: tecnologia@xpe.com | -- |TBD| 
| *I-1-INF-016* | El campo contact.email debe contener el correo electrónico del API Owner. | contact.email: tecnologia@axpe.com | -- |TBD| 

### 4.3. Sección BASEPATH

#### 4.3.1. Subsección BASEPATH

| Código          | Descripción   | Ejemplo   | Información adicional | Spectral |
| --------------- | ------------- | --------- | --------------------- | -------- |
| *B-1-BAS-001*   | La url completa de un recurso se debe componer de la siguiente manera: <br> URI = scheme ": //" BaseURI "/" BasePath [ "?" query ] [ "#" fragment ] | *https://api.axpe.com/users/{userId}/adresses/{adressId}* |  [Guia de diseño: 4.2. Partes de la URL.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#42-partes-de-la-url) | TBD |
| *B-1-BAS-002* | La url completa de un recurso debe escribirse en minúsculas. | https://api.axpe.com/users/{userId}/adresses/{adressId} | [Guia de diseño: 4.2. Partes de la URL.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#42-partes-de-la-url)  | TBD |
| *B-1-BAS-003* | La url completa de un recurso debe contener el protocolo sobre el que se trabaja. Utilizaremos siempre HTTPS. | **https**://api.axpe.com/users/{userId}/adresses/{adressId} | [Guia de diseño: 4.2. Partes de la URL.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#42-partes-de-la-url)  | TBD |
| *B-1-BAS-004* | La url completa de un recurso debe contener el dominio o nombre de máquina. Se definirá a nivel de servidor. | http://**api.axpe.com**/users/{userId}/adresses/{adressId} | [Guia de diseño: 4.2. Partes de la URL.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#42-partes-de-la-url)  | TBD |
| *B-1-BAS-005* | La url completa de un recurso debe contener el nombre de la API (contexto). | http://api.axpe.com/**users**/{userId}/adresses/{adressId} | [Guia de diseño: 4.2. Partes de la URL.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#42-partes-de-la-url)   | TBD |
| *B-1-BAS-006* | La url completa de un recurso debe contener la MAJOR version. |http://api.axpe.com/users/**v1**/{userId}/adresses/{adressId} | [Guia de diseño: 4.2. Partes de la URL.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#42-partes-de-la-url)   | TBD |
| *B-1-BAS-007* | La url completa de un recurso debe contener el recurso específico al que se quiere acceder.  |http://api.axpe.com/users/v1/{userId}/**adresses**/{adressId} | [Guia de diseño: 4.2. Partes de la URL.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#42-partes-de-la-url)   | TBD |
| *B-1-BAS-008* | La url completa de un recurso puede contener path param, para identificar el recurso que le precede.  |http://api.axpe.com/users/v1/**{userId}**/adresses/{adressId} | [Guia de diseño: 4.2. Partes de la URL.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#42-partes-de-la-url)   | TBD |
| *B-1-BAS-009* | La url de un recurso puede contener query params, como parámetros de filtrado del recurso. Los query params se colocan inmediatamente después del recurso al que hacen referencia, y van precedidos del simbolo "?", pudiendo concatenar tantos como se hayan definido con "&".|http://api.axpe.com/users/v1/{userId}/adresses/{adressId}**?country=spain** | [Guia de diseño: 4.2. Partes de la URL.](../Guia%20de%20Dise%C3%B1o/100_dise%C3%B1o_de_api.md#42-partes-de-la-url)   | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |

### 4.4. Sección PATHS

#### 4.4.1. Subsección PATHS

| Código          | Descripción   | Ejemplo   | Información adicional | Spectral |
| --------------- | ------------- | --------- | --------------------- | -------- |
| *P-1-PAT-001* | Los nombres de los recursos deben estar alineados con las necesidades que requieren la parte de negocio. | /sales-products | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |

#### 4.4.2. Subsección PARAMETERS

| Código          | Descripción   | Ejemplo   | Información adicional | Spectral |
| --------------- | ------------- | --------- | --------------------- | -------- |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
| --------------- | ------------- | --------- | --------------------- | TBD |
