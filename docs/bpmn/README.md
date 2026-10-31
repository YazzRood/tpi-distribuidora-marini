# Modelo BPMN: recepción de compras, costeo y actualización de precios

![Modelo BPMN del proceso](proceso-compra-costeo-precios.png)

## Archivos

| Archivo | Qué es |
|---|---|
| `proceso-compra-costeo-precios.bpmn` | Modelo editable en BPMN 2.0. Se abre en https://demo.bpmn.io (botón *Open*) o en Camunda Modeler. |
| `proceso-compra-costeo-precios.svg` | Imagen del diagrama que se puede agrandar sin perder calidad. |
| `proceso-compra-costeo-precios.png` | La misma imagen, en PNG. |

## Cómo leerlo

**Pools:** Distribuidora Marini tiene el proceso completo. Proveedor y Clientes son pools externos: solo se ven los mensajes que cruzan con Marini.

**Lanes de Marini:** Compras, Depósito, Sistema (módulo), Dirección General, y Administración y Finanzas. Son las áreas del organigrama de la Entrega N.º 3. La lane *Sistema* muestra lo que el módulo hace solo, por eso sus tareas son de servicio (ícono de engranaje). Comercial no tiene lane porque usa la lista nueva después, cuando vende.

### Flujo estándar

1. Llega la mercadería con la factura del proveedor (evento de inicio de mensaje).
2. Depósito controla la cantidad, la cadena de frío y los vencimientos.
3. Si todo llegó bien y no hay artículos nuevos, Depósito carga la compra y sus lotes en el módulo.
4. El módulo calcula el costo final de cada lote y suma el stock: precio de factura × (1 − descuento) × (1 + IVA).
5. El módulo calcula los precios nuevos con el margen de cada artículo y mide cuánto sube cada uno.
6. Si ningún artículo sube más del 15 %, el módulo actualiza los costos, publica la lista nueva y se la envía a los clientes.

### Excepciones (compuertas exclusivas)

| Compuerta | Cuándo pasa | Qué se hace |
|---|---|---|
| ¿Llegó todo bien? | Faltan bultos, la mercadería llegó sin frío o con poco vencimiento. | Compras reclama la diferencia al proveedor. |
| ¿Quedó algo para cargar? | Se rechazó toda la entrega. | El proceso termina en «Entrega rechazada». Si se aceptó una parte, se carga solo esa parte. |
| ¿Hay artículos nuevos? | La factura trae un producto que no existe en el sistema. | Administración y Finanzas lo da de alta con su familia, márgenes y stock mínimo, antes de la carga. |
| ¿Algún artículo sube más del 15 %? | El precio nuevo de al menos un artículo sube más de lo normal. | La Dirección revisa la suba antes de publicar. |
| ¿Aprueba la suba? | La Dirección encuentra un error. | Administración y Finanzas corrige la carga y el sistema vuelve a calcular costos y precios. |

Las compuertas sin pregunta son de unión: juntan los caminos para que el proceso siga por uno solo.

El alta del artículo va antes de la carga porque un LOTE guarda el `id_articulo` como clave foránea: no se puede guardar si el artículo todavía no existe.

El modelo pasa las reglas recomendadas de **bpmnlint** (el validador que usa Camunda Modeler).
