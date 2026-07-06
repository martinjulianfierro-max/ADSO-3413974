# Backlog Técnico

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

El backlog técnico registra la **deuda técnica identificada**, mejoras de arquitectura pendientes y refactorizaciones planeadas. No es deuda "mala"; es trabajo técnico necesario que se pospone de forma consciente para cumplir plazos del MVP.

---

## Deuda técnica activa

| ID | Descripción | Impacto | Urgencia | Origen |
|----|-------------|---------|---------|--------|
| TD-001 | No hay refresh token; el usuario debe hacer login cada 8h | UX degradada para usuarios frecuentes | Baja — aceptable en MVP | Decisión de alcance |
| TD-002 | Los servicios se comunican por REST síncrono para verificar existencia; esto crea acoplamiento temporal | Fragilidad ante caídas | Media | Restricción de tiempo |
| TD-003 | El API Gateway no implementa rate limiting completo en MVP; solo para login | Riesgo de abuso | Baja | Restricción de tiempo |
| TD-004 | No hay caché de respuestas frecuentes (listado de fichas, instructores) | Rendimiento en picos | Baja | Complejidad |
| TD-005 | Las imágenes Docker no usan multi-stage build; son más pesadas de lo óptimo | Mayor tiempo de build y deploy | Baja | Falta de tiempo |
| TD-006 | No hay documentación de Swagger/OpenAPI generada automáticamente | Dificulta el consumo de la API | Media | Pendiente de implementación |

---

## Mejoras planificadas (post-MVP)

| ID | Mejora | Fase objetivo | Descripción |
|----|--------|--------------|-------------|
| MEJ-001 | Implementar refresh tokens | Fase 2 | Mejorar UX permitiendo sesiones más largas sin login repetido |
| MEJ-002 | Agregar caché Redis para consultas frecuentes | Fase 2 | Reducir carga en BD para listados de fichas e instructores |
| MEJ-003 | Migrar de RabbitMQ a Apache Kafka | Fase 3 | Mayor throughput y garantías de orden de eventos si el volumen crece |
| MEJ-004 | Implementar Circuit Breaker en todos los servicios | Fase 2 | Completar la resiliencia en `fichas-service` y `notificaciones-service` |
| MEJ-005 | Generar documentación OpenAPI automática con Springdoc | Fase 1 (fin) | Publicar Swagger UI en `/api-docs` |
| MEJ-006 | Internacionalizar los mensajes de error | Fase 3 | Preparar el sistema para potencial expansión a otros centros |
| MEJ-007 | Implementar exportación de horarios a PDF/Excel | Fase 2 | Solicitud frecuente de los coordinadores |

---

## Refactorizaciones identificadas

| ID | Archivo/Módulo | Problema | Solución propuesta |
|----|---------------|---------|-------------------|
| REF-001 | `horarios-service` → validación de conflictos | La lógica de validación está en el service; debería estar en el dominio | Mover la lógica al agregado `Horario` |
| REF-002 | `usuarios-service` → gestión de disponibilidad | La disponibilidad mezcla lógica de usuario y de horarios | Considerar moverla a `horarios-service` |
| REF-003 | Frontend → llamadas a API | Las llamadas están dispersas en componentes; no hay capa de API centralizada | Crear un módulo `api/` con todos los clients de cada servicio |

---

## Proceso para agregar ítems al backlog técnico

Cualquier miembro del equipo puede agregar un ítem si:
1. Identifica una deuda técnica o mejora necesaria.
2. Crea un issue en GitHub con la etiqueta `tech-debt` o `improvement`.
3. Agrega el ítem a esta tabla en el siguiente PR de documentación.

Los ítems se revisan y priorizan en la reunión de refinamiento de cada iteración.
