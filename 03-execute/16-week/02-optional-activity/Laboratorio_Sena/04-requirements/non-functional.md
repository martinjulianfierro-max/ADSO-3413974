# Requisitos No Funcionales

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## RNF-001 — Rendimiento

| Atributo | Detalle |
|----------|---------|
| **ID** | RNF-001 |
| **Categoría** | Rendimiento |
| **Descripción** | El tiempo de respuesta de las APIs para operaciones de lectura (consulta de horarios, fichas, instructores) no debe superar los **2 segundos** en el percentil 95 bajo carga normal (hasta 50 usuarios concurrentes). Las operaciones de escritura (crear/editar horario) no deben superar **3 segundos**. |
| **Métrica** | p95 latencia < 2s (lectura), < 3s (escritura) con 50 usuarios concurrentes |

---

## RNF-002 — Disponibilidad

| Atributo | Detalle |
|----------|---------|
| **ID** | RNF-002 |
| **Categoría** | Disponibilidad |
| **Descripción** | El sistema debe estar disponible al menos el **99%** del tiempo durante el horario institucional (lunes a sábado, 06:00–22:00). Las ventanas de mantenimiento planificado se realizan los domingos. |
| **Métrica** | Uptime ≥ 99% en horario institucional |

---

## RNF-003 — Seguridad

| Atributo | Detalle |
|----------|---------|
| **ID** | RNF-003 |
| **Categoría** | Seguridad |
| **Descripción** | Toda la comunicación entre cliente y servidor debe realizarse exclusivamente por **HTTPS** en producción. Las contraseñas deben almacenarse con **bcrypt** (factor de coste mínimo 12). Los tokens JWT deben expirar en máximo 8 horas. Los inputs del usuario deben sanitizarse para prevenir XSS e inyección SQL. |

---

## RNF-004 — Escalabilidad

| Atributo | Detalle |
|----------|---------|
| **ID** | RNF-004 |
| **Categoría** | Escalabilidad |
| **Descripción** | El sistema debe diseñarse con una arquitectura de microservicios que permita escalar horizontalmente cada servicio de forma independiente. En el MVP, se escala verticalmente (un solo nodo por servicio); en versiones futuras debe soportar múltiples instancias con balanceo de carga. |

---

## RNF-005 — Usabilidad

| Atributo | Detalle |
|----------|---------|
| **ID** | RNF-005 |
| **Categoría** | Usabilidad |
| **Descripción** | Un coordinador sin entrenamiento previo debe poder crear su primer horario en menos de **10 minutos** usando solo la interfaz del sistema. La interfaz debe ser responsiva y funcionar en pantallas desde 360px de ancho (celulares) hasta 1920px (escritorio). |

---

## RNF-006 — Compatibilidad

| Atributo | Detalle |
|----------|---------|
| **ID** | RNF-006 |
| **Categoría** | Compatibilidad |
| **Descripción** | El frontend debe funcionar correctamente en las últimas 2 versiones de Chrome, Firefox y Edge. No se requiere soporte para Internet Explorer. La interfaz debe funcionar en conexiones de mínimo 1 Mbps. |

---

## RNF-007 — Mantenibilidad

| Atributo | Detalle |
|----------|---------|
| **ID** | RNF-007 |
| **Categoría** | Mantenibilidad |
| **Descripción** | El código debe seguir los estándares de cada tecnología (Google Java Style Guide, ESLint para JavaScript). La cobertura de pruebas unitarias del backend debe ser igual o superior al **80%**. Cada microservicio debe tener su propio `README.md` con instrucciones de despliegue local. |

---

## RNF-008 — Privacidad de datos

| Atributo | Detalle |
|----------|---------|
| **ID** | RNF-008 |
| **Categoría** | Privacidad |
| **Descripción** | El sistema debe cumplir con la Ley 1581 de 2012 (Habeas Data). Los logs de aplicación no deben incluir datos personales en texto plano (cédulas, correos, nombres completos). Solo usuarios con rol `ADMIN` o `COORDINADOR` pueden ver datos personales de instructores. |

---

## RNF-009 — Recuperación ante fallos

| Atributo | Detalle |
|----------|---------|
| **ID** | RNF-009 |
| **Categoría** | Confiabilidad |
| **Descripción** | El sistema de base de datos debe tener respaldos automáticos diarios. El RTO (Recovery Time Objective) es de máximo 4 horas. El RPO (Recovery Point Objective) es de máximo 24 horas (se acepta perder máximo 1 día de datos en caso de fallo catastrófico). |

---

## RNF-010 — Internacionalización

| Atributo | Detalle |
|----------|---------|
| **ID** | RNF-010 |
| **Categoría** | Localización |
| **Descripción** | El sistema opera exclusivamente en **español (Colombia)**. Las fechas y horas se muestran en formato DD/MM/YYYY y HH:mm respectivamente. La zona horaria de presentación es siempre **America/Bogota (UTC-5)**. |
