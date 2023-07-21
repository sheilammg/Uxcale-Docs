
# Catalogación funcional de APIs

## Estandarización con BIAN

La catalogación funcional de las APIs en el banco está basada en el estandar [BIAN](https://bian.org/servicelandscape-9-0/). 

BIAN es un estándar encargado de definir y clasificación de los distintos componentes de negocios específicos dentor del sector bancario.

Este modelo se base en una jerarquía de tres niveles:

> **Área de negocio / Dominio / Dominio de servicio**

El componente o área más importante del modelo BIAN es el Dominio de servicio, que representa los componentes funcionales de negocio.

El Dominio de servicio es un concepto que define la responsabilidad de cada componente de negocio, de manera similar al Contexto acotado de Domain Driven Design. 

Principales características:

+ Se trata de una capacidad de negocio discreta, no superpuesta y elemental, responsable de manejar el ciclo de vida completo de su función de negocio.

+ Es estable e incremental en el tiempo, y cuenta con una función o propósito de negocio que se define independientemente de la forma en que se pueda implementar, y que puede mejorarse con características adicionales.

+ Es un elemento canónico, soporta altos niveles de interoperabilidad, y define los bloques funcionales genéricos que componen cualquier banco, de manera agnóstica a la tecnología.

## Catalogación funcional de APIs por capas

En el ecosistema de APIs en el banco se clasifican en las siguientes capas APIs:

### APIs de sistema

En esta capa, la catalogación está basada en la Estructura organizacional del banco: 

 > **Sistema / Subsistema / Dominio servicio BIAN**

Siendo la nomenclatura para las APIs de sistema la siguiente:

 > **dominio-servicio-BIAN-subsistema**

Tomando como base el ejemplo anterior de Reclamación de movimientos de tarjeta, la catalogación para estas APIs de sistema sería la siguiente:

> **Medios de pago / IH / Card case**

> **Web / BD / Transaction authorization**

Y los nombres de las APIs:

> **card-case-IH**

> **transaction-authorization-BD**


De esta manera, logramos:

+ Mayor involucración de los equipos, al catalogar las APIs según los sistemas / subsistemas actuales
+ Evolución progresiva, con un primer paso en la adopción de un lenguaje ubicuo a través de la estandarización y normalización de nombres de APIs y de estructuras de datos subyacentes, que además son reutilizables
+ Owner actual, la responsabilidad se mantiene unida a la responsabilidad actual de MainFrame



### APIs de BaaS / Experiencia

En la capa de BaaS y experiencia, la catalogación está basada en BIAN:

> **Área negocio / Dominio / Dominio de servicio**

Siendo la nomenclatura para las APIs de BaaS la siguiente:

> **dominio-servicio-BIAN**

Y la nomenclatura para las APIs de experiencia la siguiente:

> **dominio-servicio-BIAN-canal**

Tomando como base el ejemplo anterior de Reclamación de movimientos de tarjetas, la catalogación para estas APIs de BaaS y experiencia sería la siguiente:

> **Customers / Customer care / Card case**

El nombre de la API de BaaS:

> **card-case**

Y el de la API de experiencia:

> **card-case-digital**

De esta manera, logramos:

+ Inventario catalogado de todas las piezas necesarias para componer productos bancarios en un modelo Open Banking
+ Estandarización
+ Interoperabilidad
+ Orientación a Domain Driven Design, correspondencia entre Dominios de servicio BIAN y Bounded Context DDD
	- Principio de Responsabilidad Única, a través de la separación de responsabilidades con los Dominios de servicio BIAN
	- Lenguaje Ubicuo, a través de la estandarización de nombres de API y estructuras de datos subyacentes, que además son reutilizables
+ Posible configuración de responsabilidad separada de la parte de Sistema, permitiendo una evolución gradual hacia un sistema basado en BIAN


## Catalogación funcional de APIs en Bitbucket

La catalogación funcional de las APIs tiene su reflejo en las estructuras de Bitbucket. 

Dependiendo de la capa de API, la nomenclatura para los proyectos es la siguiente:

- APIs de sistema: API Nb Sistema MF - Nb Subsistema MF
- APIs BaaS y experiencia: API Nb Área negocio BIAN - Nb Dominio BIAN

![Bitbucket](./_images/system-proyecto-medios-de-pago-ih.PNG)

![Bitbucket](./_images/baas-experience-proyecto-customers-customer-care.png)

De la misma manera, dependiendo de la capa de API, la nomenclatura para los repositorios es la siguiente:

- APIs de sistema: api-nb-dominio-servicio-bian-system-nb-subsistema-v(major version)
- APIs BaaS: api-nb-dominio-servicio-bian-bian-baas-v(major version)
- APIs Experiencia: api-nb-dominio-servicio-bian-experience-nb-canal-v(major version)  

![Bitbucket](./_images/system-repo-api-card-case.PNG)

![Bitbucket](./_images/baas-experience-repos-api-card-case.png)




