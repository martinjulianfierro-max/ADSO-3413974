# ADR-001 — Estilo Arquitectónico: Microservicios

> Estado: Aceptado | Fecha: 2026-07-06
> Autor: Equipo ADSO

---

## Contexto

El sistema de horarios SENA necesita gestionar al menos 4 bounded contexts independientes (Horarios, Fichas, Usuarios, Notificaciones). El equipo debe decidir si construir un monolito, un monolito modular o microservicios.

## Opciones consideradas

| Opción | Ventajas | Desventajas |
|--------|----------|-------------|
| Monolito | Simple de desplegar; un solo proyecto | Difícil de escalar; acoplamiento alto |
| Monolito modular | Estructura clara; despliegue simple | Límites de módulos difíciles de mantener |
| **Microservicios** | Independencia; escalabilidad; boundaries claros | Mayor complejidad operativa; red entre servicios |

## Decisión

Se adopta **arquitectura de microservicios** con 4 servicios iniciales: `horarios-service`, `fichas-service`, `usuarios-service`, `notificaciones-service`.

## Consecuencias

- ✅ Cada servicio puede evolucionar, desplegarse y escalarse de forma independiente.
- ✅ Los límites del dominio se refuerzan técnicamente.
- ⚠️ Mayor complejidad de configuración local (Docker Compose necesario).
- ⚠️ La comunicación entre servicios introduce latencia de red.
- ⚠️ El equipo debe aprender a gestionar múltiples servicios.

## Estado de revisión

Aceptado por el equipo en la reunión de kick-off del proyecto.
