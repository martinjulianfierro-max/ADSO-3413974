# Estrategia de Migración de Base de Datos

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Herramienta elegida: Flyway

Se usa **Flyway** para gestionar el versionado y la migración del esquema de cada base de datos. Flyway aplica scripts SQL numerados de forma secuencial y mantiene un historial de migraciones aplicadas en la tabla `flyway_schema_history`.

**Razón de elección sobre Liquibase:** Flyway usa SQL puro, lo que facilita la revisión de cambios por todo el equipo sin necesidad de aprender un lenguaje de cambios adicional (XML/YAML).

---

## Convención de nombres de scripts

```
V{version}__{descripcion_en_snake_case}.sql
```

Ejemplos:
- `V1__create_horarios_table.sql`
- `V2__create_ambientes_table.sql`
- `V3__add_estado_to_horarios.sql`

**Reglas:**
- La versión es un número entero incrementado secuencialmente.
- Nunca modificar un script ya aplicado en producción; crear uno nuevo con la corrección.
- Los scripts deben ser idempotentes o incluir comprobaciones (`IF NOT EXISTS`).

---

## Ubicación de los scripts

Los scripts de migración se ubican dentro del código de cada microservicio:

```
horarios-service/
  src/main/resources/db/migration/
    V1__create_horarios_table.sql
    V2__create_ambientes_table.sql
    V3__create_historial_cambios_table.sql
```

---

## Plan de migración del MVP

| Versión | Servicio | Script | Descripción |
|---------|----------|--------|-------------|
| V1 | horarios-service | `V1__create_ambientes_table.sql` | Crea tabla de ambientes |
| V2 | horarios-service | `V2__create_horarios_table.sql` | Crea tabla de horarios |
| V3 | horarios-service | `V3__create_historial_cambios_table.sql` | Crea tabla de historial |
| V1 | fichas-service | `V1__create_fichas_table.sql` | Crea tabla de fichas |
| V1 | usuarios-service | `V1__create_usuarios_table.sql` | Crea tabla de usuarios |
| V2 | usuarios-service | `V2__create_disponibilidad_table.sql` | Crea tabla de disponibilidad |
| V1 | notificaciones-service | `V1__create_notificaciones_table.sql` | Crea tabla de notificaciones |

---

## Datos iniciales (seed)

Los datos de prueba y configuración inicial se cargan mediante scripts de seed separados (no gestionados por Flyway). Se documentan en `06-data/seed-data.md`.

En el arranque del entorno `local` y `dev`, el Docker Compose ejecuta los scripts de seed automáticamente.

---

## Rollback

Flyway Community no soporta rollback automático. En caso de necesitar revertir:

1. Crear un nuevo script `V{n+1}__rollback_{descripcion}.sql` que deshaga los cambios.
2. Aplicar el script via el pipeline de CI/CD.
3. Documentar el incidente en `15-project-control/decisions-log.md`.
