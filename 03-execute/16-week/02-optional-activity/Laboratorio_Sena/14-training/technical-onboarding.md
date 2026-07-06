# Onboarding Técnico para Nuevos Desarrolladores

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Bienvenida

Bienvenido al equipo del Sistema de Horarios SENA. Este documento te guiará para configurar tu entorno de desarrollo y entender la arquitectura del proyecto en el menor tiempo posible.

---

## Paso 1: Leer la documentación base (< 1 hora)

Antes de escribir una sola línea de código, lee estos documentos en orden:

1. [`README.md`](../README.md) — Vista general del repositorio.
2. [`01-context/overview.md`](../01-context/overview.md) — Qué es el sistema y por qué existe.
3. [`01-context/scope.md`](../01-context/scope.md) — Qué hace y qué no hace el sistema.
4. [`02-domain/entities-and-rules.md`](../02-domain/entities-and-rules.md) — Las entidades y reglas de negocio que vas a programar.
5. [`05-architecture/overview.md`](../05-architecture/overview.md) — La arquitectura del sistema.
6. [`00-governance/git-conventions.md`](../00-governance/git-conventions.md) — Cómo trabaja el equipo con Git.

---

## Paso 2: Configurar el entorno local (30-60 min)

Sigue la guía completa en [`10-devops/local-setup.md`](../10-devops/local-setup.md).

**Resumen rápido:**

```bash
# Clonar
git clone https://github.com/<org>/sena-horarios.git
cd sena-horarios

# Configurar .env para cada servicio
cp services/horarios-service/.env.example services/horarios-service/.env
# (repetir para cada servicio)

# Levantar infraestructura
docker compose up -d

# Verificar
curl http://localhost:8080/actuator/health
```

---

## Paso 3: Entender la estructura del proyecto

```
sena-horarios/
├── 00-governance/       ← Reglas del equipo (leer primero)
├── 01-context/          ← Contexto institucional y alcance
├── 02-domain/           ← Modelo de dominio y reglas de negocio
├── 03-product/          ← Visión, roadmap y backlog
├── 04-requirements/     ← RF, RNF, historias de usuario
├── 05-architecture/     ← Arquitectura y ADRs
├── 06-data/             ← Modelos de BD y migraciones
├── 07-api/              ← Contratos OpenAPI y guías REST
├── 08-uml/              ← Diagramas UML
├── 09-microservices/    ← Catálogo de servicios
├── 10-devops/           ← CI/CD, ambientes, setup local
├── 11-quality/          ← Testing y code review
├── 12-ux-ui/            ← Sistema de diseño y wireframes
├── 13-operations/       ← Observabilidad e incidentes
├── 14-training/         ← Manuales de usuario
├── 15-project-control/  ← Riesgos, dependencias, backlog técnico
└── services/            ← Código fuente de los microservicios
    ├── horarios-service/
    ├── fichas-service/
    ├── usuarios-service/
    ├── notificaciones-service/
    └── frontend-web/
```

---

## Paso 4: Ejecutar las pruebas

```bash
# Pruebas unitarias del backend
cd services/horarios-service
mvn test

# Pruebas del frontend
cd services/frontend-web
npm test
```

Asegúrate de que **todas las pruebas pasen** antes de empezar a modificar código.

---

## Paso 5: Tu primera tarea

1. Busca en los **Issues de GitHub** una tarea con etiqueta `good-first-issue`.
2. Asígnatela a ti mismo.
3. Crea tu rama siguiendo las convenciones: `hu-{N}-dev` o `feat/doc-{descripcion}`.
4. Desarrolla el cambio, escribe las pruebas y abre un PR hacia `dev`.
5. Solicita revisión a tu compañero.

---

## Recursos útiles

| Recurso | URL |
|---------|-----|
| Spring Boot Docs | https://docs.spring.io/spring-boot/docs/current/reference/html/ |
| React Docs | https://react.dev/ |
| PlantUML | https://plantuml.com/ |
| Conventional Commits | https://www.conventionalcommits.org/ |
| Flyway Docs | https://documentation.red-gate.com/fd |
| RabbitMQ Tutorials | https://www.rabbitmq.com/tutorials/ |

---

## Contacto del equipo

- **Líder técnico:** (definir por el equipo)
- **Canal de comunicación:** (WhatsApp / Discord del equipo)
- **Issues y PRs:** GitHub del repositorio
