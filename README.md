# PS5NES

Experiencia NES para PS5, diseñada por **El Doffy**.

> **Estado:** integración de frontend en progreso. El paquete para PS5 usa el core FCEUmm incluido en PS5 RetroArch y el frontend EmulationStation. PS5NES no es un título `.pkg` independiente y no incluye ROMs ni cores.

## Qué contiene este repositorio

- [`prototype/index.html`](prototype/index.html): maqueta interactiva de la biblioteca en carrusel y sus opciones de vídeo, mando y carpeta de ROMs.
- [`integration/`](integration/README.md): tema instalable de EmulationStation para mostrar la biblioteca como cartuchos y jugar con el FCEUmm de PS5 RetroArch.
- [`docs/propuesta-tecnica.md`](docs/propuesta-tecnica.md): alcance, arquitectura candidata, fases y puntos técnicos por resolver.

La página HTML sigue siendo una maqueta de diseño con datos ficticios. El tema de integración presenta la lista y sus carátulas como cartuchos; la biblioteca y el lanzamiento de los juegos los gestiona EmulationStation dentro de una instalación compatible de PS5 RetroArch.

## Dirección del proyecto

La integración parte del port abierto [PS5_RetroArch](https://github.com/mihawk-99/PS5_RetroArch), que incluye EmulationStation y el core FCEUmm para NES/Famicom. PS5NES distribuye únicamente su tema y sus assets; instala PS5 RetroArch por separado. Conserva las atribuciones y licencias de terceros. La compatibilidad con PS5 en firmware **12.40** está pendiente de comprobar en la consola objetivo.

## Próximos pasos

1. Confirmar arranque y entrada DualSense en firmware 12.40.
2. Abrir una ROM de prueba aportada por el usuario y comprobar audio, guardado y salida de vídeo.
3. Comprobar biblioteca, scraper de carátulas, controles y filtros en la PS5 objetivo.
4. Evaluar una aplicación `.pkg` propia solo después de confirmar firmware, SDK y runtime compatibles.

No se incluyen ROMs ni BIOS. La biblioteca debe usar copias y archivos que aporte legalmente el usuario.

