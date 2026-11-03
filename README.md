# Módulo de Gestión de Inventario y Costeo Dinámico — Distribuidora Marini

Trabajo Práctico Integrador y Progresivo (TPI) de **Organización Empresarial**.
Tecnicatura Universitaria en Programación a Distancia — Universidad Tecnológica Nacional (UTN).

## Descripción del sistema

Distribuidora Marini vende lácteos, fiambres, aderezos y descartables. Hoy calcula a mano el costo de cada compra y cambia los precios después, así que con subas seguidas puede vender con menos margen.

El módulo propuesto hace cuatro cosas:

1. Recibe cada compra con su costo final (descuento e IVA incluidos).
2. Controla el stock por lote y fecha de vencimiento.
3. Recalcula los precios solos cuando cambia el costo.
4. Muestra alertas e indicadores de control.

Este repositorio guarda la documentación técnica del proyecto: el modelo BPMN, el diccionario de datos, las historias de usuario y los indicadores.

## Integrante

- Yazmin Dana Rodriguez — Comisión 7

Docente titular: Gabriela Martínez · Docente adjunta: Noemi Andrea Ramos · Tutor: Pablo García

## Enlaces

- Tablero de gestión (GitHub Projects): https://github.com/users/YazzRood/projects/1
- Modelo BPMN: carpeta [`docs/bpmn`](docs/bpmn)
- Entregas en PDF: carpeta [`docs/entregas`](docs/entregas)

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

## Cómo se trabaja

- `main` guarda la versión estable. Ningún cambio entra a `main` sin un Pull Request.
- Cada tema se trabaja en una rama con el prefijo `docs/`.
- Los mensajes de commit siguen la forma `tipo(alcance): qué se hizo` (tipos: `docs`, `fix`, `chore`).
- Antes de cada merge se revisa el PR con la lista de control de la plantilla.
