# Reparación de móviles e informática: brief de diseño

Plantilla `reparacion-moviles` creada el 02/11/2026 a partir de `taller-mecanico` con `php artisan plantillas:nueva`
y rediseñada entera (fila 10 del brief de la tercera tanda «a ancho completo»). Este fichero se queda en el repo: es
lo que lee quien (persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: tiendas de reparación de móviles, servicios técnicos de informática, tiendas de tecnología y
  telefonía (`sectores`: reparacion-moviles, informatica, tienda-tecnologia, telefonia, servicio-tecnico). Su cliente
  llega con la pantalla rota o el portátil lento: quiere saber si se lo arreglan hoy, cuánto le cuesta y si sus
  datos están a salvo.
- **Qué tiene que conseguir la web**: que pidan presupuesto o llamen. Teléfono en cabecera, consola del hero,
  preguntas, contacto, pie y barra fija de móvil; «Pedir presupuesto» en cabecera, hero y reparaciones.
- **Tono y estilo** (`estilo: tecnologico`): preciso, rápido y cercano. Referencia que sí: losmartesnohayluna.com
  por las bandas a sangre y la tipografía grande; una terminal de comandos, una placa de pruebas, el visor de una
  cámara. Que no: la caja centrada estrecha con tarjetas blancas; el naranja, las franjas de señalización, los
  titulares estrechos en mayúsculas y las esquinas achaflanadas de `taller-mecanico` (de la que parte).
- **Paleta de ejemplo**: primario `#3dff8f` (verde neón), acento `#0b7a3e` (verde oscuro, legible sobre claro),
  fondo `#f3f4f5` (gris muy claro), texto `#0c0e10` (casi negro). Derivados en `global.css` con `color-mix`:
  `--grafito` (bandas gris oscuro: garantías y formulario), `--panel` (fichas sobre claro), `--linea`,
  `--linea-oscura`, `--brillo` (halo verde de los botones). `--sobre-primario` decide letra negra o blanca sobre el
  verde (oklch).
- **Tipografía**: del sistema. Titulares en sans pesada (`system-ui`, 800) con interletrado muy cerrado (-0,04 em) y
  en minúsculas; el título del hero llega a 6,75 rem en escritorio (2,6 en móvil) con la última palabra en verde y
  un cursor de bloque que parpadea. Monoespaciada (`ui-monospace`, Cascadia, SF Mono, Consolas) para antetítulos
  («//» delante, como un comentario de código), botones, precios, tiempos, cifras, etiquetas y el pie.
- **Formas**: esquinas de 4 px; chips con borde fino; leds verdes con halo; rejilla de puntos verdes sobre las bandas
  oscuras (y gris tenue sobre las claras); marco de esquinas verdes sobre la foto de garantías; «[+]» / «[−]» en las
  preguntas.
- **Ritmo de bandas** (todas de borde a borde; contenido hasta 90 rem, 16 px de margen en móvil):
  1. `hero` — negro con foto a sangre velada desde la izquierda y puntos a la derecha, 88 svh; en escritorio,
     consola con los datos de contacto; abajo, tira con los aparatos que se reparan.
  2. `reparaciones` — claro con puntos; cabecera partida (nota y botón a la derecha); filtros por aparato (radios +
     `:has`, sin JavaScript); tabla técnica en dos columnas desde 1200 px.
  3. `marcas` — negro; teclado de «teclas» 2/3/6 columnas.
  4. `proceso` — verde pleno; tres nodos «01-03» en barra de progreso (vertical en móvil); franja de tres fotos a
     sangre.
  5. `garantias` — grafito 50/50 con la foto vertical a sangre a la izquierda y rejilla 2×2 de compromisos.
  6. `productos` — claro; fichas cuadradas 2 (móvil) / 4 (escritorio) columnas con el estado en chip.
  7. `cifras` — verde; cuatro números monoespaciados separados por filetes.
  8. `opiniones` — negro; la primera opinión como cita grande, el resto en columnas con filete verde.
  9. `preguntas` — claro; cabecera con WhatsApp y teléfono; acordeón en dos columnas.
  10. `presupuesto` — partida: foto a sangre velada con titular, ventajas y nota; grafito con el formulario.
  11. `contacto` — claro 50/50: datos con iconos en chip negro y teléfono enorme; fachada a sangre con la localidad.
  Pie: negro con puntos, filete verde que se apaga y cuatro columnas. Barra fija de móvil: «Llamar» verde y
  «WhatsApp» negro.
- **Apartados y listas propias**: `reparaciones.reparaciones` (`nombre, texto, precio, tiempo, dispositivo`),
  `marcas.items` (`titulo`), `proceso.items` + `proceso.galeria`, `garantias.items`, `productos.productos`
  (`nombre, texto, categoria, precio, estado, imagen`), `presupuesto.items`. Las que salen vacías no se pintan
  (marcas, cifras, preguntas) o pintan solo su titular (reparaciones, productos, opiniones).
- **Fotos** (`fotos.json`, 11): banco de reparación con un móvil abierto (hero), multímetro, placa al microscopio y
  móvil con pantalla nueva (proceso), mesa de servicio técnico vertical (garantías), cuatro fotos de producto sobre
  gris (reacondicionados, funda, cargador), mostrador (presupuesto) y fachada de la tienda (contacto). Sin texto
  legible, sin logotipos ni personas.
- **Qué no hacer**: tarjetas blancas flotando en una caja estrecha; naranja, franjas diagonales o chaflanes (son de
  `taller-mecanico`); logotipos de marcas; precios o cifras inventados en los componentes.
