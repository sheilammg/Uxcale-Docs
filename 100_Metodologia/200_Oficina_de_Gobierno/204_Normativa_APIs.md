|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|11/04/2023|Axpe|Versión inicial|


# Normativa de APIs 

## Índice
---

[1. Introducción](#introduccion)

[2. Estructura de las reglas](#estructura)

<a id="introduccion"></a>
## 1. Introducción

Este documento tiene como objetivo recoger el conjunto de reglas, de obligado cumplimiento, que aplica a todas las APIs que se desarrollen para una organización concreta. 

Dado que una API es un elemento atómico no divisible para su utilización, la modificación de alguna de las partes de una API existente, implicará que la API completa cumpla con la normativa vigente.

<a id="estructura"></a>
## 2. Estructura de las reglas

Para facilitar la comprensión y localización de las reglas, cada una de ellas tiene asignado un código. 

Este código se compone de la siguiente manera:

- **AXPE**-X-X-XXX-XXX La primera cadena se corresponde con el conjunto de reglas al que pertenece:
  1. AXPE: Reglas personalizadas de AXPE  
  2. OWASP: Reglas del Top 10 de OWASP.
  3. OPENAPI: Reglas básicas para OPENAPI.
  4. ASYNCAPI: Reglas básicas para ASYNCAPI.
  5. SISTEMA: Reglas personalizadas para APIs de sistema.
  6. EXPERIENCIA: Reglas personalizadas para APIs de experiencia.
  7. BAAS: Reglas personalizadas para APIs de baas.
- XXXX-**G**-X-XXX-XXX El segundo carácter se corresponde con el nombre de la sección del yaml a la que hace referecia la regla:
  1. **A**pi
  2. **G**eneral
  3. **I**nfo
  4. **S**ervers
  5. **T**ags
  6. **P**aths
  7. **C**omponents
- XXXX-X-**1**-XXX-XXX El siguiente dígito se corresponde con la severidad de la regla:
  1. Error: Regla cuyo incumplimiento compromete el funcionamiento o la seguridad de la API.
  2. Warning: Regla que debe atenderse, advierte sobre un complemento faltante o incoherente, provocando un error leve.
  3. Information: Informa sobre una corrección que no compromete seriamente la estructura o diseño de la API.
  4. Hint: Regla que indica una recomendación.
- XXXX-X-X-**GEN**-XXX Los tres siguientes caracteres se corresponden con el nombre de la subsección del yaml a la que hace referencia la regla:
  1. Api, servers, tags, info y general: **GEN**eral
  2. Paths: **GEN**eral, **OPE**rations o **RES**ponses
  3. Components: **GEN**eral o **SEC**urity
- XXXX-X-X-XXX-**001** Los tres últimos dígitos se corresponden con un ordinal, asignado dentro de la sección.
