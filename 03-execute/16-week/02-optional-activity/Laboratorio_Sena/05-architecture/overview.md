# Vista General de Arquitectura

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Estilo arquitectónico

El sistema de horarios SENA adopta una **arquitectura de microservicios** con comunicación mayoritariamente **REST síncrona** entre servicios y **mensajería asíncrona** (eventos de dominio) para notificaciones.

Se eligió este estilo para:
- Permitir que cada bounded context evolucione de forma independiente.
- Facilitar el despliegue y escala independiente de cada componente.
- Preparar el sistema para futuras integraciones (Territorium, SOFIA Plus).

> Ver decisión de arquitectura: [ADR-001](decisions/records/ADR-001-estilo-arquitectonico.md)

---

## Diagrama de alto nivel (C4 — Nivel Contexto)

```
                          ┌───────────────────────────────┐
                          │   Sistema de Horarios SENA    │
                          │                               │
   [Coordinador] ────────▶│  API Gateway (puerto 8080)    │
   [Instructor]  ────────▶│                               │
   [Aprendiz]    ────────▶│  • horarios-service  :8081    │
                          │  • fichas-service    :8082    │
                          │  • usuarios-service  :8083    │
                          │  • notificaciones    :8084    │
                          │                               │
                          │  PostgreSQL :5432             │
                          │  Message Broker (futuro)      │
                          └───────────────────────────────┘
                                        │
                                        │ SMTP
                                        ▼
                                [Servidor de correo]
```

---

## Componentes principales

| Componente | Tecnología | Responsabilidad |
|-----------|------------|-----------------|
| **Frontend Web** | React 18 + Vite | Interfaz de usuario para todos los roles |
| **API Gateway** | Spring Cloud Gateway (o Nginx) | Enrutamiento, autenticación JWT, CORS |
| `horarios-service` | Spring Boot 3 (Java 17) | CRUD de horarios, detección de conflictos |
| `fichas-service` | Spring Boot 3 (Java 17) | CRUD de fichas |
| `usuarios-service` | Spring Boot 3 (Java 17) | Autenticación, roles, gestión de instructores |
| `notificaciones-service` | Spring Boot 3 (Java 17) | Envío de emails en respuesta a eventos |
| **Base de datos** | PostgreSQL 15 | Persistencia relacional (una BD por servicio) |
| **Message Broker** | RabbitMQ (MVP) | Cola de eventos entre microservicios |

---

## Principios arquitectónicos aplicados

1. **Database per service:** Cada microservicio tiene su propia base de datos. No se permiten joins entre servicios.
2. **API First:** Los contratos OpenAPI se definen antes de implementar.
3. **Fail fast:** Las validaciones críticas (conflictos de horario) se ejecutan en el servidor, no solo en el cliente.
4. **Event-driven para side effects:** Las notificaciones se disparan como reacción a eventos, no como llamadas directas.
5. **Stateless services:** Los servicios no guardan estado de sesión; el estado de auth viaja en el JWT.

---

## Flujo típico: Crear un horario

```
Frontend (React)
    │ POST /api/horarios
    ▼
API Gateway
    │ Valida JWT → extrae rol y userId
    │ Enruta a horarios-service
    ▼
horarios-service
    │ Valida datos (RN-H01 a RN-H05)
    │ Consulta fichas-service y usuarios-service para verificar existencia
    │ Persiste en PostgreSQL (horarios_db)
    │ Publica evento HorarioCreado en RabbitMQ
    ▼
notificaciones-service (consume evento)
    │ Construye email con plantilla
    │ Envía por SMTP al instructor
    ▼
[Respuesta 201 Created al frontend]
```
