# **Metodología y Responsabilidades de los Equipos y Roles en el ciclo de vida de las APIs**

## Índice

---

En este documento se especifica las funciones, responsabilidades y roles de los equipos participantes  de los procesos que se realizan en cada una de las fase del ciclo de vida API.

## 1. Fase de Diseño

Esta fase se compone de las estapas de: planificación e identificación de la API, diseño y validación de la interfaz.

### 1.1. Planificación e Identificación

El objetio de esta fase es analizar las necesidades de negocio de la organización para identificar un conjunto de APIs que aporten valor. Esto generará un listado de **APIs candidatas o objetivo** a definir, implementar, publicar, evolución y gestion en el catálogo de servicios API de laorganización.

Un primer paso, analizar las funcinalidades del proyecto, ver las necesidades y realizar una estimación a alto nivel. Para iniciar esta fase el equipo de proyecto tendrá que realizar una petición, para ello utilizaremos la herramienta de **jira/trello** para gestionar la peticion. En la tarea el equipo de proyecto tendrá que indicar la necesidad de negocio y adjuntar la documentación necesaria asociada a los requerimientos. Como objetivo, el equipo de la Oficina de Gobierno offrecera una *plantilla HLE* que se definirán un listado de APIs a alto nivel que aporte valor 

**Recursos**

- _**Plantilla HLE**_: Excel que se utiliza como [plantilla](./_resources/Plantilla-base-HLE.xlsx) para determinar una estimación de alto nivel.

**Participantes:**

Equipo                         | Rol               | Responsabilidad
------------------------------ | ----------------- | ---------------
Oficina de Gobierno            |                   | Garantizar soporte al equipo de desarrolo para dar analizar requisitos funcionales requeridos, intermediar entre las partes afectadas, y gestionar e identifar las nuevas APIs como su evolución. Encargado de revisión y validación, gestionar la catalogación de APIs y mantenimiento de las APIs.
Equipo de Proyecto (API Owner) | API Owner         | Responsable de iniciar y gestionar los trámites necesarios para el identificación, análisis, creación o evolución de la API requeridas para la funcionalidad requerida.
Equipo funcional del Negocio   |                   | Equipo responsable de analizar e identificarán las nuevas funcionaliades del negocio. El objetivo es recopilar un lista de APIs que tenga valor a nuestra compañia. Son responsables de dar soporte y aportar el conocimiento funcional necesario para identificar y clasificar las APIs.


### 1.2. Diseño y validación de la definición

El objetivo es definir y validar la especificación API identificadas: la interfaz de los recursos, identificando y definiendo el tipo operaciones, la estructura del cuerpo del mensaje de la solicitud y respuesta, formatos y códigos HTTP, etc. Buscando cubrir la funcionalidad definida.

El procedimiento consta de las siguientes pasos:
- Comunicación y solicitud para la clasificación de las APIs identificas dentro de la compañia.
- Almacenamiento de las APIs, donde se gestiona los cambios de las especificaciones API.
- Generar la especificación API siguiento el formato de la las [plantillas de Diseño](./_resources/Plantilla-dise%C3%B1o-API.xlsx).

**Participantes involucrados:**

Equipo                | Rol               | Responsabilidad
--------------------- | ----------------- | ---------------
Oficina de Gobierno   | -				  | Dar soporte a la catalogación de las APIs e indicar los respositorios donde se almacenarán las especificaciones API.
Oficina de Gobierno   | -			  	  | Validar las plantillas con la definición acordada y soporte al equipo de desarrollo.
Equipo API Owner      | API Owner         | Iniciar la solicitud de la catalogación de las APIs que se han acordado a diseñar.
Equipo de Negocio     | Experto funcional | Apoyo y aportar el detalle funcional.
Equipo API Owner      | API Designer	  | Genera las plantillas con el apoyo del equipo Gobierno de API.

## 2. Fase de implementación

### 2.1. Creación

Validada y documentada la interfaz de las API identificadas, se inicia el proceso de escritura en un lenguaje de especificación de API ([OpenAPI 3.X](https://swagger.io/specification/)). En esta especificación se deberá generar los métodos, parámetros y protocolos previamente identificados y validados en la fase de Diseño.

Dicho procedimiento consta de los siguientes pasos:
- Generación de la especificacion API. Se recomienda el uso del IDE Stoplight Studio, siguiendo la guía de diseño de APIs definida por la organización y revisando las validaciones del editor. En caso de no utilizar el Stoplight Studio habrá que realizar un segundo paso y será pasar el conjunto de reglas de validación.
- Almacenamiento de la especificación de la API definida, con un documento donde se reflejen los cambios y solicitud de revisión a la Oficina de Gobierno.
- Desplegar la especificación en el API Management en el entornode de Desarrollo, y establecer las configuraciones de los API Proxy y políticas.

**Participantes involucrados:**

Equipo                | Rol               | Responsabilidad
--------------------- | ----------------- | ---------------
Oficina de Gobierno   | -			      | Revisar y validar la especificación API, cumpliendo con la guía de diseño, estándares, buenas prácticas, etc.
Equipo API Owner      | API Designer      | Generación de la especificación API en lenguaje formal, almacenarlo en el repositorio indicado y generar una solicitud para su  revisión.
Equipo API Owner      | API Owner	      | Será informado del estado y evolución de la API.


### 2.2. Implementación

En esta etapa se implementa la lógica de negocio que existe detrás de la API, partiendo de la especificación API generada previamente. Así como promocionarlo entre los distintos entornos previos al productivo, generando las pruebas necesarias y mínimas para verificar su calidad.

**Participantes involucrados:**

Equipo              | Rol          | Responsabilidad
------------------- | ------------ | ---------------
Equipo API Owner    | Developer    | Desarrollar la API. Realizar pruebas minimas que verifiquen el correcto funcionamiento de la implementación. 

**Nota:** En esta etapa se debe trabajar en paralelo, donde el equipo de QA podrá comenzar a realizar sus casos de pruebas y  consumir la API pudiendo iniciar la verificación de los desarrollos.

## 3. Fase de Gestión

### 3.1. Publicación

Fase que se lleva a cargo la publicación de la API en el entorno productivo, poniéndose a disposiciónde los consumidores, para que empiecen a consumirla.

**Participantes involucrados:**

Equipo                | Rol               | Responsabilidad
--------------------- | ----------------- | ---------------
Oficina de Gobierno   |  			      | Informador de la publicacion y el encargado del mantenimiento del catálogo de APIs.
Equipo API Owner      | API Owner         | Solicita la publicación, tras las validaciones aprobadas por la Oficina de Gobierno y pruebas.
Equipo API Owner      | Developer         | Ejecución de las pipelines para la gestión de la publicación o promoción del producto.

### 3.2. Monitorización y analíticas

En esta estapa se monitoriza y análisis de estadísticas de la API en producción y definición de los puntos a medir.

**Participantes involucrados:**

Equipo                | Rol               | Responsabilidad
--------------------- | ----------------- | ---------------
Oficina de Gobierno   | API Architect     | Encargado de la plataforma y las APIs están disponibles. Por otro lado, responsable de definir métricas técnicas, KPIs, avisos y alertas a nivel técnico. 
Equipo API Owner      | API Owner         | Responsable de definir KPIs y métricas funcionales a nivel de negocio.

### 3.3. Retirada

En esta etapa se revisa el estado de la API y se decide retirar la API del catálogo. Estas se quedarán disponible durante un periodo de gracia, tras el cual se retirará completamente.

**Participantes involucrados:**

Equipo                | Rol               | Responsabilidad
--------------------- | ----------------- | ---------------
Oficina de Gobierno   | API Architect     | Verificar la revisión del impacto de la descatalogación.
Oficina de Gobierno   |                   | Responsable de manegar la retirada del producto API.
Equipo API Owner      | API Owner         | Solicitar la retirada y definir el periodo en el que estará disponible hasta su retirada final.