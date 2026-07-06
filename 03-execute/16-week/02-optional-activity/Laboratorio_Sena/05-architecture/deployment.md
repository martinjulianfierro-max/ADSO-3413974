# Despliegue del Sistema

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Estrategia de despliegue

El sistema utiliza **contenedores Docker** para todos sus componentes. En desarrollo local se usa **Docker Compose**. Para producción, el equipo evalúa una plataforma de orquestación (ver ADR-003).

---

## Ambientes

| Ambiente | Propósito | Quién despliega | URL de acceso |
|----------|-----------|-----------------|---------------|
| **local** | Desarrollo individual | Cada desarrollador | `localhost:3000` (frontend), `localhost:8080` (gateway) |
| **dev** | Integración continua, rama `dev` | Pipeline CI/CD automático | `dev.horarios-sena.local` |
| **qa** | Pruebas funcionales, rama `qa` | Pipeline CI/CD + QA manual | `qa.horarios-sena.local` |
| **prod** | Producción, rama `main` | Release manual aprobado | `horarios.sena.edu.co` (TBD) |

---

## Diagrama de despliegue (Docker Compose — local/dev)

```
┌────────────────────────────────────────────────────────────────────┐
│  Docker Compose Network: sena-horarios-net                         │
│                                                                    │
│  ┌─────────────┐   ┌──────────────────────────────────────────┐   │
│  │  frontend   │   │  api-gateway                             │   │
│  │  :3000      │──▶│  :8080                                   │   │
│  │  (React)    │   │  (Spring Cloud Gateway / Nginx)          │   │
│  └─────────────┘   └──────┬───────────┬──────────┬────────────┘   │
│                           │           │          │                  │
│                    ┌──────▼──┐  ┌─────▼──┐  ┌───▼──────────────┐  │
│                    │horarios │  │fichas  │  │usuarios          │  │
│                    │:8081    │  │:8082   │  │:8083             │  │
│                    └──┬──────┘  └───┬────┘  └──────────────────┘  │
│                       │             │                │             │
│                    ┌──▼─────────────▼────────────────▼──────────┐  │
│                    │          PostgreSQL :5432                   │  │
│                    │  • horarios_db                             │  │
│                    │  • fichas_db                               │  │
│                    │  • usuarios_db                             │  │
│                    └────────────────────────────────────────────┘  │
│                                                                    │
│  ┌─────────────────────┐   ┌──────────────────────────────────┐   │
│  │  notificaciones     │   │  RabbitMQ :5672 / UI :15672      │   │
│  │  :8084              │◀──│                                  │   │
│  └─────────────────────┘   └──────────────────────────────────┘   │
└────────────────────────────────────────────────────────────────────┘
```

---

## Variables de entorno requeridas

Cada servicio lee su configuración de variables de entorno (no se almacenan credenciales en el repositorio):

| Variable | Servicio | Descripción |
|----------|----------|-------------|
| `DB_HOST` | Todos | Host de PostgreSQL |
| `DB_PORT` | Todos | Puerto de PostgreSQL (default: 5432) |
| `DB_NAME` | Cada servicio | Nombre de su base de datos |
| `DB_USER` | Todos | Usuario de base de datos |
| `DB_PASSWORD` | Todos | Contraseña de base de datos |
| `JWT_SECRET` | `usuarios-service`, `api-gateway` | Secreto para firmar/verificar JWT |
| `JWT_EXPIRATION_MS` | `usuarios-service` | Expiración del token en ms (default: 28800000 = 8h) |
| `RABBITMQ_HOST` | `horarios-service`, `notificaciones-service` | Host de RabbitMQ |
| `RABBITMQ_USER` | ídem | Usuario RabbitMQ |
| `RABBITMQ_PASSWORD` | ídem | Contraseña RabbitMQ |
| `SMTP_HOST` | `notificaciones-service` | Servidor SMTP para emails |
| `SMTP_PORT` | ídem | Puerto SMTP |
| `SMTP_USER` | ídem | Usuario SMTP |
| `SMTP_PASSWORD` | ídem | Contraseña SMTP |

> Los archivos `.env` de cada servicio se documentan en `10-devops/local-setup.md` y **nunca se suben al repositorio** (están en `.gitignore`).

---

## Puertos expuestos

| Servicio | Puerto interno | Puerto host (local) |
|----------|---------------|---------------------|
| frontend | 3000 | 3000 |
| api-gateway | 8080 | 8080 |
| horarios-service | 8081 | 8081 |
| fichas-service | 8082 | 8082 |
| usuarios-service | 8083 | 8083 |
| notificaciones-service | 8084 | 8084 |
| PostgreSQL | 5432 | 5432 |
| RabbitMQ (AMQP) | 5672 | 5672 |
| RabbitMQ (UI) | 15672 | 15672 |
