# Versionado de las APIs

Una parte fundamental en este punto es el **versionado**, a medida que evolucionan las necesidades del negocio la API evolucionara conjuntamente. Para el versionado de nuestras APIs seguiremos un estilo de [versionamiento semántico](https://semver.org/), donde:

1. La versión indicada en el documento de especificación de la API tendrá un formato: `[MAJOR].[MINOR].[PATCH]`, siendo:
   1. `[MAJOR]` Cambios que implicará que la API se ha introducido un cambio no retro-compatible (eliminación de un recurso o un método, adición de un parámetro obligatorio, etc).
   2. `[MINOR]` Se añaden nuevas funcionalidades al API, sin afectar a las anteriores, es decir, un cambio retro-compatible (añadir un nuevo recurso o un nuevo método, convertir un campo obligatorio en opcional, etc).
   3. `[PATCH]` Corrección de errores (bugs) sobre la versión.
   
      > Ejemplo: version 1.2.5

2. El versionado _mayor_ se incluirá reflejada en la url de acceso al recurso, ya que solo se tienen en cuenta los cambios mayores, ya que estos son los que indican incompatibilidades entre las versiones.Por tanto los que afectan directamente a los consumidores (obligando a los desarrollos para adaptarse a los nuevos requisitos de esta nueva versión).
   > Ejemplo: <https://www.dominio.com/context/v1/resource>

   > Ejemplo: <https://www.dominio.com/context/v2/resource>

#### Buenas prácticas

- La primera publicación en producción (drafts) se debe empezar con la versión v0.x.x.
- La primera versión definitiva debería ser la v1.0.0.
- Cualquier modificación en la especificación de la API debera quedar reflejada y subirse la versión. PAra ello se deberá tener un fichero de apoyo con los cambios realizado por cada versión, ejemplo [changelog.md](https://keepachangelog.com/).
- En alguno casos se puede obviarse subir la versión de PATCH, siempre si esta no está en el mismo repositorio que la implementación.
- Sería útil para actualizaciones significativas en las que tenga importancia que el cliente conozca la situación del API o se quiera probar una versión nueva mediante una Canary o Blue/green deployment.

#### Tipos de cambios

- **Cambios compatibles**
  - Añadir un query parameters opcional de consulta.
  - Agregar cabeceras o parameters.
  - Añadir nuevos recursos.
  - Añadir operaciones a un recurso existente.
  - Añadir nuevos atributos opcionales a un recurso.
  - Modificar atributos obligatorios a opcionales en un recurso.
  - Mejorar la documentación de la API

- **Cambios incompatibles**
  - Eliminar atributos de un recurso.
  - Modificar el tipo del atributo en un recurso (ejemplo: pasar de string a date).
  - Eliminar atributos del payload de salida (response).
  - Modificar un atributo que era opcional en el payload de entrada (request) a obligatorio.
  - Modificar un atributo que era opcional en el payload de salida (response) a obligatorio.
  - Cambiar el URI de un endpoint.
  - Añadir un atributo obligatorio a un recurso.

- **Cambios mayores**
  Si incluso el cambio más pequeño incompatible con la versión anterior requiere un aumento de la versión major ¿No voy a terminar en la versión 123.0.0 demasiado rápido?

Este es un tema de implementación responsable y de previsión. Los cambios incompatibles no debieran ser introducidos con ligereza al software del cual depende mucho código. El costo de actualizar puede ser significante. Tener que aumentar la versión major para publicar cambios incompatibles significa que vas a pensar bien el efecto de tus cambios y evaluar el costo/beneficio asociado. Hay que ser responsable e incluir los cambios que se pueden como compatibles y anticiparse, dedicando en la parte de diseño el tiempo necesario.