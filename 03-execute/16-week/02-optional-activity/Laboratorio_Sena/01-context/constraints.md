# Restricciones del Sistema

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Restricciones institucionales

| ID | Restricción | Fuente |
|----|-------------|--------|
| INST-01 | Solo personal autorizado del SENA puede crear o modificar horarios. El sistema no permite auto-asignación de instructores. | Reglamento interno CBA |
| INST-02 | Los datos personales de aprendices e instructores deben tratarse conforme a la Ley 1581 de 2012 (Habeas Data). | Legislación colombiana |
| INST-03 | El sistema debe operar durante el horario institucional (6:00–22:00, lunes a sábado). | Jornada institucional SENA |
| INST-04 | El sistema se despliega inicialmente solo para el Centro de Biotecnología Agropecuaria (CBA). | Alcance del proyecto |
| INST-05 | No se integra con SOFIA Plus ni Territorium en el MVP; la interoperabilidad se evaluará en fases futuras. | Decisión de alcance |

---

## Restricciones técnicas

| ID | Restricción | Justificación |
|----|-------------|---------------|
| TEC-01 | Stack tecnológico acordado: Spring Boot (Java 17) para backend, React para frontend, PostgreSQL para base de datos. | Decisión de arquitectura (ADR-001, ADR-002) |
| TEC-02 | La solución debe funcionar en navegadores modernos: Chrome 110+, Firefox 115+, Edge 110+. Sin soporte para IE11. | Base de usuarios institucionales |
| TEC-03 | El sistema debe soportar conexiones de baja velocidad (≥ 1 Mbps). Las respuestas de API no deben superar 2 segundos bajo carga normal. | Realidad de conectividad en centros SENA |
| TEC-04 | No se permite el uso de librerías con licencias restrictivas (GPL-3 o superior) en el componente productivo. | Política de open source del equipo |
| TEC-05 | El sistema debe operar en zona horaria America/Bogota (UTC-5). Toda fecha/hora se almacena en UTC en base de datos. | Coherencia temporal |
| TEC-06 | El backend se despliega con Docker y orquestado con Docker Compose para desarrollo local; el ambiente de producción se define en `10-devops`. | Estrategia DevOps |

---

## Restricciones regulatorias

| ID | Restricción | Norma |
|----|-------------|-------|
| REG-01 | El sistema no puede retener contraseñas en texto plano. Debe usarse bcrypt o argon2. | OWASP Top 10, buenas prácticas |
| REG-02 | Los logs del sistema no deben incluir datos personales sensibles (cédulas, correos completos). | Ley 1581 de 2012 |
| REG-03 | La comunicación entre cliente y servidor debe ser exclusivamente por HTTPS en producción. | Política de seguridad institucional |

---

## Restricciones de proyecto

| ID | Restricción | Detalle |
|----|-------------|---------|
| PROY-01 | Equipo formado exclusivamente por aprendices ADSO. No hay presupuesto para contratar personal externo. | Naturaleza del proyecto formativo |
| PROY-02 | No se pueden adquirir licencias de software propietario de pago. | Presupuesto cero |
| PROY-03 | El MVP debe estar funcional dentro del ciclo de formación vigente (~6 meses). | Cronograma académico SENA |
| PROY-04 | Toda la documentación del proyecto debe mantenerse en este repositorio. | Regla de gobernanza (ver `00-governance`) |
