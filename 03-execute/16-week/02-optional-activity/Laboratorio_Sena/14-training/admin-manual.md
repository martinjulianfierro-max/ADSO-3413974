# Manual del Administrador

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Acceso al panel de administración

El rol **ADMIN** tiene acceso a todas las funcionalidades del sistema más el módulo de gestión de usuarios.

1. Inicie sesión con sus credenciales de administrador.
2. En el menú lateral verá la sección **Administración → Usuarios**.

---

## Gestión de usuarios

### Crear un usuario

1. Vaya a **Administración → Usuarios**.
2. Haga clic en **+ Nuevo usuario**.
3. Complete el formulario:
   - **Nombre completo**
   - **Cédula** (único en el sistema)
   - **Correo institucional** (único; será el login)
   - **Rol:** COORDINADOR, INSTRUCTOR o APRENDIZ
   - **Tipo de vinculación** (solo para instructores): PLANTA o CONTRATISTA
4. El sistema generará una contraseña temporal que el usuario deberá cambiar en su primer login.
5. Haga clic en **Crear usuario**.

### Desactivar un usuario

1. Busque al usuario en el listado.
2. Haga clic en el botón **Desactivar** (ícono de candado).
3. Confirme la acción.
4. El usuario no podrá iniciar sesión mientras esté desactivado.

> ⚠️ Desactivar un usuario **no elimina** sus datos ni los horarios que tiene asignados.

### Cambiar el rol de un usuario

1. Busque al usuario en el listado.
2. Haga clic en **Editar**.
3. Modifique el campo **Rol**.
4. Guarde los cambios.

---

## Gestión de parámetros del sistema

Los parámetros de configuración del sistema (zona horaria, límites de bloques, etc.) se configuran mediante variables de entorno. Para cambiar parámetros críticos:

1. Edite el archivo `.env` del microservicio correspondiente (en el servidor).
2. Reinicie el contenedor: `docker compose restart {servicio}`.
3. Documente el cambio en `15-project-control/decisions-log.md`.

---

## Tareas de mantenimiento

### Verificar el estado de los servicios

```bash
docker compose ps
curl http://localhost:8080/actuator/health
```

### Ver logs de un servicio

```bash
docker compose logs -f horarios-service --tail=100
```

### Reiniciar un servicio con problemas

```bash
docker compose restart horarios-service
```

### Ejecutar backup manual de la base de datos

```bash
./scripts/backup-now.sh
```

---

## Escalación de problemas

| Problema | Acción |
|---------|--------|
| Un servicio no responde al healthcheck | Revisar logs, reiniciar contenedor, escalar al líder técnico si no se resuelve |
| Error masivo de autenticación (todos los usuarios no pueden entrar) | Verificar `usuarios-service` y el secreto JWT; escalar inmediatamente |
| Base de datos sin conexión | Verificar contenedor de PostgreSQL; intentar reiniciar; restaurar desde backup si es necesario |
| Mensajes acumulados en la Dead Letter Queue | Revisar logs de `notificaciones-service`; verificar configuración SMTP |
