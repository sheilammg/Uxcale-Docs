 # **Equipos y roles en el ciclo de vida API**

 ## Índice

[1. Equipo de la Oficina de Gobierno](#1-equipo-de-la-oficina-de-gobierno)
- [1.1. Diseñador API API Designer.](#11-dise%C3%B1ador-api-api-designer)
- [1.2. Arquitecto API API Architect.](#12-arquitecto-api-api-architect)
- [1.3. API Evangelist](#13-api-evangelist)

[2. Equipo de proyecto API Owner.](#2-equipo-de-proyecto-api-owner)
- [2.1. API Owner.](#21-api-owner)
- [2.2. API Designer/Developer.](#22-api-designerdeveloper)
- [2.3. Tester QA.](#23-tester-qa)

[3. Equipo funcional del negocio.](#3-equipo-funcional-del-negocio)

---

En este documento se identifica y detallan todos los equipos involucrados en procedimiento del ciclo de vida API, juntos cons sus roles que aportan durante el mismo.

Se compone de todos aquellos actores (Contriibutors) que estan involucrados durante el ciclo de vida API, perteneciendo a cualquiera de los equipos que se detallan a continuación (Equipo de gobierno, equipo de proyecto (API Owner) y/o equipo funcional del negocio)


## 1. Equipo de la Oficina de Gobierno

La Oficina de Gobierno API esta compuesta por aquellas actores que se involucran en todas las fases del procedimiento del ciclo de vida API. Esta compuesto por personas que tiene un cierto grado de "expertis" en el área de apificación, encarganandose de validar la definición de las APIs, mantenimiento y su correcta gestion y ejecución.

Sus tareas y responsabilidades:

- Fomentar y consolidar el enfoque API First en la organización.
- Apoyar y guiar a los responsables de negocio y equipo de proyecto a la hora de definir APIs que aporten valor.
- Administrar un catálogo de las APIs versionadas que se utilicen como referencia a la hora de la creación.
- Definir y gestionar adecuadamente las políticas requeridas y necesarias para el funcionamiento de las API.
- Monitorización y anális de las APIs.

Este equipo se diferencia los siguienres roles:

### 1.1. Diseñador API (API Designer).

Son aquellas actores que se encuentran trabajando conjuntamente con el equipo de proyecto en todo el ciclo de vida API. Encargado de ayudar a definir la interfaz, de validar las interfaces, y verificar que la definición cumple con el documento de diseño definido por la organización. Por otro lada, revisarán y garantizarán que la documentación aportada a la hora de la definición de las APIs ón sigue la normalización de calidad y nomenclatura establecidos.

### 1.2. Arquitecto API (API Architect).

Son aquellos actores que encarga de gestionar y lidera la estategia de "apificación" implantada y responsables de su cumplimento.

Por otro lado, tendra funciones de validación  de los diseños definidos e implmentados, y de gestionar las APIs del catálogo.

### 1.3. API Evangelista

Aquellos expertos que han definido la metodología de gobierno, normativa de diseño, las guia de diseño API siguiendo los estándares y el gobierno de las APIs. 

Entre sus funciones se encuentra en ayudar al diseñador API a tomar dicisiones y validar el diseño de las APIs, asegurando que las APIs definidas aporten valor.


## 2. Equipo de proyecto (API Owner).

El equipo de proyecto esta compuesto por el responsable de la API y las personas que se encargan de su definición, su mantenimiento y su correcta ejecución y se encuentra involucradas en todas las fases del ciclo de vida API.

Este equipo está compuesto por los siguientes roles:

### 2.1. API Owner.

Persona o area que asume la propiedad de la API, gestionando su producto y estableciendo los objetivo que persigue su funcionalidad, prestaciones y segmento de negocio. Para ello hara de enlace entre tecnología y negocio y podrá ayudar a identificar las APIs candidatas en los proyectos que este participando.

### 2.2. API Designer/Developer.

Son aquellos actores que estan al cargo de diseñar las interfaces, según la metodología aportada desde la Oficina de Gobierno. Siguiendo los estandares y nomenclatura definidas.

Por otro lado, también será el encargado de implmentación, que tendrá la lógica de negocio que se expone en la API.Principalmente estará presente en la fase de implantación del ciclo de vida API. 

Este rol, dependiendo de la complejidad del servicio a *"apificar"*, podrá tener una estructura simple o compleja y se podrán encontrar otro roles mas especificos como como Technical lead o arquitecto.

### 2.3. Tester (QA).

Son aqueillas personsnas encargado de controlar y administrar la calidad del software entregado por el equipo, a nivel funcional. Como el caso anterior, se pueden encontrar roles más específicos dentro de este grupo, como Technical lead o analista.

## 3. Equipo funcional del negocio.

Este equipo esta formado por aquellas personas que tienen un conocimiento detallado del área de negocio y de la funcionalidad que se requerie exponer vía API. Principalmente estos actores se encontrarn involucrados en la fase de planificación, donde indicarán las necesidades del proyecto. Ayudaran a obtner el conjunto de APIs objetivo aportando todo el conocimiento funcional necesario.