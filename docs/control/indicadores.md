# Indicadores de control y estándares de desempeño

Controlar es medir el desempeño, compararlo con un estándar y corregir los desvíos (Robbins y Coulter, 2014). Estos indicadores sirven para la **auditoría técnica** del Módulo de Gestión de Inventario y Costeo Dinámico. La mayoría de los datos salen de las entidades del [diccionario de datos](../datos/diccionario-de-datos.md); los demás, de un conteo físico o de registros simples.

## Mecanismos de control según el momento en que actúan

| Tipo | Mecanismo | Dónde está |
|---|---|---|
| Preventivo | El sistema no deja guardar un lote si le falta la cantidad o el vencimiento. | Validación del módulo (HU-01) |
| Preventivo | Si un artículo sube más del 15 %, la suba pasa por la Dirección antes de publicarse. | Compuerta del BPMN |
| Preventivo | Desde que se armó la base del repositorio, ningún cambio entra a `main` sin un PR aprobado por un par. | Regla del repositorio |
| Concurrente | Alertas diarias de stock bajo y de lotes por vencer. | Tablero de indicadores (HU-03) |
| Retroalimentación | Auditoría mensual: conteo físico contra el stock del sistema y revisión de los indicadores. | Informe a la Dirección |

## De dónde sale cada indicador

Los indicadores salen de las entregas anteriores:

- **Metas de la Entrega N.º 2.** I1 controla la M5 (stock confiable), I3 la M4 (precios al día) e I6 la M2 (tiempo de respuesta). Medir el I6 a medida que crece la base también controla la M3 (escalabilidad).
- **Problemas de la Entrega N.º 1.** I2 controla los costos mal calculados, I4 la mercadería que se vence e I5 los faltantes de stock.
- **Amenaza del FODA (Entrega N.º 2).** I7 mide si el sistema está disponible, porque una actualización del sistema de gestión puede cortar la conexión.
- La **M1 (plazo)** es del proyecto y no del sistema: se controla con el Gantt y con el tablero.

## Indicadores

| ID | Indicador | Cómo se mide | Fuente de datos | Estándar | Frecuencia | Responsable |
|---|---|---|---|---|---|---|
| I1 | Exactitud del stock (M5) | \|stock del sistema − conteo físico\| ÷ conteo físico × 100, en 30 artículos al azar | LOTE y planilla de conteo | < 2 % | Mensual | Depósito |
| I2 | Costo bien calculado | Facturas con todos los costos bien ÷ facturas revisadas × 100 (10 por mes) | COMPRA, LOTE y facturas | 100 % | Mensual | Administración y Finanzas |
| I3 | Precios al día (M4) | Compras costeadas el mismo día en que llegaron ÷ compras recibidas × 100. Con 100 %, ningún artículo queda con costo nuevo y precio viejo | COMPRA (`fecha_recepcion` y `fecha_costeo`) | 100 % | Diaria | Administración y Finanzas |
| I4 | Mercadería vencida | Costo de lotes vencidos sin vender ÷ costo de lo comprado en el mes × 100 | LOTE y COMPRA | ≤ 1 % | Mensual | Depósito |
| I5 | Quiebre de stock | Artículos activos bajo su mínimo ÷ artículos activos × 100 | ARTICULO y LOTE | ≤ 5 % | Diaria | Compras |
| I6 | Tiempo de respuesta (M2 y M3) | Segundos que tarda el módulo en buscar un artículo por código de barras y en recalcular los precios de una factura (promedio de 10 pruebas) | Registro de tiempos del módulo | Búsqueda < 1 s y recálculo < 5 s | Mensual | Administración y Finanzas |
| I7 | Disponibilidad del sistema | Horas sin caídas ÷ horas de atención × 100 | Registro de caídas | ≥ 99 % | Mensual | Administración y Finanzas |

## Semáforo y acciones correctivas

Verde: cumple el estándar. Amarillo: se aleja un poco y hay que mirarlo. Rojo: se aleja mucho y pide una acción correctiva. Los límites no dejan huecos entre un color y otro.

| ID | 🟢 Verde | 🟡 Amarillo | 🔴 Rojo | Acción si queda en rojo |
|---|---|---|---|---|
| I1 | menos de 2 % | de 2 a 4 % | más de 4 % | Recontar los artículos con diferencia, revisar las cargas del mes y repasar con Depósito cómo se cargan los lotes. |
| I2 | 100 % | de 90 a menos de 100 % | menos de 90 % | Revisar descuentos y alícuotas de IVA (algunos productos llevan 10,5 % y no 21 %), corregir los lotes y recalcular precios. |
| I3 | 100 % | de 95 a menos de 100 % | menos de 95 % | Buscar las compras sin costear (subas frenadas en la Dirección o artículos sin alta) y destrabarlas en el día. |
| I4 | ≤ 1 % | más de 1 y hasta 2 % | más de 2 % | Depósito avisa a Comercial para vender primero los lotes que vencen antes, y Compras ajusta las cantidades. |
| I5 | ≤ 5 % | más de 5 y hasta 10 % | más de 10 % | Revisar los stocks mínimos y la frecuencia de los pedidos. |
| I6 | menos de 1 s y de 5 s | de 1 a 1,5 s o de 5 a 7,5 s | más de 1,5 s o de 7,5 s | Revisar con el programador las búsquedas lentas y, si la base creció, repetir la prueba con datos masivos de la meta M3. |
| I7 | ≥ 99 % | de 97 a menos de 99 % | menos de 97 % | Registrar cada caída, buscar la causa y pedir soporte técnico. |

## Cómo se hace la auditoría

1. Los indicadores diarios (I3 e I5) los sigue cada área en el tablero del módulo. Una vez por mes se calculan todos con una muestra; la primera medición es la tarea 18 del Gantt de la Entrega N.º 2, que mide las metas para cerrar el proyecto. Mientras dure el proyecto lo hacen el tester del equipo y Administración y Finanzas; como el equipo del proyecto es temporal, después la tarea queda en Administración y Finanzas.
2. Se arma un informe corto para la Dirección General, con el semáforo de cada indicador.
3. La Dirección decide las acciones para los rojos.
4. Cada tres meses, la Dirección revisa si los estándares siguen siendo los correctos. Si un estándar no se cumple nunca, quizás la meta de la planificación (Entrega N.º 2) estaba mal puesta.

Para medir I3 se sumó el campo `COMPRA.fecha_costeo` al diccionario de datos: el campo `costeada` de la Entrega N.º 3 dice si una compra se costeó, pero no cuándo. El indicador I1 va a ganar detalle cuando se sume la entidad de movimientos de stock (meta M3 de la Entrega N.º 2): con ella, cada diferencia se podrá rastrear movimiento por movimiento.

Los estándares de I1, I3 e I6 son las metas M5, M4 y M2 de la Entrega N.º 2. Los demás valores (y el tope del 15 % para las subas) son supuestos que propuso la IA: se revisó que fueran razonables y hay que confirmarlos con las primeras mediciones (ver la Declaración de Uso de IA en el README).

**Referencia:** Robbins, S. P. y Coulter, M. (2014). *Administración* (12.ª ed.). Pearson Educación.
