

# **Versionado de las APIs**
|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|10/03/2023|Axpe|Versión inicial.|




# Índice
- [1. Versionado de las APIs	](#Versionado)

  - [1.1 Buenas prácticas	](#Buenas_practicas)

  - [1.2 Tipos de cambios	](#Tipos_cambios)




# <a id="Versionado"></a>Versionado de las APIs
Una parte fundamental en este punto es el versionado. A medida que evolucionan las necesidades del negocio, la API evolucionará conjuntamente. Para el versionado de nuestras APIs seguiremos un estilo de versionado semántico, donde:

1. La versión indicada en el documento de especificación de la API tendrá un formato: [MAJOR].[MINOR].[PATCH], siendo:
   1. [MAJOR] Cambios que implicará que la API se ha introducido un cambio no retro-compatible (eliminación de un recurso o un método, adición de un parámetro obligatorio, etc).
   1. [MINOR] Se añaden nuevas funcionalidades al API, sin afectar a las anteriores, es decir, un cambio retro-compatible (añadir un nuevo recurso o método, convertir un campo obligatorio en opcional, etc).
   1. [PATCH] Corrección de errores (bugs) sobre la versión.
1. El versionado major se incluirá en la url de acceso al recurso. Sólo se tienen en cuenta los cambios mayores, ya que estos son los que indican incompatibilidades entre las versiones. Por tanto, son los que afectan directamente a los consumidores (obligando a los desarrollos para adaptarse a los nuevos requisitos de esta nueva versión).

Ejemplo: https://www.dominio.com/context/v1/resource

Ejemplo: https://www.dominio.com/context/v2/resource
## <a id="Buenas_practicas"></a>Buenas prácticas
- La primera publicación en producción (drafts) se debe empezar con la versión v0.x.x.
- La primera versión definitiva debería ser la v1.0.0.
- Cualquier modificación en la especificación de la API deberá quedar reflejada y subirse la nueva versión. Para ello se deberá tener un fichero de apoyo con los cambios realizado por cada versión, por ejemplo: changelog.md.
- En algunos casos se puede obviarse subir la versión de PATCH, siempre que no esté en el mismo repositorio que la implementación.
- Sería útil para actualizaciones significativas en las que tenga importancia que el cliente conozca la situación del API o se quiera probar una versión nueva mediante una Canary o Blue/green deployment.
## <a id="Tipos_cambios"></a>Tipos de cambios
- **Cambios incompatibles**
  - Endpoints y operaciones 
	- Borrar un endpoint o  un a operacion 
	- Actualizar un endpoint o realizar cambios en algunos de sus métodos
  - Request Body
    - Añadir un campo obligatorio.
	- Borrar o renombrar un campo, incluso aunque ese campo sea opcional.
	- Cambiar un campo de opcional a requerido.
	- Cambiar el tipo de dato de un atributo.
	- Borrar o renombrar un elemento de una enumeración, de un campo.
	- Disminuir el maxLength de un campo.
	- Realizar una validacion que sea más estricta. 
  - Responses 
    - Borrar o renombrar un campo.
	- Convertir a requerido un campo que era opcional.
	- Cambiar el tipo de dato de un atributo.
	- Añadir o renombrar un elemento de una enumeración.
	- Incrementar el maxLength de un campo 
  - Otros cambios 
	- Agregar cabeceras obligatorias 
	
- **Cambios compatibles**
  - Endpoints y operaciones
    - Añadir un nuevo endpoint u operacion 
  - Request Body
    - Añadir un campo opcional
    - Convertir un campo requerido a opcional 
    - Añadir un elemento a una enumeración
    - Incrementar el maxLength de un campo 
    - Realizar una validación menos estricta
  - Responses 
    - Añadir un campo, aunque sea requerido
    - Convertir a opciona un campo requerido 
    - Borrar un elemento de una enumeracion 
    - Decrementar el maxLength de un campo.
  - Otros cambios 
    - Añadir query parameters opcionales de consulta
    - Agregar cabeceras o parametros de entrada opcionales a los recursos existentes
    - Mejorar la documentación de la API.

    
Si incluso el cambio más pequeño incompatible con la versión anterior requiere un aumento de la versión major, ¿no voy a terminar en la versión 123.0.0 demasiado rápido?

Este es un tema de implementación responsable y de previsión. Los cambios incompatibles no debieran ser introducidos con ligereza al software del cual depende mucho código. El costo de actualizar puede ser significante. Tener que aumentar la versión major para publicar cambios incompatibles significa que vas a pensar bien el efecto de tus cambios y evaluar el costo/beneficio asociado. Hay que ser responsable e incluir los cambios que se pueden como compatibles y anticiparse, dedicando en la parte de diseño el tiempo necesario.
