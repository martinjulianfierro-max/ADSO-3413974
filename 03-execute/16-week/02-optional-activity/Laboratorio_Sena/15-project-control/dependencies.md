# Dependencias Externas

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Dependencias de runtime (producción)

### Backend (Spring Boot — Java 17)

| Librería | Versión | Licencia | Propósito |
|---------|---------|----------|-----------|
| `spring-boot-starter-web` | 3.2.x | Apache 2.0 | API REST |
| `spring-boot-starter-data-jpa` | 3.2.x | Apache 2.0 | Persistencia con JPA/Hibernate |
| `spring-boot-starter-security` | 3.2.x | Apache 2.0 | Seguridad y control de acceso |
| `spring-boot-starter-validation` | 3.2.x | Apache 2.0 | Validación de inputs |
| `spring-boot-starter-amqp` | 3.2.x | Apache 2.0 | Integración con RabbitMQ |
| `spring-boot-starter-actuator` | 3.2.x | Apache 2.0 | Health checks y métricas |
| `spring-cloud-gateway` | 4.x | Apache 2.0 | API Gateway |
| `jjwt-api` + `jjwt-impl` | 0.12.x | Apache 2.0 | Generación y validación de JWT |
| `postgresql` (driver JDBC) | 42.x | BSD-2 | Conexión a PostgreSQL |
| `flyway-core` | 10.x | Apache 2.0 | Migraciones de base de datos |
| `resilience4j-spring-boot3` | 2.x | Apache 2.0 | Circuit Breaker, Retry, Timeout |

### Frontend (React 18)

| Librería | Versión | Licencia | Propósito |
|---------|---------|----------|-----------|
| `react` + `react-dom` | 18.x | MIT | Framework UI |
| `vite` | 5.x | MIT | Build tool y dev server |
| `react-router-dom` | 6.x | MIT | Routing del SPA |
| `axios` | 1.x | MIT | Cliente HTTP |
| `lucide-react` | 0.x | MIT | Íconos |
| `date-fns` | 3.x | MIT | Manejo de fechas y zonas horarias |
| `react-hook-form` | 7.x | MIT | Gestión de formularios |
| `zod` | 3.x | MIT | Validación de esquemas |

---

## Dependencias de infraestructura

| Componente | Versión | Propósito |
|-----------|---------|-----------|
| PostgreSQL | 15.x | Base de datos relacional |
| RabbitMQ | 3.12.x | Message broker (eventos de dominio) |
| Docker | 24.x | Contenedorización |
| Docker Compose | 2.x | Orquestación local |
| GitHub Actions | N/A | CI/CD |

---

## Dependencias de pruebas (testing)

| Librería | Ámbito | Propósito |
|---------|--------|-----------|
| `junit-jupiter` | Backend | Framework de pruebas unitarias |
| `mockito-core` | Backend | Mocking de dependencias |
| `testcontainers-postgresql` | Backend | PostgreSQL real en pruebas de integración |
| `spring-boot-starter-test` | Backend | Soporte de MockMvc y Spring Test |
| `jest` + `@testing-library/react` | Frontend | Pruebas unitarias de componentes |
| `cypress` | E2E | Pruebas end-to-end en navegador |

---

## Servicios externos

| Servicio | Propósito | Alternativa si no está disponible |
|---------|-----------|----------------------------------|
| Servidor SMTP (institucional SENA) | Envío de notificaciones por email | Gmail SMTP (`smtp.gmail.com:587`) con cuenta del proyecto |
| GitHub (repositorio) | Control de versiones y CI/CD | GitLab self-hosted si GitHub no está disponible |

---

## Dependencias institucionales

| Dependencia | Responsable externo | Impacto si no se resuelve |
|------------|---------------------|--------------------------|
| Infraestructura de despliegue (servidor o nube) | Dirección del centro CBA | El MVP no puede desplegarse en producción |
| Cuentas de correo institucional para usuarios | Gestión de TI del SENA | Las notificaciones no pueden enviarse |
| Datos iniciales de fichas e instructores | Coordinación académica | No se puede poblar el sistema para el lanzamiento |
