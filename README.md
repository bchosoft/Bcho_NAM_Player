# Bcho NAM Player 1.7.5

**[English](#english)** · **[Español](#español)** · [Downloads / Descargas](https://github.com/bchosoft/Bcho_NAM_Player/releases/tag/v1.7.5) · [Support on Ko-fi](https://ko-fi.com/bchosoft)

![Bcho NAM Player 1.7.5](docs/Portada_1.7.5.png)

---

## English

### Overview

Bcho NAM Player is a guitar processor built around **Neural Amp Modeler** captures, cabinet **impulse responses** and a rack of studio effects. It is available as a portable **standalone application** and as an audio-effect **plug-in** (VST3 on Windows, macOS and Linux, plus AU on macOS).

It has **two complete, independent signal paths - L and R**. Each path owns its own BLOCK NAM 1, BLOCK NAM 2, cabinet IR, eight-effect rack with free block order, gate, tone stack, master level, IR blend, IR cabinet volume, **input gain**, output gain, power, input calibration and tuner. In **MONO** one path plays; in **STEREO** both run side by side.

### What's new in 1.7.5

- **DAW sessions restore for real.** Reopening a project re-loads the saved NAM, pedal NAM and IR of **both** paths into the audio engine - not just their names in the lists - with every block's exact on/off state. It works whichever order the DAW uses to restore state and prepare audio, and with the editor closed.
- **No clicks, no noise.** Start-up, session restore, loading or replacing a NAM, loading a pedal NAM, preparing or re-initialising audio, and sample-rate or buffer-size changes all fade in from silence. Switching from one NAM to another fades out, installs the new (pre-warmed) capture and fades back in, so the waveform is never cut.
- **Always-stereo plug-in output.** On a mono track in STEREO both chains receive the same input, so one guitar drives two rigs; L feeds the left output and R the right output. INPUT GAIN is independent for L and R.
- **L/R effect links.** In STEREO a chain icon links an effect of L to the same effect of R: one edit changes both, while each block keeps its own on/off switch and position.
- **Eye view selector.** The block body enables or bypasses a block; the eye on each block chooses which block the shared controls and browsers describe. A bypassed block cannot be viewed.
- **TONE3000 library, faster and complete.** Selecting a tone loads it into the current NAM block at once (about one second to first sound; instant for tones you already downloaded). **RESTORE PREVIOUS MODEL** puts back the capture the block had before. A2 captures now load from every list, IR-only tones are marked, and the full-catalogue picker closes by itself when you choose a tone.
- **Clean shutdown in DAWs.** Closing a project that contains the plug-in no longer leaves the DAW process running.
- **Support the project** from the settings window: **[ko-fi.com/bchosoft](https://ko-fi.com/bchosoft)**.
- **Rewritten manuals**, English and Spanish, documenting every control with screenshots.

### Compatibility

| Platform | Standalone | Plug-in |
| --- | --- | --- |
| Windows 10/11 x64 | Portable `.exe` (ASIO, Windows Audio, DirectSound) | VST3 |
| macOS 11+ Apple Silicon (`arm64`) | `.app` | VST3 and AU |
| macOS 11+ Intel (`x86_64`) | `.app` | VST3 and AU |
| Linux x86_64 | AppImage | VST3 |

Match the plug-in package to your DAW's architecture. AAX is not included. macOS builds are ad-hoc signed and not Apple-notarized.

### Standalone

- Its own **Audio Setup**: driver (including ASIO on Windows), interface, active channels, sample rate and buffer size.
- **Four physical output routes**: MAIN (final sound), PRE (BLOCK NAM 2 before tone/effects/cabinet), DI (untouched input) and WET (post-cabinet).
- **DUAL MONO / SPLIT L/R** in STEREO: one guitar into both chains, or input 1 to L and input 2 to R. The L/R path selectors sit to the right of the two rack rows, clear of the input switch.
- **Remembers the last session** on a normal exit: both paths, captures, IRs, block order, bypass states, links, skin, device and routing. A first launch starts safely in MONO with nothing loaded.
- **Input Cali**: automatic calibration from your interface's dBu reference and the capture's `input_level_dbu` metadata.
- Eleven front-panel finishes, animated speaker cones driven by the real output level, update checks.

### VST3 / AU plug-in

- Audio effect with **stereo output on mono and stereo tracks**. MONO copies the left path to both outputs; STEREO sends L to the left output and R to the right output.
- The DAW project stores both paths, all controls, file references, rack order, algorithms, parameters, bypass states and L/R links. Sessions restore into the engine as described above.
- Host-automatable parameters per path: input gain, gate, tone controls (main and NAM 1), master, IR blend, IR volume, output gain, power, input calibration and tuner, plus the global MONO/STEREO switch.
- Uses the DAW's audio device; always the Astra / Obsidian finish.

### Captures, pedal NAM and IRs

- **BLOCK NAM 2** (amp) and **BLOCK NAM 1** (pedal or preamp) per path, each with its own folder, list and deep-search option. NAM A1, A2 Standard and A2 Nano are detected automatically. BLOCK NAM 1 has its own BASS / MID / TREBLE / PRESENCE.
- Load from **BROWSE LOCAL**, the list, **TONE3000**, a double-click on the block, or drag and drop onto the list or the block.
- **Cabinet IRs** (`.wav`, mono or stereo, up to 8192 samples) are resampled to the device rate and **never normalized**. **IR BLEND** mixes dry and cabinet; **IR VOL** sets the cabinet branch from -24 to 0 dB (default -12 dB).
- Hover a NAM block or list row for the **capture information card**: metadata and artwork.

### Rack and effects

Eleven blocks per path in processing order, freely reorderable around the BLOCK NAM 2 and IR anchors. **Click the block body to enable or bypass it; click the eye to view it; double-click to open its editor or file chooser.** Compressor, octaver, pitch shifter, chorus, flanger, phaser, delay and reverb, each with **three algorithms and six real-unit parameters**; changes are smoothed and feedback is bounded.

### Portable `.bnpp` presets

A preset embeds its captures and IR (verified with SHA-256) together with rack order, algorithms, parameters, bypass states and controls. Standalone presets hold both paths and the L/R links; plug-in presets hold the selected path. Audio device and routing are deliberately excluded, so presets move between computers.

### TONE3000 and WebView2

Connect your TONE3000 account once; the player keeps an encrypted refresh token and never needs a browser again on that computer. Browse **TRENDING, LATEST, FAVOURITES, DOWNLOADED and MINE**, audition by selecting, or open **SEARCH FULL CATALOGUE**. On Windows the embedded pages use **Microsoft WebView2**; it is detected directly (also inside DAWs, with a writable per-user data folder). If it is missing you can open Microsoft's official download page, use your external browser or cancel - **nothing is installed automatically**, and local audio never needs WebView2. macOS uses WKWebView; Linux uses the system browser.

### Installing

**Standalone** - extract the ZIP and keep its files together.

- Windows: run `Bcho NAM Player.exe`; install your interface's ASIO driver for the lowest latency.
- macOS: open `Bcho NAM Player.app` (right-click → **Open** the first time if Gatekeeper asks).
- Linux: `chmod +x` the AppImage and run it.

**Plug-in** - close the DAW, copy the **whole bundle**, restart and rescan.

| System | Copy to |
| --- | --- |
| Windows VST3 | `C:\Program Files\Common Files\VST3\Bcho NAM Player.vst3` |
| macOS VST3 | `~/Library/Audio/Plug-Ins/VST3/Bcho NAM Player.vst3` |
| macOS AU | `~/Library/Audio/Plug-Ins/Components/Bcho NAM Player.component` |
| Linux VST3 | `~/.vst3/Bcho NAM Player.vst3` |

### Using the standalone in five steps

1. Gear → **AUDIO SETUP**: choose driver, interface, input channel, sample rate, buffer, and make sure **MAIN** points at your monitors.
2. **BROWSE LOCAL** (or **TONE3000**) to load an amp capture into BLOCK NAM 2.
3. **BROWSE IR** to load a cabinet (skip it if your capture already includes one).
4. Set **INPUT GAIN** while watching INPUT VU, then **MASTER VOL** and **OUTPUT GAIN**.
5. Click effect blocks to add them; double-click to edit.

Start at a low monitoring level. With every block bypassed the dry signal passes through.

### Downloads

All files for this version: **[Bcho NAM Player v1.7.5](https://github.com/bchosoft/Bcho_NAM_Player/releases/tag/v1.7.5)**

| Package | File |
| --- | --- |
| Windows standalone (embedded browser) | [BchoNAMPlayer-v1.7.5-Windows-x64-Standalone-EmbeddedBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-Windows-x64-Standalone-EmbeddedBrowser.zip) |
| Windows VST3 (embedded browser) | [BchoNAMPlayer-v1.7.5-Windows-x64-VST3-EmbeddedBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-Windows-x64-VST3-EmbeddedBrowser.zip) |
| Windows standalone (external browser) | [BchoNAMPlayer-v1.7.5-Windows-x64-Standalone-ExternalBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-Windows-x64-Standalone-ExternalBrowser.zip) |
| Windows VST3 (external browser) | [BchoNAMPlayer-v1.7.5-Windows-x64-VST3-ExternalBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-Windows-x64-VST3-ExternalBrowser.zip) |
| macOS Apple Silicon standalone (embedded browser) | [BchoNAMPlayer-v1.7.5-macOS-arm64-Standalone-EmbeddedBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-arm64-Standalone-EmbeddedBrowser.zip) |
| macOS Apple Silicon VST3 + AU (embedded browser) | [BchoNAMPlayer-v1.7.5-macOS-arm64-Plugins-EmbeddedBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-arm64-Plugins-EmbeddedBrowser.zip) |
| macOS Apple Silicon standalone (external browser) | [BchoNAMPlayer-v1.7.5-macOS-arm64-Standalone-ExternalBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-arm64-Standalone-ExternalBrowser.zip) |
| macOS Apple Silicon VST3 + AU (external browser) | [BchoNAMPlayer-v1.7.5-macOS-arm64-Plugins-ExternalBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-arm64-Plugins-ExternalBrowser.zip) |
| macOS Intel standalone (embedded browser) | [BchoNAMPlayer-v1.7.5-macOS-x86_64-Standalone-EmbeddedBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-x86_64-Standalone-EmbeddedBrowser.zip) |
| macOS Intel VST3 + AU (embedded browser) | [BchoNAMPlayer-v1.7.5-macOS-x86_64-Plugins-EmbeddedBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-x86_64-Plugins-EmbeddedBrowser.zip) |
| macOS Intel standalone (external browser) | [BchoNAMPlayer-v1.7.5-macOS-x86_64-Standalone-ExternalBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-x86_64-Standalone-ExternalBrowser.zip) |
| macOS Intel VST3 + AU (external browser) | [BchoNAMPlayer-v1.7.5-macOS-x86_64-Plugins-ExternalBrowser.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-x86_64-Plugins-ExternalBrowser.zip) |
| Linux standalone (AppImage) | [BchoNAMPlayer-v1.7.5-Linux-x86_64-Standalone.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-Linux-x86_64-Standalone.zip) |
| Linux VST3 | [BchoNAMPlayer-v1.7.5-Linux-x86_64-VST3.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-Linux-x86_64-VST3.zip) |
| Checksums | [SHA256SUMS.txt](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/SHA256SUMS.txt) |

Every ZIP includes its English and Spanish PDF manual in a `manuals` folder. The manuals are also online: [standalone](docs/USER_MANUAL.en.md) · [plug-in](docs/PLUGIN_MANUAL.en.md), and as PDF in [docs/manuals](docs/manuals).

### Support the project

Bcho NAM Player is free. If it is useful to you, you can support it at **[ko-fi.com/bchosoft](https://ko-fi.com/bchosoft)** - also reachable from **SUPPORT PROJECT ON KO-FI** in the standalone settings and **OPEN KO-FI** in the plug-in settings.

### Credits, licences and integrity

Bcho NAM Player by **Bcho Soft**. It is built with [JUCE 8.0.12](https://github.com/juce-framework/JUCE/tree/8.0.12) and [NeuralAmpModelerCore 0.5.4](https://github.com/sdatkinson/NeuralAmpModelerCore/tree/v0.5.4) (with Eigen and JSON for Modern C++); see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). Verify downloads against `SHA256SUMS.txt`.

This public repository contains documentation and release downloads, **not the application source code**; GitHub's automatic "Source code" archives contain only this documentation. NAM captures and impulse responses have their own licences - sharing presets does not grant rights to third-party resources.

---

## Español

### Descripción general

Bcho NAM Player es un procesador de guitarra construido alrededor de capturas **Neural Amp Modeler**, **respuestas impulsionales** de pantalla y un rack de efectos de estudio. Está disponible como **aplicación standalone** portable y como **plugin** de efecto de audio (VST3 en Windows, macOS y Linux, y AU en macOS).

Tiene **dos rutas de señal completas e independientes, L y R**. Cada ruta tiene su propio BLOCK NAM 1, BLOCK NAM 2, IR de pantalla, rack de ocho efectos con orden libre, puerta de ruido, sección de tonos, volumen máster, IR blend, volumen de pantalla, **ganancia de entrada**, ganancia de salida, encendido, calibración de entrada y afinador. En **MONO** suena una ruta; en **STEREO** funcionan las dos a la vez.

### Novedades de la 1.7.5

- **Las sesiones del DAW se restauran de verdad.** Al reabrir un proyecto, los NAM, NAM de pedal e IR guardados de **las dos** rutas vuelven a cargarse en el motor de audio —no solo sus nombres en las listas— con el estado activado/desactivado exacto de cada bloque. Funciona sea cual sea el orden en que el DAW restaura el estado y prepara el audio, y con el editor cerrado.
- **Sin chasquidos ni ruido.** El arranque, la restauración de sesión, cargar o sustituir un NAM, cargar un NAM de pedal, preparar o reinicializar el audio y los cambios de frecuencia de muestreo o de tamaño de búfer entran con fundido desde silencio. Al pasar de un NAM a otro, la cadena hace fundido de salida, instala la captura nueva (ya precalentada) y vuelve con fundido de entrada, así que la onda nunca se corta.
- **Salida del plugin siempre estéreo.** En una pista mono en STEREO, las dos cadenas reciben la misma entrada, así que una guitarra mueve dos equipos; L alimenta la salida izquierda y R la derecha. INPUT GAIN es independiente para L y R.
- **Enlaces de efectos L/R.** En STEREO, un icono de cadena enlaza un efecto de L con el mismo efecto de R: una edición cambia ambos, y cada bloque conserva su interruptor y su posición.
- **Selector de visualización con el ojo.** El cuerpo del bloque lo activa o lo pone en bypass; el ojo de cada bloque elige qué bloque describen los controles compartidos y los navegadores. Un bloque desactivado no se puede visualizar.
- **Biblioteca TONE3000 más rápida y completa.** Seleccionar un tone lo carga al instante en el bloque NAM actual (alrededor de un segundo hasta que suena; inmediato si ya lo habías descargado). **RESTORE PREVIOUS MODEL** devuelve la captura que tenía el bloque antes. Las capturas A2 ya se cargan desde todas las listas, los tones que solo tienen IR se marcan, y el buscador del catálogo completo se cierra solo al elegir un tone.
- **Cierre limpio en los DAW.** Cerrar un proyecto que contiene el plugin ya no deja el proceso del DAW en marcha.
- **Apoya el proyecto** desde la ventana de ajustes: **[ko-fi.com/bchosoft](https://ko-fi.com/bchosoft)**.
- **Manuales reescritos**, en inglés y español, con cada control documentado y capturas de pantalla.

### Compatibilidad

| Plataforma | Standalone | Plugin |
| --- | --- | --- |
| Windows 10/11 x64 | `.exe` portable (ASIO, Windows Audio, DirectSound) | VST3 |
| macOS 11+ Apple Silicon (`arm64`) | `.app` | VST3 y AU |
| macOS 11+ Intel (`x86_64`) | `.app` | VST3 y AU |
| Linux x86_64 | AppImage | VST3 |

Usa el paquete de plugin que coincida con la arquitectura de tu DAW. No se incluye AAX. Las versiones de macOS tienen firma ad-hoc y no están notarizadas por Apple.

### Standalone

- Su propio **Audio Setup**: driver (incluido ASIO en Windows), interfaz, canales activos, frecuencia de muestreo y tamaño de búfer.
- **Cuatro rutas a salidas físicas**: MAIN (sonido final), PRE (BLOCK NAM 2 antes de tonos, efectos y pantalla), DI (entrada sin tocar) y WET (después de la pantalla).
- **DUAL MONO / SPLIT L/R** en STEREO: una guitarra a las dos cadenas, o entrada 1 a L y entrada 2 a R. Los selectores de ruta L/R están a la derecha de las dos filas del rack, sin solaparse con el conmutador de entrada.
- **Recuerda la última sesión** al cerrar con normalidad: las dos rutas, capturas, IR, orden de bloques, bypass, enlaces, acabado, dispositivo y ruteo. El primer arranque es seguro: MONO y sin nada cargado.
- **Input Cali**: calibración automática a partir de la referencia en dBu de tu interfaz y de los metadatos `input_level_dbu` de la captura.
- Once acabados del panel frontal, conos animados que siguen el nivel real de salida y comprobación de actualizaciones.

### Plugin VST3 / AU

- Efecto de audio con **salida estéreo en pistas mono y estéreo**. MONO copia la ruta izquierda a las dos salidas; STEREO envía L a la salida izquierda y R a la derecha.
- El proyecto del DAW guarda las dos rutas, todos los controles, las referencias a archivos, el orden del rack, algoritmos, parámetros, bypass y enlaces L/R. Las sesiones se restauran en el motor como se describe arriba.
- Parámetros automatizables por ruta: ganancia de entrada, puerta, tonos (principales y de NAM 1), máster, IR blend, volumen de pantalla, ganancia de salida, encendido, calibración de entrada y afinador, además del conmutador global MONO/STEREO.
- Usa el dispositivo de audio del DAW; siempre con el acabado Astra / Obsidian.

### Capturas, NAM de pedal e IR

- **BLOCK NAM 2** (amplificador) y **BLOCK NAM 1** (pedal o previo) por ruta, cada uno con su carpeta, su lista y su opción de búsqueda profunda. NAM A1, A2 Standard y A2 Nano se detectan automáticamente. BLOCK NAM 1 tiene sus propios BASS / MID / TREBLE / PRESENCE.
- Carga desde **BROWSE LOCAL**, la lista, **TONE3000**, doble clic en el bloque, o arrastrando y soltando sobre la lista o el bloque.
- Las **IR de pantalla** (`.wav`, mono o estéreo, hasta 8192 muestras) se remuestrean a la frecuencia del dispositivo y **nunca se normalizan**. **IR BLEND** mezcla seco y pantalla; **IR VOL** ajusta la rama de pantalla de -24 a 0 dB (por defecto -12 dB).
- Pasa el ratón por un bloque NAM o una fila de la lista para ver la **ficha de la captura**: metadatos y carátula.

### Rack y efectos

Once bloques por ruta en orden de proceso, reordenables libremente alrededor de las anclas BLOCK NAM 2 e IR. **Clic en el cuerpo del bloque para activarlo o ponerlo en bypass; clic en el ojo para visualizarlo; doble clic para abrir su editor o su selector de archivo.** Compresor, octavador, transpositor, chorus, flanger, phaser, delay y reverb, cada uno con **tres algoritmos y seis parámetros en unidades reales**; los cambios se suavizan y la realimentación está acotada.

### Presets portables `.bnpp`

Un preset incrusta sus capturas e IR (verificadas con SHA-256) junto con el orden del rack, algoritmos, parámetros, bypass y controles. Los presets del standalone contienen las dos rutas y los enlaces L/R; los del plugin, la ruta seleccionada. El dispositivo de audio y el ruteo quedan fuera a propósito, para que los presets viajen entre ordenadores.

### TONE3000 y WebView2

Conecta tu cuenta de TONE3000 una vez; el reproductor guarda un token de refresco cifrado y no vuelve a necesitar un navegador en ese ordenador. Navega por **TRENDING, LATEST, FAVOURITES, DOWNLOADED y MINE**, preescucha seleccionando, o abre **SEARCH FULL CATALOGUE**. En Windows las páginas integradas usan **Microsoft WebView2**, que se detecta directamente (también dentro de los DAW, con una carpeta de datos por usuario con permisos de escritura). Si falta, puedes abrir la página oficial de descarga de Microsoft, usar tu navegador externo o cancelar: **nunca se instala nada automáticamente**, y el audio local no necesita WebView2. macOS usa WKWebView; Linux, el navegador del sistema.

### Instalación

**Standalone**: descomprime el ZIP y mantén juntos sus archivos.

- Windows: ejecuta `Bcho NAM Player.exe`; instala el driver ASIO de tu interfaz para la latencia más baja.
- macOS: abre `Bcho NAM Player.app` (clic derecho → **Abrir** la primera vez si Gatekeeper lo pide).
- Linux: da permiso con `chmod +x` al AppImage y ejecútalo.

**Plugin**: cierra el DAW, copia el **paquete completo**, reinicia y vuelve a escanear.

| Sistema | Copiar en |
| --- | --- |
| Windows VST3 | `C:\Program Files\Common Files\VST3\Bcho NAM Player.vst3` |
| macOS VST3 | `~/Library/Audio/Plug-Ins/VST3/Bcho NAM Player.vst3` |
| macOS AU | `~/Library/Audio/Plug-Ins/Components/Bcho NAM Player.component` |
| Linux VST3 | `~/.vst3/Bcho NAM Player.vst3` |

### El standalone en cinco pasos

1. Engranaje → **AUDIO SETUP**: elige driver, interfaz, canal de entrada, frecuencia y búfer, y comprueba que **MAIN** apunta a tus monitores.
2. **BROWSE LOCAL** (o **TONE3000**) para cargar una captura de amplificador en BLOCK NAM 2.
3. **BROWSE IR** para cargar una pantalla (sáltatelo si tu captura ya la incluye).
4. Ajusta **INPUT GAIN** mirando el vúmetro de entrada y después **MASTER VOL** y **OUTPUT GAIN**.
5. Pulsa los bloques de efecto para añadirlos; doble clic para editarlos.

Empieza con un nivel de escucha bajo. Con todos los bloques en bypass, pasa la señal seca.

### Descargas

Todos los archivos de esta versión: **[Bcho NAM Player v1.7.5](https://github.com/bchosoft/Bcho_NAM_Player/releases/tag/v1.7.5)**

| Paquete | Archivo |
| --- | --- |
| Windows standalone | [BchoNAMPlayer-v1.7.5-Windows-x64-Standalone.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-Windows-x64-Standalone.zip) |
| Windows VST3 | [BchoNAMPlayer-v1.7.5-Windows-x64-VST3.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-Windows-x64-VST3.zip) |
| macOS Apple Silicon standalone | [BchoNAMPlayer-v1.7.5-macOS-arm64-Standalone.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-arm64-Standalone.zip) |
| macOS Apple Silicon VST3 + AU | [BchoNAMPlayer-v1.7.5-macOS-arm64-Plugins.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-arm64-Plugins.zip) |
| macOS Intel standalone | [BchoNAMPlayer-v1.7.5-macOS-x86_64-Standalone.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-x86_64-Standalone.zip) |
| macOS Intel VST3 + AU | [BchoNAMPlayer-v1.7.5-macOS-x86_64-Plugins.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-macOS-x86_64-Plugins.zip) |
| Linux standalone (AppImage) | [BchoNAMPlayer-v1.7.5-Linux-x86_64-Standalone.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-Linux-x86_64-Standalone.zip) |
| Linux VST3 | [BchoNAMPlayer-v1.7.5-Linux-x86_64-VST3.zip](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/BchoNAMPlayer-v1.7.5-Linux-x86_64-VST3.zip) |
| Sumas de verificación | [SHA256SUMS.txt](https://github.com/bchosoft/Bcho_NAM_Player/releases/download/v1.7.5/SHA256SUMS.txt) |

Cada ZIP incluye su manual PDF en inglés y español en la carpeta `manuals`. Los manuales también están en línea: [standalone](docs/USER_MANUAL.es.md) · [plugin](docs/PLUGIN_MANUAL.es.md), y en PDF en [docs/manuals](docs/manuals).

### Apoya el proyecto

Bcho NAM Player es gratuito. Si te resulta útil, puedes apoyarlo en **[ko-fi.com/bchosoft](https://ko-fi.com/bchosoft)**, también accesible desde **SUPPORT PROJECT ON KO-FI** en los ajustes del standalone y **OPEN KO-FI** en los ajustes del plugin.

### Créditos, licencias e integridad

Bcho NAM Player, de **Bcho Soft**. Está construido con [JUCE 8.0.12](https://github.com/juce-framework/JUCE/tree/8.0.12) y [NeuralAmpModelerCore 0.5.4](https://github.com/sdatkinson/NeuralAmpModelerCore/tree/v0.5.4) (con Eigen y JSON for Modern C++); consulta [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). Verifica las descargas con `SHA256SUMS.txt`.

Este repositorio público contiene documentación y las descargas de cada versión, **no el código fuente de la aplicación**; los archivos automáticos "Source code" de GitHub solo contienen esta documentación. Las capturas NAM y las respuestas impulsionales tienen sus propias licencias: compartir presets no otorga derechos sobre recursos de terceros.
