# Historias de usuario

Formato formal: **Como** [usuario], **quiero** [funcionalidad], **para** [beneficio].

Cada historia es una *issue* del repositorio con la etiqueta `historia de usuario`. Su estado (Por hacer, En progreso o Listo) se sigue en el tablero del proyecto.

Las historias salen de las cuatro funciones del módulo que propuse en la Entrega N.º 1, y sus criterios respetan las metas de la Entrega N.º 2.

## HU-01 · Cargar compras con lotes y costo

**Como** encargado de Depósito, **quiero** cargar cada compra con sus lotes y vencimientos, **para** tener el stock y el costo al día.

**Criterios de aceptación**

- [ ] No deja guardar un lote si le falta la cantidad o la fecha de vencimiento.
- [ ] Al guardar, calcula el costo final con descuento e IVA.
- [ ] El stock del artículo es la suma de lo disponible en sus lotes.

## HU-02 · Recalcular precios cuando cambia el costo

**Como** responsable de Administración y Finanzas, **quiero** que los precios se recalculen solos cuando cambia el costo, **para** no vender con precios viejos.

**Criterios de aceptación**

- [ ] Precio de cada lista = costo × (1 + margen de esa lista).
- [ ] Si un artículo sube más del 15 %, su precio espera la aprobación de la Dirección.
- [ ] Los precios nuevos salen el mismo día en que se carga la factura (meta M4 de la Entrega N.º 2).

## HU-03 · Ver alertas de stock y vencimientos

**Como** dueño de la distribuidora, **quiero** ver alertas de stock bajo y de vencimientos cercanos, **para** decidir a tiempo qué comprar y qué vender primero.

**Criterios de aceptación**

- [ ] Avisa cuando un artículo baja de su stock mínimo.
- [ ] Avisa los lotes que vencen en los próximos 15 días.
- [ ] Muestra los indicadores de control con colores (verde, amarillo y rojo).

## Definición de Listo (etapa de análisis y diseño)

Es lo que en Scrum se llama *Definición de Terminado*. Una historia pasa a **Listo** cuando:

1. Tiene criterios de aceptación claros y revisados.
2. Su flujo está en el modelo BPMN.
3. Sus datos están en el diccionario de datos.
4. El cambio entró a `main` con un Pull Request revisado.
