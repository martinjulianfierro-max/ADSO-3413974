# Overview del Sistema

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Contexto institucional

El **Servicio Nacional de Aprendizaje (SENA)** es una entidad pública colombiana adscrita al Ministerio del Trabajo, encargada de invertir en el desarrollo social y técnico de los trabajadores colombianos mediante programas de formación profesional gratuita y de calidad. Cuenta con presencia en los 32 departamentos del país y atiende anualmente a más de 5 millones de aprendices.

El programa **Análisis y Desarrollo de Software (ADSO)** es una titulación tecnológica de 2 años y 6 meses que forma profesionales capaces de diseñar, construir, administrar y mantener soluciones de software. Las fichas del programa ADSO en el Centro de Biotecnología Agropecuaria (CBA) agrupan entre 25 y 30 aprendices por grupo, distribuidos en jornadas diurna, tarde y nocturna.

---

## Problema que resuelve el sistema

Actualmente la gestión de horarios del SENA se realiza de forma **manual y descentralizada**: coordinadores usan hojas de cálculo, correos electrónicos y comunicaciones informales para asignar instructores a fichas, reservar ambientes y comunicar los horarios a los aprendices.

Este proceso genera múltiples problemas:

| Problema | Impacto |
|----------|---------|
| Conflictos de horario (instructor asignado a dos fichas simultáneamente) | Formación interrumpida, malestar institucional |
| Ambientes sobre-reservados o subutilizados | Ineficiencia en el uso del espacio físico |
| Falta de visibilidad para los aprendices | Aprendices sin acceso oportuno a su horario actualizado |
| Cambios de último minuto sin notificación | Alta tasa de ausentismo y desorientación |
| Sin historial de cambios ni trazabilidad | Imposible auditar o resolver disputas |

---

## Objetivos del sistema

### Objetivo general

Desarrollar un **sistema web de gestión de horarios** para el programa ADSO del SENA que permita a coordinadores e instructores planificar, asignar, consultar y modificar horarios académicos de manera centralizada, evitando conflictos y garantizando visibilidad en tiempo real para todos los actores involucrados.

### Objetivos específicos

1. **Centralizar** la información de horarios en una plataforma única, accesible desde cualquier dispositivo con navegador.
2. **Automatizar la detección de conflictos** de instructor y ambiente en tiempo real durante la asignación.
3. **Notificar automáticamente** a instructores y aprendices los cambios en horarios con anticipación suficiente.
4. **Proveer vistas diferenciadas** según el rol del usuario: coordinador (gestión), instructor (mi horario), aprendiz (consulta de ficha).
5. **Registrar el historial** de cambios en cada horario para garantizar trazabilidad y auditoría.
6. **Escalar** la solución como una arquitectura de microservicios, permitiendo incorporar nuevas funcionalidades de forma independiente.

---

## Actores principales

| Actor | Rol en el sistema |
|-------|-------------------|
| Coordinador | Crea, modifica y aprueba horarios; gestiona instructores y ambientes |
| Instructor | Consulta su horario personal; puede declarar disponibilidad |
| Aprendiz | Consulta el horario de su ficha (solo lectura) |
| Administrador del sistema | Gestiona usuarios, roles y parámetros de configuración |

---

## Referencias

- Acuerdo 009 de 2024 — Reglamento del aprendiz SENA
- Ley 119 de 1994 — Ley de creación del SENA
- Documentación interna del Centro de Biotecnología Agropecuaria (CBA)
- Programa de formación ADSO — Plan de estudios vigente
