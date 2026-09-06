# Corporación Estalingrado — Sistemas Centrales

Portal oficial de la Corporación Estalingrado. Plataforma central que agrupa todos los servicios, proyectos y sistemas de la organización.

## 🌐 GitHub Pages

**[Visitar el sitio →](https://estalingradocorp.github.io/EstalingradoCorp/)**

## Estructura del sitio

El portal está compuesto por tres páginas HTML estáticas (sin build, sin dependencias):

| Archivo | Sección | Descripción |
|---|---|---|
| `index.html` | Inicio | Landing, servicios, proyectos activos y pipeline de desarrollo |
| `market.html` | Market | Catálogo de productos y licencias con filtros y carrito |
| `empresa.html` | Empresa | Historia, identidad corporativa y productos físicos |

## Servicios integrados

| Plataforma | Descripción |
|---|---|
| [Buscador Estalingrado](https://estalingradocorp.qzz.io/) | Motor de búsqueda principal |
| [EC WebSend](https://nicotips27.github.io/ECwebSend/) | Transferencia segura de archivos |
| [EC News](https://nicotips27.github.io/ECnews/) | Portal de noticias corporativas |
| [EC Download](https://nicotips27.github.io/ec-download/) | Centro de descargas |
| [EC-OS](https://estalingradocorp.github.io/EstalingradoCorp/market.html#producto=ecospro) | Sistema operativo webizado (redirige a la licencia en el market) |
| [Big Data (Intranet)](https://nicotips27.github.io/ec-Intra-net/) | Análisis de datos |
| [Antigua Wiki](https://estalingradocorp.github.io/Intra-net/) | Documentación legacy |
| [IA 27](https://estalingradocorp.github.io/agente-IA27-/) | Página explicativa del Agente IA |

## Market (market.html)

Catálogo de productos con filtros por categoría, búsqueda, carrito y compra por WhatsApp.

### Categorías

| Filtro | Contenido |
|---|---|
| **Todos** | Todos los productos |
| **EC Market** | Productos propios de la corporación |
| **Físico** | Productos físicos (hardware, merchandising) |
| **Programas** | Software para PC |
| **Juegos** | Juegos y motores de juego |
| **Android** | Apps para Android (AppGallery, F-Droid) |
| **Juegos Android** | Juegos multiplataforma con soporte Android (Luanti) |

### Productos destacados

- **EC-OS Pro License** (PRD-001): licencia premium del sistema operativo webizado. Actualmente en **oferta limitada por tiempo** — precio antiguo $20.000, **Gratis**. El botón azul "Obtener" muestra un aviso de redirección y luego conduce al producto.
- **OpenCode Desktop** (PRD-009): app de escritorio del agente de codificación IA open source.
- **Cámara IP IA-27** (PRD-015), **C-01 CENTINELA** (PRD-004), **Pack Hacking Ético** (PRD-013), **Windows 10 Enterprise LTSC** (PRD-014) y más.

### Flujos clave

- **Filtros + búsqueda**: las tarjetas usan el atributo `data-type` (códigos separados por espacio) que el JS cruza con el filtro activo. Un producto puede pertenecer a varias categorías.
- **Apertura por hash**: `market.html#producto=<key>` abre automáticamente el detalle del producto. Se usa para enlaces compartidos y para que el servicio EC-OS llegue directo a su licencia.
- **Compra**: botón "Comprar por WhatsApp" / "Finalizar compra" → genera un pedido a través de WhatsApp (`wa.me`).
- **Redirección con aviso**: la función `redirectTo()` muestra un loader animado con mensaje antes de abrir el destino (pestaña nueva o misma pestaña según el caso).

## Servicios (index.html)

- El servicio **EC-OS** redirige en la misma pestaña a `market.html#producto=ecospro` mostrando un aviso de redirección animado, para que el usuario aterrice directamente en la oferta de la licencia.
- Los servicios se abren en un modal estilo sistema operativo con logo, descripción, estado y características.

## Proyectos Activos (index.html)

Tabla de seguimiento con ID, designación, fase y estado. Todos los proyectos enlazan a la organización **https://github.com/Estalingradocorp**.

| ID | Proyecto |
|---|---|
| PRJ-101 | EC WebSend |
| PRJ-102 | Estalingrado Corp Buscador |
| PRJ-103 | EC News |
| PRJ-104 | Demiurgo Box |
| PRJ-105 | EC Download |
| PRJ-106 | Portal NOA |
| PRJ-107 | IA-27 Agente |
| PRJ-108 | Centinela |
| PRJ-109 | Auralis |

## Stack

- HTML5 + Tailwind CSS (CDN)
- Font Awesome 6
- Google Fonts (Inter, JetBrains Mono, Playfair Display)
- JavaScript vanilla (animaciones, partículas, modales, sistema de ventanas estilo macOS)

## Despliegue

El sitio se despliega automáticamente en GitHub Pages desde la rama `main`. Cualquier cambio commiteado y pusheado a `main` se publica automáticamente.