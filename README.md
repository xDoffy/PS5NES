# PS5NES

Emulador NES para PS5, diseñado por **El Doffy**.

> **Estado:** prototipo visual y propuesta técnica. El emulador todavía no está integrado ni es compilable.

## Qué contiene este repositorio

- [`prototype/index.html`](prototype/index.html): maqueta interactiva de la biblioteca en carrusel y sus opciones de vídeo, mando y carpeta de ROMs.
- [`docs/propuesta-tecnica.md`](docs/propuesta-tecnica.md): alcance, arquitectura candidata, fases y puntos técnicos por resolver.

La maqueta usa juegos y datos ficticios para mostrar el diseño. No escanea discos, descarga carátulas, abre ROMs ni ejecuta juegos.

## Dirección del proyecto

La propuesta parte del port abierto [PS5_RetroArch](https://github.com/mihawk-99/PS5_RetroArch), que incluye el core FCEUmm para NES/Famicom. Antes de integrar o redistribuir código habrá que conservar sus atribuciones y licencias de terceros. La compatibilidad con PS5 en firmware **12.40** está pendiente de comprobar en la consola objetivo.

## Próximos pasos

1. Confirmar arranque y entrada DualSense en firmware 12.40.
2. Abrir una ROM de prueba aportada por el usuario y comprobar audio, guardado y salida de vídeo.
3. Integrar el core NES y la biblioteca local con carátulas y perfiles por juego.
4. Conectar los controles de vídeo, remapeo y carpeta mostrados en el prototipo.

No se incluyen ROMs ni BIOS. La biblioteca debe usar copias y archivos que aporte legalmente el usuario.

