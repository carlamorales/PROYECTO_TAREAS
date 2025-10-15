## Recursos y URIs

**Recurso principal:** `/api/v1/tareas/`

**URIs disponibles:**
- `/api/v1/tareas/` → colección de tareas (GET, POST)
- `/api/v1/tareas/{id}/` → detalle individual (GET, PATCH, DELETE)

## Verbos y Códigos HTTP

| Método | URI | Descripción | Código esperado |
|---------|-----|-------------|----------------|
| **GET** | `/api/v1/tareas/` | Lista todas las tareas | `200 OK` |
| **POST** | `/api/v1/tareas/` | Crea una nueva tarea | `201 Created` |
| **GET** | `/api/v1/tareas/{id}/` | Consulta una tarea específica | `200 OK` |
| **PATCH** | `/api/v1/tareas/{id}/` | Actualiza título o estado (hecho) | `200 OK` |
| **DELETE** | `/api/v1/tareas/{id}/` | Elimina una tarea existente | `204 No Content` |

**Errores esperados:**
- `400 Bad Request` → Datos inválidos o título vacío  
- `404 Not Found` → ID inexistente

## Reglas REST

- **Stateless:** Cada solicitud HTTP se procesa de forma independiente; no se guarda información de sesión en el servidor.  
- **JSON:** Todas las peticiones y respuestas usan el formato `application/json`.  
- **Versionado:** La API incluye versión en la ruta base: `/api/v1/`.  
- **Idempotencia:** Repetir una misma operación (por ejemplo, un PATCH o GET) no genera cambios adicionales en el recurso.

**Explicación detallada:**

- **Stateless (sin estado):**  
  Cada petición HTTP se procesa de manera independiente.  
  El servidor **no guarda información de sesión ni contexto** entre peticiones.  
  Por ejemplo, al crear o consultar una tarea, el servidor solo utiliza los datos que llegan en esa solicitud, sin depender de lo que ocurrió antes.  
  Esto facilita la escalabilidad y hace que la API sea predecible.

- **JSON como formato estándar:**  
  Todas las comunicaciones entre cliente y servidor se realizan usando el formato **JSON (JavaScript Object Notation)**.  
  Esto asegura interoperabilidad entre distintos clientes (Postman, aplicaciones web, móviles, etc.).  

- **Versionado en la ruta:**  
  El prefijo `/api/v1/` indica la versión actual de la API.  
  Esto permite evolucionar la aplicación (por ejemplo, lanzar `/api/v2/`) sin romper la compatibilidad con clientes antiguos.  
  El versionado explícito es una buena práctica esencial en APIs públicas o de largo mantenimiento.

- **Idempotencia:**  
  Significa que ejecutar varias veces una misma operación produce **el mismo resultado final**.  
  Por ejemplo:  
  - Hacer varias solicitudes **GET** no cambia los datos.  
  - Enviar repetidamente el mismo **PATCH** que marca una tarea como hecha (`"hecho": true`) no altera su estado más allá de la primera vez.  
  Este principio evita efectos secundarios inesperados y mejora la confiabilidad de la API.


## Diagrama de Arquitectura

```text
CLIENTE (curl / SPA / Postman)
│
├── HTTP / JSON
│
├── API /api/v1/ (ViewSets y URLs con DRF)
│
├── Serializers (validación y transformación de datos)
│
├── Modelos Django (ORM)
│
└── Base de Datos SQLite (local)
```

**Descripción por capa:**

**Cliente**: envía peticiones HTTP y muestra las respuestas JSON.

**API**: define los endpoints y métodos REST (GET, POST, PATCH, DELETE).

**Serializers**: validan los datos y los convierten entre JSON y objetos Python.

**Modelos**: representan la estructura y lógica de negocio de las tareas.

**Base de datos**: almacena las tareas en SQLite localmente.
