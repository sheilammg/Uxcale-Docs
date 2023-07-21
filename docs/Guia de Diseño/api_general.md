
## Conclusión/resumen

Una API es una interfaz expuesta por un sistema para establecer una forma técnica y funcional de interacción con múltiples sistemas. Es un contrato y una vía de acceso que permite la interoperabilidad entre sistemas.

- Una API debe tener expuesta una versión mock.

    - Se trata de una versión de la API que se comporta como la real, pero carece de muchas características funcionales y no-funcionales, limitándose a responder con un conjunto de datos estáticos que simulan el comportamiento de la API real.

- Debe ser implementada como un servicio REST siempre que sea posible
    
    - Debe tener recursos identificados. 
    - Los recursos pueden tener subrecursos.
    - Debe usar métodos HTTP correctamente para cubrir las funcionalidades identificadas.
    - Es deseable que contemple [HATEOAS](./hateoas.md).

- Las APIs deben tener la visibilidad apropiada (API Portal)
    
    - La API debe estar referenciada en el portal de Documentación.
        -   Descripción de la API
        -   Listado de recursos, subrecursos y métodos.
        -   Localización de los endpoints a consumir.
        -   Enlace al API portal de la plataforma de APIs donde se encuentre implementada.

    - La API debe aparecer en el API portal asociado a la plataforma de APIs donde se encuentre dicha API. En caso de carecer de API Portal, esta información debe aparecer en el portal de documentación genérico.
        -   Descripción funcional de la API.
        -   Ejemplos de casos de uso (deseado)
        -   Listado y descripción de métodos expuestos y entidades asociadas.
        -   Instrucciones de consumo del mock asociado en caso de existir
        -   Instrucciones de consumo del API

- Deben estar correctamente [versionadas](./101_versionado.md).

- El consumo de la misma debe estar manejado mediante permisos de las aplicaciones, planes de consumo y visibilidad de la misma.

- Debe tener una definición única (versionada en caso de ser necesario)

- Debe estar definida utilizando un estándar:
    
    - Swagger 3.0
    - RAML 1.0

- La definición debe estar desacoplada de la implementación.

- Diseño e implementación deben estar en español/inglés (Preferentemente Inglés). 

- Documentación de la API pueden estar en español/Inglés (Preferentemente Inglés).

- Debe estar bien documentada y debe poderse consumir en base a su documentación
