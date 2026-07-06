# Objetos de Valor

> Estado: 🟢 | Última actualización: 2026-07-06
> Autor: Equipo ADSO | Equipo: Desarrollo

---

Los **objetos de valor** son tipos inmutables que no tienen identidad propia pero encapsulan lógica de validación y significado del dominio.

---

## RangoHorario

Representa un intervalo de tiempo con inicio y fin. Encapsula las reglas de validación de bloques.

```
RangoHorario {
  inicio: DateTime   // en UTC
  fin:    DateTime   // en UTC
}
```

**Reglas de validación:**
- `fin` debe ser estrictamente mayor que `inicio`.
- La duración debe ser mínimo 1 hora y máximo 4 horas.
- `inicio` debe caer en un múltiplo de 30 minutos (HH:00 o HH:30).
- Ambos valores deben estar en zona horaria UTC al persistir.

**Comportamientos:**
- `solapaCon(otro: RangoHorario): Boolean` — retorna `true` si los rangos se solapan.
- `duracionHoras(): Double` — calcula la duración en horas.
- `enZonaLocal(): String` — retorna el rango formateado en America/Bogota.

---

## Jornada

Franja horaria institucional del SENA.

```
Jornada (enum) {
  DIURNA   → 06:00 – 14:00
  TARDE    → 14:00 – 22:00
  NOCTURNA → 18:00 – 22:00
}
```

**Comportamientos:**
- `contieneBloque(rango: RangoHorario): Boolean` — verifica si un bloque cae dentro de la jornada.
- `label(): String` — retorna etiqueta legible para UI.

---

## Email

Dirección de correo electrónico validada.

```
Email {
  valor: String
}
```

**Reglas:**
- Debe cumplir formato `usuario@dominio.tld`.
- No puede estar vacío ni contener espacios.

---

## Cedula

Número de identificación colombiano.

```
Cedula {
  numero: String
}
```

**Reglas:**
- Solo dígitos numéricos.
- Entre 6 y 10 caracteres.
- No puede estar vacía.

---

## CodigoFicha

Código oficial de una ficha SENA.

```
CodigoFicha {
  valor: String
}
```

**Reglas:**
- Exactamente 7 dígitos numéricos.
- Ejemplo válido: `2879723`.
