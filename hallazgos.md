# Hallazgos

## Tabla de peticiones

| # |        Petición              | Código esperado | Código obtenido | ¿Coincide? |
| 1 | GET       /posts/1           | 200             |         200        |si|
| 2 | GET       /posts             | 200             |    200             |si|
| 3 | GET       /posts/9999        | 404             |      404           |si|
| 4 | POST      /posts             | 201             |                    | |
| 5 | PUT       /posts/1           | 200             |                    | |
| 6 | PATCH     /posts/1           | 200             |                    | |
| 7 | DELETE    /posts/1           | 200             |                    | |

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