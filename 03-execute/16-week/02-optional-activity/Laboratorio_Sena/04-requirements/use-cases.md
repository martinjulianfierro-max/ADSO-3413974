# Casos de Uso

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## CU-001 — Autenticar usuario

| Atributo | Detalle |
|----------|---------|
| **Actor principal** | Usuario (Coordinador, Instructor, Aprendiz, Admin) |
| **Precondición** | El usuario tiene una cuenta activa en el sistema |
| **Postcondición** | El usuario obtiene un JWT válido y accede al sistema |

**Flujo principal:**
1. El usuario navega a la pantalla de login.
2. Ingresa su correo institucional y contraseña.
3. El sistema valida las credenciales contra la base de datos.
4. Si son correctas, el sistema genera un JWT con el rol del usuario y lo retorna.
5. El cliente almacena el JWT y redirige al dashboard del rol.

**Flujos alternativos:**
- **3a.** Credenciales inválidas: el sistema muestra "Correo o contraseña incorrectos" y no emite token.
- **3b.** Cuenta inactiva: el sistema muestra "Cuenta desactivada. Contacte al administrador."
- **3c.** 5 intentos fallidos: el sistema bloquea la cuenta por 15 minutos y muestra el mensaje correspondiente.

---

## CU-002 — Crear horario

| Atributo | Detalle |
|----------|---------|
| **Actor principal** | Coordinador |
| **Actores secundarios** | Sistema (validación de conflictos), `horarios-service` |
| **Precondición** | El coordinador está autenticado; existen al menos una ficha activa, un instructor activo y un ambiente disponible |
| **Postcondición** | El horario queda registrado con estado ACTIVO; se publica el evento `HorarioCreado` |

**Flujo principal:**
1. El coordinador accede al módulo de horarios y selecciona "Nuevo horario".
2. Completa el formulario: ficha, instructor, ambiente, competencia, bloque de inicio y fin.
3. Al seleccionar instructor + ambiente + rango, el sistema consulta conflictos en tiempo real.
4. El sistema retorna "Sin conflictos — puede guardar".
5. El coordinador confirma la creación.
6. El sistema persiste el horario y publica `HorarioCreado`.
7. El sistema muestra mensaje de éxito y redirige al listado de horarios.

**Flujos alternativos:**
- **3a.** Conflicto de instructor: el sistema muestra "El instructor ya tiene una asignación de HH:mm a HH:mm el DD/MM". El coordinador no puede continuar hasta elegir otro instructor o cambiar el bloque.
- **3b.** Conflicto de ambiente: el sistema muestra "El ambiente ya está reservado en ese bloque". Similar al anterior.
- **5a.** El coordinador cancela: no se guarda nada, se vuelve al listado.

---

## CU-003 — Modificar horario

| Atributo | Detalle |
|----------|---------|
| **Actor principal** | Coordinador |
| **Precondición** | El horario existe y está en estado ACTIVO |
| **Postcondición** | El horario se actualiza; el cambio queda registrado en el historial; se publica `HorarioModificado` |

**Flujo principal:**
1. El coordinador selecciona un horario existente y elige "Editar".
2. Modifica uno o más campos.
3. El sistema re-valida conflictos con los nuevos valores.
4. El coordinador confirma los cambios.
5. El sistema actualiza el horario, agrega una entrada al historial y publica `HorarioModificado`.

**Flujos alternativos:**
- **3a.** Los nuevos valores generan conflicto: igual que CU-002, flujo alternativo 3a/3b.

---

## CU-004 — Cancelar horario

| Atributo | Detalle |
|----------|---------|
| **Actor principal** | Coordinador |
| **Precondición** | El horario existe y está en estado ACTIVO |
| **Postcondición** | El horario pasa a estado CANCELADO; se registra el motivo; se publica `HorarioCancelado` |

**Flujo principal:**
1. El coordinador selecciona un horario y elige "Cancelar".
2. El sistema solicita confirmación y un motivo (obligatorio).
3. El coordinador ingresa el motivo y confirma.
4. El sistema cambia el estado a CANCELADO, registra el cambio en el historial y publica `HorarioCancelado`.

**Flujos alternativos:**
- **2a.** El coordinador cancela la acción: no ocurre ningún cambio.
- **3a.** El motivo tiene menos de 10 caracteres: error de validación, no se procede.

---

## CU-005 — Consultar horario de ficha (aprendiz)

| Atributo | Detalle |
|----------|---------|
| **Actor principal** | Aprendiz |
| **Precondición** | Ninguna (consulta pública) |
| **Postcondición** | El aprendiz visualiza el horario semanal de su ficha |

**Flujo principal:**
1. El aprendiz accede a la página pública de consulta de horarios.
2. Ingresa el código de su ficha (7 dígitos).
3. El sistema busca los horarios activos de la semana actual para esa ficha.
4. Muestra los bloques: instructor, competencia, ambiente, hora de inicio y fin.

**Flujos alternativos:**
- **2a.** Código de ficha no encontrado: "No se encontró una ficha con ese código."
- **3a.** No hay horarios para la semana actual: "No hay horarios publicados para esta semana."
