# Integración PS5NES para PS5 RetroArch

PS5NES se integra como tema de **EmulationStation** en [PS5 RetroArch](https://github.com/mihawk-99/PS5_RetroArch). PS5 RetroArch aporta el frontend, el core FCEUmm para NES/Famicom, la entrada DualSense y el lanzamiento de los juegos. Este paquete solo contiene el tema y sus assets: no es un `.pkg` independiente, no incluye el emulador ni ROMs.

## Instalar el tema

1. Instala por separado una versión compatible de PS5 RetroArch que incluya EmulationStation y FCEUmm.
2. Cierra el título en la PS5 y copia la carpeta `PS5NES-es-de` a `PPSA99169/es-de/themes/PS5NES-es-de/` en los archivos del título. Por FTP, la carpeta suele estar en `/data/homebrew/PPSA99169/`.
3. Abre PS5 RetroArch, elige EmulationStation y selecciona **PS5NES** en **UI Settings → Theme Set**.
4. Añade tus ROMs a la biblioteca de RetroArch. Al volver a abrir EmulationStation aparecerán en el carrusel.

El tema usa la imagen **cover** de cada juego como etiqueta del cartucho y una imagen genérica cuando falta la portada. La descarga de carátulas se hace desde las funciones de biblioteca/descarga de medios del port y necesita conexión; este tema no descarga imágenes por sí solo.

## ROMs, mandos e imagen

El directorio de contenido del título es el destino recomendado para que el sandbox de PS5 RetroArch pueda leer los juegos: en FTP, `/data/homebrew/PPSA99169/content/nes/`; dentro del título, `/app0/content/nes/`. La ruta `/data/roms/nes` que aparece en la maqueta HTML no debe usarse como predeterminada para este port, ya que puede quedar fuera de su sandbox. También puedes usar una unidad USB montada por el entorno homebrew compatible.

El core FCEUmm acepta imágenes NES `.nes` y también `.fds`, `.unf` y `.unif`; para esta integración usa `.nes` sin comprimir. El soporte de `.zip` depende del build y de la extracción de archivos del frontend, y no se da por confirmado aquí.

PS5 RetroArch ya gestiona el DualSense, el remapeo, los shaders y los filtros. FCEUmm incluye opciones de paleta y filtro NTSC; configura esos controles desde sus ajustes de core. NES dibuja gráficos 2D de baja resolución, así que 4K significa salida/escalado de pantalla y no una mejora universal de texturas.

## Estado de compatibilidad

El código de tema sigue la estructura del motor de temas ES-DE. No se pudo compilar ni ejecutar en una PS5 desde este entorno: no hay una distribución WSL configurada ni está instalado el SDK de PS5. La compatibilidad con firmware **12.40** debe confirmarse en la consola objetivo antes de anunciar el release como probado.

No se incluyen ROMs, BIOS ni archivos del core. El core FCEUmm está bajo GPL-2.0 y se obtiene a través de PS5 RetroArch; conserva allí sus licencias y avisos de terceros.

