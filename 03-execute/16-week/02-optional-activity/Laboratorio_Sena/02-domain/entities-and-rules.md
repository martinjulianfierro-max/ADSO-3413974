# Entidades y Reglas de Negocio

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Entidades del dominio

### Ficha

Representa un grupo de aprendices matriculados en un programa de formación.

| Atributo | Tipo | Descripción | Regla |
|----------|------|-------------|-------|
| `id` | UUID | Identificador interno del sistema | Generado automáticamente |
| `codigo` | String | Código oficial SENA (ej: `2879723`) | Obligatorio, único, 7 dígitos |
| `programa` | String | Nombre del programa (ej: ADSO) | Obligatorio |
| `jornada` | Enum | `DIURNA`, `TARDE`, `NOCTURNA` | Obligatorio |
| `fechaInicio` | Date | Fecha de inicio de la formación | Obligatorio |
| `fechaFin` | Date | Fecha estimada de finalización | Obligatorio; debe ser > `fechaInicio` |
| `estado` | Enum | `ACTIVA`, `INACTIVA` | Por defecto `ACTIVA` |

**Reglas de negocio:**
- RN-F01: No pueden existir dos fichas con el mismo `codigo`.
- RN-F02: Una ficha `INACTIVA` no puede recibir nuevas asignaciones de horario.
- RN-F03: La `fechaFin` no puede ser anterior a la `fechaInicio`.

---

### Instructor

Persona encargada de impartir formación en una o más fichas.

| Atributo | Tipo | Descripción | Regla |
|----------|------|-------------|-------|
| `id` | UUID | Identificador interno | Generado automáticamente |
| `nombre` | String | Nombre completo | Obligatorio |
| `cedula` | String | Número de cédula | Obligatorio, único |
| `email` | String | Correo institucional | Obligatorio, formato válido |
| `tipo` | Enum | `PLANTA`, `CONTRATISTA` | Obligatorio |
| `especialidades` | List\<String\> | Áreas de conocimiento | Al menos 1 |
| `estado` | Enum | `ACTIVO`, `INACTIVO` | Por defecto `ACTIVO` |

**Reglas de negocio:**
- RN-I01: Un instructor `INACTIVO` no puede ser asignado a nuevos horarios.
- RN-I02: Un instructor no puede tener dos horarios que se solapen en el mismo bloque de tiempo (**regla de exclusividad temporal**).
- RN-I03: La disponibilidad declarada por el instructor es informativa; el coordinador puede asignar fuera de ella, pero el sistema genera una advertencia.

---

### Ambiente

Espacio físico o virtual donde se desarrolla la actividad formativa.

| Atributo | Tipo | Descripción | Regla |
|----------|------|-------------|-------|
| `id` | UUID | Identificador interno | Generado automáticamente |
| `nombre` | String | Nombre del ambiente (ej: "Sala 204") | Obligatorio, único |
| `tipo` | Enum | `AULA`, `LABORATORIO`, `TALLER`, `SALA_SISTEMAS`, `VIRTUAL` | Obligatorio |
| `capacidad` | Integer | Número máximo de personas | Obligatorio, > 0 |
| `estado` | Enum | `DISPONIBLE`, `EN_MANTENIMIENTO`, `INACTIVO` | Por defecto `DISPONIBLE` |

**Reglas de negocio:**
- RN-A01: Un ambiente `EN_MANTENIMIENTO` o `INACTIVO` no puede ser asignado.
- RN-A02: Un ambiente no puede tener dos horarios activos en el mismo bloque de tiempo (**regla de exclusividad de espacio**).

---

### Horario

Asignación concreta que une una ficha, un instructor y un ambiente en un bloque de tiempo.

| Atributo | Tipo | Descripción | Regla |
|----------|------|-------------|-------|
| `id` | UUID | Identificador interno | Generado automáticamente |
| `fichaId` | UUID | Referencia a la ficha | Obligatorio; ficha debe estar `ACTIVA` |
| `instructorId` | UUID | Referencia al instructor | Obligatorio; instructor debe estar `ACTIVO` |
| `ambienteId` | UUID | Referencia al ambiente | Obligatorio; ambiente debe estar `DISPONIBLE` |
| `competencia` | String | Nombre de la competencia a impartir | Obligatorio |
| `bloqueInicio` | DateTime | Inicio del bloque (fecha + hora, zona UTC) | Obligatorio |
| `bloqueFin` | DateTime | Fin del bloque (fecha + hora, zona UTC) | Obligatorio; debe ser > `bloqueInicio` |
| `estado` | Enum | `ACTIVO`, `CANCELADO`, `MODIFICADO` | Por defecto `ACTIVO` |
| `creadoPor` | UUID | ID del coordinador que creó el horario | Obligatorio |
| `creadoEn` | DateTime | Timestamp de creación | Automático |

**Reglas de negocio:**
- RN-H01: El sistema debe verificar que ni el instructor ni el ambiente estén ya asignados en el rango `[bloqueInicio, bloqueFin)` antes de guardar.
- RN-H02: `bloqueInicio` debe ser un múltiplo de 30 minutos (ej: 08:00, 08:30, 09:00...).
- RN-H03: La duración mínima de un bloque es de 1 hora; la máxima es de 4 horas continuas.
- RN-H04: No se pueden crear horarios en días no hábiles (domingos y festivos nacionales colombianos).
- RN-H05: Los cambios a un horario `ACTIVO` deben quedar registrados en el historial.

---

### HistorialCambio

Registro inmutable de cada modificación realizada a un horario.

| Atributo | Tipo | Descripción |
|----------|------|-------------|
| `id` | UUID | Identificador |
| `horarioId` | UUID | Horario afectado |
| `campoModificado` | String | Nombre del campo que cambió |
| `valorAnterior` | String | Valor antes del cambio |
| `valorNuevo` | String | Valor después del cambio |
| `modificadoPor` | UUID | Usuario que hizo el cambio |
| `modificadoEn` | DateTime | Timestamp del cambio |

---

## Resumen de reglas de negocio

| ID | Entidad | Regla |
|----|---------|-------|
| RN-F01 | Ficha | El código de ficha debe ser único |
| RN-F02 | Ficha | Fichas inactivas no reciben horarios |
| RN-F03 | Ficha | fechaFin > fechaInicio |
| RN-I01 | Instructor | Instructores inactivos no se asignan |
| RN-I02 | Instructor | Sin solapamiento temporal (exclusividad) |
| RN-I03 | Instructor | Advertencia al asignar fuera de disponibilidad |
| RN-A01 | Ambiente | Ambientes no disponibles no se asignan |
| RN-A02 | Ambiente | Sin solapamiento temporal (exclusividad) |
| RN-H01 | Horario | Verificar conflictos antes de guardar |
| RN-H02 | Horario | Inicio en múltiplos de 30 minutos |
| RN-H03 | Horario | Duración entre 1h y 4h |
| RN-H04 | Horario | Sin horarios en domingos y festivos |
| RN-H05 | Horario | Cambios registrados en historial |
