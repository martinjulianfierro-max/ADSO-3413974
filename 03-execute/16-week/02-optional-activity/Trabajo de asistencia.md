# Sistema Inteligente de Asistencia Biométrica Automatizada

## Descripción general

El proyecto surge de la necesidad de modernizar el control de asistencia, reemplazando métodos tradicionales como el carnet o el código QR por un mecanismo biométrico más confiable y difícil de manipular. La idea central es que el sistema reconozca al aprendiz de forma automática, capture evidencia del entorno, detecte posibles intentos de suplantación y gestione toda la información sin requerir intervención manual constante.

Con esto se busca agilizar el proceso, reducir errores humanos y garantizar que los registros de asistencia sean verídicos y trazables.

---

# Actores del sistema

## Aprendiz
Persona que interactúa con el sistema para registrar su asistencia mediante biometría.

## Instructor
Consulta el estado de asistencia de los aprendices a su cargo.

## Administrador
Supervisa el funcionamiento general del sistema, revisa reportes y gestiona el historial de asistencia.

---

# Funcionalidades principales

## 1. Registro biométrico de asistencia
El aprendiz se identifica mediante un mecanismo biométrico (reconocimiento facial o huella dactilar), sin necesidad de portar ningún dispositivo físico.

## 2. Validación automática de identidad
El sistema compara la biometría capturada con los datos previamente registrados del aprendiz para confirmar su identidad antes de marcar la asistencia.

## 3. Captura de evidencia fotográfica del entorno
En el momento del registro, el sistema fotografía el ambiente como respaldo de que la asistencia ocurrió en el lugar y tiempo correctos.

## 4. Detección de evidencia duplicada
El sistema analiza cada fotografía capturada para identificar si ya fue utilizada anteriormente, previniendo así el fraude mediante imágenes reutilizadas.

## 5. Registro automático de fecha y hora
Cada asistencia queda almacenada con el sello de tiempo exacto del ingreso, sin intervención del instructor.

## 6. Marcado automático de asistencia
Una vez validada la identidad, el sistema registra la asistencia de forma inmediata y autónoma.

## 7. Generación de alertas por fraude
Ante cualquier inconsistencia en la biometría o en la evidencia fotográfica, el sistema notifica al administrador mediante una alerta.

## 8. Consulta de reportes de asistencia
El instructor y el administrador pueden revisar en cualquier momento el historial de asistencias, inasistencias y tardanzas por aprendiz o grupo.

## 9. Limpieza automática de evidencias antiguas
Las fotografías de respaldo se eliminan automáticamente transcurrido un mes, liberando espacio de almacenamiento sin intervención manual.

## 10. Gestión del historial de asistencia
El sistema organiza y conserva los registros históricos de cada aprendiz, permitiendo su consulta y exportación.

---

# Requisitos funcionales

| Código | Descripción |
|--------|-------------|
| RF-01 | El sistema registrará la asistencia del aprendiz mediante autenticación biométrica. |
| RF-02 | El sistema validará automáticamente la identidad del aprendiz antes de confirmar el registro. |
| RF-03 | El sistema capturará una fotografía del entorno como evidencia en el momento del registro. |
| RF-04 | El sistema verificará que la fotografía capturada no haya sido utilizada previamente. |
| RF-05 | El sistema registrará automáticamente la fecha y hora de cada ingreso. |
| RF-06 | El sistema marcará la asistencia de forma autónoma una vez confirmada la identidad biométrica. |
| RF-07 | El sistema generará una alerta cuando detecte un intento de fraude o suplantación. |
| RF-08 | El sistema permitirá al instructor y al administrador consultar reportes de asistencia. |
| RF-09 | El sistema eliminará automáticamente las fotografías de evidencia con más de un mes de antigüedad. |
| RF-10 | El sistema almacenará y organizará el historial de asistencia de cada aprendiz. |

---

# Instrumento de recolección de datos

## Encuesta de caracterización del proceso actual de asistencia

**Propósito:** Identificar las principales dificultades del control de asistencia actual y validar la pertinencia de una solución biométrica automatizada.  
**Dirigido a:** Instructores y aprendices del centro de formación.

---

### Sección A — Información general

| # | Pregunta | Opciones de respuesta |
|---|----------|-----------------------|
| 1 | ¿Cuál es su rol dentro del proceso de formación? | ☐ Aprendiz ☐ Instructor ☐ Administrativo |
| 2 | ¿Cuánto tiempo lleva vinculado al programa de formación? | ☐ Menos de 6 meses ☐ Entre 6 y 12 meses ☐ Más de 1 año |

---

### Sección B — Proceso de asistencia actual

| # | Pregunta | Opciones de respuesta |
|---|----------|-----------------------|
| 3 | ¿Cuál es el método que actualmente se usa para registrar la asistencia? | ☐ Firma en papel ☐ Carnet / QR ☐ Lista verbal ☐ Otro: __________ |
| 4 | ¿Con qué frecuencia se presentan errores o inconsistencias en el registro de asistencia? | ☐ Nunca ☐ Pocas veces ☐ Frecuentemente ☐ Siempre |
| 5 | ¿Ha presenciado o conoce casos de suplantación o fraude en el registro de asistencia? | ☐ Sí ☐ No ☐ No estoy seguro/a |
| 6 | ¿Cuánto tiempo aproximado toma registrar la asistencia de todos los aprendices de un grupo? | ☐ Menos de 5 minutos ☐ Entre 5 y 15 minutos ☐ Más de 15 minutos |

---

### Sección C — Percepción frente a una solución biométrica

| # | Pregunta | Escala (1 = Muy bajo — 5 = Muy alto) |
|---|----------|--------------------------------------|
| 7 | ¿Qué tan útil considera que sería un sistema de asistencia por reconocimiento biométrico? | 1 ☐ 2 ☐ 3 ☐ 4 ☐ 5 ☐ |
| 8 | ¿Qué tan confiable le parece el reconocimiento facial como método de verificación de identidad? | 1 ☐ 2 ☐ 3 ☐ 4 ☐ 5 ☐ |
| 9 | ¿Qué tan importante considera la captura de evidencia fotográfica del entorno durante el registro? | 1 ☐ 2 ☐ 3 ☐ 4 ☐ 5 ☐ |

---

### Sección D — Observaciones

| # | Pregunta | Tipo de respuesta |
|---|----------|-------------------|
| 10 | ¿Qué aspectos del proceso de asistencia actual considera que deberían mejorar con mayor urgencia? | Respuesta abierta |
| 11 | ¿Tiene alguna inquietud o sugerencia frente al uso de datos biométricos para el control de asistencia? | Respuesta abierta |

---

# Objetivo general

Desarrollar un sistema de asistencia biométrica automatizada que registre la presencia de los aprendices de manera segura y autónoma, reduciendo la intervención manual, minimizando el riesgo de suplantación y generando registros confiables y trazables.

---

# Objetivos específicos

- Implementar un mecanismo de autenticación biométrica para el registro de asistencia.
- Capturar y almacenar evidencia fotográfica del entorno en cada registro.
- Verificar que la evidencia capturada no sea repetida ni manipulada.
- Registrar automáticamente la fecha, hora e historial de asistencia de cada aprendiz.
- Permitir la consulta de reportes por parte del instructor y el administrador.
- Automatizar la limpieza de evidencias antiguas para optimizar el almacenamiento.