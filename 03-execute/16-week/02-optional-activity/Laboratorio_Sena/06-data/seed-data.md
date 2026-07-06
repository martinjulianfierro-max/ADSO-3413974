# Datos Semilla (Seed Data)

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

Los datos semilla se cargan automáticamente al iniciar el entorno `local` y `dev` mediante el script `scripts/seed-local.sh`. Permiten al equipo trabajar con datos realistas sin depender de datos de producción.

---

## Usuarios de prueba

| Email | Contraseña | Rol | Descripción |
|-------|-----------|-----|-------------|
| `admin@sena.edu.co` | `Admin1234!` | ADMIN | Administrador del sistema |
| `coordinador@sena.edu.co` | `Coord1234!` | COORDINADOR | Coordinador académico del CBA |
| `carlos.mendez@sena.edu.co` | `Instr1234!` | INSTRUCTOR | Instructor de Desarrollo de Software |
| `laura.gomez@sena.edu.co` | `Instr1234!` | INSTRUCTOR | Instructora de Bases de Datos |
| `aprendiz@sena.edu.co` | `Apr1234!` | APRENDIZ | Aprendiz de la ficha 2879723 |

> ⚠️ Estas contraseñas son solo para entornos de desarrollo. **Nunca usar en producción.**

---

## Fichas de prueba

| Código | Programa | Jornada | Fecha inicio | Fecha fin | Estado |
|--------|---------|---------|-------------|----------|--------|
| `2879723` | Análisis y Desarrollo de Software | DIURNA | 2025-03-01 | 2027-09-01 | ACTIVA |
| `2956841` | Análisis y Desarrollo de Software | TARDE | 2025-06-01 | 2028-01-01 | ACTIVA |
| `2734512` | Programación de Software | NOCTURNA | 2024-09-01 | 2026-03-01 | ACTIVA |

---

## Ambientes de prueba

| Nombre | Tipo | Capacidad | Estado |
|--------|------|-----------|--------|
| Sala de Sistemas 101 | SALA_SISTEMAS | 30 | DISPONIBLE |
| Sala de Sistemas 204 | SALA_SISTEMAS | 25 | DISPONIBLE |
| Aula 305 | AULA | 35 | DISPONIBLE |
| Taller de Redes | LABORATORIO | 20 | DISPONIBLE |
| Plataforma Teams (Virtual) | VIRTUAL | 100 | DISPONIBLE |

---

## Horarios de prueba (semana actual)

| Ficha | Instructor | Ambiente | Competencia | Día | Hora |
|-------|-----------|---------|-------------|-----|------|
| 2879723 | Carlos Méndez | Sala 204 | Construcción de Software | Lunes | 8:00–10:00 |
| 2879723 | Laura Gómez | Sala 101 | Gestión de Bases de Datos | Lunes | 10:00–12:00 |
| 2956841 | Carlos Méndez | Sala 101 | Construcción de Software | Lunes | 14:00–16:00 |

---

## Cómo ejecutar el seed

```bash
# Desde la raíz del proyecto
./scripts/seed-local.sh

# O manualmente con psql
psql -U sena_user -d usuarios_db -f scripts/seed/usuarios.sql
psql -U sena_user -d fichas_db -f scripts/seed/fichas.sql
psql -U sena_user -d horarios_db -f scripts/seed/ambientes.sql
psql -U sena_user -d horarios_db -f scripts/seed/horarios.sql
```

> Los scripts de seed están en `scripts/seed/` en el repositorio de código.
