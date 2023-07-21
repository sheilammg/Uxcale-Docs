


Hipermedia es una extensión de hipertexto. Es un medio de información no lineal que incluye gráficos, audio, video, texto plano e hipervínculos. Hipermedia como el motor de estado de la aplicación (HATEOAS, Hypermedia As The Engine Of Application State) es una restricción de la arquitectura de aplicación REST.
En el contexto de un API RESTful, un cliente podría interactuar con un servicio completamente a través de hipervínculos proporcionados dinámicamente por el servicio. Un servicio de esta manera proporciona una representación de sus recursos a sus clientes para poder navegar por el API de manera dinámica al incluir enlaces hipermedia en sus respuestas.


## Ejemplos


Request
POST https://api.acciona.com/v1/customer/users
{
    "name": "Tobias",
    "surname" : "Beckett",
    ...

}
Response
Para este caso, el API crea un nuevo user con los datos de entrada y devuelve los siguientes links:
•	Un link a la representación completa del user (self) (GET)
•	Un link a la actualización de user (PUT)
•	Un link a la actualización parcial del user (PATCH)
•	Un link al borrado del user (DELETE)
{
HTTP/1.1 201 CREATED
Content-Type: application/json
...

"links": [
    {
        "href": "https://api.acciona.com/v1/customer/users/ALT-JFWXHGUV7VI",
        "rel": "self",
        
    },
    {
        "href": "https://api. acciona.com/v1/customer/users/ALT-JFWXHGUV7VI",
        "rel": "delete",
        "method": "DELETE"
    },
    {
        "href": "https://api. acciona.com/v1/customer/users/ALT-JFWXHGUV7VI",
        "rel": "replace",
        "method": "PUT"
    },
    {
        "href": "https://api. acciona.com/v1/customer/users/ALT-JFWXHGUV7VI",
        "rel": "edit",
        "method": "PATCH"
    }
]
}

Request
GET https://api.aciona.com/v1/customer/users
Response
{
    "totalItems": "166",
    "totalPages": "83",
    "users": [
    {
        “id”: “ALT-JFWXHGUV7VI”, 
        "givenName": "Tobias",
        "surname": "Beckett",
        ...
        "links": [
            {
                "href": "https://api.acciona.com/v1/customer/users/ALT-JFWXHGUV7VI",
                "rel": "self"
            }
        ]
    },
    {
        “id”: “ALT-EDBGKFID2”,
        "givenName": "Zam",
        "surname": "Wesell",
        ...
        "links": [
            {
                "href": "https://api.acciona.com/v1/customer/users/ALT-MDFSKFGIFJ86DSF",
                "rel": "self"
            }
   },
   ...
}

Request
DELETE https://api.acciona.com/v1/customer/ALT-JFWXHGUV7VI



Resumiendo:
•	Existe un punto de entrada bien definido desde donde el cliente del API puede navegar por todos los recursos.
•	El cliente del API no necesita construir la lógica de componer URI para ejecutar diferentes solicitudes.
•	El cliente de un API reconoce que el proceso de creación de URI recae en el servidor.
•	Las APIs que usan hipermedia en sus representaciones pueden extenderse sin problemas. A medida que se introducen nuevos métodos, las respuestas pueden ampliarse con enlaces HATEOAS. De esta manera, los clientes pueden aprovechar la funcionalidad de manera incremental.



5.1.2	Descripción del objeto link
Los enlaces (objeto link) debe describirse utilizando el esquema LDO (Link Description Object).
•	href:
o	Debe proveerse un valor para href.
o	Su valor debe ser una URI.
o	Deben usarse únicamente URI absolutas.
•	rel:
o	Debe proveerse un valor para rel.
o	Define el tipo de relación del enlace
o	Su valor indica el nombre de dichas relación con el recurso objetivo.
•	method:
o	Identifica el método HTTP que debe ser usado para hacer la petición al link. 
o	Por defecto se asume el valor de GET
•	title:
o	Proporciona un título para el link que sea útil para los clientes del API. 
o	No es obligatoria.
La propiedad links devuelta en los cuerpos de las respuestas debe ser un array que contenga los distintos objetos link asociados a la respuesta.

La siguiente tabla muestra los distintos valores que la propiedad rel puede contener:

Link relation type	Descripción
self	Identificador para el context del enlace. Por lo general, un enlace que apunta al recurso mismo.
create	Link que permite crear un nuevo recurso
edit	Link que permite editar (parcial o completamente) el recurso. Suele representar la operación PATCH
delete	Link que permite el borrado del recurso.
replace	Link que permite la modificación completa de un recurso. Suele representar la operación PUT.
collection	Indica que el recurso es una colección.
first	Link a la primera página del listado de resultados.
last	Link a la última página del listado de resultados.
next	Link a la siguiente página del listado de resultados.
prev	Link a la anterior página del listado de resultados.
up	Link al recurso padre en una jerarquía de recurso.



