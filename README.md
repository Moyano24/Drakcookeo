# Web Drak Cookeo

Landing de una sola página. Todo vive en `index.html`: el CSS y el JS van
embebidos, no hay build, no hay npm, no hay dependencias salvo las fuentes
de Google. Para publicarla se arrastra esta carpeta entera.

    index.html           la web completa
    assets/              imágenes de la marca
    PROMPT-WEB.md        el brief con el que se construyó
    DATOS-PENDIENTES.md  planilla para completar los datos que faltan

---

## 1. Qué falta completar y en qué línea está

Los números de línea son de `index.html`. Si editás el archivo y se corren,
buscá el texto de la última columna: cada dato pendiente tiene un texto de
relleno inconfundible.

### Contacto

| Dato | Línea | Qué buscar |
|---|---|---|
| Número de WhatsApp (hero) | **510** | `549261XXXXXXX` |
| Número de WhatsApp (cómo comprar) | **692** | `549261XXXXXXX` |
| Número de WhatsApp (botón flotante) | **771** | `549261XXXXXXX` |

Los tres son el mismo número. Lo más rápido es un buscar-y-reemplazar de
`549261XXXXXXX` en todo el archivo.

> **El formato importa:** va `549` + código de área **sin el 0** + número
> **sin el 15**, todo junto y sin espacios ni guiones.
> Mendoza queda así: `5492611234567`.
> Si le ponés el 0 o el 15, el link no abre el chat.

### Sabores

| Sabor | Nombre | Descripción | Precio |
|---|---|---|---|
| 1 | línea **581** | línea **582** | línea **583** |
| 2 | línea **594** | línea **595** | línea **596** |
| 3 | línea **607** | línea **608** | línea **609** |

Buscar: `Sabor pendiente`, `Descripción pendiente`, `$ —`.

### Horarios y zona

| Dato | Línea | Qué buscar |
|---|---|---|
| Zona de referencia | **717** | `Zona pendiente` |
| Días y horarios | **722** | `Horario pendiente` |
| Cierre de pedidos | **727** | `Horario pendiente` |
| Zona de delivery | **668** | `Zona de delivery pendiente` |
| Medios de pago | **685** | `Medios de pago pendientes` |

### Promoción

| Dato | Línea | Qué buscar |
|---|---|---|
| Vigencia del 15% OFF | **532** | `Vigencia pendiente` |

### Después de publicar

| Dato | Línea | Qué buscar |
|---|---|---|
| `og:url` | **53** | `TU-USUARIO` |
| `og:image` | **56** | `TU-USUARIO` |

Ver el punto 5.

---

## 2. Fotos de los sabores

Sacalas cuadradas, con luz de ventana y fondo liso. Que pesen menos de
200 KB cada una — [tinypng.com](https://tinypng.com) las comprime gratis.

Guardalas en `assets/` como `sabor-1.jpg`, `sabor-2.jpg`, `sabor-3.jpg`.

Después, en cada tarjeta de la sección Sabores:

1. Descomentá el `<img class="tarjeta__foto" ...>` (líneas **575-577**,
   **588-590**, **601-603**).
2. Borrá la línea de abajo, la del `<div class="foto-pendiente">`.
3. Cambiá el `alt` por el nombre real del sabor.

El recuadro "Foto pendiente" ya ocupa exactamente el mismo espacio que va a
ocupar la foto, así que la grilla no se va a mover.

## 3. Agregar un cuarto sabor

En la línea **612** hay una cuarta tarjeta ya escrita, comentada. Borrá el
`<!--` de arriba y el `-->` de abajo y aparece. La grilla se reacomoda sola.

## 4. Sacar la promoción del 15%

Buscá `INICIO BLOQUE PROMO` (línea **525**) y `FIN BLOQUE PROMO`
(línea **534**), y borrá todo lo que hay entre esos dos comentarios,
comentarios incluidos. No comparte estilos con ninguna otra sección: sacarla
no rompe nada.

## 5. Publicar

### Opción A — GitHub Pages

El repo ya está inicializado y con el primer commit hecho. Falta crearlo en
GitHub y empujarlo. Los pasos están en la sección "Publicar en GitHub Pages"
más abajo.

URL final: `https://TU-USUARIO.github.io/drakcookeo/`

### Opción B — Netlify Drop

1. Entrá a [app.netlify.com/drop](https://app.netlify.com/drop)
2. Arrastrá **esta carpeta entera** (no solo el `index.html`: necesita
   `assets/`)
3. Te da una URL tipo `drakcookeo.netlify.app`
4. Actualizá `og:url` y `og:image` (líneas **53** y **56**) con la URL real.
   Eso es lo que hace que al pasar el link por WhatsApp aparezca la foto de
   la cookie y no un cuadro gris. Volvé a arrastrar la carpeta.
5. Probala en un celular real antes de ponerla en la biografía de Instagram.

Para actualizar después: arrastrás la carpeta de nuevo y listo.

## 6. Medir los clics al WhatsApp (Google Analytics)

Ya está preparado. Los tres botones de WhatsApp tienen un listener que
dispara el evento `click_whatsapp`, pero **solo si Google Analytics está
cargado**. Mientras no lo esté, no hace nada y no rompe.

Cuando tengas la cuenta, pegá el script de GA justo antes del `</body>`
(línea **782**, donde dice *"Aca va el script de Google Analytics"*). No hay
que tocar nada más: la medición arranca sola.

---

## Cosas que conviene no romper

- **`--caramelo` (#D98E2B) nunca va como color de texto sobre fondo claro.**
  Da contraste 2,1 y no se lee al sol, que es justo donde se va a leer esta
  página. Va solo como relleno: fondo de botón, franja, subrayado grueso. Si
  necesitás el naranja como texto, usá `--caramelo-t` (#8F5210).
- Los `<img>` tienen `width` y `height` puestos a propósito, para que el
  layout no salte mientras cargan. Si cambiás una imagen, actualizá esos
  números.
- No hay formulario de contacto, ni carrito, ni mapa, ni `localStorage`.
  Es deliberado: la página existe para que la persona termine escribiendo
  por WhatsApp.

---

## Publicar en GitHub Pages — paso a paso

El repo local ya está listo: `git init` hecho, primer commit hecho,
`.nojekyll` y `.gitignore` incluidos. Falta solo conectarlo con GitHub.

### 1. Crear el repo vacío en GitHub

Entrá a [github.com/new](https://github.com/new) y completá:

- **Repository name:** `drakcookeo`
- **Public** ← obligatorio, Pages no funciona en repos privados con plan gratis
- **NO** marques *Add a README file*, *Add .gitignore* ni *Choose a license*.
  Tiene que quedar completamente vacío o el push va a chocar.

Click en **Create repository**.

### 2. Conectar y subir

En la pantalla que aparece, copiá la URL del repo (la que termina en
`.git`). Después, en la terminal, parado en esta carpeta:

    git remote add origin https://github.com/TU-USUARIO/drakcookeo.git
    git push -u origin main

La primera vez te va a pedir usuario y contraseña. **La contraseña de
GitHub no sirve**: hay que usar un Personal Access Token. Se saca en
Settings → Developer settings → Personal access tokens → Tokens (classic) →
Generate new token, con el permiso `repo` marcado. Copiá el token y pegalo
donde pide la contraseña.

(Si preferís evitar el token: instalá GitHub Desktop y arrastrá la carpeta.)

### 3. Activar Pages

En el repo, arriba: **Settings** → en el menú izquierdo, **Pages**.

- **Source:** Deploy from a branch
- **Branch:** `main` — carpeta `/ (root)`
- **Save**

### 4. Esperar

Tarda 1 a 3 minutos la primera vez. En la pestaña **Actions** del repo se ve
el progreso. Cuando termina, arriba en Settings → Pages aparece la URL:

    https://TU-USUARIO.github.io/drakcookeo/

### 5. Arreglar la miniatura de WhatsApp

Con la URL ya real, en `index.html` reemplazá `TU-USUARIO` por tu usuario en
las líneas **53** (`og:url`) y **56** (`og:image`). Después:

    git add index.html
    git commit -m "og: URL real de GitHub Pages"
    git push

Sin esto, al pasar el link por WhatsApp sale un cuadro gris en vez de la
cookie. Las dos URLs tienen que ser absolutas (`https://...`), no relativas.

### Para actualizar la web de acá en más

    git add -A
    git commit -m "que cambiaste"
    git push

En 1-2 minutos se actualiza sola.

### Si algo sale mal

| Síntoma | Causa casi siempre |
|---|---|
| 404 en toda la web | Pages todavía no terminó, o Branch mal elegido en Settings → Pages |
| La web carga pero sin logo ni personaje | Faltó subir la carpeta `assets/` |
| Cuadro gris al pasar el link por WhatsApp | `og:image` sigue con `TU-USUARIO`, o no es absoluta |
| WhatsApp muestra la miniatura vieja | Tiene caché. Agregale `?v=2` al final del link para forzar |
| `git push` rechazado | El repo en GitHub no se creó vacío |

> **Nota:** esta carpeta está dentro de OneDrive. Tener un `.git` adentro de
> una carpeta sincronizada a veces genera conflictos si editás desde dos
> máquinas a la vez. Para un proyecto de una persona no suele dar problemas,
> pero si empieza a molestar, mové la carpeta fuera de OneDrive: con el repo
> en GitHub ya vas a tener el respaldo cubierto.
