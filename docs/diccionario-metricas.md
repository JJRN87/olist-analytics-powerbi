# Diccionario de métricas — Olist Analytics

Esta página recoge qué significa cada indicador de la primera versión del informe. Las definiciones se basan en las medidas creadas durante el proyecto.

| Indicador | Cálculo | Qué conviene tener en cuenta |
| --- | --- | --- |
| Importe Vendido | `SUM(stgArticulos[price])` | Importe de artículos registrados, sin transporte. No es margen, beneficio ni ventas netas completadas. |
| Pedidos Totales | `DISTINCTCOUNT(stgPedidos[order_id])` | Incluye todos los estados de pedido, no solo entregados. |
| Clientes Únicos | `DISTINCTCOUNT(stgClientes[customer_unique_id])` | Diferencia compradores de referencias `customer_id` asociadas a pedidos. Su filtrado por producto/vendedor requiere validación específica. |
| Ticket Medio | Importe de artículos / pedidos distintos presentes en `stgArticulos` | Su denominador no incluye pedidos sin líneas de artículos. |
| Pedidos Entregados | Pedidos en categorías **En plazo** o **Con retraso** | Excluye entregas sin fecha suficiente y otros estados. |
| Pedidos Retrasados | Pedidos con `Estado Entrega = "Con retraso"` | Compara por fecha natural de entrega frente a fecha prevista. |
| Porcentaje Retrasos | Pedidos retrasados / pedidos entregados evaluables | No confundir con el porcentaje sobre todos los pedidos del gráfico de anillos. |
| Días Medios Entrega | Media de `DATEDIFF(compra, entrega, DAY)` en pedidos entregados con fechas | Aproximación en días enteros por pedido, no tiempo exacto en horas. |
| Valoración Media | `AVERAGE(stgValoraciones[review_score])` | Media por registro, no necesariamente una valoración por pedido. |
| Valoraciones Registradas | `COUNTROWS(stgValoraciones)` | Cuenta todas las filas de valoración. |
| Pedidos Valorados | `DISTINCTCOUNT(stgValoraciones[order_id])` | Cada pedido se cuenta una sola vez. |
| Valoraciones adicionales | Registros de valoración menos pedidos valorados | No demuestra por sí mismo errores o reseñas fraudulentas. |
| Valoraciones negativas | Registros con puntuación 1–2 / total de registros de valoración | Calculado por registro de valoración. |
| Pedidos Sin Fecha Entrega | Estado `delivered` sin fecha real de entrega | Caso que necesita revisión; no clasificar automáticamente como puntual. |
| Pedidos Fecha Incoherente | Fecha de entrega anterior a compra, entre registros con ambas fechas | La comprobación encontró cero casos bajo esta regla. |
| Pedidos Sin Artículos | Pedidos sin coincidencia en tabla de artículos | Puede incluir estados legítimos sin artículos registrados. |

## Decisiones de visualización

- El calendario filtra por **fecha de compra**.
- Se excluyó del gráfico mensual el último mes con información incompleta; el filtro es visual y no borra datos del modelo.
- El gráfico de satisfacción según puntualidad compara únicamente **En plazo** frente a **Con retraso**.
- Los controles de calidad se calcularon inicialmente sobre el conjunto histórico y requieren revisión cuando se introduzcan más filtros.

## Pendiente de validar

- Comportamiento de determinados KPI cuando se seleccionan categorías o vendedores, debido a la dirección de las relaciones.
- Criterio de venta completada y exclusión de pedidos cancelados.
- Tratamiento de múltiples reseñas del mismo pedido.
- Umbral mínimo de pedidos evaluables en los porcentajes por estado.
