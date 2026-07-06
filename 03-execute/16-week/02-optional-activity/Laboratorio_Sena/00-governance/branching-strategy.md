# Estrategia de Ramas (Branching Strategy)

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Diagrama visual del flujo de ramas

```
                    ┌─────────────────────────────┐
                    │           main               │ ← Documentación estable / Producción
                    └──────────────┬──────────────┘
                                   │
                    ┌──────────────▼──────────────┐
                    │            qa                │ ← Validación funcional
                    └──────────────┬──────────────┘
                                   │
                    ┌──────────────▼──────────────┐
                    │            dev               │ ← Integración continua
                    └──────┬──────────────┬────────┘
                           │              │
             ┌─────────────▼──┐    ┌──────▼──────────────┐
             │  hu-01-dev      │    │  hu-02-dev           │  ← Ramas de trabajo
             └─────────────────┘    └─────────────────────┘
```

---

## Ramas protegidas

| Rama | Protección | Descripción |
|------|------------|-------------|
| `main` | Push directo bloqueado. Requiere PR con 2 aprobaciones. | Documentación estable y código en producción. |
| `qa` | Push directo bloqueado. Requiere PR con 1 aprobación. | Ambiente de validación funcional. |
| `dev` | Push directo bloqueado. Requiere PR con 1 aprobación + CI verde. | Integración continua de trabajo en desarrollo. |

---

## Tipos de ramas de trabajo

| Tipo | Formato | Rama base | Ejemplo | Descripción |
|------|---------|-----------|---------|-------------|
| Historia de usuario (dev) | `hu-{N}-dev` | `dev` | `hu-01-dev` | Implementación de una HU hacia el ambiente dev |
| Historia de usuario (qa) | `hu-{N}-qa` | `qa` | `hu-01-qa` | Validación de una HU en ambiente qa |
| Release | `release/{iteración}` | `main` | `release/iteration-01` | Acumula HUs de una iteración para producción |
| Documento nuevo | `feat/doc-{descripción}` | `dev` | `feat/doc-api-guidelines` | Nuevo documento en el repo |
| Corrección de contenido | `fix/doc-{descripción}` | `dev` | `fix/doc-scope` | Corrección en un documento existente |
| Hotfix en producción | `fix/doc-{descripción}` | `main` | `fix/doc-broken-contract` | Corrección urgente en `main` |
| Reorganización | `chore/doc-{descripción}` | `dev` | `chore/doc-move-adr` | Mover o renombrar archivos |

---

## Flujo estándar de una historia de usuario

```bash
# 1. Partir desde dev actualizado
git checkout dev && git pull origin dev

# 2. Crear rama de trabajo
git checkout -b hu-05-dev

# 3. Desarrollar (commits pequeños)
git add <archivos>
git commit -m "docs(04-requirements): add HU-005 criteria"

# 4. Push y abrir PR → dev
git push origin hu-05-dev
# Abrir PR en GitHub: hu-05-dev → dev

# 5. Review aprobado → merge (squash recomendado)
# GitHub hace el merge

# 6. Cuando la HU pasa a QA
git checkout qa && git pull origin qa
git checkout -b hu-05-qa
git cherry-pick <commit-sha-o-merge-dev>
git push origin hu-05-qa
# Abrir PR: hu-05-qa → qa

# 7. Release a main
git checkout main && git pull origin main
git checkout -b release/iteration-01
git cherry-pick <commits de las HUs de la iteración>
git push origin release/iteration-01
# Abrir PR: release/iteration-01 → main
```

---

## Reglas adicionales

- Una rama `hu-*` representa **una sola historia de usuario**. No mezclar HUs.
- Las ramas obsoletas (ya mergeadas) deben eliminarse del remoto.
- No hacer commits directamente en `dev`, `qa` o `main`.
- Si el pipeline CI falla en un PR, el autor es responsable de corregirlo antes de solicitar review.
