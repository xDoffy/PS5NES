# PS5NES

Experiencia NES para PS5, diseñada por **El Doffy**.

> **Estado:** prototipo visual. El siguiente release está redefinido como una aplicación homebrew PS5 autónoma en formato carpeta: ejecutable propio, core NES incorporado y carpetas propias bajo `/data/homebrew/<TITLE_ID>/`. La integración con RetroArch/EmulationStation deja de ser el objetivo del proyecto.

## Qué contiene este repositorio

- [`prototype/index.html`](prototype/index.html): maqueta interactiva de la biblioteca en carrusel y sus opciones de vídeo, mando y carpeta de ROMs.
- [`standalone/`](standalone/README.md): arquitectura y estructura de datos prevista para la aplicación independiente.
- [`integration/`](integration/README.md): complemento anterior de EmulationStation, conservado como referencia y fuera del siguiente release.
- [`docs/propuesta-tecnica.md`](docs/propuesta-tecnica.md): alcance, arquitectura candidata, fases y puntos técnicos por resolver.

La página HTML sigue siendo una maqueta con datos ficticios. Todavía no hay una carpeta de título compilada con `eboot.bin` lista para instalar. El siguiente release debe ejecutar el emulador y su biblioteca desde PS5NES, sin requerir RetroArch, EmulationStation ni un juego anfitrión.

## Dirección del proyecto

La nueva arquitectura enlazará el core abierto FCEUmm directamente con el frontend de PS5NES. El título se instalará como carpeta bajo `/data/homebrew/<TITLE_ID>/`; sus datos quedarán en `data/roms/nes`, `data/covers`, `data/saves`, `data/states` y `data/config`. Se conservarán las licencias del core y no se incluirán juegos. La compatibilidad con firmware **12.40** está pendiente de comprobar en la consola objetivo.

## Próximos pasos

1. Crear una carpeta de título homebrew con `eboot.bin`, `sce_sys/param.json` y su propio identificador.
2. Integrar FCEUmm directamente, con una capa PS5NES para vídeo, audio y DualSense.
3. Conectar carrusel/carátulas y guardar ROMs, portadas, partidas y ajustes bajo la carpeta de PS5NES.
4. Compilar y probar la carpeta de título en una PS5 con firmware 12.40 antes de publicar el release.

No se incluyen ROMs ni BIOS. La biblioteca debe usar copias y archivos que aporte legalmente el usuario.

