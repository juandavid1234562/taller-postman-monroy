## Tarea 8: idempotencia

Un método es idempotente cuando ejecutarlo una vez o muchas veces con la
misma petición deja el sistema en el mismo estado. No importa que la
respuesta sea idéntica, importa el efecto sobre el servidor.

| Método | ¿Idempotente? | Razón |
| GET    | Sí            | Solo lee, no cambia nada |
| PUT    | Sí            | Reemplazar por los mismos datos deja el mismo resultado |
| DELETE | Sí            | Después de borrar, repetirlo deja el recurso igualmente borrado (aunque la 2.ª respuesta pueda ser 404) |
| POST   | No            | Cada envío crea un recurso nuevo |
| PATCH  | No garantizado| Depende: "poner título X" es idempotente, "sumar 1 al contador" no |

Lo que observé en Postman: 
tres PUT idénticos dieron tres respuestas idénticas. 
Los tres POST idénticos también devolvieron el mismo id (101), pero eso se debe a que JSONPlaceholder no guarda nada. En una API real cada POST habría creado un recurso distinto (101, 102, 103), y por eso reintentar un POST por error puede generar duplicados, mientras que reintentar un PUT es seguro.

## Tarea 9: cabeceras de la respuesta

- Content-Type (valor visto: `application/json; charset=utf-8`): indica
  en qué formato viene el cuerpo de la respuesta y con qué codificación.
- Cache-Control(valor visto: `max-age=43200`): le dice al cliente o al
  navegador durante cuánto tiempo puede reutilizar la respuesta sin volver
  a pedirla al servidor (aquí, 12 horas).
- Content-Length (valor visto: el tuyo): tamaño del cuerpo en bytes.

¿Por qué importa Content-Type al probar una API?
 Porque me dice cómo debo interpretar el cuerpo. Un servidor con problemas puede devolver un
200 con una página HTML de error en lugar del JSON esperado; el código
parece exitoso pero el contenido no lo es. Al verificar Content-Type
detecto ese caso, y mis pruebas que leen JSON no fallan por razones confusas.

