# Diccionario de datos

Entidades clave del módulo, tomadas de la Entrega N.º 3. Se sumó el campo `COMPRA.fecha_costeo` para medir el indicador I3 (Entrega N.º 4).

## Relaciones

- Un PROVEEDOR hace muchas COMPRAS; cada compra es de un solo proveedor (1:N).
- Una COMPRA genera uno o más LOTES, uno por artículo de la factura (1:N).
- Un ARTICULO tiene muchos LOTES, con distintos vencimientos (1:N).
- LOTE une COMPRA con ARTICULO y resuelve la relación N:M.

## Tipos y claves

| Tipo o clave | Qué significa |
| --- | --- |
| Integer | Número entero, sin coma. |
| String | Texto. También números que no se usan en cuentas (CUIT, teléfono). |
| Decimal | Número con coma. Se usa para plata, kilos y porcentajes. |
| Date | Fecha. |
| Boolean | Sí o no. |
| PK | Clave primaria: identifica cada registro. |
| FK | Clave foránea: une con otra entidad. |

## PROVEEDOR

| Campo | Tipo | Clave | Descripción |
| --- | --- | --- | --- |
| id_proveedor | Integer | PK | Número único de cada proveedor. |
| razon_social | String | – | Nombre de la empresa que vende la mercadería. |
| cuit | String | – | CUIT del proveedor. |
| telefono | String | – | Teléfono o WhatsApp para pedidos. |
| activo | Boolean | – | Si se le sigue comprando. |

## COMPRA

| Campo | Tipo | Clave | Descripción |
| --- | --- | --- | --- |
| id_compra | Integer | PK | Número interno de cada compra. |
| id_proveedor | Integer | FK | Proveedor de la factura. Une con PROVEEDOR. |
| nro_factura | String | – | Número de factura del proveedor. |
| fecha_recepcion | Date | – | Día en que llega la mercadería. |
| total | Decimal | – | Importe total de la factura, en pesos. |
| costeada | Boolean | – | Si ya se recalcularon costos y precios con esta compra. |
| fecha_costeo | Date | – | Día en que se costeó la compra. Campo nuevo de la Entrega N.º 4. |

## LOTE

| Campo | Tipo | Clave | Descripción |
| --- | --- | --- | --- |
| id_lote | Integer | PK | Número único de cada lote. |
| id_compra | Integer | FK | Compra en la que entró. Une con COMPRA. |
| id_articulo | Integer | FK | Artículo del lote. Une con ARTICULO. |
| cantidad_ingresada | Decimal | – | Unidades o kilos que entraron. |
| cantidad_disponible | Decimal | – | Lo que queda hoy. Baja con cada venta. |
| costo_unitario | Decimal | – | Costo final de una unidad, con descuento e IVA. |
| fecha_vencimiento | Date | – | Día en que vence. |

Costo final = precio de factura × (1 − descuento) × (1 + IVA). El stock de un artículo es la suma de lo disponible en sus lotes.

## ARTICULO

| Campo | Tipo | Clave | Descripción |
| --- | --- | --- | --- |
| id_articulo | Integer | PK | Código del artículo, el mismo del sistema de gestión. |
| codigo_barras | String | – | Código del envase. Puede empezar con cero. |
| descripcion | String | – | Nombre del producto. |
| familia | String | – | Lácteos, fiambres, aderezos o descartables. |
| costo_actual | Decimal | – | Último costo final. Lo actualiza cada compra. |
| margen_mayorista | Decimal | – | Porcentaje de ganancia de la lista mayorista. |
| margen_minorista | Decimal | – | Porcentaje de ganancia de la lista minorista. |
| stock_minimo | Decimal | – | Si el stock baja de acá, el tablero avisa. |
| activo | Boolean | – | Si se vende o no. Se usa en vez de borrar. |

Los precios no se guardan: el módulo los calcula con el costo y el margen.
