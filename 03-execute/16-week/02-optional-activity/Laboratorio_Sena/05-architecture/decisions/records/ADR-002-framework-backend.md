# ADR-002 — Elección de Framework Backend: Spring Boot

> Estado: Aceptado | Fecha: 2026-07-06
> Autor: Equipo ADSO

---

## Contexto

El equipo necesita elegir el framework backend para implementar los microservicios. Las opciones más relevantes dado el perfil del equipo (formación ADSO con Java) son Spring Boot y Node.js/Express.

## Opciones consideradas

| Opción | Ventajas | Desventajas |
|--------|----------|-------------|
| **Spring Boot (Java 17)** | Ecosistema robusto; gran documentación; Spring Security para JWT; el equipo tiene base en Java | Verboso; curva de aprendizaje para microservicios |
| Node.js + Express | Ligero; rápido de prototipo | El equipo tiene menos experiencia; manejo de tipos más débil |
| Quarkus | Arranque rápido; cloud-native | Menos familiar para el equipo |

## Decisión

Se adopta **Spring Boot 3 con Java 17** para todos los microservicios backend.

## Consecuencias

- ✅ Alineado con el perfil de formación ADSO (Java es el lenguaje principal del programa).
- ✅ Spring Security facilita la implementación de JWT y control de roles.
- ✅ Spring Data JPA simplifica la capa de persistencia con PostgreSQL.
- ⚠️ Los archivos JAR son relativamente pesados; las imágenes Docker deben optimizarse con multi-stage builds.

## Estado de revisión

Aceptado por unanimidad del equipo.
