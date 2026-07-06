# Agregados del Dominio

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

Los **agregados** son grupos de entidades y objetos de valor que se tratan como una unidad para garantizar consistencia. Cada agregado tiene una **raíz** que es el único punto de entrada para modificaciones.

---

## Agregado: Horario

**Raíz de agregado:** `Horario`

**Entidades incluidas:**
- `Horario` (raíz)
- `HistorialCambio` (lista de cambios del horario)

**Invariantes que el agregado garantiza:**

| Invariante | Descripción |
|------------|-------------|
| INV-H01 | El `RangoHorario` siempre es válido (inicio < fin, duración 1–4h, múltiplos de 30 min). |
| INV-H02 | La ficha referenciada existe y está `ACTIVA` en el momento de la creación. |
| INV-H03 | El instructor referenciado existe y está `ACTIVO` en el momento de la asignación. |
| INV-H04 | El ambiente referenciado existe y está `DISPONIBLE`. |
| INV-H05 | Cada `HistorialCambio` es inmutable una vez registrado. |

**Operaciones permitidas sobre la raíz:**

```
Horario.crear(fichaId, instructorId, ambienteId, rango, competencia, creadoPor)
Horario.modificar(campo, nuevoValor, modificadoPor)
Horario.cancelar(motivoCancelacion, canceladoPor)
```

Ninguna entidad externa puede modificar directamente un `HistorialCambio`; solo la raíz `Horario` puede agregar entradas al historial.

---

## Agregado: Ficha

**Raíz de agregado:** `Ficha`

**Invariantes:**

| Invariante | Descripción |
|------------|-------------|
| INV-F01 | El `CodigoFicha` es único en todo el sistema. |
| INV-F02 | `fechaFin > fechaInicio` siempre. |
| INV-F03 | Solo el coordinador puede cambiar el estado a `INACTIVA`. |

**Operaciones permitidas:**

```
Ficha.registrar(codigo, programa, jornada, fechaInicio, fechaFin)
Ficha.actualizar(campo, nuevoValor)
Ficha.inactivar()
```

---

## Agregado: Instructor (parte de Usuario)

**Raíz de agregado:** `Usuario` (con rol `INSTRUCTOR`)

**Invariantes:**

| Invariante | Descripción |
|------------|-------------|
| INV-I01 | La `Cedula` es única en todo el sistema. |
| INV-I02 | El `Email` debe ser único y válido. |
| INV-I03 | Un instructor tiene al menos una especialidad. |

**Operaciones permitidas:**

```
Instructor.registrar(nombre, cedula, email, tipo, especialidades)
Instructor.actualizarDisponibilidad(semana, rangosDisponibles)
Instructor.inactivar()
```

---

## Regla de acceso entre agregados

> Los agregados **nunca se referencian directamente por objeto**; solo se referencian por **ID (UUID)**. Esto garantiza que los límites de consistencia se mantengan y que cada agregado pueda evolucionar de forma independiente.

Por ejemplo, `Horario` no contiene un objeto `Ficha` completo; solo almacena `fichaId: UUID`. Para obtener los datos de la ficha, el servicio hace una llamada al `fichas-service`.
