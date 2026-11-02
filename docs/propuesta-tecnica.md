# PS5NES — propuesta técnica

**Estado:** alcance inicial, 2 de noviembre de 2026  
**Nombre del proyecto:** PS5NES
**Autor:** El Doffy
**Consola objetivo:** PS5, firmware 12.40

## Objetivo

Crear una aplicación homebrew enfocada en NES/Famicom para PS5 con una biblioteca visual de juegos presentada como cartuchos, controles DualSense, guardados y opciones de imagen. La aplicación leerá juegos y carátulas que aporte el usuario; no incluirá ROMs comerciales.

## Base recomendada

Partir del port abierto [PS5_RetroArch](https://github.com/mihawk-99/PS5_RetroArch) y mantener inicialmente el core [FCEUmm](https://github.com/libretro/libretro-fceumm), derivado de FCE Ultra y ya compilado para PS5 por ese port. Su tabla de sistemas identifica NES/Famicom → FCEUmm; también documenta render de software con salida por Vulkan, shaders, filtros de CPU, overlays, artwork y una biblioteca compartida entre RetroArch y EmulationStation. La versión publicada que consulté declara verificación en PS5 con firmware 13.40, no en 12.40; la primera fase debe comprobar el arranque en tu consola antes de fijar compatibilidad.

Como referencia técnica alternativa, [pNES5](https://github.com/ITSeniy/pNES5) ya implementa NES nativo, controles DualSense y menú, pero es un emulador propio limitado a los mappers enumerados en su README; no es el port de un core de PC que buscamos. Puede servir como referencia para detalles de integración PS5.

## Diseño funcional

- **Biblioteca de cartuchos:** carrusel horizontal controlado con D-pad: el juego seleccionado al centro, los demás cartuchos a los lados con perspectiva. Cada juego se representa como cuerpo de cartucho NES con su propia portada en la etiqueta, nombre y región; favoritos, búsqueda y “continuar jugando”. Si no hay portada, mostrar un cartucho con arte de reemplazo y el título. Crear el marco y tema con arte original o licencia permisiva; no heredar el tema Alekfull NX, que tiene restricciones no comerciales.
- **Portadas automáticas:** al importar juegos y al actualizar la biblioteca, poner en cola los juegos sin portada y descargarlas desde las fuentes configuradas en el emulador. La base ya hace descarga automática al añadir un juego y trae fuentes Libretro, LaunchBox y ScreenScraper; el trabajo específico es que el escaneo normal de la biblioteca encole también lo que falte, sin exigir abrir un navegador. Guardar en caché local, conservar el arte que el usuario ya tenga, mostrar progreso y permitir reintento. Si no hay coincidencia o conexión, mantener el cartucho de reemplazo y seguir jugando.
- **Carga de biblioteca:** la maqueta muestra `/app0/content/nes`, ruta interna recomendada para el sandbox de PS5 RetroArch (en FTP: `/data/homebrew/PPSA99169/content/nes`). El tema de integración no explora rutas por su cuenta; la biblioteca, el escaneo y la gestión de carátulas los proporcionan PS5 RetroArch y EmulationStation.
- **Juego:** FCEUmm, entrada DualSense, guardado de SRAM y estados, pausa, reinicio y regreso a biblioteca.
- **Vídeo:** mantener la imagen fuente y escalarla en la salida de vídeo a 4K cuando la ruta gráfica lo permita; preservar proporción y ofrecer nearest-neighbor, filtros CRT/scanline, compuesto y paletas. Probar rendimiento y estabilidad en hardware antes de declarar 4K como garantía.
- **“Mejora de texturas”:** NES usa gráficos 2D de tiles/paleta, así que no existe una mejora universal de texturas como en juegos 3D. Lo que sí encaja es escalado limpio, shaders/filtros, paletas alternativas y, en una fase posterior, parches o reemplazos específicos por juego.
- **Ajustes por juego:** relación de aspecto, filtro, paleta, mapeo de botones, estado de guardado y carátula.

## Fases

1. **Arranque mínimo:** construir el proyecto base y abrir una ROM de prueba aportada por el usuario en la PS5 objetivo; comprobar vídeo, audio, DualSense y persistencia de archivos.
2. **Producto NES:** dejar el inicio centrado en NES, escáner de biblioteca, carátulas estilo cartucho, metadatos, favoritos y ajustes simples.
3. **Imagen:** presets de escalado y filtros; ajustar salida 4K y relación de aspecto en la consola real.
4. **Pulido:** estados, historial, opciones por juego, arte personalizado, rendimiento, accesibilidad y empaquetado/documentación.

## Integración del siguiente release

El siguiente release entrega un tema `PS5NES-es-de` para el frontend EmulationStation incluido en [PS5_RetroArch](https://github.com/mihawk-99/PS5_RetroArch). Ese port ya integra FCEUmm, reconoce la biblioteca de RetroArch y lanza los juegos desde EmulationStation. El tema usa la portada descargada de cada juego dentro de una silueta original de cartucho NES y la foto de consola proporcionada por el autor como fondo semitransparente.

PS5NES no redistribuye PS5 RetroArch ni el core. El usuario debe instalar el port compatible por separado y aportar sus copias de juegos. El camino de datos recomendado es la carpeta `content/nes` del título RetroArch (en FTP: `/data/homebrew/PPSA99169/content/nes`; dentro del título: `/app0/content/nes`). La ruta `/data/roms/nes` mostrada por la maqueta no se debe prometer como accesible dentro del sandbox del título.

La integración no sustituye la validación en consola. La compatibilidad con firmware 12.40, la descarga de carátulas en ese firmware y el rendimiento de los filtros se deben confirmar en la PS5 objetivo antes de anunciar soporte.

## Riesgos técnicos a resolver temprano

- La compatibilidad del homebrew depende del firmware, método de carga y bibliotecas/toolchain disponibles. El SDK público de PS5 se describe como experimental y sin soporte completo para aplicaciones; conviene usar la cadena de compilación probada por el port y comprobar el arranque específicamente en firmware 12.40.
- FCEUmm y el frontend tienen licencias y avisos de terceros propios. Al redistribuir compilaciones deben mantenerse los textos, atribuciones y fuentes correspondientes; la compilación inicial seguirá el esquema legal del proyecto base.
- La resolución de salida, shader y efecto de filtros debe comprobarse con la PS5 objetivo, no solo en escritorio.

## Referencias consultadas

- [PS5_RetroArch — README, sistemas, gráficos, archivos y compilación](https://github.com/mihawk-99/PS5_RetroArch)
- [PS5_RetroArch — último release consultado](https://github.com/mihawk-99/PS5_RetroArch/releases)
- [PS5_RetroArch v1.0.0-beta.1 — descarga automática al añadir juegos](https://github.com/mihawk-99/PS5_RetroArch/releases/tag/v1.0.0-beta.1)
- [FCEUmm — documentación del core y licencia GPLv2](https://docs.libretro.com/library/fceumm/)
- [FCEUmm — fuente abierta](https://github.com/libretro/libretro-fceumm)
- [pNES5 — alternativa nativa y límites documentados](https://github.com/ITSeniy/pNES5)
- [PS5 SDK — estado experimental y limitaciones](https://github.com/PS5Dev/PS5SDK)
- [Libretro — playlists y carátulas](https://docs.libretro.com/guides/roms-playlists-thumbnails/)
- [ES-DE — tema con carrusel y tipos de arte](https://gitlab.com/es-de/emulationstation-de/-/blob/master/THEMES.md)



