# Changelog

Todos los cambios notables de este proyecto se documentan en este archivo.

El formato se basa en [Keep a Changelog](https://keepachangelog.com/es/1.1.0/) y el proyecto usa [Versionado Semántico](https://semver.org/lang/es/).

## [No versionado] — En desarrollo

Cambios realizados sobre el estado publicado en GitHub Pages.

### Cambios en Market (`market.html`)

#### Añadido
- **Categorías nuevas**: filtros **Android** y **Juegos Android** en la barra de filtros.
- Asignación de productos a las nuevas categorías:
  - **AppGallery HUAWEI** → categoría Android.
  - **F-Droid** → categoría Android.
  - **Luanti** → categoría Juegos Android (mantiene su presencia en Juegos por ser multiplataforma).

#### Cambiado
- **EC-OS Pro License (PRD-001)**:
  - Cambiada a oferta gratuita por tiempo limitado: precio **Gratis** (antes $6.000).
  - Precio antiguo (tachado) establecido en **$20.000**.
  - Badge de oferta ahora más visible: color rojo y texto "Oferta Limitada".
  - Botón de compra cambiado a **"Obtener"** de color azul, que muestra un aviso de redirección (loader animado) y luego conduce al sitio EC-OS.
- **OpenCode → OpenCode Desktop** (PRD-009):
  - Renombrado el producto a "OpenCode Desktop".
  - Descripción actualizada para describir la app de escritorio del agente IA.
  - Link de descarga actualizado a `https://opencode.ai/es/download`.
  - Etiqueta "Terminal" → "Escritorio".

#### Corregido / Reorganizado
- Las apps Android (AppGallery, F-Droid) ya **no** aparecen en la categoría "Programas": quedan solo en **Android**, dejando "Programas" exclusivamente para software de PC.
- Badges de tarjeta y modal de AppGallery y F-Droid actualizados de "Programa" a "Android".

### Cambios en Inicio (`index.html`)

#### Añadido
- **Proyecto Auralis** (PRJ-109) en la tabla de Proyectos Activos (fase Desarrollo, estado En Proceso).
- **Logo** del servicio EC-OS agregado a la tarjeta de servicios y al modal de detalle.

#### Cambiado
- El servicio **EC-OS** ahora redirige en la **misma pestaña** a `market.html#producto=ecospro`, mostrando un aviso de redirección animado antes de navegar.
- Todos los proyectos en la tabla de Proyectos Activos (PRJ-101 a PRJ-109) ahora enlazan a la organización **https://github.com/Estalingradocorp**.

## Despliegue

Todo lo anterior está publicado en GitHub Pages: https://estalingradocorp.github.io/EstalingradoCorp/