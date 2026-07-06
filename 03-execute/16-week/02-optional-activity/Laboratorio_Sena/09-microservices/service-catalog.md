# Catálogo de Microservicios

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Servicios del sistema

| Servicio | Responsabilidad | Puerto | Tecnología | Repositorio / Módulo | Equipo dueño |
|---------|----------------|--------|------------|---------------------|--------------|
| `horarios-service` | CRUD de horarios, detección de conflictos, historial de cambios | 8081 | Spring Boot 3 (Java 17) + PostgreSQL | `services/horarios-service/` | Equipo Backend A |
| `fichas-service` | CRUD de fichas de aprendices | 8082 | Spring Boot 3 (Java 17) + PostgreSQL | `services/fichas-service/` | Equipo Backend B |
| `usuarios-service` | Autenticación (JWT), gestión de usuarios, roles y disponibilidad de instructores | 8083 | Spring Boot 3 (Java 17) + PostgreSQL | `services/usuarios-service/` | Equipo Backend B |
| `notificaciones-service` | Envío de emails en respuesta a eventos de dominio | 8084 | Spring Boot 3 (Java 17) + RabbitMQ | `services/notificaciones-service/` | Equipo Backend A |
| `api-gateway` | Enrutamiento, validación JWT, CORS, rate limiting | 8080 | Spring Cloud Gateway | `services/api-gateway/` | Equipo Infra |
| `frontend-web` | Interfaz de usuario para todos los roles | 3000 | React 18 + Vite | `services/frontend-web/` | Equipo Frontend |

---

## Dependencias entre servicios

```
frontend-web ──────────────────────────────▶ api-gateway
                                                  │
                    ┌─────────────────────────────┤
                    │                             │
                    ▼                             ▼
           horarios-service              usuarios-service
                    │                    fichas-service
                    │
                    ▼ (evento)
         notificaciones-service
```

---

## Contratos de API publicados

| Servicio | Archivo OpenAPI | Estado |
|---------|----------------|--------|
| `horarios-service` | `07-api/contracts/horarios-service.yaml` | 🔴 Pendiente |
| `fichas-service` | `07-api/contracts/fichas-service.yaml` | 🔴 Pendiente |
| `usuarios-service` | `07-api/contracts/usuarios-service.yaml` | 🔴 Pendiente |
| `notificaciones-service` | N/A (solo consume eventos) | — |

---

## Estado de implementación

| Servicio | Documentado | Implementado | Desplegado (dev) |
|---------|-------------|--------------|-----------------|
| `horarios-service` | 🔴 | 🔴 | 🔴 |
| `fichas-service` | 🔴 | 🔴 | 🔴 |
| `usuarios-service` | 🔴 | 🔴 | 🔴 |
| `notificaciones-service` | 🔴 | 🔴 | 🔴 |
| `api-gateway` | 🔴 | 🔴 | 🔴 |
| `frontend-web` | 🔴 | 🔴 | 🔴 |
