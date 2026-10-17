# Análisis técnico de Orderflow Engine y preguntas de revisión

---

## 1. Objetivo y criterio de evaluación

El análisis debe partir del documento original `assignment/Prueba_Tecnica_Tech_Lead_1.pdf`, porque es la fuente de verdad para determinar qué solicitó el cliente. Los demás documentos —`SPEC.md`, `architecture.md`, `api-contract.md`, `data-model.md`, `TASKS.md`, `HANDOFF.md` y el ADR— sirven para entender cómo se interpretaron esos requisitos y cómo se afirma que fueron implementados.

> **Precisión importante:** el ZIP recibido contiene documentación, pero no el código fuente de `orderflow-engine-api` ni de los demás repositorios de implementación. El propio `README.es.md` indica que el código entregable está en `orderflow-engine-api`. Por eso, es posible realizar una evaluación de trazabilidad documental y del cumplimiento declarado, pero no certificar directamente que el código satisface todos los requisitos sin revisar esos repositorios.

---

## 2. Lectura de los requisitos originales

La prueba técnica divide el trabajo en tres bloques obligatorios y un complemento opcional.

### A1. Motor de cálculo del pedido

Implementar un caso de uso o endpoint que calcule el desglose económico, combine descuentos por escala, combos, obsequios e impuestos, evalúe el crédito y garantice que el precio cotizado no cambie al confirmar el pedido.

### A2. Confirmación, idempotencia y consistencia

Evitar pedidos duplicados y dobles consumos de crédito; garantizar que un pedido respondido con HTTP 201 exista y pueda consultarse; y gestionar los efectos externos de notificaciones push y publicación para el ERP.

### A3. Registro de decisión arquitectónica (ADR)

Elaborar un documento de máximo una página que explique las decisiones, las alternativas descartadas, lo que no se implementó deliberadamente, qué revisar en un code review y un riesgo con su mitigación.

### Complemento opcional: frontend

Construir una pantalla de resumen del pedido en Angular o Flutter. Debe mostrar líneas, descuentos y su origen, obsequios, impuestos y total. La evaluación visual contempla textos largos, controles que no queden ocultos y criterios uniformes para las imágenes.

### Exigencias transversales

Además, el cliente exige seis pruebas golden mínimas, un comando único para ejecutar las pruebas, un README con las decisiones esenciales y un historial de commits comprensible. La prueba no exige desplegar infraestructura productiva.

---

## 3. Contraste entre el enunciado y la solución documentada

La siguiente matriz diferencia lo que solicita el cliente de lo que registran los documentos técnicos.

| Requisito original | Evidencia documental | Evaluación |
|---|---|---|
| Cálculo detallado por línea y totales | `SPEC.md` define el desglose y `api-contract.md` especifica la cotización. | Cubierto en el diseño. |
| Convivencia y orden de las palancas comerciales | `SPEC.md` define la secuencia y sus reglas. | Cubierto en el diseño. |
| Evaluación del cupo de crédito | `SPEC.md` y `data-model.md` describen la evaluación y las restricciones. | Cubierto en el diseño. |
| Igualdad entre cotización y confirmación | Se define una cotización sellada, persistida e inmutable. | Cubierto en el diseño. |
| Precisión monetaria y configuración por país | Se documentan `BigDecimal`, escala, redondeo y datos por país. | Cubierto en el diseño. |
| Seis pruebas golden obligatorias | Se identifican GT-01 a GT-06 y sus verificaciones. | Evidencia de pruebas declarada; falta inspeccionar el código y ejecutarlas independientemente. |
| Idempotencia y garantía de HTTP 201 | Se documentan transacciones, claves de idempotencia y consultas del pedido. | Cubierto en el diseño. |
| Notificaciones push y publicación al ERP | Se describe el patrón *transactional outbox*, los reintentos y la deduplicación. | Diseño cubierto; la integración externa real está fuera del alcance. |
| ADR de máximo una página | Existen entregables del ADR en español e inglés, en Word y PDF. | Entregable documentado; su cumplimiento formal requiere revisar su extensión y contenido final. |
| Comando único, README e historial legible | Se describen `./mvnw verify` y las convenciones de commits y pull requests. | Declarado en la documentación. |
| Frontend opcional | Se documenta una ampliación a un flujo completo de compra en Angular. | Va más allá de la pantalla solicitada; no constituye por sí mismo un incumplimiento. |

### Resultado preliminar

La documentación presenta una solución coherente con los requisitos principales y desarrolla decisiones técnicas concretas para los problemas más críticos: precisión monetaria, consistencia de precios, concurrencia, idempotencia y publicación de efectos externos.

Sin embargo, el estado documentado no equivale a una auditoría independiente del código. En particular, la presencia de nombres de pruebas y criterios de aceptación demuestra que existe un plan de verificación, pero no basta por sí sola para demostrar que todas las pruebas pasan en la versión entregada.

---

## 4. Tecnologías, frameworks y conocimientos de negocio identificados

### Stack tecnológico

Según `SPEC.md`, `architecture.md` y `plan.md`, la solución documentada utiliza:

| Tecnología | Función dentro de la solución |
|---|---|
| Java 21 | Lenguaje principal y lógica del dominio. |
| Spring Boot | Servicios HTTP, casos de uso e integración con la persistencia. |
| PostgreSQL | Persistencia transaccional, restricciones e integridad de datos. |
| Liquibase | Versionamiento y ejecución de cambios en el esquema y los datos iniciales. |
| JUnit 5 | Pruebas automatizadas del backend. |
| Testcontainers | Pruebas de integración con dependencias reales en contenedores. |
| Angular | Interfaz de usuario para el flujo de compra. |
| Docker y Docker Compose | Ejecución local de los componentes y pruebas integrales. |
| JaCoCo y PIT | Medición de cobertura y análisis mediante pruebas de mutación. |
| ArchUnit | Verificación automatizada de reglas arquitectónicas. |

No debe confundirse este stack documentado con una verificación directa de las dependencias y versiones presentes en el código fuente, que no está incluido en el ZIP analizado.

### Entendimientos de negocio necesarios

Para desarrollar o auditar correctamente el sistema, se requiere comprender estos conceptos:

- **Marketplace B2B multi-tenant:** diferentes clientes empresariales operan en una misma plataforma, pero sus productos, reglas, monedas y datos deben permanecer aislados.
- **Descuentos por escala:** los porcentajes se aplican según los tramos de unidades adquiridas.
- **Combos comerciales:** un conjunto de productos recibe un precio negociado, evitando duplicar descuentos sobre las unidades consumidas por el combo.
- **Obsequios:** los productos gratuitos tienen una cantidad y un origen identificables, pero pueden generar obligaciones tributarias.
- **Base gravable:** los impuestos se calculan después de aplicar los descuentos comerciales correspondientes.
- **Crédito comercial:** confirmar una compra a crédito consume cupo disponible y requiere controlar las operaciones concurrentes.
- **Cotización y confirmación:** el precio acordado debe conservarse aunque cambien los precios o las reglas comerciales.
- **Idempotencia:** repetir una solicitud por un fallo de red no debe producir otra compra.
- **Consistencia transaccional:** una respuesta exitosa no puede preceder a la persistencia definitiva del pedido.
- **Entrega de eventos externos:** las notificaciones y publicaciones deben poder recuperarse de fallos sin crear efectos duplicados.

---

## 5. Identificación de la solución técnica

La arquitectura documentada adopta un **monolito modular con arquitectura hexagonal**, en el que los casos de uso del negocio se mantienen separados de los mecanismos de entrada, la base de datos y los sistemas externos.

El diseño se puede resumir así:

```text
Frontend Angular / API REST
Carrito, cotización, confirmación e historial
            │
            ▼
Casos de uso del dominio
Motor de precios · Cotización · Confirmación · Crédito
            │
            ▼
Adaptadores de persistencia
PostgreSQL · Transacciones · Restricciones · Migraciones
            │
            ▼
Efectos externos
Outbox transaccional → Push y ERP mediante adaptadores
```

La decisión central consiste en separar el cálculo puro de precios de la confirmación persistente del pedido. De esa manera, la lógica comercial se puede probar con entradas y resultados deterministas, mientras que la persistencia garantiza que la confirmación no duplique pedidos ni consuma crédito dos veces.

El modelo de datos respalda esta estrategia con cotizaciones inmutables, ajustes de precio registrados por origen, restricciones de unicidad, un registro de consumo de crédito y eventos pendientes de entrega. La documentación también define la expiración de las cotizaciones y el tratamiento de errores.

---

## 6. Cómo utilizar estas preguntas en la evaluación

Estas diez preguntas no deben interpretarse automáticamente como diez defectos encontrados. Son puntos de revisión que surgen de los requisitos originales y que requieren evidencia.

En particular, los documentos complementarios ya desarrollan respuestas para varios de ellos: el orden de las palancas, el tratamiento tributario de los obsequios, la expiración de cotizaciones, la idempotencia, la transacción de confirmación y el patrón *transactional outbox*. Esas decisiones deben evaluarse contra la implementación real, no volver a presentarse como ausencias sin comprobarlas.

El orden de trabajo recomendado para completar la auditoría es:

1. Revisar el código de `orderflow-engine-api` y ejecutar las seis pruebas golden originales.
2. Contrastar cada requisito A1, A2 y A3 con su implementación y prueba verificable.
3. Revisar el ADR para comprobar que las decisiones, las exclusiones y los riesgos coinciden con el código.
4. Si se evalúa el complemento opcional, inspeccionar el repositorio Angular y ejecutar sus pruebas de presentación y flujo.
5. Clasificar los hallazgos como **cumplido**, **parcialmente cumplido**, **no cumplido** o **no verificable**, citando el requisito original y la evidencia correspondiente.
