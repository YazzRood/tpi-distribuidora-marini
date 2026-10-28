# Diccionario de datos inicial

Diccionario de datos del Módulo de Gestión de Inventario y Costeo Dinámico (Entrega N.º 3). Para cada campo indica el nombre, el tipo de dato, la clave y para qué sirve.

## Tipos de datos y claves

| Tipo o clave | Qué significa |
|---|---|
| Integer | Número entero, sin coma. Ej.: 1502. |
| String | Texto. También números que no se usan en cuentas (CUIT, teléfono). |
| Decimal | Número con coma. Es exacto, por eso se usa para plata, kilos y porcentajes. |
| Date | Fecha. Ej.: 17/10/2026. |
| Boolean | Solo dos valores: sí o no (verdadero o falso). |
| PK | Clave primaria. Identifica a cada registro y no se repite. |
| FK | Clave foránea. Guarda la clave de otra entidad para unir los datos. |

## Relaciones

- Un PROVEEDOR puede hacer muchas COMPRAS, pero cada compra es de un solo proveedor (1:N).
- Una COMPRA genera uno o más LOTES: uno por cada artículo de la factura (1:N).
- Un ARTICULO puede tener muchos LOTES, con distintas fechas de vencimiento (1:N).
- LOTE une a COMPRA con ARTICULO y resuelve la relación de muchos a muchos (N:M).

## PROVEEDOR

Guarda los datos de cada empresa que le vende mercadería a Marini.

| Campo | Tipo de dato | Clave | Descripción |
|---|---|---|---|
| `id_proveedor` | Integer | PK | Número único de cada proveedor. |
| `razon_social` | String | – | Nombre de la empresa que vende la mercadería. |
| `cuit` | String | – | CUIT del proveedor. Va como texto porque no se usa en cuentas. |
| `telefono` | String | – | Teléfono o WhatsApp para hacer los pedidos. |
| `activo` | Boolean | – | Indica si se le sigue comprando (sí o no). |

## COMPRA

Guarda los datos de cada factura de compra que llega al depósito.

| Campo | Tipo de dato | Clave | Descripción |
|---|---|---|---|
| `id_compra` | Integer | PK | Número interno de cada compra. |
| `id_proveedor` | Integer | FK | Proveedor que hizo la factura. Une con PROVEEDOR. |
| `nro_factura` | String | – | Número de la factura del proveedor. Va como texto por los guiones. |
| `fecha_recepcion` | Date | – | Día en que llega la mercadería al depósito. |
| `total` | Decimal | – | Importe total de la factura, en pesos. |
| `costeada` | Boolean | – | Indica si ya se recalcularon los costos y precios con esta compra. |

## LOTE

Guarda cada ingreso de un artículo, con su costo y su fecha de vencimiento.

| Campo | Tipo de dato | Clave | Descripción |
|---|---|---|---|
| `id_lote` | Integer | PK | Número único de cada lote. |
| `id_compra` | Integer | FK | Compra en la que entró. Une con COMPRA. |
| `id_articulo` | Integer | FK | Artículo del lote. Une con ARTICULO. |
| `cantidad_ingresada` | Decimal | – | Unidades o kilos que entraron. |
| `cantidad_disponible` | Decimal | – | Lo que queda hoy. Baja con cada venta. |
| `costo_unitario` | Decimal | – | Costo final de una unidad, con descuento e IVA. |
| `fecha_vencimiento` | Date | – | Día en que vence. El tablero avisa antes. |

El costo final es: precio de factura × (1 − descuento) × (1 + IVA). El stock de un artículo es la suma de lo disponible en sus lotes.

## ARTICULO

Guarda los datos de cada producto que vende Marini.

| Campo | Tipo de dato | Clave | Descripción |
|---|---|---|---|
| `id_articulo` | Integer | PK | Código del artículo. Es el mismo del sistema de gestión. |
| `codigo_barras` | String | – | Código del envase. Va como texto porque puede empezar con cero. |
| `descripcion` | String | – | Nombre. Ej.: «Queso cremoso horma 4 kg». |
| `familia` | String | – | Lácteos, fiambres, aderezos o descartables. |
| `costo_actual` | Decimal | – | Último costo final (de reposición). Lo actualiza cada compra. |
| `margen_mayorista` | Decimal | – | Porcentaje de ganancia de la lista mayorista. |
| `margen_minorista` | Decimal | – | Porcentaje de ganancia de la lista minorista. |
| `stock_minimo` | Decimal | – | Cantidad mínima. Si el stock baja de ahí, el tablero avisa. |
| `activo` | Boolean | – | Si se vende o no. Se usa en vez de borrar: el sistema de gestión no deja dar de baja códigos con ventas. |

Los precios no se guardan: el módulo los calcula con el costo y el margen. Así, cuando cambia el costo, el precio se actualiza solo.

## Qué área usa cada entidad

| Entidad | La carga | La consultan |
|---|---|---|
| PROVEEDOR | Compras | Administración y Finanzas |
| COMPRA | Depósito, al recibir la mercadería | Compras, y Administración y Finanzas |
| LOTE | Depósito, al recibir la mercadería | Mostrador, Depósito y Dirección (tablero) |
| ARTICULO | Administración y Finanzas (costos y márgenes) | Ventas mayoristas, Mostrador y Dirección |
