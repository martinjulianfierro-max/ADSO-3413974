# Sistema de Diseño

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

## Paleta de colores

| Token | Valor hex | Uso |
|-------|-----------|-----|
| `--color-primary` | `#003B8E` | Color principal SENA (azul institucional) |
| `--color-primary-light` | `#0052C2` | Hover de elementos primarios |
| `--color-secondary` | `#E8A400` | Acento dorado SENA |
| `--color-success` | `#1A7F4B` | Estados positivos, horario activo |
| `--color-warning` | `#D97706` | Advertencias, disponibilidad parcial |
| `--color-error` | `#DC2626` | Errores, conflictos de horario |
| `--color-background` | `#F8FAFC` | Fondo general de la aplicación |
| `--color-surface` | `#FFFFFF` | Fondo de tarjetas y paneles |
| `--color-text-primary` | `#111827` | Texto principal |
| `--color-text-secondary` | `#6B7280` | Texto secundario, etiquetas |
| `--color-border` | `#E5E7EB` | Bordes de tarjetas y separadores |

---

## Tipografía

| Uso | Fuente | Peso | Tamaño |
|-----|--------|------|--------|
| Títulos de página (H1) | Inter | 700 (Bold) | 28px |
| Subtítulos (H2) | Inter | 600 (SemiBold) | 22px |
| Encabezados de sección (H3) | Inter | 600 | 18px |
| Cuerpo de texto | Inter | 400 (Regular) | 16px |
| Texto secundario | Inter | 400 | 14px |
| Etiquetas de formulario | Inter | 500 (Medium) | 14px |
| Código / monoespaciado | JetBrains Mono | 400 | 14px |

**CDN de fuentes:**
```html
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
```

---

## Iconografía

- **Librería:** [Lucide React](https://lucide.dev/) (open source, MIT).
- Los íconos se usan siempre acompañados de texto o `aria-label` para accesibilidad.
- Tamaño estándar: 20px (inline), 24px (standalone).

---

## Espaciado

Sistema de espaciado basado en múltiplos de 4px:

| Token | Valor | Uso típico |
|-------|-------|------------|
| `--spacing-1` | 4px | Espaciado mínimo |
| `--spacing-2` | 8px | Padding interno de badges |
| `--spacing-3` | 12px | Gap entre ítems de lista |
| `--spacing-4` | 16px | Padding de componentes |
| `--spacing-6` | 24px | Espaciado entre secciones |
| `--spacing-8` | 32px | Margen entre bloques |
| `--spacing-12` | 48px | Padding de contenedores |

---

## Componentes base

### Botón primario
- Fondo: `--color-primary`, texto blanco, border-radius: 8px, padding: 10px 20px.
- Hover: `--color-primary-light`.
- Disabled: opacidad 50%, cursor `not-allowed`.

### Botón secundario (outline)
- Borde: `--color-primary`, texto: `--color-primary`, fondo transparente.

### Botón de peligro
- Fondo: `--color-error`, texto blanco.

### Tarjeta (Card)
- Fondo: `--color-surface`, borde: `1px solid --color-border`, border-radius: 12px, sombra: `0 1px 3px rgba(0,0,0,0.1)`.

### Badge de estado

| Estado | Color de fondo | Color de texto |
|--------|---------------|----------------|
| ACTIVO | `#D1FAE5` | `#065F46` |
| CANCELADO | `#FEE2E2` | `#991B1B` |
| EN_MANTENIMIENTO | `#FEF3C7` | `#92400E` |

### Formularios
- Inputs con borde `--color-border`, border-radius: 6px, focus con outline `--color-primary`.
- Los campos con error muestran borde `--color-error` y mensaje de error en rojo debajo.

---

## Breakpoints (responsive)

| Nombre | Min-width | Descripción |
|--------|-----------|-------------|
| `sm` | 360px | Celulares pequeños |
| `md` | 768px | Tablets |
| `lg` | 1024px | Laptops |
| `xl` | 1280px | Pantallas grandes |
