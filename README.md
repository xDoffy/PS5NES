# PS5NES

Experiencia NES para PS5, diseñada por **El Doffy**.

> **Estado:** integración de frontend en progreso. El paquete para PS5 usa el core FCEUmm incluido en PS5 RetroArch y el frontend EmulationStation. PS5NES no es un título `.pkg` independiente y no incluye ROMs ni cores.

## Qué contiene este repositorio

- [`prototype/index.html`](prototype/index.html): maqueta interactiva de la biblioteca en carrusel y sus opciones de vídeo, mando y carpeta de ROMs.
- [`integration/`](integration/README.md): tema instalable de EmulationStation para mostrar la biblioteca como cartuchos y jugar con el FCEUmm de PS5 RetroArch.
- [`docs/propuesta-tecnica.md`](docs/propuesta-tecnica.md): alcance, arquitectura candidata, fases y puntos técnicos por resolver.

La página HTML sigue siendo una maqueta de diseño con datos ficticios. El paquete de integración es el que conecta la biblioteca real y el lanzamiento de juegos, usando una instalación compatible de PS5 RetroArch.

## Dirección del proyecto

La integración parte del port abierto [PS5_RetroArch](https://github.com/mihawk-99/PS5_RetroArch), que incluye EmulationStation y el core FCEUmm para NES/Famicom. PS5NES distribuye únicamente su tema y sus assets; instala PS5 RetroArch por separado. Conserva las atribuciones y licencias de terceros. La compatibilidad con PS5 en firmware **12.40** está pendiente de comprobar en la consola objetivo.

## Próximos pasos

1. Confirmar arranque y entrada DualSense en firmware 12.40.
2. Abrir una ROM de prueba aportada por el usuario y comprobar audio, guardado y salida de vídeo.
3. Integrar el core NES y la biblioteca local con carátulas y perfiles por juego.
4. Conectar los controles de vídeo, remapeo y carpeta mostrados en el prototipo.

No se incluyen ROMs ni BIOS. La biblioteca debe usar copias y archivos que aporte legalmente el usuario.

