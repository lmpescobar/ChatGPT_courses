# Prompt: clon pixel-perfect de la página de inicio de DeepSeek

Construye un clon de **solo frontend** de la página de inicio de DeepSeek (`https://www.deepseek.com/en/`), replicando su UX/UI y su stack tecnológico, con la mayor fidelidad visual posible a nivel de píxel. Es un ejercicio de reproducción de interfaz; no es un producto oficial de DeepSeek.

## 1. Alcance

**Incluido**
- Solo la página de inicio en inglés (`/en/`).
- Header y navegación (con menús desplegables), hero, todas las secciones y footer.
- Estados de interacción: hover, focus, active, menús, pestañas, acordeones y carruseles, si existen.
- Animaciones de entrada y de scroll, con las mismas duraciones y curvas de easing que el original.
- Responsive en los viewports de la sección 3.
- Textos idénticos al original, porque afectan a la comparación visual.

**Excluido**
- Chat, login, registro, pagos y cualquier llamada a backend o API.
- Otras páginas: sus enlaces apuntan a `#`.
- Analytics, cookies de terceros y scripts de tracking.
- Otros idiomas.

## 2. Stack tecnológico

Antes de escribir código, determina el stack real a partir del HTML de `/en/`:

- **Framework y bundler**: busca `/_next/` y `__NEXT_DATA__` (Next.js), `/_nuxt/` (Nuxt), `/_astro/` (Astro), `/assets/index-*.js` (Vite), `___gatsby` (Gatsby) o `wp-content` (WordPress).
- **CSS**: identifica si usa Tailwind, CSS Modules, CSS-in-JS, Sass o CSS plano.
- **Fuentes**: familia, pesos y formato (woff2).

Usa ese mismo framework y versión mayor, y regístralo en el `README.md`. Si no puedes determinarlo con certeza, detente y pregunta: el stack es un requisito central.

## 3. Viewports de referencia

| Nombre | Ancho × alto |
|---|---|
| Desktop XL | 1920 × 1080 |
| Desktop | 1440 × 900 |
| Tablet horizontal | 1024 × 768 |
| Tablet vertical | 768 × 1024 |
| Móvil | 390 × 844 |

Captura siempre en el mismo estado: fuentes cargadas (`document.fonts.ready`), animaciones terminadas o desactivadas, vídeos pausados, scroll en 0 y captura de página completa. Usa el Chromium de Playwright que ya esté instalado; no ejecutes `playwright install`.

## 4. Fidelidad a nivel de píxel

- **Fuente de verdad**: los valores medidos del DOM original, no estimaciones a ojo. Por cada elemento, mide con `getBoundingClientRect` y `getComputedStyle` la posición, el tamaño, `font-*`, `line-height`, `letter-spacing`, `color`, `background`, `padding`, `margin`, `gap`, `border-radius` y `box-shadow`, en cada viewport.
- **Fuentes**: misma familia y pesos. Si la fuente es propietaria y no puede obtenerse legalmente, usa la alternativa libre más cercana y documenta la diferencia.
- **Iconos**: recréalos como SVG propios, con la misma forma y el mismo tamaño.
- **Logo y marca**: placeholder del mismo tamaño y posición, salvo que el usuario confirme que puede usar el logo oficial en este proyecto.
- **Imágenes e ilustraciones**: mismas dimensiones, `object-fit` y `alt`.
- **Transiciones**: mismas duraciones y easing que en el CSS original.

## 5. Proceso

1. Captura la referencia en los cinco viewports: screenshots de página completa y métricas del DOM.
2. Detecta el stack (sección 2) y crea el proyecto con ese stack.
3. Construye sección por sección, de arriba abajo, y compara cada una al terminarla.
4. Itera sobre las diferencias hasta cumplir la sección 6.
5. Verifica las interacciones: menús, hover, navegación por teclado y responsive.

## 6. Criterios de aceptación

- **Diff de píxeles**: el objetivo es 0 % de diferencia. El mínimo aceptable es **0,5 %** de píxeles distintos por viewport, con pixelmatch y umbral 0,1. Las zonas dinámicas (vídeo, carruseles en movimiento, contadores) se excluyen y se documentan.
- **Build** sin errores ni warnings.
- **Consola** sin errores al cargar ni al interactuar.
- **Móvil 390 px**: sin scroll horizontal.
- **Accesibilidad básica**: HTML semántico, `lang="en"`, `alt` en imágenes, foco visible y el mismo contraste que el original.
- **`<head>`**: mismo `<title>`, `meta description`, Open Graph y favicon.
- **Red**: ninguna petición a dominios externos, salvo fuentes o CDN declarados en el proyecto.

## 7. Entregables

Carpeta `deepseek-clone/` en la raíz del repo, con:

- `README.md`: stack detectado, comandos (`install`, `dev`, `build`), desviaciones conocidas y aviso de que es un clon de práctica no afiliado a DeepSeek.
- Script de captura y comparación (`scripts/compare`) que genere las capturas del original y del clon, y las imágenes de diferencia por viewport.
- `reports/summary.md`: porcentaje de diferencia por viewport y desviaciones.

## 8. Restricciones

- Sin backend ni envío de datos: los formularios no envían nada.
- Sin suplantación: el clon no se publica en un dominio ni con branding que haga pensar que es DeepSeek.
- Sin copia del código del sitio: no copies bundles JS minificados ni hojas de estilo completas. Recrea la UI con código propio a partir de los valores medidos.
- No cargues recursos directamente desde el dominio original: descárgalos a `public/` o `assets/`.

## 9. Prerrequisitos y entradas alternativas

- **Acceso a `www.deepseek.com`** desde el entorno. Si no hay acceso, el usuario puede aportar el HTML guardado de `/en/` con sus recursos, capturas de pantalla a 1440 y 390 px, y los archivos de fuente.

## 10. Defaults si no se indica otra cosa

- Uso: práctica local y educativa.
- Logo: placeholder.
- Carpeta: `deepseek-clone/`.
- Umbral de aceptación: 0,5 %.
