# Plantilla «Reparación de móviles e informática» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **tecnológico**
(negro + verde neón + grises, rejilla de puntos como una placa de pruebas, titulares en sans pesada del sistema,
detalles en monoespaciada, esquinas pequeñas y bandas a todo el ancho de la ventana). Todo en castellano de España,
frases cortas, sin jerga. El brief de diseño completo está en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`…
  - `primario` = verde neón de botones, bandas verdes (cómo trabajamos, cifras), cursor del hero, leds e iconos sobre negro. La letra encima se calcula sola (`--sobre-primario`: negra si el primario es claro, blanca si es oscuro).
  - `acento` = verde oscuro para textos y detalles verdes sobre fondo claro (antetítulos, etiquetas de aparato, categorías, «[+]» de preguntas). Tiene que leerse sobre el fondo.
  - `texto` = color de la letra **y** de las bandas oscuras (cabecera, hero, marcas, opiniones, presupuesto, pie; garantías y el formulario usan una versión algo más clara, `--grafito`). En ellas la letra usa `fondo`. Si el cliente pide fondo oscuro, el diseño se invierte solo.
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-titulos` = sans pesada del sistema, 800, interletrado cerrado; `--fuente-mono` = Cascadia / SF Mono / Consolas… para antetítulos, botones, precios, cifras y etiquetas; botones `.btn` con flecha, `.btn-sec`, `.btn-negro`; `.chip`; `.cursor`; bandas `.banda-clara`, `.banda-negra`, `.banda-grafito`, `.banda-neon`; `.puntos` y `.puntos-claros`; filas partidas a sangre `.partida`, `.partida--md`, `.partida-texto--izq/--der`, `.partida-foto`; cabecera, formularios, pie y barra inferior de móvil). Sin fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (lista y descripción en `fotos.json`); las de relleno, en `public/placeholders/` (`producto.svg` sale en las fichas de la tienda sin foto). En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`).
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en un chip con led verde + nombre.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Todas son bandas a todo el ancho.
- `hero` → `hero.astro`: foto a sangre con velo negro; `antetitulo`, `titulo` enorme (la última palabra en verde, con cursor), `texto`, `cta` (presupuesto) y `cta_secundario` (llamar: `url: "tel:+34…"`). En escritorio, una «consola» con teléfono, WhatsApp, horario y dirección de `contacto`. Abajo, tira con los aparatos (los `dispositivo` de `reparaciones`).
- `reparaciones` → `reparaciones.astro`: `reparaciones: [{nombre, texto, precio, tiempo, dispositivo}]` en tabla de dos columnas con filtros por aparato (sin JavaScript); `nota` y `cta` en la cabecera. Los aparatos y los nombres son las opciones del formulario de presupuesto. Sin precio, no sale precio. **No inventes precios.**
- `marcas` → `marcas.astro`: banda negra con «teclas» (`items: [{titulo}]`, solo texto, nunca logotipos). **No se pinta si `items` está vacío.**
- `proceso` → `proceso.astro` (Cómo trabajamos): banda verde con pasos numerados en barra de progreso (`items: [{titulo, texto, icono}]`) y `galeria` (lista de fotos) en franja de borde a borde.
- `garantias` → `garantias.astro`: banda grafito partida, `imagen` a sangre a la izquierda con marco de visor; `texto` e `items: [{titulo, texto, icono}]` en rejilla 2×2.
- `productos` → `productos.astro` (Tienda): `productos: [{nombre, texto, categoria, precio, estado, imagen}]` en fichas (2 columnas en móvil, 4 en escritorio) con el `estado` en chip. `cta` opcional.
- `cifras` → `cifras.astro`: `items: [{titulo: "+300", texto}]` en banda verde. **No se pinta si `items` está vacío.** No inventes cifras.
- `opiniones` → `opiniones.astro`: `testimonios: [{texto, autor, nota}]`; la primera como cita grande, el resto en columnas. No inventes opiniones.
- `preguntas` → `preguntas.astro`: cabecera con WhatsApp y teléfono y acordeón `details/summary` en dos columnas (`preguntas: [{pregunta, respuesta}]`). Sin preguntas no se pinta.
- `presupuesto` → `presupuesto.astro`: mitad con `imagen` a sangre velada, titular, `items` y `nota`; mitad grafito con el formulario (nombre, teléfono, aparato, marca y modelo, qué le pasa, mensaje). `boton_formulario` opcional.
- `contacto` → `contacto.astro`: datos de `contacto` en filas (teléfono enorme) e `imagen` a sangre a la derecha con la localidad. Si `presupuesto` no está activa, en lugar de la foto sale el formulario de contacto.
- `texto` → `texto.astro`: apartado genérico (párrafos, `imagen` a sangre, `items`, `cta`). Para apartados nuevos: `tipo: texto`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. Procura alternar bandas (`reparaciones`, `productos`, `preguntas` y `contacto` son claras; `proceso` y `cifras`, verdes; el resto, oscuras).
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas.
4. **Listas planas**: nunca una lista dentro de un elemento de lista. Precios y cifras siempre como texto entre comillas (`"desde 49 €"`, `"+300"`). Máximo 24 elementos por lista. Para agrupar reparaciones, el campo `dispositivo`.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: mejor un apartado con `tipo:` (`tipo: texto`, `tipo: reparaciones`, `tipo: productos`…) y su propio id. Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)` y una banda a todo el ancho. `src/pages/index.astro` la recoge sola: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` son obligatorios. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio —tipo `ElectronicsStore`— y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto (`.contenedor`, `.partida-texto`) con las fotos y fondos tocando el borde, sin scroll horizontal en móvil, botones de 48 px, barra inferior fija de móvil («Llamar» / «WhatsApp»: sale sola si hay teléfono o WhatsApp). Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. Los formularios no tienen servidor: abren el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Iconos disponibles: ver `src/components/ui/Icono.astro` (de la tienda: `movil, tablet, portatil, consola, chip, lupa, candado, escudo, herramienta, euro, check, reloj, whatsapp, telefono`…). El icono de cada reparación sale de su `dispositivo` (Móvil, Tablet, Portátil, Consola; otro, `chip`).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Páginas propias (fichas por elemento)
- Listas con página propia (espejo de `fichas:` de template.yaml en `src/data/fichas.ts`): `secciones.reparaciones.reparaciones` → `/reparaciones/<slug>/` (reparación).
  **Solo los elementos con `detalle`** (texto largo, párrafos separados por una línea en blanco, ≤ 3000 caracteres, sin HTML) tienen página;
  los demás siguen como hasta ahora. Campos opcionales del elemento: `slug` (si falta, sale del nombre; no lo pongas sin motivo)
  e `imagenes` («/fotos/a.jpg; /fotos/b.jpg», galería de la ficha; la foto principal es `imagen` o, si no hay, la primera de `imagenes`).
  El resto de campos (precio, duración…) salen en la tabla de datos de la ficha.
- Una orden «añade una página para X» = escribir su `detalle` en site.yaml. Nunca crees a mano páginas en
  `src/pages/reparaciones/`: salen solas de `src/pages/[coleccion]/[slug].astro`.
- No tocar `src/lib/paginas.ts`, `src/lib/slug.ts` ni `src/lib/seo.ts` (comunes a todas las plantillas). Las páginas propias entran solas en
  `sitemap.xml` y `llms.txt`, con su JSON-LD (migas y servicio/producto con precio si lo hay).
