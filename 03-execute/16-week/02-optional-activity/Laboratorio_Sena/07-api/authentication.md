# Autenticación y Autorización de la API

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Mecanismo de autenticación

El sistema usa **JWT (JSON Web Tokens)** con firma **HMAC-SHA256** para autenticación sin estado.

### Flujo de autenticación

```
Cliente                   API Gateway              usuarios-service
  │                           │                         │
  │ POST /auth/login           │                         │
  │ { email, password }        │                         │
  │──────────────────────────▶│                         │
  │                           │ Ruta pública (sin JWT)  │
  │                           │────────────────────────▶│
  │                           │                         │ Valida credenciales
  │                           │                         │ Genera JWT
  │                           │◀────────────────────────│
  │                           │ { token: "eyJ..." }     │
  │◀──────────────────────────│                         │
  │                           │                         │
  │ GET /api/horarios          │                         │
  │ Authorization: Bearer eyJ..│                         │
  │──────────────────────────▶│                         │
  │                           │ Valida JWT              │
  │                           │ Extrae rol              │
  │                           │ Enruta a horarios-service│
```

---

## Estructura del JWT

**Header:**
```json
{ "alg": "HS256", "typ": "JWT" }
```

**Payload:**
```json
{
  "sub": "uuid-del-usuario",
  "email": "usuario@sena.edu.co",
  "rol": "COORDINADOR",
  "iat": 1720270000,
  "exp": 1720298800
}
```

**Firma:** HMAC-SHA256 del header + payload con el secreto configurado en `JWT_SECRET`.

---

## Política de acceso por endpoint

| Método | Endpoint | Roles permitidos |
|--------|----------|-----------------|
| POST | `/auth/login` | Público |
| GET | `/api/fichas/{codigo}/horarios` | Público (consulta aprendiz) |
| GET | `/api/horarios` | ADMIN, COORDINADOR |
| POST | `/api/horarios` | ADMIN, COORDINADOR |
| PUT | `/api/horarios/{id}` | ADMIN, COORDINADOR |
| DELETE/PATCH estado | `/api/horarios/{id}/cancelar` | ADMIN, COORDINADOR |
| GET | `/api/horarios/instructor/{id}` | ADMIN, COORDINADOR, INSTRUCTOR (propio) |
| GET | `/api/fichas` | ADMIN, COORDINADOR |
| POST | `/api/fichas` | ADMIN, COORDINADOR |
| PUT | `/api/fichas/{id}` | ADMIN, COORDINADOR |
| GET | `/api/instructores` | ADMIN, COORDINADOR |
| POST | `/api/instructores` | ADMIN, COORDINADOR |
| PUT | `/api/instructores/{id}/disponibilidad` | ADMIN, COORDINADOR, INSTRUCTOR (propio) |
| GET | `/api/ambientes` | ADMIN, COORDINADOR |
| POST | `/api/ambientes` | ADMIN, COORDINADOR |
| GET | `/api/usuarios` | ADMIN |
| POST | `/api/usuarios` | ADMIN |
| DELETE | `/api/usuarios/{id}` | ADMIN |
| GET | `/actuator/health` | Público |

---

## Expiración y renovación

- Los JWT expiran en **8 horas** desde su emisión.
- No existe refresh token en el MVP: el usuario debe hacer login nuevamente.
- En versiones futuras se evaluará implementar refresh tokens de larga duración.

---

## Seguridad adicional

- El secreto JWT (`JWT_SECRET`) debe tener al menos 256 bits de entropía.
- El secreto se configura exclusivamente mediante variables de entorno; nunca en código.
- Los endpoints de `actuator` distintos a `/health` están bloqueados en producción.
- Se aplica **rate limiting** en `/auth/login`: máximo 10 intentos por IP por minuto.
