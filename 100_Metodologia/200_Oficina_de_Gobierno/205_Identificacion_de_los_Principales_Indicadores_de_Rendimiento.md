|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|11/04/2023|Axpe|Versión inicial|



# **Identificación de los principales indicadores de rendimiento**

## Índice

[1. Introducción](#introduccion)

[2. Clasificación de los indicadores](#clasificacion)
  - [Portafolio](#portafolio).
  - [Operación](#operacion)
  - [Procesos](#procesos)
  - [Consumo](#consumo)
[3. Indicadores seleccionados para esta primera etapa](#primera-etapa)
  - [Portafolio](#portafolio1).
  - [Operación](#operacion1)
  - [Procesos](#procesos1)
  - [Consumo](#consumo1)
[4. Mediciones](#mediciones)
  - [Mediciones de negocio](#mediciones-de-negocio)
  - [Mediciones técnicas](#mediciones-tecnicas)


<a id="introduccion"></a>
## 1. Introducción.

Como parte del programa de Gobierno de API se deben establecer criterios y puntos de medición a lo largo del ciclo de vida del API, así como del modelo de adopción del ecosistema, con el fin de conocer el nivel de madurez que va adquiriendo una orfanización en cuanto al fomento y uso de APIs para la exposición de sus servicios.
Una vez establecidos los objetivos clave del ecosistema a lo largo del tiempo, se determina el modelo que nos permita llevar a cabo un seguimiento del cumplimiento a través de estos indicadores.

Los indicadores deben basarse escencialmente en el ciclo de vida del API, tomando en consideración los elementos que nos permitan tomar medidas cualitativas y cuantitativas de los resultados; y que a la vez nos permitan establecer modelos de comparación con los planteados en los objetivos clave. Así mismo, se debe establecer un mecanismo de iteración que permita al equipo de Gobierno analizar, ajustar los indicadores y modelos. y afinar las herramientas de recolección de datos.

<a id="clasificacion"></a>
## 2. Clasificación de los indicadores.

Se han establecido cuatro elementos globales de medición, que van desde la visión de Negocio hasta el aspecto técnico. La clasificación propuesta se presenta en el siguiente diagrama, donde podemos observar que sobre la base de negocio se establecen los criterios técnicos con los que se sustentará el ecosistema.

![Diagramas-apoyo-KPI-Identify-piramid.png](../../../assets/images/Diagramas-apoyo-KPI-Identify-piramid.png)


A continuación más detalle sobre cada elemento participante en el modelo de clasificación de los indicadores.

<a id="portafolio"></a>
### Portafolio

El portafolio de APIs esta basado en el aspecto funcional, es decir las áreas de negocio como impulsoras de los productos expuestos a través del ecosistema. Con el objetivo de tener una visión global sobre el estado del portafolio en un momento del tiempo, podríamos considerar un gráfico en tres ejes, donde tenemos las aristas que representan la funcionalidad expuesta, los actores que participan y se befician de esta, y el tiempo que esta llevando la habilitación de las funciones de negocio. Existen otros factores que tienen un impacto directo sobre esta medición, por ejemplo la resolución de dependencias con las áreas técnicas de producto, organización de la información en los sistemas actuales, gestión de equipos de desarrollo y deuda técnica, etcétera.

![Diagramas-apoyo-KPI-Identify-graphic.png](../../../assets/images/Diagramas-apoyo-KPI-Identify-graphic.png)

La propuesta de ámbitos identificados para considerar en esta clasificación son:

- Dominio a partir del área de negocio o dominio, o bien estableciendo un acercamiento a los servicios de dominio.
- Tipos de API, marcando las que serán de uso local para el propio dominio, las comunes y requisitadas; igualmente identificar las que serán internas de las externas.
- Estados del API por fase dentro del ciclo de vida. Requeridas, requeridas aprobadas, diseñadas, definiciones aprobadas, disponibles en entorno Sandbox, Live, retiradas, etcétera.
- Funcion de negocio, por ejemplo información de tarjetas, medición de riesgo financiero, información de cuenta, posición.
- Audiencia, identificar a quien va dirigida el API y los cambios de audiencia sobre la misma.
- Esquemas de seguridad, conocer los distintos mecanismos de seguridad por audiencia, establecer los patrones de uso sobre los productos y su orientación.

Bajo este grupo de ámbitos se proponen los siguientes indicadores para iniciar la medición del Portafolio.

- Número de servicios por dominio representados ( cumulative, % )
- Número de suscripciones (aplicaciones consumidoras) y uso (api calls) ( sum, cumulative, % )
- Número de APIs por estado en el ciclo de vida ( cumulative, % )
- Audiencia: Partners, Externa, Interna ( cumulative, % )

<a id="operacion"></a>
### Operación

Representan la más básica de las mediciones del API en cuanto a su ejecución. A través de estos indicadores se espera conocer el nivel de adopción que están teniendo las APIs, así como información que permite a los equipos de diseño hacer mejoras en las interfaces, así como facilitar la gestión de los recursos técnicos de infraestructura.

En escencia, estos indicadores pretenden dar una mirada a la continuidad del negocio en tiempo real y la estabilidad de la plataforma API, por hora, por día, por semana y/o por mes.

![Diagramas-apoyo-KPI-Identify-operations.png](../../../assets/images/Diagramas-apoyo-KPI-Identify-operations.png)

Indicadores propuestos para esta clasificación.

- Disponibilidad (avg, %)
- Tasa de fallos por tipo (4xx, 5xx) (avg, cumulative/period, %)
- Latencia y tiempos de respuesta (avg, %)
- Número de operaciones a través de los dominios (cumulative, %)
- Uso de infraestructura (cumulative/period, avg, %)

<a id="procesos"></a>
### Procesos

Dentro de esta clasificación se identifican las mediciones sobre el ciclo de vida del API, pretenden mostrar la efectividad del mismo y su ejecución desde el equipo de gobierno. Representa el tiempo hasta poner productiva un API y los costos directos derivados en la generación del API, su puesta en marcha y ejecución. Otro de los elementos que pretende medir es el nivel de reusabilidad a nivel de operaciones y API completa.

El modelo para conocer la capacidad del equipo de gobierno depende directamente de la madurez de las personas con respecto al conocimiento del ciclo de vida, los procesos y las herramientas. Acompañado a estas mediciones se recomienda mantener una estrategia de evaluación y supervisión necesarios para los equipos de diseño y desarrollo.

El crecimiento de la capacidad implica una curva de aprendizaje y, por lo tanto, una gran inercia inicial, por lo que cierto nivel de exceso sobre la capacidad del equipo de gobierno podría ser seguro y eficiente.

Los indicadores propuestos son.

- Tiempo API por estado en el ciclo de vida (avg, %)
- Costo incurrido por API, personas y materiales (avg, %) -> materiales: Sandbox
- Reusabilidad del API (completa, parcial y número de peticiones para el API) (%)
- Casos de prueba automatizados por dominio (cumulative, %)
- Número de peticiones a servicios (cumulative/period, avg, %)
- Estabilidad del API (cumulative/period, %)

<a id="consumo"></a>
### Consumo

Representa el volumen de llamadas identificado por los diferentes consumidores, los defectos y su clasificación, atención de los defectos.

- Número de incidencias (cumulative/period %)
- Número de tickets por estado en el ciclo de vida (cumulative/period %)
- Tiempo de resolución por incidente (avg, cumulative)
- Defectos por severidad ( % )

El panel propuesto sería como se muestra en la imagen

![Diagramas-apoyo-KPI-Identify-detailed.png](../../../assets/images/Diagramas-apoyo-KPI-Identify-detailed.png)


<a id="primera-etapa"></a>
## 3. Indicadores seleccionados para esta primera etapa.

<a id="portafolio1"></a>
### Portafolio

- APIs desplegados por dominio vs llamadas por API
- APIs desplegadas por dominio vs suscriptores
- APIs por dominio vs % Audiencia
- APIs por dominio vs API por estado
- APIs desplegadas
- Suscriptores (Internos + Externos)
- Media de llamadas por API

<a id="operacion1"></a>
### Operación

- % errores 4xx
- Instancias gateway

<a id="procesos1"></a>
### Procesos

- **Dominios en el ecosistema API vs casos de prueba automatizados**
- Reusabilidad del API (#suscriptores vs API)
- Tiempo API por estado en el ciclo de vida
- Estabilidad del API
- Disponibilidad de Sandbox
- Dominios en el ecosistema API vs Costo incurrido por API
- APIs desplegadas vs % Estabilidad del API
- API reutilizadas parcial/completa vs Tiempo de puesta en marcha de nuevas API
- API por dominio vs reutilización APi

<a id="consumo1"></a>
### Consumo

- ~ latencia gateway
- ~ disponibilidad del gateway

<a id="mediciones"></a>
## 4. Mediciones

<a id="mediciones-de-negocio"></a>
### Mediciones de negocio

Para la toma de mediciones de negocio, se deberán establecer como criterios para la selección de las herramientas de soporte a usar el que otorguen al menos lo idicadores principales.

<a id="mediciones-tecnicas"></a>
### Mediciones técnicas

Con base a los indicadores técnicos que se están seleccionando, se considera la toma de mediciones para la generación de estos a partir del Gateway.

<a id="latencia-ej"></a>
#### Latencia

- Latencia Media
- Latencia por hora
- Latencia por día

<a id="errores-ej"></a>
#### Errores

- Media de la tasa de error
- Errores por servicios
- Errores por tipo (cliente, servidor)

<a id="aplicaciones-ej"></a>
#### Aplicaciones

- Media de tráfico por aplicación
- Top x de tráfico en aplicaciones
- Top x de aplicaciones a API
