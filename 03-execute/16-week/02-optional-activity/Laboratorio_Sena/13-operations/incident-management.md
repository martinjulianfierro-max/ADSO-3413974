# Gestión de Incidentes

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Definición de incidente

Un incidente es cualquier evento que interrumpe o degrada la disponibilidad o correctitud del sistema en producción. Esto incluye: caídas de servicios, errores masivos (>5% de requests), pérdida de datos, accesos no autorizados.

---

## Severidades

| Nivel | Nombre | Descripción | Tiempo de respuesta | Tiempo de resolución |
|-------|--------|-------------|---------------------|---------------------|
| P1 | Crítico | Sistema completamente caído o pérdida de datos | < 15 minutos | < 2 horas |
| P2 | Alto | Funcionalidad principal degradada (ej: no se pueden crear horarios) | < 30 minutos | < 4 horas |
| P3 | Medio | Funcionalidad secundaria afectada (ej: notificaciones no llegan) | < 2 horas | < 24 horas |
| P4 | Bajo | Problema cosmético o de UX que no bloquea el flujo | < 1 día hábil | < 1 semana |

---

## Proceso de gestión de incidentes

```
1. DETECCIÓN
   ↓ (monitoreo, reporte de usuario, alerta automática)

2. NOTIFICACIÓN
   → Abrir issue en GitHub con etiqueta "incidente" y severidad
   → Notificar al líder técnico por el canal de comunicación del equipo

3. EVALUACIÓN
   → Asignar nivel de severidad (P1-P4)
   → Asignar responsable de la resolución

4. MITIGACIÓN (acción inmediata)
   → Restablecer servicio (reiniciar contenedor, rollback, etc.)
   → Comunicar el estado a los usuarios afectados si es P1/P2

5. RESOLUCIÓN
   → Implementar fix definitivo
   → Documentar causa raíz y solución en el issue

6. POST-MORTEM (para P1 y P2)
   → Redactar post-mortem en 5-minutes-to-fix format:
     - ¿Qué pasó?
     - ¿Cuándo se detectó?
     - ¿Cómo se resolvió?
     - ¿Qué hacer para que no vuelva a pasar?
   → Guardar en 15-project-control/decisions-log.md
```

---

## Canales de alerta

| Severidad | Canal principal | Canal secundario |
|-----------|----------------|-----------------|
| P1 | WhatsApp grupal del equipo | Llamada directa al líder técnico |
| P2 | WhatsApp grupal | Issue en GitHub |
| P3 | Issue en GitHub | — |
| P4 | Issue en GitHub | — |

---

## Responsables por área

| Área | Responsable en turno | Contacto |
|------|---------------------|----------|
| Backend / microservicios | Líder de backend del equipo | (definir por el equipo) |
| Frontend | Líder de frontend | (definir por el equipo) |
| Infraestructura / DevOps | Líder de DevOps | (definir por el equipo) |
| Base de datos | DBA del equipo | (definir por el equipo) |

---

## Historial de incidentes

Los incidentes se registran en issues de GitHub con la etiqueta `incident`. El post-mortem de P1/P2 se archiva en `15-project-control/decisions-log.md`.
