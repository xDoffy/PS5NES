# PS5NES autónomo

## Objetivo

Convertir PS5NES en un título homebrew de PS5 instalable por separado. La app tendrá su propio proceso, interfaz y datos; no iniciará RetroArch ni EmulationStation y no requerirá un juego comercial como anfitrión.

## Core NES

La propuesta es enlazar directamente [FCEUmm](https://github.com/libretro/libretro-fceumm), un core NES/Famicom de código abierto. PS5NES proporcionará sus callbacks libretro de vídeo, audio, entrada y opciones de entorno. **RetroArch no se incluirá ni se ejecutará**: se reutiliza el core, no su frontend.

FCEUmm está bajo GPL-2.0. Un release que lo enlace debe preservar la licencia, atribuciones y ofrecer el código fuente correspondiente. No se incluirán ROMs, BIOS ni juegos.

## Carpetas propias

Estructura lógica prevista dentro de los datos de PS5NES:

```text
PS5NES/
├── eboot.bin
├── data/
│   ├── roms/nes/       # ROMs .nes del usuario
│   ├── covers/         # carátulas descargadas o aportadas
│   ├── saves/          # SRAM por juego
│   ├── states/         # estados de guardado
│   ├── config/         # preferencias globales y por juego
│   └── shaders/        # presets visuales
└── licenses/           # licencias y avisos de terceros
```

En la interfaz se mostrará `data/roms/nes` como ruta predeterminada y se permitirá elegir otra carpeta accesible. El empaquetado debe mapear esta estructura a una ubicación persistente accesible por FTP en la consola; no se fija una ruta `/app0` o `/data/homebrew/<TITLE_ID>` hasta tener el título y probar los permisos reales.

## Funciones previstas

- Carrusel DualSense con cartuchos NES, portada por juego y fallback cuando no haya arte.
- Descarga de carátulas con conexión, caché local y progreso; la biblioteca y los juegos seguirán disponibles sin conexión.
- Ajustes propios para mapeo de botones, proporción, escalado, filtros, volumen y preferencias por juego.
- SRAM y estados en las carpetas de PS5NES.

La salida 4K es escalado de la imagen NES; no una mejora universal de texturas. Resolución, filtros y rendimiento deben medirse en la PS5.

## Estado técnico

El contenido actual de `prototype/` sigue siendo una maqueta, y el antiguo tema ES-DE está archivado en `integration/`. Todavía no hay un frontend PS5 autónomo, un paquete `.pkg` ni un release instalable de esta arquitectura.

El entorno de trabajo no tiene el toolchain de PS5 ni una distribución WSL. Además, el [PS5SDK público](https://github.com/PS5Dev/PS5SDK) se describe como experimental y advierte que todavía no puede generar aplicaciones completas. Antes del release hace falta elegir y configurar una cadena compatible con títulos homebrew, crear el punto de entrada y el empaquetado, y probarlo en una PS5 con firmware 12.40.

Como referencia de hardware se revisó [pNES5](https://github.com/ITSeniy/pNES5), que contiene emulación NES y entrada DualSense para PS5. Su método de ejecución documentado requiere LuaC0re y un juego anfitrión concreto, por eso no cumple el objetivo de título autónomo.

