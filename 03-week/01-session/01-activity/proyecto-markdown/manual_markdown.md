# 📘 Manual de Markdown

## ¿Qué es Markdown?

Markdown es un lenguaje de marcado ligero que permite crear documentos estructurados usando texto simple.

Es muy usado en:

- Documentación de software
- GitHub
- Blogs técnicos
- Wikis

---

# Sintaxis básica

## Títulos

```
# Título 1
## Título 2
### Título 3
```

---

## Negrita y cursiva

```
**Texto en negrita**
*Texto en cursiva*
```

---

## Listas

Lista con viñetas:

```
- Elemento 1
- Elemento 2
- Elemento 3
```

Lista numerada:

```
1. Paso uno
2. Paso dos
3. Paso tres
```

---

## Enlaces

```
[Ir a GitHub](https://github.com)
```

---

## Código

Código en línea:

```
`git commit`
```

Bloque de código:

```bash
git status
git add .
git commit -m "Actualización del manual"
```

---

## Tablas

```
| Nombre | Edad |
|------|------|
| Juan | 20 |
| Ana | 22 |
```

---

# Uso de Git para guardar cambios

Para guardar cambios en un proyecto se usan **commits**.

Ejemplo:

```bash
git status
git add .
git commit -m "Creación del manual Markdown"
git push origin main
```

Esto permite registrar los cambios en el historial del proyecto.

---

# Conclusión

Markdown es una herramienta sencilla y poderosa para crear documentación clara y organizada, especialmente en proyectos de desarrollo de software.