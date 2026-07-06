# Alcance del Sistema

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## En alcance

Las siguientes funcionalidades **sí** forman parte del sistema:

- **Gestión de horarios:** Crear, editar, eliminar y consultar asignaciones de horario (ficha + instructor + ambiente + bloque de tiempo).
- **Gestión de fichas:** Registrar y mantener la información de fichas activas (código, programa, jornada, fechas).
- **Gestión de instructores:** Registrar instructores con sus datos básicos (nombre, especialidad, tipo de vinculación, disponibilidad declarada).
- **Gestión de ambientes:** Registrar aulas, laboratorios y salas con su capacidad y disponibilidad.
- **Detección de conflictos:** Alertar en tiempo real si un instructor o ambiente ya tiene asignación en el bloque seleccionado.
- **Consulta de horarios por rol:** Vista de horario para coordinador (todos), instructor (propio) y aprendiz (su ficha).
- **Notificaciones:** Envío de alertas por correo electrónico cuando un horario es creado, modificado o cancelado.
- **Autenticación y roles:** Login con JWT y control de acceso diferenciado por rol (coordinador, instructor, aprendiz, admin).
- **Historial de cambios:** Registro de quién hizo qué cambio y cuándo en cada horario.
- **API REST documentada:** Endpoints públicos documentados con OpenAPI/Swagger para consumo desde el frontend.

---

## Fuera de alcance

Las siguientes funcionalidades **no** forman parte de este sistema:

- ❌ **Gestión de nómina o pagos** a instructores (corresponde a Gestión Humana del SENA).
- ❌ **Calificaciones o evaluaciones** de aprendices (corresponde a Territorium/LMS).
- ❌ **Gestión de matrícula o inscripción** de aprendices a fichas (proceso administrativo externo).
- ❌ **Integración directa con Territorium** en esta versión (posible en versiones futuras).
- ❌ **Aplicación móvil nativa** (iOS/Android). La solución es web-responsive.
- ❌ **Gestión de centros de formación** distintos al Centro de Biotecnología Agropecuaria (CBA). El sistema se diseña para un centro piloto.
- ❌ **Manejo de vacaciones, licencias o permisos** de instructores.
- ❌ **Integración con sistemas ERP externos** del SENA (SOFIA Plus, etc.) en esta versión.

---

## Supuestos

1. El equipo de coordinación tiene acceso a computadores con navegador moderno (Chrome 110+, Firefox 115+).
2. Los instructores y aprendices disponen de correo electrónico institucional activo para recibir notificaciones.
3. El SENA proveerá o autorizará la infraestructura de despliegue (servidor o nube) para el ambiente productivo.
4. Los datos iniciales de fichas, instructores y ambientes se cargarán manualmente en la etapa de puesta en marcha (seed data).
5. No existe un sistema previo con datos históricos que deban migrarse automáticamente en el MVP.
6. El sistema operará en zona horaria **America/Bogota (UTC-5)**.

---

## Restricciones

| Tipo | Restricción |
|------|------------|
| **Técnica** | El backend debe desarrollarse en Java (Spring Boot) o Node.js, según decisión de arquitectura (ver ADR-002). |
| **Técnica** | La base de datos principal debe ser relacional (PostgreSQL preferido). |
| **Técnica** | El sistema debe funcionar correctamente en conexiones de baja velocidad (mínimo 1 Mbps). |
| **Institucional** | El sistema no puede almacenar datos personales de aprendices sin cumplir la Ley 1581 de 2012 (Habeas Data). |
| **Institucional** | Solo el coordinador asignado al centro puede modificar horarios. Los instructores no pueden auto-asignarse. |
| **Proyecto** | El MVP debe entregarse dentro del ciclo de formación ADSO (aproximadamente 6 meses de desarrollo). |
| **Proyecto** | El equipo está compuesto exclusivamente por aprendices del programa ADSO; no hay presupuesto para licencias de software propietario. |
