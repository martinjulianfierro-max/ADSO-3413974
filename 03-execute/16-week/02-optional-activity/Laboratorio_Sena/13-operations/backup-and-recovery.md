# Backup y Recuperación

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Estrategia de backup

### Frecuencia y tipo

| Tipo | Frecuencia | Retención | Herramienta |
|------|------------|-----------|-------------|
| Backup completo (full) | Diario — 02:00 AM (Bogotá) | 30 días | `pg_dump` + script automatizado |
| Backup incremental | Cada 6 horas | 7 días | WAL archiving de PostgreSQL |

### Qué se respalda

| Componente | Respaldado | Notas |
|-----------|------------|-------|
| `horarios_db` | ✅ | Base de datos principal |
| `fichas_db` | ✅ | — |
| `usuarios_db` | ✅ | Incluye hashes de contraseñas |
| `notificaciones_db` | ✅ | — |
| Archivos de configuración | ✅ | `.env` no se respalda (secretos en gestor de secretos) |
| Código fuente | ✅ | Versionado en Git (GitHub) |

### Almacenamiento de backups

- Los backups se almacenan en almacenamiento externo al servidor de producción (carpeta segura en la red interna del SENA o servicio de almacenamiento en nube — TBD según infraestructura disponible).
- Los backups están comprimidos con `gzip`.
- Los archivos de backup están encriptados con `gpg` antes de ser transferidos.

---

## Objetivos de recuperación

| Métrica | Objetivo |
|---------|---------|
| **RTO** (Recovery Time Objective) | ≤ 4 horas — tiempo máximo para restablecer el sistema |
| **RPO** (Recovery Point Objective) | ≤ 24 horas — máximo de datos que se acepta perder |

---

## Procedimiento de restauración

### Restauración completa (fallo catastrófico)

```bash
# 1. Detener todos los contenedores
docker compose down

# 2. Restaurar la base de datos desde el backup más reciente
pg_restore -h localhost -U sena_user -d horarios_db /backups/horarios_db_YYYY-MM-DD.dump
pg_restore -h localhost -U sena_user -d fichas_db /backups/fichas_db_YYYY-MM-DD.dump
pg_restore -h localhost -U sena_user -d usuarios_db /backups/usuarios_db_YYYY-MM-DD.dump
pg_restore -h localhost -U sena_user -d notificaciones_db /backups/notificaciones_db_YYYY-MM-DD.dump

# 3. Verificar integridad de los datos
psql -U sena_user -d horarios_db -c "SELECT COUNT(*) FROM horarios;"

# 4. Levantar los servicios
docker compose up -d

# 5. Verificar health checks
curl http://localhost:8080/actuator/health
```

### Restauración parcial (tabla o datos corruptos)

1. Identificar la tabla afectada.
2. Restaurar solo esa tabla desde el backup usando `pg_restore --table={tabla}`.
3. Validar la consistencia con queries de verificación.
4. Documentar el incidente en `15-project-control/decisions-log.md`.

---

## Verificación de backups

Los backups se verifican **semanalmente**:
1. Restaurar el backup más reciente en un ambiente aislado (de prueba).
2. Ejecutar un conjunto de queries de validación de integridad.
3. Registrar el resultado en el log de operaciones.

> Un backup no probado no es un backup.
