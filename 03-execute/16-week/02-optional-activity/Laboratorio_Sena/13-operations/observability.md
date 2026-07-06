# Observabilidad del Sistema

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Stack de observabilidad

| Pilar | Herramienta | Propósito |
|-------|------------|-----------|
| **Logging** | SLF4J + Logback (JSON) → consola → (futuro: Loki + Grafana) | Registrar eventos y errores de cada servicio |
| **Métricas** | Spring Boot Actuator → (futuro: Prometheus + Grafana) | Monitorear latencia, errores, uso de recursos |
| **Trazabilidad** | X-Trace-Id propagado por headers | Correlacionar una solicitud a través de múltiples servicios |
| **Health checks** | `/actuator/health` en cada servicio | Verificar disponibilidad de cada componente |

---

## Logging

### Formato estándar

Todos los microservicios emiten logs en formato JSON estructurado:

```json
{
  "timestamp": "2026-07-06T14:30:00.123Z",
  "level": "INFO",
  "service": "horarios-service",
  "traceId": "abc-123-def",
  "message": "Horario creado",
  "horarioId": "uuid",
  "fichaId": "2879723",
  "durationMs": 145
}
```

### Qué se registra obligatoriamente

| Evento | Nivel |
|--------|-------|
| Inicio y fin de cada request HTTP | INFO |
| Errores de validación (400) | WARN |
| Errores de negocio (409) | WARN |
| Errores no esperados (500) | ERROR |
| Intentos de acceso no autorizado (401, 403) | WARN |
| Eventos de dominio publicados | INFO |
| Inicio/parada del servicio | INFO |

### Qué NO se registra

- Contraseñas ni hashes.
- Cédulas o números de identificación completos.
- Correos electrónicos completos (solo el dominio, si es necesario).
- Tokens JWT completos.

---

## Métricas (MVP — Spring Boot Actuator)

En el MVP, las métricas se exponen vía `/actuator/metrics` para consumo manual o integración futura con Prometheus.

**Métricas clave a monitorear:**

| Métrica | Descripción |
|---------|-------------|
| `http.server.requests` | Latencia y tasa de errores por endpoint |
| `jvm.memory.used` | Uso de heap JVM |
| `hikaricp.connections.active` | Conexiones activas a PostgreSQL |
| `rabbitmq.consumed` | Mensajes consumidos de RabbitMQ |
| `custom.horarios.creados` | Contador de horarios creados (métrica de negocio) |

---

## Alertas (futuro)

En fases posteriores se configurarán alertas automáticas para:

- Tasa de errores HTTP 5xx > 5% en ventana de 5 minutos.
- Tiempo de respuesta p95 > 2 segundos sostenido por 5 minutos.
- Servicio sin health check exitoso por más de 30 segundos.
- Dead Letter Queue con más de 10 mensajes acumulados.

---

## Dashboard de monitoreo (futuro)

Se planifica un dashboard en Grafana con los siguientes paneles:

1. **Latencia por servicio** (p50, p95, p99).
2. **Tasa de errores por endpoint**.
3. **Horarios creados/modificados/cancelados por día**.
4. **Uso de memoria y CPU por contenedor**.
5. **Estado de health checks** (semáforo por servicio).
