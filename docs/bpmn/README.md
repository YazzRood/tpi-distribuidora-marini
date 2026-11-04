# Modelo BPMN — Recepción de compras, costeo y actualización de precios

Notación BPMN 2.0. Muestra el proceso que el módulo va a cambiar: desde que llega la mercadería al depósito hasta que los precios quedan al día.

## Archivos

- `.bpmn`: modelo editable. Se abre en https://demo.bpmn.io (Abrir → elegir el archivo).
- `.svg` y `.png`: imagen del modelo para verlo sin abrir nada.

## Pools y lanes

- **Distribuidora Marini** (pool principal), con cinco lanes: cuatro áreas del organigrama (Compras, Depósito, Dirección General y Administración y Finanzas) y la lane Sistema (módulo), con las tareas que el software hace solo.
- **Proveedor** y **Clientes**: pools externos. Se comunican con Marini por flujos de mensaje.

## Flujo estándar

1. Llega la mercadería con la factura.
2. Depósito controla cantidad, cadena de frío y vencimientos.
3. Si todo llegó bien y no hay artículos nuevos, Depósito carga la compra y sus lotes.
4. El módulo calcula el costo final de cada lote y suma el stock.
5. El módulo calcula los precios nuevos y mide cuánto sube cada uno.
6. Si ningún artículo sube más del 15 %, publica la lista nueva y se la envía a los clientes.

## Compuertas de excepción

| Compuerta | Qué se hace |
| --- | --- |
| ¿Llegó todo bien? | Si no, Compras reclama la diferencia al proveedor. |
| ¿Quedó algo para cargar? | Si se rechazó todo, termina en «Entrega rechazada». |
| ¿Hay artículos nuevos? | Administración y Finanzas los da de alta antes de la carga. |
| ¿Algún artículo sube más del 15 %? | La Dirección revisa la suba antes de publicar. |
| ¿Aprueba la suba? | Si hay un error, Administración corrige y el sistema recalcula. |

Historias relacionadas: HU-01 y HU-02 (ver `docs/historias-de-usuario.md`).
