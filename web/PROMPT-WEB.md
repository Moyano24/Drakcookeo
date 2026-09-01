# Brief para construir la web de Drak Cookeo

> **Cómo usar este archivo:** poné esta carpeta entera como proyecto en Claude Code y escribile:
> «Leé `PROMPT-WEB.md` y construí la web siguiendo ese brief.»
> Si preferís pegar el prompt a mano, copiá todo lo que está debajo de la línea.

---

Construí una landing page de una sola página para **Drak Cookeo**, una marca de cookies estilo Nueva York de Mendoza Capital, Argentina. Vende desde casa con take away y delivery, no tiene local a la calle.

La única función de la página es que alguien que vio el flyer o el perfil de Instagram termine escribiendo por WhatsApp para hacer un pedido. No es un e-commerce: no lleva carrito, ni login, ni pasarela de pago.

## Restricciones técnicas

- **Un solo archivo `index.html`** con el CSS y el JS embebidos. Sin frameworks, sin build, sin npm. Tiene que poder subirse arrastrando la carpeta a Netlify.
- **Mobile-first.** Más del 90% del tráfico va a llegar del link de la biografía de Instagram, o sea desde un celular. Diseñá primero para 390px de ancho y después ampliá.
- Las imágenes salen de la carpeta `assets/` que ya está en el proyecto. No generes imágenes ni uses placeholders de servicios externos.
- Tipografías desde Google Fonts con `<link>`, con stack de respaldo real en cada `font-family`.
- Sin librerías externas salvo las fuentes.

## Identidad visual (usar exactamente estos valores)

```css
:root{
  --cacao:      #2A1810;  /* texto, fondos oscuros */
  --masa:       #F4E4CC;  /* fondo principal */
  --caramelo:   #D98E2B;  /* relleno de botones y franjas */
  --caramelo-t: #8F5210;  /* acento cuando va escrito sobre fondo claro */
  --horneado:   #7A4A24;  /* texto secundario */
  --cereza:     #9B3626;  /* solo promociones */
  --leche:      #FFFBF5;  /* tarjetas */
  --linea:      #DFC9A8;  /* bordes */
}
```

Tipografías:

- **Fraunces** 900/700 — títulos, nombre de marca, precios grandes. Nunca todo en mayúscula.
- **Archivo** 400/600/700 — textos, botones, descripciones.
- **IBM Plex Mono** 600 — etiquetas, precios chicos, horarios. Siempre mayúscula con `letter-spacing`.

```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,700;9..144,900&family=Archivo:wght@400;600;700&family=IBM+Plex+Mono:wght@600&display=swap">
```

**Regla de color que no se puede romper:** `--caramelo` (#D98E2B) sobre fondo claro da contraste 2,1 y no se lee al sol. Usalo solo como relleno (fondo de botón, franja, subrayado grueso). Si necesitás el acento como texto sobre `--masa`, usá `--caramelo-t` (#8F5210).

Proporción de uso: 60% Masa, 25% Cacao, 10% Caramelo, 5% Cereza y Horneado. `--cereza` aparece únicamente en el bloque de la promoción.

## Estructura de la página, en este orden

1. **Hero** — `assets/logo-horizontal.png`, el slogan «Cookies de calidad con el real sabor de Nueva York» y un botón grande **Pedir por WhatsApp**. Todo tiene que entrar sin scrollear en una pantalla de celular. Debajo, una línea chica: «Mendoza Capital · Take away y delivery».
2. **Franja de promoción** — fondo `--cereza`, texto «15% OFF la primera semana». Es una sección que se puede sacar entera después, así que dejala como un bloque independiente y comentado en el HTML.
3. **Historia** — dos párrafos sobre el concepto «Del asfalto neoyorquino a tu barrio» y quién es Drak. Al costado, `assets/drak-personaje.png`.
4. **Sabores** — grilla de tarjetas (`--leche` sobre `--masa`), una por sabor: foto, nombre en Fraunces, descripción corta y precio en IBM Plex Mono. Arrancá con **3 tarjetas**, y dejá el HTML armado de forma que agregar una cuarta sea copiar un bloque.
5. **Cómo comprar** — take away y delivery, zona de entrega, medios de pago. Tres ítems con iconos hechos en SVG inline (no uses una librería de iconos).
6. **Dónde y cuándo** — zona de referencia y horarios. Sin dirección exacta: venden desde casa, la dirección se pasa por WhatsApp al confirmar el pedido.
7. **Pie** — links a Instagram y TikTok (`@drakcookeo`), y el año.
8. **Botón flotante de WhatsApp** — fijo abajo a la derecha mientras se scrollea, visible en toda la página menos cuando el botón del hero está en pantalla.

## Datos que faltan

Todavía no están definidos el número de WhatsApp, los sabores con sus precios, los horarios ni la zona de delivery. **Poné constantes claramente marcadas al principio del `<head>`, en un solo bloque**, para que reemplazarlas después sea cambiar un lugar y no buscar por todo el archivo:

```html
<!-- ====== COMPLETAR ESTOS DATOS ====== -->
<!-- WHATSAPP: 549261XXXXXXX  (549 + código de área sin el 0 + número sin el 15) -->
<!-- SABOR 1: nombre / descripción / precio -->
<!-- ... -->
```

Usá textos de relleno evidentes (`Sabor pendiente`, `$ —`) para que nadie los confunda con contenido real. Lo mismo con las fotos de los sabores: mientras no estén, dejá un recuadro con fondo `--leche`, borde `--linea` y la leyenda «Foto pendiente».

## Detalles técnicos que suelen olvidarse

- **Link de WhatsApp con mensaje pre-escrito:**
  `https://wa.me/549261XXXXXXX?text=Hola%20Drak%20Cookeo!%20Quiero%20hacer%20un%20pedido`
  El número va con **549** adelante y **sin el 15**. Si no, el link no abre el chat.
- **Open Graph**, para que cuando pasen el link por WhatsApp aparezca la cookie y no un cuadro gris:
  `og:title`, `og:description`, `og:image` apuntando a `assets/og-image.jpg` (ya está, 1200×630), `og:type="website"` y `og:url`. Agregá también `twitter:card="summary_large_image"`.
- **Favicon:** `assets/favicon-512.png` y `assets/apple-touch-icon.png`.
- **Medición de clics al WhatsApp:** cada `<a>` que lleve a WhatsApp tiene que tener `data-evento="whatsapp"` y un listener que dispare `gtag('event','click_whatsapp')` **solo si `window.gtag` existe**. Así el día que peguen el script de Google Analytics empieza a medir sin tocar nada más, y mientras tanto no rompe.
- **`<title>`:** «Drak Cookeo — Cookies estilo Nueva York en Mendoza». Y una `meta description` que nombre Mendoza y cookies.
- `lang="es-AR"`, `<meta name="viewport">`, `alt` real en todas las imágenes, `width` y `height` en los `<img>` para que no salte el layout al cargar.
- Foco visible en botones y links (`:focus-visible`), y respetar `prefers-reduced-motion`.
- Animaciones: como mucho una aparición suave al scrollear. Nada de parallax ni de contadores.

## Lo que NO hay que hacer

- No inventes sabores, precios, direcciones ni horarios: dejalos como pendientes.
- No uses `localStorage` ni nada que guarde datos: la página no lo necesita.
- No agregues formulario de contacto. El contacto es WhatsApp.
- No pongas mapa embebido de Google Maps: no hay local a la calle.
- No uses imágenes de bancos de fotos. Las fotos reales entran después.

## Cuando termines

1. Abrí la página y revisala a 390px de ancho, no solo en escritorio.
2. Verificá que el botón de WhatsApp funcione (aunque el número sea el de ejemplo).
3. Dejá un `README.md` con: qué datos faltan completar y en qué línea están, y los pasos para publicar en Netlify Drop.
