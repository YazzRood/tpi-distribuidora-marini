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

- Tablero de gestión (GitHub Projects): https://github.com/users/YazzRood/projects/2
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


## Declaración de Uso de IA

Usé un asistente de IA, Claude (Anthropic), en este trabajo. Lo usé para proponer el modelo BPMN, redactar textos (las historias de usuario y los indicadores), guiarme paso a paso al cargar todo en GitHub y cruzar el trabajo con mis entregas anteriores.

**Lo que hice y decidí yo:** los datos del caso (áreas, circuito de compras, reglas de costos y precios) salen de mis entregas anteriores. Hice todo el trabajo en GitHub: repositorio, ramas, commits, Pull Requests, revisiones y tablero. Me hago responsable de todo lo que dice el trabajo.

### Prompts que usé y qué corregí

| Prompt | Por qué lo escribí así | Qué controlé o corregí |
| --- | --- | --- |
| «Revisa que todo este correcto.» | Antes de entregar pedí una revisión final con la lista «Antes de entregar» de la cátedra. | Revisé las correcciones de forma de las Entregas 1 a 3: corchetes de la plantilla, una frase repetida, puntos finales, numeración de consignas y un error de tipeo. |

### Mirada crítica

El primer prompt fue muy amplio y dejó en manos de la IA decisiones que me tocaban a mí. La IA llenó esos huecos con supuestos: dijo que yo había validado cifras con datos reales, que un compañero revisaría los PR, y propuso estándares sin conocer mis metas. Nada de eso era cierto y lo corregí.

Las cifras de control que no salen de mis metas de la Entrega N.º 2 (el tope del 15 % y algunos estándares) son supuestos que propuso la IA y que revisé. Se confirman con las primeras mediciones.

Me llevo que la IA sirve para avanzar rápido, pero hay que revisar cada cosa que afirma.
