# Patrones de Comunicación entre Microservicios

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Comunicación síncrona (REST)

Se usa para operaciones en las que el cliente necesita una respuesta **inmediata** para continuar su flujo.

| Llamada | Origen | Destino | Endpoint |
|---------|--------|---------|----------|
| Verificar existencia de ficha | `horarios-service` | `fichas-service` | `GET /api/fichas/{id}` |
| Verificar existencia de instructor | `horarios-service` | `usuarios-service` | `GET /api/instructores/{id}` |
| Validar token JWT | `api-gateway` | `usuarios-service` | Interno (shared secret) |

**Consideraciones:**
- Timeout: máximo 3 segundos por llamada entre servicios.
- Si el servicio destino no responde, se retorna error 503 al cliente con mensaje claro.
- Se aplica patrón **Circuit Breaker** (Resilience4j) en `horarios-service` para las llamadas a `fichas-service` y `usuarios-service`.

---

## Comunicación asíncrona (Eventos — RabbitMQ)

Se usa para **side effects** que no bloquean la respuesta principal: notificaciones, logs de auditoría, actualizaciones de caché.

**Broker:** RabbitMQ (MVP). Se evalúa Apache Kafka para versiones con mayor volumen de eventos.

### Exchanges y colas

| Exchange | Tipo | Cola suscrita | Servicio consumidor |
|----------|------|---------------|---------------------|
| `sena.horarios` | Direct | `notificaciones.horarios` | `notificaciones-service` |
| `sena.fichas` | Direct | `notificaciones.fichas` | `notificaciones-service` |

### Routing keys

| Evento | Routing key |
|--------|-------------|
| `HorarioCreado` | `horario.created` |
| `HorarioModificado` | `horario.updated` |
| `HorarioCancelado` | `horario.cancelled` |
| `FichaInactivada` | `ficha.inactivated` |

### Garantías de entrega

- Los mensajes se publican con `persistent: true` (sobreviven reinicios del broker).
- `notificaciones-service` usa ACK manual: solo confirma el mensaje al broker después de enviarlo exitosamente.
- Si el envío falla, el mensaje vuelve a la cola para reintento (hasta 3 veces). Después pasa a una **Dead Letter Queue (DLQ)**.

---

## Patrones de resiliencia

### Circuit Breaker (Resilience4j)

Aplicado en `horarios-service` para llamadas a servicios externos:

| Configuración | Valor |
|--------------|-------|
| Umbral de apertura | 50% de fallos en ventana de 10 llamadas |
| Tiempo en estado abierto | 30 segundos |
| Llamadas de prueba en semi-abierto | 3 |

**Comportamiento cuando el circuito está abierto:** retorna inmediatamente con error 503 y mensaje "Servicio temporalmente no disponible."

### Retry

Para llamadas REST entre servicios: máximo **3 reintentos** con backoff exponencial (1s, 2s, 4s).

### Timeout

Timeout de 3 segundos en todas las llamadas HTTP entre microservicios.

---

## Patrón Saga (futuro)

Para operaciones que involucran múltiples servicios (ej: crear horario + notificar + actualizar catálogo), se evaluará implementar el patrón **Saga coreografiado** basado en eventos en fases posteriores del proyecto.
