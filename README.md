# Calculadora de capacidad y balanceo

Aplicación web de una sola página para comparar alternativas de proceso, calcular cargas por estación, capacidad, cuello de botella, cumplimiento de demanda, faltante, coste diario y productividad.

## Cómo ejecutar
Abrir `index.html` en un navegador. No requiere instalación, servidor ni dependencias externas.

## Datos simulados del anexo
**Estos datos son inventados para poder desarrollar y probar la herramienta. No son el anexo oficial del docente.**

Tiempos en segundos por unidad:

| Estación | Referencia | B | C |
|---|---:|---:|---:|
| A | 30 | 28 | 32 |
| B | 40 | 35 | 38 |
| C | 50 | 30* | 45 |
| D | 25 | 30 | 34 |

| Alternativa | Coste fijo diario | Coste variable por unidad |
|---|---:|---:|
| Referencia | $540 | $25 |
| B | $600 | $27 |
| C | $570 | $24 |

* El tiempo C de B es el parámetro del piloto, con valor inicial de 30 s/unidad.

## Supuestos
- Ventana neta de la prueba: 420 minutos.
- Inventario máximo: 350 unidades.
- Cuatro estaciones y una persona asignada a cada estación.
- Siete horas netas por persona: 28 horas-persona por jornada.
- Coste diario = coste fijo diario + coste variable unitario × volumen realizable.
- Productividad = volumen realizable / 28 horas-persona.

## Predicciones manuales para las pruebas de aceptación
Se usa capacidad por estación = (420 × 60) / tiempo de estación. La capacidad de línea es el mínimo de las capacidades de estación. El volumen realizable es el mínimo entre demanda, capacidad de línea e inventario.

| Prueba | Alternativa | Demanda | Tiempos A/B/C/D (s/u) | Cuello | Capacidad línea | Volumen realizable | Faltante | Coste diario | Productividad |
|---|---|---:|---|---|---:|---:|---:|---:|---:|
| 1 | Referencia | 300 | 30/40/50/25 | C | 504 | 300 | 0 | $8,040 | 10.71 u/h-persona |
| 2 | B | 300 | 28/35/30/30 | B | 720 | 300 | 0 | $8,700 | 10.71 u/h-persona |
| 3 | C | 308 | 32/38/45/34 | C | 560 | 308 | 0 | $7,962 | 11.00 u/h-persona |

En las tres pruebas la capacidad teórica de línea supera 350 unidades, por lo que la app debe advertir que el inventario limita el volumen máximo posible. Las demandas indicadas sí se cubren porque son menores que 350.

## Fórmulas
- Capacidad estación (unidades/jornada) = ventana neta (min) × 60 / tiempo normal (s/unidad).
- Capacidad línea = mínimo de las capacidades de estación.
- Volumen realizable = mínimo(demanda, capacidad línea, 350).
- Faltante = máximo(0, demanda − volumen realizable).
- Coste diario = coste fijo diario + coste variable unitario × volumen realizable.
- Productividad = volumen realizable / 28 horas-persona.

## Limitaciones
Es un cálculo de régimen: supone tiempos constantes y no modela variabilidad, fallas, reprocesos, aprendizaje, esperas correlacionadas ni restricciones adicionales. Los resultados deben sustituirse o validarse cuando se reciba el anexo patrón real.
