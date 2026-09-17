# Bcho NAM Player 1.7.0

[English](README.md) | [Descargas](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest) | [Manual standalone](docs/USER_MANUAL.es.md) | [Manual plugin](docs/PLUGIN_MANUAL.es.md)

![Bcho NAM Player 1.7.0](docs/Caratula_BNAMP.png)

Procesador de guitarra con Neural Amp Modeler, pantallas IR y efectos. Aplicación standalone y plugin VST3; en macOS también Audio Unit (AU).

## Novedades de la 1.7.0

- Dos rutas independientes L/R, cada una con BLOCK NAM 1, BLOCK NAM 2, IR y rack de efectos.
- MONO / STEREO; en standalone, DUAL MONO envía una guitarra a ambas cadenas y SPLIT L/R procesa dos entradas por separado.
- Selectores NAM 1 L, NAM 2 L, NAM 1 R, NAM 2 R e IR L/R. NAM 1 conserva su propia ecualización.
- Dos filas de rack en estéreo, listas NAM/IR separadas y vúmetros por canal.
- Tarjetas de información de las capturas con metadatos e imagen cuando están disponibles.
- TONE3000: favoritos, descargados, tendencias, novedades, modelos propios y búsqueda del catálogo completo. Acceso y búsqueda integrada comparten sesión para evitar un segundo inicio innecesario.
- Detección de WebView2 en Windows. Si no está disponible, permite descargarlo desde Microsoft, usar el navegador externo o cancelar. No instala nada automáticamente.
- Recuperación de la última configuración del standalone, incluido el bypass. Primer inicio en MONO, con todos los bloques desactivados y sin cargar automáticamente modelos.
- Escala IR VOL separada del fader, indicaciones L/R sin recortes y tornillos con márgenes simétricos.
- Mejoras en recuperación de sesiones del plugin y procesamiento de bloques grandes durante renderizado.

## Sonido y manejo

Dos bloques NAM por ruta, IR sin normalización, mezcla IR BLEND, volumen de cabina entre -24 y 0 dB, puerta de ruido, tono, ganancias y afinador. Compresor, octavador, pitch shifter, chorus, flanger, phaser, delay y reverb: tres algoritmos y seis parámetros por efecto.

Presets portables `.bnpp` con recursos integrados y comprobación SHA-256. El standalone guarda ambas rutas; el plugin guarda una ruta por preset y ambas dentro del proyecto del DAW. Conserva los archivos NAM/IR originales para recuperar proyectos del DAW.

El standalone añade Audio Setup, ASIO en Windows, rutas MAIN/PRE/DI/WET, calibración con referencia de interfaz, once skins, conos animados y comprobación de actualizaciones. El plugin utiliza el dispositivo y las conexiones del DAW y el acabado Astra / Obsidian; no incluye el panel de dispositivos ni las rutas físicas del standalone.

## Paquetes e inicio rápido

- Windows x64: standalone portable y VST3.
- macOS Intel (`x86_64`) y Apple Silicon (`arm64`): standalone, VST3 y AU.
- Linux x86_64: standalone AppImage y VST3.

Los adjuntos de la release indican los paquetes realmente disponibles. El plugin debe coincidir con la arquitectura del DAW. AU solo existe en macOS. Los paquetes macOS tienen firma ad-hoc, no notarización de Apple.

Descomprime el ZIP. Para standalone abre **Bcho NAM Player**, configura AUDIO SETUP y carga NAM/IR. Para plugin consulta la ubicación de instalación en su manual, vuelve a escanear plugins y añádelo como efecto de audio en el DAW. Empieza con volumen bajo: con todos los bloques desactivados pasa señal seca.

WebView2 solo se necesita para TONE3000 integrado en Windows, no para audio local. En macOS se usa WKWebView y en Linux el navegador del sistema. Obtén los drivers de tu interfaz de su fabricante.

## Documentación e integridad

Los ZIP incluyen los manuales PDF de standalone y plugin en español e inglés. Versiones de lectura en [docs](docs). Comprueba los ZIP con `SHA256SUMS.txt`.

El repositorio público contiene documentación y descargas, **no el código fuente de la aplicación**. Los archivos automáticos de GitHub llamados “Source code” corresponden únicamente al contenido documental del repositorio público.

Consulta [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). Los modelos e IR tienen sus propias licencias; compartir presets no concede derechos sobre recursos de terceros.
