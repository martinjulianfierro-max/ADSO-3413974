# Matriz de Riesgos

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Escala de evaluación

**Probabilidad:** 1 (Muy baja) → 5 (Muy alta)
**Impacto:** 1 (Mínimo) → 5 (Catastrófico)
**Nivel de riesgo = Probabilidad × Impacto**

| Nivel | Rango | Color |
|-------|-------|-------|
| Bajo | 1–4 | 🟢 |
| Medio | 5–9 | 🟡 |
| Alto | 10–15 | 🟠 |
| Crítico | 16–25 | 🔴 |

---

## Riesgos identificados

| ID | Riesgo | Probabilidad | Impacto | Nivel | Plan de mitigación | Responsable |
|----|--------|-------------|---------|-------|--------------------|-------------|
| R-001 | El equipo no tiene experiencia previa en microservicios, lo que puede retrasar el desarrollo | 4 | 4 | 🟠 16 | Capacitaciones tempranas, uso de Spring Boot que simplifica la configuración, arrancar con un servicio antes de dividir | Líder técnico |
| R-002 | Rotación de miembros del equipo (aprendices que abandonan el proyecto) | 3 | 4 | 🟠 12 | Documentación exhaustiva, onboarding técnico completo, knowledge sharing constante | Líder técnico |
| R-003 | El SENA no provee infraestructura de despliegue a tiempo para el MVP | 3 | 3 | 🟡 9 | Preparar despliegue en nube alternativa (Railway, Render, o servidor propio) como contingencia | Equipo DevOps |
| R-004 | Cambios en los requisitos a mitad del proyecto por parte del coordinador del SENA | 4 | 3 | 🟠 12 | Revisiones frecuentes con el cliente, historias de usuario bien definidas y priorización rigurosa | Product Owner |
| R-005 | Conflictos de horario no detectados correctamente por errores en la lógica de validación | 2 | 5 | 🟠 10 | Pruebas exhaustivas del motor de conflictos (unitarias + integración); revisión por pares obligatoria | Equipo Backend |
| R-006 | Pérdida de datos por fallo de la base de datos sin backup reciente | 1 | 5 | 🟡 5 | Backups diarios automatizados, prueba semanal de restauración (ver `13-operations`) | Equipo DevOps |
| R-007 | El sistema no es usable en móviles, afectando a los aprendices | 3 | 3 | 🟡 9 | Diseño mobile-first desde el inicio; pruebas en dispositivos reales en cada iteración | Equipo Frontend |
| R-008 | Brecha de seguridad por implementación incorrecta de JWT | 2 | 5 | 🟠 10 | Revisión de código enfocada en seguridad; uso de librerías establecidas (Spring Security) | Equipo Backend |
| R-009 | Dependencia externa no disponible (servidor SMTP bloqueado en red SENA) | 3 | 2 | 🟢 6 | Configurar SMTP alternativo (Gmail SMTP) como fallback | Equipo DevOps |
| R-010 | El tiempo del proyecto se acaba antes de completar el MVP | 3 | 4 | 🟠 12 | Priorizar las HUs del MVP estrictamente; aplicar timeboxing en las iteraciones | Product Owner |

---

## Riesgos críticos y plan de acción inmediata

### R-001 — Curva de aprendizaje en microservicios

**Acción inmediata:**
- Semana 1: Taller interno de microservicios con Spring Boot (2 horas).
- Arrancar con un monolito modular y dividir en servicios cuando el equipo tenga confianza.
- Pair programming entre el desarrollador más experimentado y los más nuevos.

### R-004 — Cambios de requisitos

**Acción inmediata:**
- Establecer un mecanismo formal de cambio: cualquier cambio de requisito debe documentarse como issue, evaluarse en impacto y aprobarse antes de implementarse.
- Reunión de revisión con el cliente cada 2 semanas.
