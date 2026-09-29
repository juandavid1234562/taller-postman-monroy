# taller-postman-monroy
**Estudiante:** Juan david monroy
**Código:** Tu código estudiantil
**Asignatura:** Ingeniería de Software II — Cotecnova
# Taller de APIs y Postman
## Tarea 1 #### ¿Qué es una API REST?
Investiga y explica en un párrafo. Tu respuesta debe incluir:
-Qué significa que una API sea «REST»
-Qué es un recurso y qué es un endpoint
-Un ejemplo de una aplicación que uses a diario y que dependa de APIs
enlace de la fuente consultada.

-es una forma de diseñar servicios que permite que diferentes aplicaciones se comuniquen mediante HTTP, utilizando métodos como GET, POST, PUT y DELETE para consultar, crear, modificar o eliminar informacióç

-REST significa que sigue principios de arquitectura REST y trabaja con recursos, que son los objetos o datos que maneja el sistema, por ejemplo, usuarios, productos o pedidos

-Un endpoint es la dirección específica mediante la cual se puede acceder a un recurso, por ejemplo, /api/productos

-Un ejemplo de una aplicación que usamos diariamente y que depende de APIs es Google Maps, ya que aplicaciones y sitios web pueden utilizar las APIs de Google Maps para mostrar mapas, lugares, rutas y obtener información de ubicación.

https://developer.mozilla.org/en-US/docs/Glossary/REST?utm_source=chatgpt.com
https://developers.google.com/maps/apis-by-platform?hl=es-419&utm_source=chatgpt.com


# Tarea 2 #### Los métodos HTTP y el CRUD
Completa esta tabla investigando qué hace cada método y a qué operación del CRUD
corresponde:

Método	  Operación CRUD	      Qué hace
GET	      Read (Leer)	          Consulta o obtiene información de uno o varios recursos.
POST	  Create (Crear)	      Crea un nuevo recurso o envía información al servidor.
PUT	      Update (Actualizar)     Actualiza o reemplaza completamente un recurso existente.
PATCH	  Update (Actualizar)     Modifica parcialmente un recurso existente.
DELETE	  Delete (Eliminar)	      Elimina un recurso existente.



# Tarea 3 #### Las familias de códigos de estado
Los códigos HTTP se agrupan en cinco familias: 1xx, 2xx, 3xx, 4xx y 5xx. Investiga qué
significa cada familia y da un ejemplo concreto de cada una.
Responde además esta pregunta, que es la que importa: ¿por qué se separan los errores
4xx de los 5xx? ¿Qué cambia entre unos y otros desde el punto de vista de quién tiene
la culpa?

- 1xx (informativos): la petición se recibió y sigue en proceso. Ej.: 101 Switching Protocols.

- 2xx (éxito): todo salió bien. Ej.: 201 Created.

- 3xx (redirección): hay que ir a otra dirección. Ej.: 301 Moved Permanently.

- 4xx (error del cliente): la petición está mal hecha. Ej.: 404 Not Found.

- 5xx (error del servidor): el servidor falló. Ej.: 500 Internal Server Error.

¿Por qué se separan 4xx y 5xx?
En el 4xx el error lo cometió quien pide
(URL mal escrita, datos inválidos), así que se corrige del lado del cliente.
En el 5xx la petición estaba bien y el fallo es del servidor, así que
lo debe corregir quien lo administra.
