---
layout: post
title: "Ejemplo: Tablas Markdown vs HTML"
---

Este es un ejemplo para probar ambos formatos de tabla.

## Tabla en Markdown

Simple y editable, pero formato limitado:

| Concepto     | Q1    | Q2    | Q3    | Q4    |
|--------------|------:|------:|------:|------:|
| Ventas       | 1.250 | 1.380 | 1.420 | 1.590 |
| Costes       |   890 |   920 |   950 | 1.010 |
| **Margen**   |   360 |   460 |   470 |   580 |

## Tabla en HTML

Más control, útil al copiar desde Excel guardado como HTML:

<table>
  <thead>
    <tr>
      <th>Concepto</th>
      <th class="num">Q1</th>
      <th class="num">Q2</th>
      <th class="num">Q3</th>
      <th class="num">Q4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Ventas</td>
      <td class="num">1.250</td>
      <td class="num">1.380</td>
      <td class="num">1.420</td>
      <td class="num">1.590</td>
    </tr>
    <tr>
      <td>Costes</td>
      <td class="num">890</td>
      <td class="num">920</td>
      <td class="num">950</td>
      <td class="num">1.010</td>
    </tr>
    <tr>
      <td><strong>Margen</strong></td>
      <td class="num"><strong>360</strong></td>
      <td class="num"><strong>460</strong></td>
      <td class="num"><strong>470</strong></td>
      <td class="num"><strong>580</strong></td>
    </tr>
  </tbody>
</table>

---

## Notas

- Las tablas Markdown son más rápidas de escribir
- Las tablas HTML permiten clases CSS (como `num` para alinear números)
- Desde Excel: Guardar como HTML → copiar el `<table>` generado
