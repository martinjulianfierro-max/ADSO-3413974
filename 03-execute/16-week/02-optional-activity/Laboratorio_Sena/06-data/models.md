# Modelos de Datos

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Modelo Entidad-Relación (ER)

Cada microservicio tiene su propia base de datos. A continuación se documenta el modelo de cada una.

---

### horarios_db — Servicio de Horarios

```
┌─────────────────┐        ┌──────────────────────┐
│    horarios     │        │  historial_cambios    │
├─────────────────┤        ├──────────────────────┤
│ id (UUID) PK    │◀───────│ id (UUID) PK          │
│ ficha_id (UUID) │        │ horario_id (UUID) FK  │
│ instructor_id   │        │ campo_modificado      │
│ ambiente_id     │        │ valor_anterior        │
│ competencia     │        │ valor_nuevo           │
│ bloque_inicio   │        │ modificado_por (UUID) │
│ bloque_fin      │        │ modificado_en         │
│ estado          │        └──────────────────────┘
│ creado_por      │
│ creado_en       │        ┌──────────────────────┐
│ actualizado_en  │        │    ambientes          │
└─────────────────┘        ├──────────────────────┤
                           │ id (UUID) PK          │
                           │ nombre (UNIQUE)       │
                           │ tipo                  │
                           │ capacidad             │
                           │ estado                │
                           │ creado_en             │
                           └──────────────────────┘
```

**Tabla `horarios`:**

| Columna | Tipo | Restricciones |
|---------|------|---------------|
| `id` | UUID | PK, NOT NULL |
| `ficha_id` | UUID | NOT NULL (ref. externa a fichas_db) |
| `instructor_id` | UUID | NOT NULL (ref. externa a usuarios_db) |
| `ambiente_id` | UUID | NOT NULL, FK → ambientes.id |
| `competencia` | VARCHAR(255) | NOT NULL |
| `bloque_inicio` | TIMESTAMPTZ | NOT NULL |
| `bloque_fin` | TIMESTAMPTZ | NOT NULL, CHECK (bloque_fin > bloque_inicio) |
| `estado` | VARCHAR(20) | NOT NULL, DEFAULT 'ACTIVO', CHECK IN ('ACTIVO','CANCELADO','MODIFICADO') |
| `creado_por` | UUID | NOT NULL |
| `creado_en` | TIMESTAMPTZ | NOT NULL, DEFAULT NOW() |
| `actualizado_en` | TIMESTAMPTZ | NOT NULL, DEFAULT NOW() |

---

### fichas_db — Servicio de Fichas

**Tabla `fichas`:**

| Columna | Tipo | Restricciones |
|---------|------|---------------|
| `id` | UUID | PK, NOT NULL |
| `codigo` | VARCHAR(7) | NOT NULL, UNIQUE |
| `programa` | VARCHAR(255) | NOT NULL |
| `jornada` | VARCHAR(20) | NOT NULL, CHECK IN ('DIURNA','TARDE','NOCTURNA') |
| `fecha_inicio` | DATE | NOT NULL |
| `fecha_fin` | DATE | NOT NULL, CHECK (fecha_fin > fecha_inicio) |
| `estado` | VARCHAR(20) | NOT NULL, DEFAULT 'ACTIVA', CHECK IN ('ACTIVA','INACTIVA') |
| `creado_en` | TIMESTAMPTZ | NOT NULL, DEFAULT NOW() |

---

### usuarios_db — Servicio de Usuarios

**Tabla `usuarios`:**

| Columna | Tipo | Restricciones |
|---------|------|---------------|
| `id` | UUID | PK, NOT NULL |
| `nombre` | VARCHAR(255) | NOT NULL |
| `cedula` | VARCHAR(10) | NOT NULL, UNIQUE |
| `email` | VARCHAR(255) | NOT NULL, UNIQUE |
| `password_hash` | VARCHAR(255) | NOT NULL |
| `rol` | VARCHAR(20) | NOT NULL, CHECK IN ('ADMIN','COORDINADOR','INSTRUCTOR','APRENDIZ') |
| `tipo_vinculacion` | VARCHAR(20) | NULLABLE, CHECK IN ('PLANTA','CONTRATISTA') |
| `estado` | VARCHAR(20) | NOT NULL, DEFAULT 'ACTIVO' |
| `creado_en` | TIMESTAMPTZ | NOT NULL, DEFAULT NOW() |

**Tabla `disponibilidad`:**

| Columna | Tipo | Restricciones |
|---------|------|---------------|
| `id` | UUID | PK |
| `instructor_id` | UUID | NOT NULL, FK → usuarios.id |
| `dia_semana` | SMALLINT | NOT NULL, CHECK (dia_semana BETWEEN 1 AND 6) |
| `hora_inicio` | TIME | NOT NULL |
| `hora_fin` | TIME | NOT NULL |

---

### notificaciones_db — Servicio de Notificaciones

**Tabla `notificaciones`:**

| Columna | Tipo | Restricciones |
|---------|------|---------------|
| `id` | UUID | PK |
| `tipo_evento` | VARCHAR(50) | NOT NULL |
| `destinatario_email` | VARCHAR(255) | NOT NULL |
| `asunto` | VARCHAR(255) | NOT NULL |
| `cuerpo` | TEXT | NOT NULL |
| `estado` | VARCHAR(20) | NOT NULL, DEFAULT 'PENDIENTE' |
| `intentos` | SMALLINT | NOT NULL, DEFAULT 0 |
| `enviado_en` | TIMESTAMPTZ | NULLABLE |
| `creado_en` | TIMESTAMPTZ | NOT NULL, DEFAULT NOW() |
