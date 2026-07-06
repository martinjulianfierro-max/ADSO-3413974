# Revisión de Código

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Proceso de revisión

Todo código que se integra a las ramas protegidas (`dev`, `qa`, `main`) debe pasar por al menos **1 revisión aprobada** de un compañero de equipo antes del merge. Las ramas `dev` y `qa` requieren 1 revisor; `main` requiere 2.

---

## Checklist de revisión (el revisor debe verificar cada ítem)

### Funcionalidad
- [ ] El código implementa lo que describe la historia de usuario o el ADR.
- [ ] Los criterios de aceptación de la HU quedan cubiertos.
- [ ] No se introduce lógica no solicitada ("gold plating").

### Calidad del código
- [ ] No hay código duplicado que debería estar en un método/clase reutilizable.
- [ ] Los nombres de variables, métodos y clases son descriptivos y en inglés.
- [ ] No hay comentarios que expliquen "qué hace" el código (el código debe ser autoexplicativo); solo comentarios que expliquen "por qué" si es no obvio.
- [ ] No hay código comentado ni `TODO` sin ticket asociado.
- [ ] El código cumple el estilo definido (Checkstyle para Java, ESLint para JavaScript).

### Pruebas
- [ ] Se incluyen pruebas unitarias para la lógica nueva.
- [ ] Las pruebas fallan si se revierte el cambio (son efectivas).
- [ ] No hay lógica de prueba en el código de producción.
- [ ] La cobertura de pruebas del PR no disminuye respecto a la rama base.

### Seguridad
- [ ] No hay credenciales, secretos ni tokens hardcodeados.
- [ ] Los inputs del usuario se validan y sanitizan en el servidor.
- [ ] Los endpoints nuevos están protegidos con el rol correcto.
- [ ] No se registran datos personales en logs.

### Arquitectura
- [ ] El código respeta los límites del bounded context de su microservicio.
- [ ] No hay referencias directas a tablas o BDs de otros servicios.
- [ ] Las dependencias nuevas están justificadas y documentadas.

### Documentación
- [ ] Si se modifica un contrato de API, el archivo OpenAPI está actualizado.
- [ ] Si se crea una entidad nueva, el diccionario de datos está actualizado.
- [ ] El `CHANGELOG.md` tiene una entrada para el cambio (si aplica).

---

## Criterios de aprobación

Un PR se puede mergear si:
- ✅ Todos los ítems del checklist están verificados.
- ✅ El pipeline CI pasa completamente (lint + build + pruebas).
- ✅ Al menos 1 revisor (o 2 para `main`) ha aprobado formalmente.
- ✅ No hay conversaciones sin resolver en el PR.

---

## Criterios de rechazo (request changes)

Un revisor debe pedir cambios si detecta:
- ❌ Lógica de negocio incorrecta o incompleta.
- ❌ Credenciales o datos sensibles en el código.
- ❌ Ausencia total de pruebas en lógica nueva.
- ❌ Violación de los límites entre microservicios.
- ❌ Código que no compila o pruebas que fallan localmente.

---

## Tiempo de revisión esperado

- El revisor asignado debe dar feedback en máximo **1 día hábil**.
- Si el autor no recibe feedback en 1 día hábil, puede asignar otro revisor.
- Reviews bloqueados por más de 2 días sin respuesta se escalan al líder técnico.
