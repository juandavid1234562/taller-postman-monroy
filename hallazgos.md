# Hallazgos

## Tabla de peticiones

| # |        Petición              | Código esperado | Código obtenido | ¿Coincide? |
| 1 | GET       /posts/1           | 200             |         200        |si|
| 2 | GET       /posts             | 200             |    200             |si|
| 3 | GET       /posts/9999        | 404             |      404           |si|
| 4 | POST      /posts             | 201             |        101            | No|
| 5 | PUT       /posts/1           | 200             |        200            | Si|
| 6 | PATCH     /posts/1           | 200             |        200            | Si|
| 7 | DELETE    /posts/1           | 200             |        200            | si|

# ¿En qué se diferencian los criterios de aceptación?
Al pedir un recurso verifico un solo objeto: que exista, que sea el id pedido y que
tenga todos sus campos con valores coherentes. Al pedir una colección ya
no basta mirar un objeto: verifico que la respuesta sea una lista, que
traiga la cantidad esperada (100), que cada elemento tenga la misma
estructura y que no haya elementos repetidos o vacíos. Además, una
colección puede legítimamente venir vacía y seguir siendo un éxito,
mientras que un recurso individual vacío no.
**¿Pasó o falló?** Pasó. Yo esperaba un 404 porque ese recurso no existe,
y obtuve 404. Un defecto existe cuando el resultado obtenido es distinto
del esperado, no cuando el código es distinto de 200.

# ¿Y si hubiera devuelto 200 con cuerpo vacío?** Sí sería un defecto. 
El recurso no existe, así que lo correcto es avisarlo con 404. Un 200 le
diría al cliente que la operación fue exitosa cuando no encontró nada,
y una aplicación podría seguir su flujo creyendo que todo salió bien.

## Tarea 6: POST

Las cinco veces la API respondió 201 Created con el mismo id: 101.

¿Por qué ocurre?
Porque JSONPlaceholder solo simula la creación: acepta
mi petición y me devuelve cómo quedaría el recurso, pero no guarda nada
en una base de datos. Por eso el id siempre es el siguiente al último
existente (100).

¿Cómo comprobaría en una API real que se creó?
 Haría un GET al id que devolvió el POST (por ejemplo /posts/101) y verificaría que responde 200 con
los datos que envié. También haría un GET a la colección para ver que hay un
elemento más. Si el GET da 404, el 201 no era confiable.

## Tarea 7: PUT vs PATCH

**Respuesta completa del PUT** (envié solo `title`):

    { "title": "Titulo corregido", "id": 1 }

**Respuesta completa del PATCH** (envié solo `title`):

    { "userId": 1, "id": 1, "title": "Titulo corregido", "body": "..." }

##  **¿Qué diferencia encontré?** Con PUT el recurso quedó con solo `title` e
`id`: se perdieron `userId` y `body`, porque PUT reemplaza el recurso
completo por lo que envío. Con PATCH se cambió únicamente `title` y los
demás campos se conservaron.

##  **¿Cuál usaría para corregir un error de escritura en un solo campo?**
PATCH, porque solo modifica lo que envío. Con PUT tendría que reenviar
todos los campos.
 si olvido alguno, lo borraría sin darme cuenta, que es
justo el daño grave que se produce en la práctica cuando se usa PUT
pensando que actúa como PATCH.
