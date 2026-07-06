# Entornos del Sistema

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Ambientes definidos

### local

| Atributo | Valor |
|----------|-------|
| **Propósito** | Desarrollo individual en máquina local |
| **Rama Git** | Cualquier rama de trabajo (`hu-*`, `feat/*`) |
| **URL frontend** | `http://localhost:3000` |
| **URL API Gateway** | `http://localhost:8080` |
| **Base de datos** | PostgreSQL en Docker (`localhost:5432`) |
| **Datos** | Seed de datos de prueba cargados manualmente |
| **Quien despliega** | Cada desarrollador (Docker Compose) |
| **Logs** | Nivel DEBUG en consola |

---

### dev

| Atributo | Valor |
|----------|-------|
| **Propósito** | Integración continua; prueba de cambios integrados |
| **Rama Git** | `dev` |
| **URL frontend** | `http://dev.horarios-sena.local` (red interna) |
| **URL API Gateway** | `http://dev.horarios-sena.local:8080` |
| **Base de datos** | PostgreSQL en servidor compartido del equipo |
| **Datos** | Seed de datos de prueba, reiniciado en cada deploy |
| **Quien despliega** | Pipeline CI/CD automático al hacer merge a `dev` |
| **Logs** | Nivel DEBUG |

---

### qa

| Atributo | Valor |
|----------|-------|
| **Propósito** | Pruebas funcionales y de aceptación |
| **Rama Git** | `qa` |
| **URL frontend** | `http://qa.horarios-sena.local` (red interna) |
| **URL API Gateway** | `http://qa.horarios-sena.local:8080` |
| **Base de datos** | PostgreSQL dedicado para QA (datos más estables) |
| **Datos** | Dataset de prueba fijo + datos generados por QA |
| **Quien despliega** | Pipeline CI/CD semiautomático (requiere aprobación) |
| **Logs** | Nivel INFO |

---

### prod

| Atributo | Valor |
|----------|-------|
| **Propósito** | Ambiente de producción — Centro CBA SENA |
| **Rama Git** | `main` |
| **URL frontend** | `https://horarios.sena.edu.co` (TBD) |
| **URL API Gateway** | `https://api.horarios.sena.edu.co` (TBD) |
| **Base de datos** | PostgreSQL con backups diarios |
| **Datos** | Datos reales de fichas, instructores y horarios del CBA |
| **Quien despliega** | Release manual con aprobación del líder técnico |
| **Logs** | Nivel WARN |
| **HTTPS** | Obligatorio — certificado TLS configurado |

---

## Variables de entorno por ambiente

Cada ambiente tiene su propio conjunto de variables de entorno gestionadas como **secretos en GitHub Actions** (para dev, qa, prod) o en archivos `.env` locales (para local). Ver `10-devops/local-setup.md` para detalles del ambiente local.

---

## Diferencias clave entre ambientes

| Característica | local | dev | qa | prod |
|----------------|-------|-----|----|------|
| HTTPS | ❌ | ❌ | ❌ | ✅ |
| Datos reales | ❌ | ❌ | ❌ | ✅ |
| Deploy automático | ❌ | ✅ | Parcial | ❌ |
| Nivel de log | DEBUG | DEBUG | INFO | WARN |
| Rate limiting activo | ❌ | Parcial | ✅ | ✅ |
