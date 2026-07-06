# Guía de Diseño de la API REST

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Principios generales

La API del sistema de horarios SENA sigue el estilo **REST** con nivel de madurez Richardson Level 2 (recursos + verbos HTTP).

---

## Nomenclatura de rutas

### Reglas

- Las rutas usan **sustantivos en plural** y **kebab-case**.
- Los identificadores de recursos van en el path como parámetro.
- Las acciones que no son CRUD se expresan como sub-recursos.

| Acción | Método | Ruta |
|--------|--------|------|
| Listar horarios | GET | `/api/horarios` |
| Obtener horario | GET | `/api/horarios/{id}` |
| Crear horario | POST | `/api/horarios` |
| Actualizar horario | PUT | `/api/horarios/{id}` |
| Cancelar horario | PATCH | `/api/horarios/{id}/cancelar` |
| Historial de horario | GET | `/api/horarios/{id}/historial` |
| Verificar conflictos | POST | `/api/horarios/verificar-conflicto` |

### Versionado

La API se versiona por prefijo de ruta. La versión actual es `v1`, incluida implícitamente en el path base `/api`. Si se introduce una versión incompatible, se usará `/api/v2/`.

---

## Verbos HTTP

| Verbo | Uso | Respuesta exitosa |
|-------|-----|-------------------|
| `GET` | Consultar recurso(s) | 200 OK |
| `POST` | Crear recurso | 201 Created |
| `PUT` | Reemplazar recurso completo | 200 OK |
| `PATCH` | Modificación parcial o acción | 200 OK |
| `DELETE` | Eliminar recurso | 204 No Content |

---

## Paginación

Todos los endpoints que retornan listas soportan paginación con query params:

```
GET /api/horarios?page=0&size=20&sort=bloqueInicio,asc
```

Respuesta paginada:

```json
{
  "content": [...],
  "page": 0,
  "size": 20,
  "totalElements": 87,
  "totalPages": 5
}
```

---

## Filtros

Los recursos soportan filtrado mediante query params adicionales:

```
GET /api/horarios?fichaId=uuid&semana=2026-W28&estado=ACTIVO
GET /api/horarios?instructorId=uuid&fecha=2026-07-07
```

---

## Formato de respuesta exitosa (único recurso)

```json
{
  "id": "uuid",
  "fichaId": "uuid",
  "instructorId": "uuid",
  "ambienteId": "uuid",
  "competencia": "Construcción de Software",
  "bloqueInicio": "2026-07-07T08:00:00-05:00",
  "bloqueFin": "2026-07-07T10:00:00-05:00",
  "estado": "ACTIVO",
  "creadoEn": "2026-07-06T20:00:00Z"
}
```

---

## Formato de error

Ver `07-api/error-codes.md` para el catálogo completo. Formato estándar:

```json
{
  "timestamp": "2026-07-06T14:30:00Z",
  "status": 409,
  "error": "Conflict",
  "code": "HORARIO_CONFLICT",
  "message": "El instructor ya tiene una asignación de 08:00 a 10:00 el 07/07/2026.",
  "path": "/api/horarios",
  "traceId": "abc123"
}
```

---

## Headers obligatorios

| Header | Tipo | Descripción |
|--------|------|-------------|
| `Authorization` | Request | `Bearer {jwt}` para endpoints protegidos |
| `Content-Type` | Request | `application/json` para POST y PUT |
| `X-Trace-Id` | Response | ID de trazabilidad distribuida (generado por gateway) |

---

## Códigos HTTP usados

| Código | Significado | Cuándo se usa |
|--------|-------------|---------------|
| 200 | OK | GET, PUT, PATCH exitoso |
| 201 | Created | POST exitoso (recurso creado) |
| 204 | No Content | DELETE exitoso |
| 400 | Bad Request | Datos inválidos en el body o query params |
| 401 | Unauthorized | JWT ausente o inválido |
| 403 | Forbidden | JWT válido pero rol sin permiso |
| 404 | Not Found | Recurso no encontrado |
| 409 | Conflict | Conflicto de horario o dato duplicado |
| 500 | Internal Server Error | Error inesperado del servidor |
