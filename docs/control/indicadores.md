# Indicadores de control y estándares de desempeño

Siete indicadores para la auditoría técnica del módulo. Las entidades son las del diccionario de datos.

| ID | Indicador | Cómo se mide | Estándar | Frecuencia | Responsable |
| --- | --- | --- | --- | --- | --- |
| I1 | Exactitud del stock (M5) | \|stock del sistema − conteo físico\| ÷ conteo físico × 100, en 30 artículos al azar. Fuente: LOTE y planilla de conteo. | < 2 % | Mensual | Depósito |
| I2 | Costo bien calculado | Facturas con todos los costos bien ÷ facturas revisadas × 100 (10 por mes). Fuente: COMPRA, LOTE y facturas. | 100 % | Mensual | Administración y Finanzas |
| I3 | Precios al día (M4) | Compras costeadas el mismo día en que llegaron ÷ compras recibidas × 100. Fuente: COMPRA (fecha_recepcion y fecha_costeo). | 100 % | Diaria | Administración y Finanzas |
| I4 | Mercadería vencida | Costo de lotes vencidos sin vender ÷ costo de lo comprado en el mes × 100. Fuente: LOTE y COMPRA. | ≤ 1 % | Mensual | Depósito |
| I5 | Quiebre de stock | Artículos activos bajo su mínimo ÷ artículos activos × 100. Fuente: ARTICULO y LOTE. | ≤ 5 % | Diaria | Compras |
| I6 | Tiempo de respuesta (M2 y M3) | Segundos para buscar un artículo por código de barras y para recalcular los precios de una factura (promedio de 10 pruebas). | Búsqueda < 1 s y recálculo < 5 s | Mensual | Administración y Finanzas |
| I7 | Disponibilidad del sistema | Horas sin caídas ÷ horas de atención × 100. Fuente: registro de caídas. | ≥ 99 % | Mensual | Administración y Finanzas |

## Semáforo y acciones

| ID | Verde | Amarillo | Rojo | Acción si queda en rojo |
| --- | --- | --- | --- | --- |
| I1 | menos de 2 % | de 2 a 4 % | más de 4 % | Recontar, revisar las cargas del mes y repasar con Depósito cómo se cargan los lotes. |
| I2 | 100 % | de 90 a menos de 100 % | menos de 90 % | Revisar descuentos y alícuotas de IVA (10,5 % o 21 %), corregir lotes y recalcular precios. |
| I3 | 100 % | de 95 a menos de 100 % | menos de 95 % | Buscar compras sin costear y destrabarlas en el día. |
| I4 | ≤ 1 % | más de 1 y hasta 2 % | más de 2 % | Vender primero los lotes que vencen antes y ajustar cantidades de compra. |
| I5 | ≤ 5 % | más de 5 y hasta 10 % | más de 10 % | Revisar stocks mínimos y frecuencia de pedidos. |
| I6 | menos de 1 s y de 5 s | de 1 a 1,5 s o de 5 a 7,5 s | más de 1,5 s o de 7,5 s | Revisar búsquedas lentas y repetir la prueba con datos masivos (meta M3). |
| I7 | ≥ 99 % | de 97 a menos de 99 % | menos de 97 % | Registrar cada caída, buscar la causa y pedir soporte. |

## Mecanismos de control

| Tipo | Mecanismo | Dónde está |
| --- | --- | --- |
| Preventivo | No deja guardar un lote sin cantidad o vencimiento. | Validación del módulo (HU-01) |
| Preventivo | Una suba de más del 15 % pasa por la Dirección. | Compuerta del BPMN |
| Preventivo | Ningún cambio entra a `main` sin un PR revisado. | Regla del repositorio |
| Concurrente | Alertas diarias de stock bajo y lotes por vencer. | Tablero de indicadores (HU-03) |
| Retroalimentación | Auditoría mensual: conteo físico contra sistema y revisión de indicadores. | Informe a la Dirección |

## Auditoría

- I3 e I5 se siguen todos los días en el tablero del módulo.
- Una vez por mes se calculan todos y se arma un informe corto para la Dirección.
- Cada tres meses la Dirección revisa si los estándares siguen siendo los correctos.
