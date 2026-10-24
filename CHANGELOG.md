# Changelog

Todos los cambios notables de este proyecto se documentan en este archivo.

El formato se basa en [Keep a Changelog](https://keepachangelog.com/es/1.1.0/) y el proyecto usa [Versionado Semántico](https://semver.org/lang/es/).

## [No versionado] — En desarrollo

Cambios realizados sobre el estado publicado en GitHub Pages.

### Cambios en Market (`market.html`)

#### Añadido
- **Categorías nuevas**: filtros **Android** y **Juegos Android** en la barra de filtros.
- **Categoría Mods**: nuevo filtro **Mods** en la barra de filtros.
- **Cyberpunk 2077 · CyberEngineTweaks (PRD-018)**: primer producto de la categoría Mods, con aviso de bloqueo de Windows y publicidad integrada.
- **Auralis (PRD-019)**: nuevo producto en la categoría **Android** — reproductor de música para Android, moderno y sin anuncios (Kotlin, Jetpack Compose, Clean Architecture, Hilt y Room; Android 8.0 o superior; versión v0.1.0; por EstalingradoCorp). Sus imágenes se pueden **ampliar** (zoom con rueda, arrastre y botones ±/reset) igual que los productos físicos.
- **Command & Conquer: Generals - Zero Hour (PRD-020)**: nuevo producto en la categoría **Juegos Android** (también visible en Juegos). Prueba de rendimiento del port para Android con descripción, video embebido y botón **OBTENER GRATIS** que redirige al proveedor.
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
- **Auralis (PRD-019)**: botón de descarga **activado**. Abre (con el loader de redirección) **https://nicolabarranco27-a11y.github.io/AURALIS/#descarga**. La tarjeta pasó de "Próximamente" a **Gratis**.
- **Command & Conquer: Generals - Zero Hour (PRD-020)**: botón **OBTENER GRATIS** (nuevo soporte de etiqueta de botón vía `btnLabel`) → redirige a `https://centercorpec.wixsite.com/softwarelab/post/command-and-conquer-generals-pc-full-espa%C3%B1ol`.
- **Intercambio de posiciones en "Todos"**: la tarjeta de **Auralis** y la de **Camiseta Estalingrado** se intercambiaron de lugar en el catálogo.
- **Barra de filtros/búsqueda**: la barra de búsqueda ahora se **alinea con la primera fila de etiquetas** (contenedor `#filters`: `md:items-center` → `md:items-start`).

#### Corregido / Reorganizado
- Las apps Android (AppGallery, F-Droid) ya **no** aparecen en la categoría "Programas": quedan solo en **Android**, dejando "Programas" exclusivamente para software de PC.
- Badges de tarjeta y modal de AppGallery y F-Droid actualizados de "Programa" a "Android".
- **Cyberpunk 2077 · CyberEngineTweaks (PRD-018)**:
  - Botón de descarga **deshabilitado** (ahora muestra "Próximamente").
  - **Motivo**: el framework estaba **crasheando el juego** de los usuarios. Se solicitó la corrección a los desarrolladores; la descarga se rehabilitará cuando se resuelva.

### Notas de ingeniería / Errores a evitar

> Registrado para que **no se repita**.

- **No modificar `redirectTo()` sin necesidad.** Es la función central de redirección que usan **TODOS** los botones de descarga/obtener (DeepSeek, AppGallery, LibreOffice, Malwarebytes, OpenCode, F-Droid, 0 A.D., Luanti, AssaultCube, Auralis, Command & Conquer, EC-OS, etc.).

- **Flujo correcto de `redirectTo()` (NO TOCAR):**
  1. Mostrar la pantalla de carga (loader) y animarla hasta el 100%.
  2. **Recién al llegar al 100%**, ejecutar `window.open(url,'_blank','noopener')`.
  - La apertura es **asíncrona a propósito** (después del loader), para respetar la pantalla de carga.

- **Error cometido (y revertido):** ante el reporte "el botón de Auralis no funciona", se cambió `window.open` para que fuera **síncrono** y luego se usó una **pestaña en blanco** que se navegaba al final. Ambos intentos **rompieron la pantalla de carga**: la pestaña del proveedor se abría antes de terminar el loader, o aparecía una pestaña en blanco durante la carga. Se **revirtió** al flujo original.

- **Causa raíz real del síntoma:** el navegador mostraba una **versión cacheada** del `market.html` (el botón aún decía "Próximamente"). **No** era un bug de código.

- **Regla:** ante el reporte de un botón/producto puntual, **primero** descartar caché del navegador (recarga forzada con `Ctrl+F5`). **No** tocar lógica que afecta a todos los productos por un caso aislado.

- **Si el `window.open` asíncrono es bloqueado** por el navegador: la pantalla de carga **no se toca**. Se abre la pestaña al terminar el loader **sin `noopener`** (para poder detectar el bloqueo) y, si devuelve `null`, se navega a la **misma pestaña** con `location.href`. Así el botón siempre llega al proveedor.
  - **Aclaración**: el bloqueo de popups **no es un problema de tiempo**. En Chrome/Edge la "user activation" dura ~5 s (el loader de 1,8 s ya entraba) y en Firefox/Safari un `window.open` dentro de `setTimeout`/`rAF` nunca cuenta como gesto del usuario. **Reducir el loader a 0,4 s no lo arregla.**
- **Vigilancia de bloqueos adicionales**: queda **bajo observación** un posible bloqueo distinto al ya cubierto (por ejemplo: el navegador abre la pestaña pero la deja en blanco, o una extensión bloquea sólo la URL del proveedor). Para ese caso se agregó una **comprobación a los 2,5 s**: si la pestaña sigue en `about:blank`, se cierra y la navegación se hace en la **misma pestaña**. Si se detectan nuevos casos, se documentan en esta misma sección antes de tocar el código.

### Cambios en Inicio (`index.html`)

#### Añadido
- **Proyecto Auralis** (PRJ-109) en la tabla de Proyectos Activos (fase Desarrollo, estado En Proceso).
- **Logo** del servicio EC-OS agregado a la tarjeta de servicios y al modal de detalle.

#### Cambiado
- El servicio **EC-OS** ahora redirige en la **misma pestaña** a `market.html#producto=ecospro`, mostrando un aviso de redirección animado antes de navegar.
- Todos los proyectos en la tabla de Proyectos Activos (PRJ-101 a PRJ-109) ahora enlazan a la organización **https://github.com/Estalingradocorp**.

## Despliegue

Todo lo anterior está publicado en GitHub Pages: https://estalingradocorp.github.io/EstalingradoCorp/