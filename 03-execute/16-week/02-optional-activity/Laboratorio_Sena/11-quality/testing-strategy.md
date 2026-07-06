# Estrategia de Testing

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Pirámide de pruebas

```
              /\
             /  \
            / E2E \      ← Pocas, lentas, costosas
           /--------\
          /Integración\   ← Moderadas
         /--------------\
        /   Unitarias    \  ← Muchas, rápidas, baratas
       /------------------\
```

El sistema adopta la pirámide de pruebas estándar: la mayor inversión está en pruebas unitarias, seguida por pruebas de integración, y finalmente pruebas E2E para los flujos críticos.

---

## Capas de testing

### 1. Pruebas unitarias (Unit Tests)

**Qué prueban:** Lógica de negocio aislada: servicios, entidades, objetos de valor, validaciones.

| Capa | Herramienta | Ubicación |
|------|------------|-----------|
| Backend (Java) | JUnit 5 + Mockito | `src/test/java/...` en cada microservicio |
| Frontend (React) | Jest + React Testing Library | `src/__tests__/` en el frontend |

**Cobertura mínima exigida:** ≥ 80% en backend (medido con JaCoCo).

**Ejemplos de qué probar:**
- `RangoHorario.solapaCon()` con casos de solapamiento y no solapamiento.
- `HorarioService.crear()` cuando hay conflicto vs. cuando no lo hay.
- Validación de `CodigoFicha` con códigos válidos e inválidos.

---

### 2. Pruebas de integración (Integration Tests)

**Qué prueban:** Interacción entre capas: controller → service → repository → base de datos.

| Herramienta | Uso |
|------------|-----|
| Spring Boot Test + Testcontainers | Levanta un PostgreSQL real en Docker para pruebas |
| MockMvc | Prueba los endpoints HTTP del microservicio sin levantar el servidor completo |
| WireMock | Simula llamadas HTTP a otros microservicios |

**Ejemplos de qué probar:**
- `POST /api/horarios` con body válido → 201 Created + horario en BD.
- `POST /api/horarios` con conflicto → 409 Conflict con mensaje adecuado.
- `GET /api/horarios?fichaId=uuid` → lista paginada correctamente filtrada.

---

### 3. Pruebas E2E (End-to-End)

**Qué prueban:** Flujos completos desde el frontend hasta la base de datos.

| Herramienta | Uso |
|------------|-----|
| Cypress | Pruebas E2E del frontend en navegador real |
| Postman / Newman | Pruebas de colecciones de API (smoke tests) |

**Flujos cubiertos en el MVP:**
- Login → crear horario sin conflicto → verificar en listado.
- Login → intentar crear horario con conflicto → verificar alerta.
- Consulta de horario por código de ficha (aprendiz, sin login).

---

## Cobertura mínima por ambiente

| Ambiente | Unitarias | Integración | E2E |
|----------|-----------|-------------|-----|
| PR a dev | ✅ Obligatorio | ✅ Obligatorio | ❌ |
| Merge a qa | ✅ | ✅ | ✅ (flujos críticos) |
| Merge a main | ✅ | ✅ | ✅ (suite completa) |

---

## Datos de prueba

- Las pruebas unitarias usan builders o factories in-memory.
- Las pruebas de integración usan Testcontainers + scripts de seed específicos.
- Las pruebas E2E usan el ambiente qa con datos controlados.
- **Regla:** Ningún test depende del estado de otro test; cada test es independiente y limpia su estado.
