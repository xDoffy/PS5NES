# PS5NES — propuesta técnica

**Estado:** alcance inicial, 2 de noviembre de 2026  
**Nombre del proyecto:** PS5NES
**Autor:** El Doffy
**Consola objetivo:** PS5, firmware 12.40

## Objetivo

Crear una aplicación homebrew enfocada en NES/Famicom para PS5 con una biblioteca visual de juegos presentada como cartuchos, controles DualSense, guardados y opciones de imagen. La aplicación leerá juegos y carátulas que aporte el usuario; no incluirá ROMs comerciales.

## Base recomendada

Usar el core abierto [FCEUmm](https://github.com/libretro/libretro-fceumm) directamente dentro de un título homebrew PS5 de PS5NES. PS5NES será el frontend: cargará el core y las ROMs, recibirá los cuadros y el audio, enviará la entrada DualSense y guardará las partidas. No iniciará RetroArch ni EmulationStation, ni necesitará otro juego como anfitrión.

FCEUmm implementa el core NES/Famicom como código abierto; el host aportará una capa compatible con su API libretro y usará sus componentes sin el ejecutable RetroArch. El core conserva su licencia GPL-2.0 y sus avisos. El build y los requisitos de publicación deben incluir el código fuente y avisos correspondientes.

El port [pNES5](https://github.com/ITSeniy/pNES5) sirve de referencia para DualSense, audio y renderizado en hardware PS5. No se toma como base de ejecución porque su método documentado depende de LuaC0re y de un juego anfitrión específico, lo que no satisface la meta de instalar PS5NES como título propio.

## Diseño funcional

- **Biblioteca de cartuchos:** carrusel horizontal controlado con D-pad: el juego seleccionado al centro, los demás cartuchos a los lados con perspectiva. Cada juego se representa como cuerpo de cartucho NES con su propia portada en la etiqueta, nombre y región; favoritos, búsqueda y “continuar jugando”. Si no hay portada, mostrar un cartucho con arte de reemplazo y el título. Crear el marco y tema con arte original o licencia permisiva; no heredar el tema Alekfull NX, que tiene restricciones no comerciales.
- **Portadas automáticas:** al importar juegos y al actualizar la biblioteca, poner en cola los juegos sin portada y descargarlas desde fuentes configurables. Guardar en caché en `data/covers/`, conservar el arte local, mostrar progreso y permitir reintento. Sin coincidencia o conexión, mostrar el cartucho de reemplazo.
- **Carpetas propias:** distribuir el ejecutable y el core con los datos de la app. La ruta configurable de ROMs será relativa a PS5NES y, por defecto, `data/roms/nes/`; portadas, SRAM, estados y ajustes vivirán en `data/covers/`, `data/saves/`, `data/states/` y `data/config/`.
- **Juego:** FCEUmm, entrada DualSense, guardado de SRAM y estados, pausa, reinicio y regreso a biblioteca.
- **Vídeo:** mantener la imagen fuente y escalarla en la salida de vídeo a 4K cuando la ruta gráfica lo permita; preservar proporción y ofrecer nearest-neighbor, filtros CRT/scanline, compuesto y paletas. Probar rendimiento y estabilidad en hardware antes de declarar 4K como garantía.
- **“Mejora de texturas”:** NES usa gráficos 2D de tiles/paleta, así que no existe una mejora universal de texturas como en juegos 3D. Lo que sí encaja es escalado limpio, shaders/filtros, paletas alternativas y, en una fase posterior, parches o reemplazos específicos por juego.
- **Ajustes por juego:** relación de aspecto, filtro, paleta, mapeo de botones, estado de guardado y carátula.

## Fases

1. **App autónoma:** crear el título PS5NES, su entrada de sistema, almacenamiento y empaquetado propio.
2. **Core y biblioteca:** enlazar FCEUmm directamente; escanear `data/roms/nes/`, ejecutar ROMs, guardar SRAM/estados y mostrar el carrusel de cartuchos.
3. **Interfaz y arte:** enlazar DualSense y vídeo; añadir descargas de carátulas, filtros, opciones de escala y ajustes persistentes.
4. **Validación:** compilar con una cadena de homebrew PS5 que admita títulos independientes y probar instalación/arranque en firmware 12.40 antes del release.

## Estado del siguiente release

El siguiente release objetivo es una aplicación homebrew independiente, con su propio título, proceso, interfaz y almacenamiento. El complemento ES-DE anterior se conserva como referencia visual, pero no cumple este requisito y queda fuera del release.

La arquitectura y las carpetas están definidas en [`../standalone/README.md`](../standalone/README.md). Aún falta implementar/enlazar el frontend PS5, compilar el título y confirmar funcionamiento en el firmware 12.40. No se debe publicar el paquete anterior de tema como si fuera el emulador autónomo.

## Riesgos técnicos a resolver temprano

- La compatibilidad del homebrew depende del firmware, método de carga y bibliotecas/toolchain disponibles. El SDK público de PS5 se describe como experimental y sin soporte completo para aplicaciones; hay que elegir una cadena que realmente pueda producir un título autónomo y comprobar el arranque específicamente en firmware 12.40.
- FCEUmm y el frontend tienen licencias y avisos de terceros propios. Al redistribuir compilaciones deben mantenerse los textos, atribuciones y fuentes correspondientes; la app debe publicar el código fuente que corresponda a GPL-2.0.
- La resolución de salida, shader y efecto de filtros debe comprobarse con la PS5 objetivo, no solo en escritorio.

## Referencias consultadas

- [FCEUmm — documentación del core y licencia GPLv2](https://docs.libretro.com/library/fceumm/)
- [FCEUmm — fuente abierta](https://github.com/libretro/libretro-fceumm)
- [pNES5 — emulador PS5 de referencia y requisitos de lanzamiento](https://github.com/ITSeniy/pNES5)
- [PS5 SDK — estado experimental y limitaciones](https://github.com/PS5Dev/PS5SDK)
- [ES-DE — tema con carrusel y tipos de arte](https://gitlab.com/es-de/emulationstation-de/-/blob/master/THEMES.md)



