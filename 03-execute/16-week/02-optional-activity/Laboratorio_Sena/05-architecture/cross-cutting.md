# Decisiones Transversales (Cross-Cutting)

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

Las **decisiones transversales** son aspectos que aplican a todos los microservicios del sistema. Se centralizan aquí para evitar inconsistencias entre servicios.

---

## 1. Logging

**Estándar:** Todos los microservicios usan **SLF4J + Logback** (Java) con formato JSON estructurado.

**Niveles por ambiente:**

| Ambiente | Nivel | Descripción |
|----------|-------|-------------|
| local | DEBUG | Máximo detalle para desarrollo |
| dev | DEBUG | Igual que local |
| qa | INFO | Solo mensajes relevantes |
| prod | WARN | Solo advertencias y errores |

**Campos obligatorios en cada log:**

```json
{
  "timestamp": "2026-07-06T14:30:00.123Z",
  "level": "INFO",
  "service": "horarios-service",
  "traceId": "abc123",
  "message": "Horario creado exitosamente",
  "horarioId": "uuid-del-horario"
}
```

**Restricción:** Los logs **no deben incluir** datos personales (cédulas, correos completos, contraseñas). Ver RNF-008.

---

## 2. Autenticación y autorización

- **Mecanismo:** JWT (JSON Web Token) firmado con HMAC-SHA256.
- **Emisión:** El `usuarios-service` emite el JWT en el endpoint `POST /auth/login`.
- **Validación:** El `api-gateway` valida el JWT en cada petición entrante antes de enrutar al microservicio.
- **Payload del JWT:**

```json
{
  "sub": "uuid-del-usuario",
  "email": "usuario@sena.edu.co",
  "rol": "COORDINADOR",
  "iat": 1720270000,
  "exp": 1720298800
}
```

- **Expiración:** 8 horas (28.800 segundos).
- **Renovación:** No hay refresh token en el MVP; el usuario debe hacer login nuevamente al expirar.

---

## 3. Manejo de errores

Todos los servicios retornan errores en el mismo formato JSON:

```json
{
  "timestamp": "2026-07-06T14:30:00Z",
  "status": 400,
  "error": "Bad Request",
  "code": "HORARIO_CONFLICT",
  "message": "El instructor ya tiene una asignación en ese bloque de tiempo.",
  "path": "/api/horarios",
  "traceId": "abc123"
}
```

**Códigos de error personalizados:** Se documentan en `07-api/error-codes.md`.

**Regla:** Los servicios **nunca** exponen stack traces al cliente. Solo se loguean internamente.

---

## 4. Internacionalización (i18n)

- El sistema opera **únicamente en español (Colombia)**.
- Los mensajes de error y la UI están en español.
- Formato de fechas en la UI: `DD/MM/YYYY`.
- Formato de horas en la UI: `HH:mm` (24h).
- Zona horaria de presentación: `America/Bogota (UTC-5)`.
- Internamente (base de datos, logs): todas las fechas/horas se almacenan en **UTC**.

---

## 5. Validación de inputs

- **Frontend:** Validación en cliente para UX inmediata (no bloquea al servidor).
- **Backend:** Toda validación crítica ocurre en el servidor. El frontend es **no confiable**.
- Se usa **Bean Validation (Jakarta)** en Spring Boot con anotaciones `@NotNull`, `@Size`, `@Email`, etc.
- Los inputs de texto se sanitizan para prevenir XSS antes de persistir.

---

## 6. Correlación de trazas (Trace ID)

Cada petición HTTP entrante recibe un `X-Trace-Id` generado en el API Gateway (UUID v4). Este ID se propaga a todos los microservicios involucrados en la solicitud y se incluye en todos los logs. Facilita el debugging distribuido.

---

## 7. Healthcheck

Todos los microservicios exponen el endpoint:

```
GET /actuator/health
```

Retorna:
```json
{ "status": "UP" }
```

El Docker Compose y el pipeline CI/CD usan este endpoint para verificar disponibilidad antes de enrutar tráfico.
