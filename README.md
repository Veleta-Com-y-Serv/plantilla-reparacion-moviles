# Plantilla NoExpertise · Reparación de móviles e informática

Web tecnológica en negro y verde neón para servicios técnicos: reparaciones con precio, tienda y presupuesto.

- Sectores: reparación de móviles, informática, tienda de tecnología, telefonía, servicio técnico. Estilo: tecnológico. Plan mínimo: gratis.
- Secciones: hero, reparaciones, marcas, proceso (cómo trabajamos), garantias, productos (tienda), cifras, opiniones, preguntas, presupuesto, contacto (+ `texto` para apartados nuevos).
- Campos propios: `reparaciones.reparaciones[]` (`nombre, texto, precio, tiempo, dispositivo`; filtros por aparato), `reparaciones.nota`, `marcas.items` (solo nombres; no se pinta vacía), `proceso.items` (pasos) y `proceso.galeria` (franja de fotos), `garantias.items`, `productos.productos[]` (`nombre, texto, categoria, precio, estado, imagen`), `cifras.items` (no se pinta vacía), `presupuesto.items`, `presupuesto.nota`, `presupuesto.boton_formulario`.
- Formulario de presupuesto con aparato (opciones: los `dispositivo` de las reparaciones), marca y modelo y avería (opciones: los nombres de las reparaciones); sin servidor (`mailto`).
- Barra inferior fija en móvil con «Llamar» y «WhatsApp».
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`ElectronicsStore`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas`. Sin la clave, una sola página larga.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos a generar en `fotos.json`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.reparaciones.reparaciones` con `detalle` tiene su página en `/reparaciones/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
