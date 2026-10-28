# Módulo de Gestión de Inventario y Costeo Dinámico · Distribuidora Marini

**Trabajo Práctico Integrador y Progresivo (TPI)** · Organización Empresarial
Tecnicatura Universitaria en Programación a Distancia · Universidad Tecnológica Nacional (UTN) · 2026

## Descripción del sistema

Distribuidora Marini es una PyME de Claypole, en la zona sur del Gran Buenos Aires. Vende lácteos, fiambres, aderezos y descartables por mayor y por menor.

El **Módulo de Gestión de Inventario y Costeo Dinámico** ordena el circuito de compras de la empresa. Tiene cuatro funciones:

- **Recibir compras con su costo:** Depósito carga cada factura una sola vez, con sus lotes y vencimientos.
- **Controlar el stock por lote:** el stock de cada artículo es la suma de lo disponible en sus lotes.
- **Recalcular precios:** cuando cambia el costo, el módulo calcula los precios nuevos con el margen de cada lista.
- **Mostrar indicadores:** un tablero avisa el stock bajo, los vencimientos cercanos y el estado de los controles.

## Integrante

| Nombre | Rol en el proyecto | GitHub |
|---|---|---|
| Yazmin Dana Rodriguez | Analista y líder del proyecto | [@YazzRood](https://github.com/YazzRood) |

Comisión 7 · Docente titular: Prof. Gabriela Martínez · Docente adjunta: Prof. Noemi Andrea Ramos · Tutor: Pablo García

## Estructura del repositorio

```
tpi-distribuidora-marini/
├── README.md                    → portada del proyecto
├── docs/
│   ├── entregas/                → entregas del TPI en PDF
│   ├── bpmn/                    → modelo BPMN (.bpmn, .svg y .png)
│   ├── datos/                   → diccionario de datos
│   ├── control/                 → indicadores y estándares
│   └── historias-de-usuario.md  → las tres historias y sus criterios
└── .github/
    ├── ISSUE_TEMPLATE/          → plantilla para historias de usuario
    └── pull_request_template.md → lista de control para revisar PR
```

## Cómo trabajamos

- La base del repositorio (README, entregas, datos y plantillas) se subió directo a `main`. Después se protegió la rama: desde ahí, todo cambio entra por un Pull Request (PR) aprobado por un par.
- Cada tema se trabaja en una rama `docs/...`. La lista de control para revisar está en la plantilla del PR.
- Los mensajes de commit siguen el formato `tipo(alcance): qué se hizo`; el alcance es opcional. Por ejemplo: `docs(bpmn): agrega el modelo BPMN del proceso de compra`.
- Las ramas no se borran después del merge, así queda la huella de cada cambio.
