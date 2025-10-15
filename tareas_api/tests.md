# Listar tareas
curl -X GET http://127.0.0.1:8000/api/v1/tareas/

![](images/01.png)

![](images/02.png)

# Crear tarea
curl -X POST http://127.0.0.1:8000/api/v1/tareas/

![](images/03.png)

# Detalle de una tarea
curl -X GET http://127.0.0.1:8000/api/v1/tareas/4/
![](images/04.png)

# Actualizar una tarea
curl -X PATCH http://127.0.0.1:8000/api/v1/tareas/4/ \
![](images/05.png)

# Borrar una tarea
curl -X DELETE http://127.0.0.1:8000/api/v1/tareas/5/
![](images/06.png)

![](images/07.png)

![](images/08.png)

# Status 400
![](images/09.png)

# Status 404
![](images/10.png)
