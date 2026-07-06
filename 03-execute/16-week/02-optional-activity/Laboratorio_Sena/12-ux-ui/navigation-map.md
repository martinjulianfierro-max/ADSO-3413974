# Mapa de Navegación

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Estructura de navegación por rol

### Rol: Sin autenticación (público)

```
/ (raíz)
├── /login                     ← Formulario de login
└── /horarios/ficha            ← Consulta pública de horario por código de ficha
```

---

### Rol: COORDINADOR

```
/dashboard
├── /horarios
│   ├── /horarios (listado con filtros)
│   ├── /horarios/nuevo
│   ├── /horarios/{id} (detalle)
│   │   └── /horarios/{id}/historial
│   └── /horarios/{id}/editar
├── /fichas
│   ├── /fichas (listado)
│   ├── /fichas/nueva
│   └── /fichas/{id}/editar
├── /instructores
│   ├── /instructores (listado)
│   ├── /instructores/nuevo
│   └── /instructores/{id}/editar
├── /ambientes
│   ├── /ambientes (listado)
│   ├── /ambientes/nuevo
│   └── /ambientes/{id}/editar
└── /perfil
```

---

### Rol: INSTRUCTOR

```
/dashboard
├── /mi-horario               ← Vista semanal del horario propio
│   └── /mi-horario?semana={iso-week}
├── /disponibilidad           ← Declarar disponibilidad semanal
└── /perfil
```

---

### Rol: APRENDIZ

```
/dashboard
├── /mi-ficha                 ← Horario de la ficha del aprendiz
└── /perfil
```

---

### Rol: ADMIN

```
/dashboard
├── /usuarios
│   ├── /usuarios (listado)
│   ├── /usuarios/nuevo
│   └── /usuarios/{id}/editar
├── /horarios (igual que coordinador)
├── /fichas (igual que coordinador)
├── /instructores (igual que coordinador)
├── /ambientes (igual que coordinador)
└── /perfil
```

---

## Diagrama de flujo principal (Coordinador — Crear horario)

```
[Login] ──▶ [Dashboard] ──▶ [/horarios] ──▶ [Botón "Nuevo horario"]
                                                     │
                                                     ▼
                                           [Formulario /horarios/nuevo]
                                           - Seleccionar ficha
                                           - Seleccionar instructor
                                           - Seleccionar ambiente
                                           - Elegir bloque de tiempo
                                           - Verificación de conflictos (tiempo real)
                                                     │
                                        ┌────────────┴─────────────┐
                                  [Sin conflicto]           [Conflicto detectado]
                                        │                         │
                                   [Confirmar]              [Alerta + corregir]
                                        │
                                   [Horario creado ✓]
                                   [Redirect a /horarios]
```

---

## Componentes de navegación global

| Componente | Descripción |
|-----------|-------------|
| **Barra lateral (sidebar)** | Menú de navegación principal; colapsable en mobile. Muestra las rutas según el rol. |
| **Barra superior (topbar)** | Nombre del sistema, notificaciones y menú de usuario (perfil/logout). |
| **Breadcrumbs** | Ruta de navegación actual en páginas de detalle y formularios. |
| **Tabs** | Para alternar entre semanas en la vista de horario. |
