# Preguntas para la evaluación técnica

---

## 1. Cumplimiento del motor de precios

¿En qué medida la implementación existente cumple con los requisitos originales del cliente para calcular el precio final de un pedido, incluyendo el desglose por producto, descuentos, combos, obsequios e impuestos? ¿Qué evidencias del código y de las pruebas permiten demostrar que cada componente funciona según lo solicitado y que la suma de los importes parciales coincide con el total del pedido?

**Evalúa:** requisitos, cumplimiento funcional y pruebas verificables.

---

## 2. Complejidad de los descuentos por escala

¿Qué nivel de complejidad técnica representa implementar descuentos por escala cuando existen diferentes tramos de cantidades, porcentajes y reglas comerciales? ¿Cómo se determina el descuento marginal de cada tramo, se gestionan los límites entre cantidades y se evita que un producto reciba descuentos incorrectos o duplicados? ¿Qué pruebas de frontera permiten demostrar que la solución respeta las reglas definidas por el cliente?

**Evalúa:** palanca de descuentos por escala, algoritmos y pruebas de límites.

---

## 3. Complejidad de los combos comerciales

¿Cómo se implementa la lógica de combos para relacionar varios productos con un precio negociado y determinar qué unidades participan en el combo? ¿Qué complejidad adicional aparece cuando los productos tienen precios individuales, impuestos o descuentos por escala diferentes, y cómo garantiza la solución que no se apliquen beneficios incompatibles ni se altere el total acordado?

**Evalúa:** palanca de combos, asignación de precios e interacción entre reglas.

---

## 4. Complejidad de los obsequios

¿Qué nivel de complejidad implica implementar obsequios condicionados a la compra de determinados productos o cantidades? ¿Cómo se identifica la promoción que origina cada unidad gratuita, se evita cobrarla como una unidad ordinaria y se determina su tratamiento tributario? ¿Qué sucede si el cliente cumple simultáneamente las condiciones de varios obsequios?

**Evalúa:** palanca de obsequios, trazabilidad y reglas tributarias.

---

## 5. Complejidad de impuestos y precisión monetaria

¿Cómo se ha diseñado el cálculo de impuestos para admitir diferentes monedas, tasas tributarias y escalas decimales sin utilizar aritmética de punto flotante para los importes monetarios? ¿Qué decisiones determinan el orden del redondeo, la base gravable de cada línea y el tratamiento de los residuos, y cómo se comprueba que los totales permanecen consistentes en los distintos escenarios contemplados por el proyecto?

**Evalúa:** impuestos, política monetaria y configuración por país.
