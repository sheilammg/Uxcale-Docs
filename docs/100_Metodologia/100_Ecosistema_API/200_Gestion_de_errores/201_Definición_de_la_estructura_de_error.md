

**DEFINICIÓN DE LA ESTRUCTURA DEL ERROR**


|**Versión**|**Fecha**|**Autor**|**Comentarios**|
| :- | :- | :- | :- |
|**1.0**|28/04/2023|Axpe|Versión inicial.|



# Definición de la estructura del error
Para la evolución y mantenimiento de los servicios, se debe desarrollar una buena gestión de errores, de forma que se provea un mensaje de error útil, en un formato conocido y fácilmente consumible.

Seguir una estructura del error en OpenAPI es muy importante por las siguientes razones:

- Consistencia: Una estructura uniforme asegura que todos los errores estén definidos de manera consistente en todas las aplicaciones y en todas las implementaciones de la API. Esto facilita la comprensión y resolución de los errores, y permite que los desarrolladores se centren en el desarrollo de características importantes en lugar de lidiar con errores inconsistentes.
- Documentación: Una estructura uniforme permite que los errores se documenten de manera efectiva. Los desarrolladores pueden revisar rápidamente los errores comunes y sus soluciones para acelerar el proceso de desarrollo. Los posibles errores 4XX y 5XX se verán desarrollados en el documento de propagación de errores funcionales.
- Validación y pruebas: Una estructura permite que los errores se validen y prueben fácilmente en las aplicaciones. Los desarrolladores pueden implementar pruebas automatizadas para garantizar que se manejen correctamente todos los errores posibles.

El servicio deberá devolver códigos de status HTTP prácticos. Los errores del servicio generalmente caen dentro de 2 tipos:

- La serie de códigos **4XX** para problemas en el **cliente**.
- La serie de códigos **5XX** para problemas asociados en el **servidor**.

La representación de un error debería no ser diferente a la representación de cualquier recurso, con su propio conjunto de campos. Como mínimo, el servicio debería normalizar todos los errores de la serie 4XX y 5XX. En la mayoría de los casos, en lo relativo a la devolución de errores funcionales en los servicios, debido a su complejidad, los códigos HTTP suelen cubrir todas las casuísticas posibles.

La estructura de error en formato JSON es un objeto que contiene información sobre un error que ha ocurrido en una aplicación o sistema. Este objeto tiene las siguientes propiedades:

- Un **código de error único (code)**, que pueda ser buscado para obtener más detalles en la documentación. Este campo debe ser legible (human readable), por tanto, no debería ser un código numérico, sino alfanumérico. Campo **obligatorio**.
- Un **mensaje de error útil (message)**, que describa el error. Como recomendación y por seguridad se considera que el contenido de este atributo no debe contener valores de datos internos. Campo **obligatorio**.
- Un **nivel de error (type)**, que defina los diferentes niveles de gravedad de los errores. Campo **obligatorio** cuyos valores serán los siguiente:


|Nivel|Descripción|
| :- | :- |
|CRITICAL|Indica un error que impide el funcionamiento de la aplicación completa.|
|FATAL|Errores muy graves que presumiblemente harán abortar la ejecución.|
|ERROR|Errores que aún podrían permitir que la aplicación continuase ejecutándose.|
|WARNING|Validar que la especificación generada cumpla con la guía de diseño, estándares, buenas prácticas y reglas Spectral.|
|INFO|Mensajes informativos que resalten el progreso de la aplicación|

- Una **descripción detallada (description)**. Campo opcional.

A continuación, se muestra un ejemplo de la estructura de error JSON definida. En el ejemplo se observa un error 400, que indica que el servidor no puede o no procesará la solicitud.
```json
 {
    "messages": [
      {
        "code": "BAD_REQUEST",
        "message": "Bad Request",
        "type": "ERROR",
        "description": "The request is incorrect because the selected parameters are wrong or a functional error has occurred."
      }
    ]
  }
````
