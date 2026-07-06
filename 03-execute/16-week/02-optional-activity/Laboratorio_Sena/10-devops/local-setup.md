# Configuración del Entorno Local

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Prerrequisitos

Antes de levantar el proyecto en local, instala las siguientes herramientas:

| Herramienta | Versión mínima | Verificación |
|------------|---------------|--------------|
| Docker Desktop | 24.x | `docker --version` |
| Docker Compose | 2.x (incluido con Docker Desktop) | `docker compose version` |
| Java JDK | 17 | `java -version` |
| Maven | 3.9.x | `mvn -v` |
| Node.js | 18.x LTS | `node --version` |
| Git | 2.40.x | `git --version` |

---

## Clonar el repositorio

```bash
git clone https://github.com/<org>/sena-horarios.git
cd sena-horarios
```

---

## Configurar variables de entorno

Cada microservicio tiene un archivo `.env.example` en su carpeta. Crea un `.env` a partir del ejemplo:

```bash
# Para cada servicio:
cp services/horarios-service/.env.example services/horarios-service/.env
cp services/fichas-service/.env.example services/fichas-service/.env
cp services/usuarios-service/.env.example services/usuarios-service/.env
cp services/notificaciones-service/.env.example services/notificaciones-service/.env
```

> ⚠️ **Nunca** subas los archivos `.env` al repositorio. Ya están en `.gitignore`.

**Variables clave a configurar:**

```env
# Ejemplo para usuarios-service/.env
DB_HOST=localhost
DB_PORT=5432
DB_NAME=usuarios_db
DB_USER=sena_user
DB_PASSWORD=sena_pass_local
JWT_SECRET=mi_secreto_de_al_menos_32_caracteres
JWT_EXPIRATION_MS=28800000
```

---

## Levantar la infraestructura con Docker Compose

```bash
# Desde la raíz del repositorio:
docker compose up -d postgres rabbitmq

# Verificar que los servicios estén corriendo:
docker compose ps
```

Espera a que PostgreSQL y RabbitMQ estén en estado `healthy` antes de continuar.

---

## Ejecutar las migraciones de base de datos

Las migraciones se ejecutan automáticamente al iniciar cada microservicio con Spring Boot + Flyway.

Si quieres aplicarlas manualmente:

```bash
cd services/horarios-service
mvn flyway:migrate
```

---

## Iniciar los microservicios

**Opción A — Docker Compose (recomendado):**

```bash
docker compose up --build
```

**Opción B — Ejecución individual (para desarrollo):**

```bash
# Terminal 1 — horarios-service
cd services/horarios-service
mvn spring-boot:run

# Terminal 2 — fichas-service
cd services/fichas-service
mvn spring-boot:run

# Terminal 3 — usuarios-service
cd services/usuarios-service
mvn spring-boot:run

# Terminal 4 — notificaciones-service
cd services/notificaciones-service
mvn spring-boot:run
```

---

## Iniciar el frontend

```bash
cd services/frontend-web
npm install
npm run dev
```

El frontend estará disponible en: `http://localhost:3000`

---

## Verificar que todo funciona

```bash
# Health check del API Gateway
curl http://localhost:8080/actuator/health

# Health check de un servicio específico
curl http://localhost:8081/actuator/health

# Interfaz de RabbitMQ
open http://localhost:15672  # user: guest, password: guest
```

---

## Cargar datos de prueba (seed)

```bash
# Ejecutar el seed desde el script incluido:
./scripts/seed-local.sh
```

Este script crea:
- 1 usuario administrador (`admin@sena.edu.co` / `Admin1234!`)
- 1 coordinador (`coordinador@sena.edu.co` / `Coord1234!`)
- 2 instructores de prueba
- 3 fichas activas
- 5 ambientes

---

## Solución de problemas comunes

| Problema | Causa probable | Solución |
|----------|---------------|----------|
| `Connection refused` al iniciar servicio | PostgreSQL no está listo | Esperar el healthcheck o ejecutar `docker compose up postgres` primero |
| `JWT_SECRET is required` | Variable de entorno no configurada | Revisar el archivo `.env` del servicio |
| Puerto 8080 ya en uso | Otro proceso en el mismo puerto | Cambiar el puerto en `docker-compose.yml` o detener el proceso |
| Migraciones fallidas | Esquema inconsistente | Borrar la BD y volver a crear: `docker compose down -v && docker compose up` |
