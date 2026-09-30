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

## Preguntas finales

¿Qué le faltaría a mi tabla para ser un plan de pruebas formal?
Mi tabla ya es un conjunto de casos de prueba: cada fila tiene una
entrada, un resultado esperado y uno obtenido. Para ser un plan formal le
faltaría: un identificador y un objetivo por caso, las precondiciones,
los datos de entrada detallados, los criterios de aprobación, el alcance
(qué se prueba y qué no), el entorno y las herramientas, la priorización
según el riesgo, el responsable y el cronograma.

¿Por qué un 404 puede ser buena noticia y un 200 puede ser un defecto?
Porque un caso pasa o falla según si el resultado coincide con lo
esperado, no según el código. Si pido un recurso que no existe y la API
responde 404, se comporta como debe: el caso pasó. En cambio, un 200 puede
ser un defecto si no corresponde, por ejemplo devolver 200 con cuerpo
vacío para un recurso inexistente, porque le dice al cliente que todo
salió bien y puede seguir trabajando con datos que no existen.