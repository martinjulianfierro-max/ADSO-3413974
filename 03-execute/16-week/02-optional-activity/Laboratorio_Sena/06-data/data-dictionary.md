# Diccionario de Datos

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## horarios_db.horarios

| Campo | Tipo | Nullable | Default | Descripción | Ejemplo |
|-------|------|----------|---------|-------------|---------|
| `id` | UUID | NO | gen_random_uuid() | Identificador único del horario | `a1b2c3d4-e5f6-...` |
| `ficha_id` | UUID | NO | — | ID de la ficha asignada (referencia a fichas_db) | `b2c3d4e5-...` |
| `instructor_id` | UUID | NO | — | ID del instructor asignado (referencia a usuarios_db) | `c3d4e5f6-...` |
| `ambiente_id` | UUID | NO | — | ID del ambiente asignado | `d4e5f6a7-...` |
| `competencia` | VARCHAR(255) | NO | — | Nombre de la competencia a impartir | `Construcción de Software` |
| `bloque_inicio` | TIMESTAMPTZ | NO | — | Inicio del bloque en UTC | `2026-07-07T13:00:00Z` |
| `bloque_fin` | TIMESTAMPTZ | NO | — | Fin del bloque en UTC | `2026-07-07T15:00:00Z` |
| `estado` | VARCHAR(20) | NO | `ACTIVO` | Estado del horario: `ACTIVO`, `CANCELADO`, `MODIFICADO` | `ACTIVO` |
| `creado_por` | UUID | NO | — | ID del coordinador que creó el registro | `e5f6a7b8-...` |
| `creado_en` | TIMESTAMPTZ | NO | NOW() | Timestamp de creación | `2026-07-06T20:00:00Z` |
| `actualizado_en` | TIMESTAMPTZ | NO | NOW() | Última actualización | `2026-07-06T20:00:00Z` |

---

## horarios_db.ambientes

| Campo | Tipo | Nullable | Default | Descripción | Ejemplo |
|-------|------|----------|---------|-------------|---------|
| `id` | UUID | NO | gen_random_uuid() | Identificador único | `f6a7b8c9-...` |
| `nombre` | VARCHAR(100) | NO | — | Nombre del ambiente (único) | `Sala de Sistemas 204` |
| `tipo` | VARCHAR(30) | NO | — | Tipo: `AULA`, `LABORATORIO`, `TALLER`, `SALA_SISTEMAS`, `VIRTUAL` | `SALA_SISTEMAS` |
| `capacidad` | SMALLINT | NO | — | Máximo de personas permitidas | `25` |
| `estado` | VARCHAR(20) | NO | `DISPONIBLE` | Estado: `DISPONIBLE`, `EN_MANTENIMIENTO`, `INACTIVO` | `DISPONIBLE` |
| `creado_en` | TIMESTAMPTZ | NO | NOW() | Timestamp de creación | `2026-07-01T10:00:00Z` |

---

## horarios_db.historial_cambios

| Campo | Tipo | Nullable | Default | Descripción | Ejemplo |
|-------|------|----------|---------|-------------|---------|
| `id` | UUID | NO | gen_random_uuid() | Identificador único de la entrada | — |
| `horario_id` | UUID | NO | — | FK → horarios.id | — |
| `campo_modificado` | VARCHAR(100) | NO | — | Nombre del campo que cambió | `ambiente_id` |
| `valor_anterior` | TEXT | YES | — | Valor antes del cambio (serializado) | `d4e5f6a7-...` |
| `valor_nuevo` | TEXT | YES | — | Valor después del cambio | `e5f6a7b8-...` |
| `modificado_por` | UUID | NO | — | ID del usuario que hizo el cambio | `coord-001` |
| `modificado_en` | TIMESTAMPTZ | NO | NOW() | Timestamp del cambio | `2026-07-06T21:00:00Z` |

---

## fichas_db.fichas

| Campo | Tipo | Nullable | Default | Descripción | Ejemplo |
|-------|------|----------|---------|-------------|---------|
| `id` | UUID | NO | gen_random_uuid() | Identificador único | — |
| `codigo` | VARCHAR(7) | NO | — | Código oficial SENA (7 dígitos, único) | `2879723` |
| `programa` | VARCHAR(255) | NO | — | Nombre del programa de formación | `Análisis y Desarrollo de Software` |
| `jornada` | VARCHAR(20) | NO | — | Jornada: `DIURNA`, `TARDE`, `NOCTURNA` | `DIURNA` |
| `fecha_inicio` | DATE | NO | — | Inicio de la formación | `2025-03-01` |
| `fecha_fin` | DATE | NO | — | Fin estimado de la formación | `2027-09-01` |
| `estado` | VARCHAR(20) | NO | `ACTIVA` | Estado: `ACTIVA`, `INACTIVA` | `ACTIVA` |
| `creado_en` | TIMESTAMPTZ | NO | NOW() | Timestamp de creación | — |

---

## usuarios_db.usuarios

| Campo | Tipo | Nullable | Default | Descripción | Ejemplo |
|-------|------|----------|---------|-------------|---------|
| `id` | UUID | NO | gen_random_uuid() | Identificador único | — |
| `nombre` | VARCHAR(255) | NO | — | Nombre completo | `Carlos Méndez López` |
| `cedula` | VARCHAR(10) | NO | — | Número de cédula colombiana (único) | `1030456789` |
| `email` | VARCHAR(255) | NO | — | Correo institucional (único) | `cmendez@sena.edu.co` |
| `password_hash` | VARCHAR(255) | NO | — | Hash bcrypt de la contraseña | `$2a$12$...` |
| `rol` | VARCHAR(20) | NO | — | Rol en el sistema | `INSTRUCTOR` |
| `tipo_vinculacion` | VARCHAR(20) | YES | NULL | Solo para instructores: `PLANTA`, `CONTRATISTA` | `CONTRATISTA` |
| `estado` | VARCHAR(20) | NO | `ACTIVO` | Estado de la cuenta | `ACTIVO` |
| `creado_en` | TIMESTAMPTZ | NO | NOW() | — | — |
