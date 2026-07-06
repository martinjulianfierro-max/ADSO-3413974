# Pipeline CI/CD

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Herramienta: GitHub Actions

El pipeline de integración y entrega continua se implementa con **GitHub Actions**, usando workflows definidos en `.github/workflows/`.

---

## Workflows definidos

| Workflow | Archivo | Disparador | Descripción |
|---------|---------|------------|-------------|
| CI — Pull Request | `ci-pr.yml` | Push a rama `hu-*` o PR a `dev` | Lint, build y pruebas unitarias |
| CD — Deploy dev | `cd-dev.yml` | Merge a rama `dev` | Build, pruebas, deploy al ambiente dev |
| CD — Deploy qa | `cd-qa.yml` | Merge a rama `qa` | Build, pruebas de integración, deploy qa |
| CD — Deploy prod | `cd-prod.yml` | Merge a `main` (manual) | Build, smoke tests, deploy producción |

---

## Etapas del pipeline (CI-PR)

```
┌─────────┐    ┌─────────┐    ┌───────────────┐    ┌──────────┐
│  Lint   │───▶│  Build  │───▶│  Unit Tests   │───▶│  Report  │
│ Checkstyle│  │ mvn package│ │ mvn test      │    │ Coverage │
│ ESLint  │    │ npm build│  │ Jest (frontend│    │ JaCoCo   │
└─────────┘    └─────────┘    └───────────────┘    └──────────┘
```

**Regla:** Si cualquier etapa falla, el PR no puede ser mergeado a `dev`.

---

## Etapas del pipeline (CD-dev)

```
┌─────────┐   ┌──────────┐   ┌──────────────┐   ┌───────────┐   ┌──────────┐
│  Build  │──▶│  Tests   │──▶│  Docker      │──▶│  Deploy   │──▶│ Smoke    │
│  & Lint │   │  Unit    │   │  Build &     │   │  dev env  │   │ Tests    │
│         │   │  + Integ.│   │  Push to     │   │           │   │          │
│         │   │          │   │  Registry    │   │           │   │          │
└─────────┘   └──────────┘   └──────────────┘   └───────────┘   └──────────┘
```

---

## Configuración de secretos en GitHub

Los siguientes secretos deben configurarse en `Settings → Secrets → Actions` del repositorio:

| Secreto | Descripción |
|---------|-------------|
| `DOCKER_REGISTRY_URL` | URL del registro de contenedores |
| `DOCKER_USERNAME` | Usuario para autenticación en el registry |
| `DOCKER_PASSWORD` | Contraseña del registry |
| `DEV_SERVER_HOST` | IP o hostname del servidor dev |
| `DEV_SERVER_USER` | Usuario SSH del servidor dev |
| `DEV_SERVER_KEY` | Clave privada SSH para deploy |
| `JWT_SECRET_DEV` | Secreto JWT del ambiente dev |
| `DB_PASSWORD_DEV` | Contraseña de la BD en dev |
| `SMTP_PASSWORD_DEV` | Contraseña SMTP en dev |

---

## Calidad mínima exigida para merge

| Métrica | Umbral mínimo |
|---------|---------------|
| Cobertura de pruebas unitarias (backend) | ≥ 80% |
| Pruebas unitarias pasando | 100% |
| Errores de Checkstyle (Java) | 0 |
| Errores de ESLint (Frontend) | 0 |
| Build exitoso de la imagen Docker | Sí |
