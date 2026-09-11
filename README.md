# Handoff: Frontend Exclusive Cars NQN

## Overview
Rediseño completo del frontend público + panel administrativo de **Exclusive Cars NQN**, concesionaria de 0 km y usados seleccionados en Neuquén Capital (Argentina). El objetivo de esta entrega es que un proyecto **ya existente** adopte este lenguaje visual y estas pantallas en su frontend, manteniendo su backend, su modelo de datos y su stack actual.

Seis vistas: Home, Catálogo (con filtros), Detalle de vehículo, Nosotros, Contacto y Panel admin (6 secciones internas).

## About the Design Files
El archivo incluido (`Exclusive Cars NQN.dc.html`) es una **referencia de diseño hecha en HTML**: un prototipo que muestra apariencia e interacción previstas, **no código de producción para copiar y pegar**.

La tarea es **recrear estos diseños dentro del entorno ya existente del proyecto** (React, Next.js, Vue, Laravel Blade, WordPress, lo que corresponda), usando sus patrones, su router, su sistema de componentes y su capa de datos reales. Los datos del prototipo son de muestra y deben reemplazarse por los del backend.

Notas de implementación importantes:
- El prototipo usa estilos **inline** por razones de la herramienta de diseño. En el proyecto real, trasladar esos valores a la convención del codebase (CSS Modules, Tailwind, styled-components, SCSS, etc.). Los valores exactos están documentados en *Design Tokens*.
- Todo el estado del prototipo es local y en memoria. En producción: filtros en query params de la URL (compartibles/SEO), listados desde API con paginación de servidor, y el panel admin contra endpoints reales con autenticación.
- Las fotos de vehículos son **placeholders rayados** intencionales. Reemplazar por imágenes reales (ver *Assets*).

## Fidelity
**Alta fidelidad (hifi).** Colores, tipografías, escalas, espaciados, estados hover y animaciones son definitivos. Recrear la UI fielmente. Lo único deliberadamente sin resolver son las imágenes de vehículos y el mapa de contacto (placeholders).

---

## Design Tokens

### Colores
| Token | Hex | Uso |
|---|---|---|
| `bg-base` | `#07070a` | Fondo global de la página |
| `bg-elev-1` | `#09090c` | Footer, header de tablas, sidebar admin |
| `bg-elev-2` | `#0a0a0e` | Paneles seccionados (servicios, ficha técnica, valores) |
| `bg-elev-3` | `#0b0b0f` | Cards de panel, sidebar de filtros, KPI cards |
| `bg-card` | `#0d0d12` | Card de vehículo |
| `bg-card-hover` | `#0f0f14` / `#101016` | Hover de cards y paneles |
| `accent` | `#ff2233` | Rojo del logotipo. Precios, CTA primario, activos, acentos |
| `accent-soft` | `rgba(255,34,51,.16)` | Fondo de chips/badges activos |
| `accent-glow` | `rgba(255,34,51,.5–.7)` | `box-shadow` de glow en hover |
| `accent-light` | `#ff6b73` | Texto sobre fondo rojo translúcido (badges) |
| `success` | `#38e07b` | Estados "Publicado", deltas positivos, punto online |
| `warning` | `#ffc400` | Estado "En trato" (consultas) |
| `text-primary` | `#ffffff` | Titulares y valores |
| `text-body` | `rgba(255,255,255,.85)` | Párrafos destacados |
| `text-muted` | `rgba(255,255,255,.5–.66)` | Texto secundario |
| `text-faint` | `rgba(255,255,255,.3–.42)` | Labels monoespaciados, metadatos |
| `border` | `rgba(255,255,255,.08)` | Borde estándar de cards y secciones |
| `border-strong` | `rgba(255,255,255,.12–.22)` | Inputs, botones secundarios |
| `divider` | `rgba(255,255,255,.05–.07)` | Separadores de filas y celdas |

Gradiente ambiental fijo sobre toda la página (capa `position:fixed; inset:0; pointer-events:none`):
`radial-gradient(1200px 600px at 50% -10%, rgba(255,34,51,.10), transparent 70%)`

### Tipografía
Google Fonts:
- **Saira Condensed** — 500/600/700/800/900 → titulares, botones, nav, precios, nombres de vehículo. Siempre `text-transform: uppercase` salvo en párrafos.
- **Barlow** — 300/400/500/600/700 → cuerpo de texto, inputs, labels de formulario.
- **JetBrains Mono** — 400/500 → metadatos, labels de campo, refs, contadores, breadcrumbs.

Escala aplicada:
| Rol | Familia | Size | Weight | Tracking | Line-height |
|---|---|---|---|---|---|
| H1 hero | Saira Condensed | `clamp(56px, 8.4vw, 142px)` | 900 | `-.015em` | `.86` |
| H1 de sección | Saira Condensed | `clamp(40px, 6vw, 86px)` | 900 | normal | `.9` |
| H2 | Saira Condensed | `clamp(38px, 5vw, 72px)` | 900 | normal | `.92` |
| H1 admin | Saira Condensed | 40px | 900 | normal | 1 |
| Título de card | Saira Condensed | 25px (home) / 21px (catálogo) | 800 | normal | 1.02 |
| Precio USD | Saira Condensed | 27px / 23px / 44px (detalle) | 900 | normal | 1 |
| Nav / botones | Saira Condensed | 14–16px | 700–900 | `.11–.14em` | — |
| Párrafo lead | Barlow | 17–22px | 400 | normal | 1.55–1.62 |
| Párrafo | Barlow | 14.5–16.5px | 400 | normal | 1.66–1.75 |
| Label mono | JetBrains Mono | 9–11px | 400 | `.16–.30em` | — |

Todos los párrafos largos usan `text-wrap: pretty`; el H1 del hero usa `text-wrap: balance`.

### Espaciado, radios y sombras
- Contenedor máximo: `1480px`, padding lateral `34px`.
- Padding vertical de secciones: `80–100px` (desktop).
- Radios: `2px` (botones, inputs, badges, chips rectangulares), `3px` (cards y paneles), `50%` / `99px` (avatares, chips redondeados, barras de progreso).
- Sombra de card en hover: `0 22px 60px rgba(0,0,0,.6), 0 0 0 1px rgba(255,34,51,.2)`.
- Glow de CTA en hover: `0 0 40–52px rgba(255,34,51,.6–.7)`.
- Foco de input: `border-color:#ff2233; box-shadow: 0 0 0 3px rgba(255,34,51,.12)`.

### Regla de grillas con divisores
Las tiras divididas (stats del home, servicios, valores, ficha técnica) **no** usan `gap:1px` sobre un fondo claro: con `auto-fit` las pistas vacías de la última fila pintarían bloques visibles. El patrón correcto es: wrapper con el color de la celda y divisor por celda con `box-shadow: -1px 0 0 rgba(255,255,255,.07)` (y `0 -1px 0` cuando también hace falta línea superior).

---

## Screens / Views

### Componentes globales

**Header (sticky, `top:0`, z-index 40)**
`background: rgba(7,7,10,.82)`, `backdrop-filter: blur(14px)`, borde inferior `rgba(255,255,255,.07)`, padding `14px 34px`, `display:flex; gap:28px; align-items:center`.
- Logo: círculo 44px, `overflow:hidden`, `box-shadow: 0 0 0 1px rgba(255,34,51,.55), 0 0 18px rgba(255,34,51,.35)`. A la derecha, "EXCLUSIVE CARS" (Saira Condensed 900, 19px) y debajo "NQN" (JetBrains Mono 9.5px, tracking `.42em`, color accent). Click → Home.
- Nav: Home · Catálogo · Nosotros · Contacto. Item activo en blanco, inactivo `rgba(255,255,255,.55)`. Subrayado rojo de 2px que hace `transform: scaleX(0→1)` con origen izquierdo, `transition: .35s cubic-bezier(.2,.8,.2,1)` — activo `scaleX(1)`.
- CTA derecho: "299 637-1007" con punto verde `#38e07b` con glow, borde `rgba(255,34,51,.5)`. En hover: fondo accent + glow. Click → Contacto.

**Footer**
4 columnas (`auto-fit, minmax(220px,1fr)`, gap 36px) sobre `#09090c`: marca + descripción; Local (Luis Beltrán 134, Neuquén Capital, Lun a Vie 9–13 / 16–20, Sáb 10–13); Contacto (Matías Fernández, 299 637-1007, @exclusivecarsnqn); Secciones (nav + "Panel admin"). Barra inferior centrada en JetBrains Mono 10px.

**Cursor custom** (efecto global)
Dos elementos `position:fixed`, `pointer-events:none`, z-index 9999, movidos con `transform: translate(x,y)` desde `mousemove` en `window`:
- Anillo: 26×26, borde `1px solid rgba(255,34,51,.85)`, `border-radius:50%`, `mix-blend-mode:screen`.
- Punto: 4×4, `#ff2233`.
Al pasar sobre cualquier elemento con `data-cursor="grow"` (detección con `e.target.closest('[data-cursor]')`), el anillo pasa a 58×58 con fondo `rgba(255,34,51,.14)`; transición `.22s`. Desactivar en dispositivos táctiles (`pointer: coarse`).

**Tilt 3D de cards**
En `mousemove` sobre la card se calcula la posición relativa `x,y ∈ [-0.5, 0.5]` y se aplica
`perspective(900px) rotateY(x*7deg) rotateX(-y*7deg) translateY(-5px) scale(1.012)` con `transition: transform .08s linear`.
En `mouseleave`: `transform:none` con `transition: transform .5s cubic-bezier(.2,.8,.2,1)`.

---

### 1. Home
**Propósito:** captar la consulta y llevar al catálogo.

1. **Hero** — `min-height: calc(100vh - 73px)`, contenido alineado abajo.
   - Fondo: foto del stock a pantalla completa, `object-position: 50% 62%`, `filter: grayscale(.55) contrast(1.15) brightness(.62)`.
   - Tres capas encima: degradado vertical (`rgba(7,7,10,.86)` → `.35` al 38% → `.92`), degradado horizontal (`rgba(7,7,10,.9)` → transparente al 62%) y scanlines (`repeating-linear-gradient(0deg, rgba(255,255,255,.045) 0 1px, transparent 1px 3px)`, opacidad .5).
   - **Líneas de velocidad**: 3 líneas horizontales absolutas (top 26% / 44% / 63%; ancho 22vw / 34vw / 16vw; alto 1px / 2px / 1px) con degradado a rojo o blanco, animación `ec-speed` (`translateX(-120% → 320%)`) de 3.4s / 2.6s / 4.2s, lineal, infinita, con delays 0 / .7s / 1.4s.
   - Eyebrow: línea roja de 38px + "NEUQUÉN CAPITAL · LUIS BELTRÁN 134".
   - H1: "Autos que" / "no se repiten" (segunda línea en accent con `text-shadow: 0 0 46px rgba(255,34,51,.55)`).
   - Bajada (máx. 520px) + dos CTA: "Ver catálogo" (fondo accent, hover glow + `translateY(-2px)`) y "Cotizar mi usado" (borde `rgba(255,255,255,.22)`).
2. **Tira de confianza** — 4 celdas (`auto-fit, minmax(190px,1fr)`) sobre `#0b0b0f`: **48** unidades en stock · **100%** verificadas y peritadas · **12** años en el rubro · **0km** y usados seleccionados. Número en Saira 900 40px; sufijo en accent; label mono 10.5px.
3. **Destacados** — encabezado "/ 01 — STOCK" + H2 "Destacados de la semana" + link "Ver los 48 vehículos →". Grilla `auto-fill, minmax(320px,1fr)`, gap 22px, 6 cards.
   - **Card de vehículo**: imagen `aspect-ratio 4/3` (placeholder rayado, con degradado inferior hacia el color de la card), badge de estado arriba a la izquierda (rojo sólido si es "0 km", `rgba(7,7,10,.8)` si es "Usado"), marca en mono, modelo en Saira 800 25px, versión, fila de 3 specs (Año / Km / Caja) separada por línea superior, y pie con precio USD en accent 27px + precio ARS en mono + círculo de 38px con "→". Hover: borde `rgba(255,34,51,.55)` + sombra + tilt. Click → Detalle.
4. **Servicios** — 3 paneles divididos: 01 Financiación · 02 Permutas · 03 Consignaciones. Número gigante en Saira 900 64px con color `rgba(255,34,51,.16)`, título 29px, texto, y barra inferior de 2px `linear-gradient(90deg,#ff2233,transparent)` con opacidad .35.
5. **CTA final** — "¿Buscás algo puntual?" + botón "Escribinos por WhatsApp →".

### 2. Catálogo
**Propósito:** explorar y filtrar el stock.

Layout: `grid-template-columns: 260px minmax(0,1fr)`, gap 34px.
- **Sidebar (sticky, `top:100px`)**: título "Filtros" + "limpiar"; **Condición** (Todos / 0 km / Usado, 3 botones en fila); **Marca** (chips redondeados, multi-selección); **Precio máx.** (range 8.000–90.000, step 1.000, `accent-color:#ff2233`, label "USD 90.000"); **Año desde** (range 2010–2026); contador de resultados en mono.
- **Toolbar**: buscador de ancho flexible (mínimo 240px) con glifo `⌕`, y 3 botones de orden: Recientes / Menor precio / Menor km.
- **Grilla**: `auto-fill, minmax(290px,1fr)`, gap 20px. Card compacta (imagen 16/11, "MARCA MODELO" en 21px, versión, fila mono `2018 | 68.000 km | Automático`, pie con precio USD/ARS y "→").
- Estado de chip activo: borde `#ff2233`, fondo `rgba(255,34,51,.16)`, texto blanco. Inactivo: borde `rgba(255,255,255,.13)`, fondo transparente, texto `rgba(255,255,255,.62)`.

### 3. Detalle de vehículo
Layout: `grid-template-columns: minmax(0,1.55fr) minmax(320px,.85fr)`, gap 34px. Breadcrumb mono arriba ("← Catálogo / Marca Modelo").

**Columna izquierda**
- Galería principal `aspect-ratio 16/10` con una **línea de escaneo** roja de 2px que recorre verticalmente (`@keyframes ec-scan: translateY(-100% → 700%)`, 6s lineal infinita) y contador "01 / 24" abajo a la derecha.
- Tira de miniaturas horizontal con scroll (112px de ancho, 4/3); la activa lleva borde accent. Scrollbar custom de 6px con thumb rojo.
- **Ficha técnica**: grilla `auto-fit, minmax(160px,1fr)` de 8 celdas divididas — Año, Kilómetros, Transmisión, Combustible, Motor, Tracción, Puertas, Titular.
- **Estado del vehículo**: 4 barras de progreso (Carrocería y pintura 94%, Mecánica 98%, Interior 91%, Service al día 100%). Barra de 4px, fondo `rgba(255,255,255,.09)`, relleno `linear-gradient(90deg,#ff2233,#ff6b52)` con `box-shadow: 0 0 14px rgba(255,34,51,.6)`.
- **Equipamiento**: chips redondeados.

**Columna derecha (sticky, `top:100px`)**
- Card de precio: badge de estado + "REF EC-240"; marca; modelo en Saira 900 42px; versión; bloque de precio con USD en accent 44px (`text-shadow: 0 0 36px rgba(255,34,51,.4)`) y ARS + "cotización del día"; tres CTA apilados: "Consultar por WhatsApp" (sólido), "Coordinar visita" (borde), "Entregar mi usado en parte de pago" (borde punteado); datos de contacto en mono.
- Card de **financiación estimada**: fondo `linear-gradient(135deg, rgba(255,34,51,.12), transparent)`, borde `rgba(255,34,51,.28)`, cuota en Saira 900 30px + "/ 48 cuotas".

### 4. Nosotros
- Hero de 52vh (mín. 340px) con la foto en `grayscale(.7) brightness(.5)`, eyebrow "/ NOSOTROS" y H1 "Somos de acá. De Neuquén."
- Dos columnas de texto (lead 22px + párrafo 16.5px).
- Tira de 4 valores divididos, cada uno con guion rojo de 30×2px: Peritaje real · Precio de mercado · Atención directa · Post venta.
- Tres placeholders de foto 4/3: frente del local, equipo, entrega de unidad.

### 5. Contacto
- H1 "Pasá por el local o escribinos".
- Dos columnas (`auto-fit, minmax(320px,1fr)`, gap 34px):
  - **Formulario** en card: Nombre, Teléfono, Email, Vehículo de interés + textarea Mensaje + botón "Enviar consulta". Inputs sobre `#07070a` con borde `rgba(255,255,255,.12)`; foco en accent.
  - **Info**: tres cards clickeables (WhatsApp 299 637-1007 · Dirección Luis Beltrán 134 · Horarios Lun a Sáb) y un placeholder de mapa 16/10 con un pin rojo de 16px con halo `0 0 0 8px rgba(255,34,51,.18)` y animación `ec-pulse` (opacidad .35 ↔ 1, 2.2s ease-in-out infinita).

### 6. Panel admin
Layout: `grid-template-columns: 232px minmax(0,1fr)`, alto mínimo `calc(100vh - 73px)`.

**Sidebar** (`#09090c`, borde derecho): label "PANEL INTERNO" + 6 ítems con contador — Vehículos (12) · Consultas (12) · Consignaciones (7) · Permutas (4) · Usuarios (3) · Ajustes. Activo: fondo `rgba(255,34,51,.1)` y barra izquierda de 2px accent. Abajo, card de sesión (Matías F. — Administrador).

**Encabezado**: título = sección activa, subtítulo contextual, y CTA primario que cambia por sección ("+ Nuevo vehículo", "Exportar consultas", "+ Nueva consignación", "+ Nueva tasación", "+ Invitar usuario", "Guardar todo").

**KPIs**: 4 cards (`auto-fit, minmax(190px,1fr)`) con label mono, valor en Saira 900 34px, delta coloreado (verde/rojo) y barra de progreso de 3px. El set de KPIs cambia por sección.

**Sección Vehículos**
- Buscador (por modelo o REF) + chips de estado con contador: Todos / Publicado / Reservado / Borrador / Vendido.
- Barra de selección múltiple (aparece con ≥1 seleccionado): "N seleccionados" + acciones en lote **Publicar**, **Pasar a borrador**, **Marcar vendido**, **Eliminar** + "cancelar". Fondo `rgba(255,34,51,.1)`, borde `rgba(255,34,51,.35)`.
- Tabla con columnas `34px | minmax(0,2.2fr) | .7fr | .8fr | 1fr | .9fr | .7fr | 128px`: checkbox · Vehículo (thumb 44×33 + nombre + "REF · N fotos") · Año · Km · Precio USD · Estado · Vistas · Acciones. Encabezados de Vehículo/Año/Precio ordenan (flecha ↑/↓; por defecto año descendente).
- Estado: badge clickeable que cicla Publicado → Reservado → Borrador → Vendido.
- Acciones por fila: ★ destacar (toggle, se pinta accent), ✎ editar (abre el detalle), ✕ eliminar (hover rojo).
- Fila seleccionada: fondo `rgba(255,34,51,.06)`.
- Paginación de 6 por página, con el rango descrito en mono ("1–6 de 12 vehículos").

**Sección Consultas** — tabla de leads: Cliente (+ fecha) · Contacto · Interés · Canal (WhatsApp / Formulario / Instagram / Llamada) · Estado. El estado es un badge clickeable que cicla Nueva (rojo) → Contactada (gris) → En trato (`#ffc400`) → Cerrada (verde).

**Secciones Consignaciones y Permutas** — grilla de fichas (`auto-fill, minmax(320px,1fr)`): REF + badge de estado, vehículo, titular, y dos métricas (precio pedido / días en local; o toma / diferencia).

**Sección Usuarios** — filas con avatar circular de iniciales (fondo `rgba(255,34,51,.14)`, borde accent), nombre, email, último acceso y badge de rol (Administrador en rojo, Ventas en gris).

**Sección Ajustes** — tres paneles (`auto-fit, minmax(330px,1fr)`):
1. **Cotización del dólar**: valor grande en accent + slider 1200–1800 step 5. Cambia en vivo todos los precios en ARS del sitio.
2. **Preferencias**: 4 toggles (42×23px, knob de 17px que se desplaza 19px) — Mostrar destacados en el home · Mostrar precio en ARS · Avisar consultas por email · Modo mantenimiento.
3. **Datos del local**: inputs de Dirección, Teléfono/WhatsApp, Instagram, Horarios + "Guardar cambios".

---

## Interactions & Behavior
- **Navegación**: header y footer cambian de vista; click en card de vehículo abre Detalle; breadcrumb vuelve al Catálogo; el footer tiene un acceso discreto a "Panel admin". Cada cambio de vista hace scroll al tope. En producción: rutas reales (`/`, `/catalogo`, `/vehiculo/:ref`, `/nosotros`, `/contacto`, `/admin/...`).
- **Filtros del catálogo**: combinan marca (OR entre marcas), condición, precio máximo y año mínimo (AND entre criterios). El orden se aplica después del filtrado. "Limpiar" resetea todo. Recomendado: reflejarlos en la URL.
- **Hover de cards**: tilt 3D + cambio de borde a accent + sombra. Botones primarios: glow rojo y `translateY(-2px/-3px)`.
- **Animaciones**: `ec-speed` (líneas del hero), `ec-scan` (galería del detalle), `ec-pulse` (pin del mapa), `ec-spin` (disponible para spinners de carga).
- **Accesibilidad / responsive**: respetar `prefers-reduced-motion` desactivando `ec-speed`, `ec-scan`, `ec-pulse` y el tilt. Desactivar el cursor custom con `pointer: coarse`. En < 900px: sidebar de filtros como panel desplegable, tablas del admin con scroll horizontal o vista de tarjetas, grilla de catálogo a 1–2 columnas.
- **Estados faltantes por implementar**: skeletons de carga para grillas y tablas, estado vacío ("no hay resultados con estos filtros" + botón limpiar), errores de red, validación de formulario (nombre y teléfono requeridos, email con formato, teléfono argentino), y confirmación antes de eliminar en el admin.

## State Management
Público:
- `filters { marcas: string[], condicion: 'Todos'|'0 km'|'Usado', maxPrecioUsd: number, minAnio: number, query: string }`
- `orden: 'Recientes'|'Menor precio'|'Menor km'`
- `vehiculoSeleccionado: ref`
- `cotizacionUsd: number` (global; deriva todos los precios en ARS — en producción viene de configuración/API, no del cliente)

Admin:
- `seccion`, `busqueda`, `filtroEstado`, `orden {campo, dir}`, `pagina`
- `seleccionados: id[]` (acciones en lote)
- `destacados: id[]` (máx. 6, alimentan el home)
- `preferencias { destacados, arsVisible, consultasMail, mantenimiento }`
- `datosLocal { direccion, telefono, instagram, horarios }`

Datos esperados del backend: listado de vehículos paginado y filtrable; detalle por REF con galería, ficha técnica, puntajes de estado y equipamiento; leads/consultas con estado; consignaciones; permutas; usuarios y roles; configuración del sitio.

Modelo de vehículo usado en el prototipo:
`{ ref, marca, modelo, version, anio, km, precioUsd, estado: '0 km'|'Usado', estadoPublicacion: 'Publicado'|'Reservado'|'Borrador'|'Vendido', destacado: bool, fotos: [], vistas }`
Precio en ARS = `round(precioUsd * cotizacion / 100000) * 100000`, formateado con `toLocaleString('es-AR')`. Cuota estimada = `round(precioUsd * cotizacion / 48 / 10000) * 10000`.

## Assets
- `assets/logo.jpg` — logotipo circular de Exclusive Cars NQN (provisto por el cliente desde Instagram). **Pedir una versión vectorial o PNG con fondo transparente** para producción; el JPG tiene fondo negro y se está recortando en círculo.
- `assets/showroom.jpg` — foto real del stock, usada en el hero del Home y en el hero de Nosotros (con filtros de desaturación).
- Sin librería de iconos: se usan glifos tipográficos (`→ ★ ✎ ✕ ⌕`). Si el proyecto ya tiene un set de iconos (Lucide, Feather, Material), reemplazarlos por los equivalentes.
- Placeholders rayados: `repeating-linear-gradient(135deg, #15151a 0 9px, #101014 9px 18px)` con label en JetBrains Mono. Reemplazar por fotos reales de las unidades.
- Mapa de contacto: placeholder. Integrar Google Maps / Leaflet apuntando a Luis Beltrán 134, Neuquén Capital.

## Contenido real (usar tal cual)
- Dirección: **Luis Beltrán 134 — Neuquén Capital**
- Contacto: **Matías Fernández — 299 637-1007**
- Propuesta: **Vehículos 0 km y usados seleccionados**
- Servicios: **Financiación · Permutas · Consignaciones**
- Instagram: **@exclusivecarsnqn**
- Los vehículos, precios, leads, consignaciones, permutas y usuarios del prototipo son **datos de muestra**.

## Files
- `Exclusive Cars NQN.dc.html` — prototipo completo con las 6 vistas y todos los efectos.
- `assets/logo.jpg`, `assets/showroom.jpg` — assets referenciados por el prototipo.

Para ver el prototipo basta abrir el HTML en un navegador (necesita conexión para cargar las Google Fonts).
