# Bcho NAM Player

[Español](README.es.md)

![Bcho NAM Player](docs/Caratula_BNAMP.png)

## Español

Bcho NAM Player es un procesador de guitarra standalone y portable desarrollado en C++20 con JUCE 8 y Neural Amp Modeler Core. Combina modelos NAM A1/A2, respuestas impulsionales, efectos de estudio, enrutamiento flexible, afinador estable y una interfaz fotorrealista Bcho.

### Descarga e instalación

Descarga la [última release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest). Incluye paquetes independientes para Windows x64, Linux x86_64, macOS Intel (`x86_64`) y macOS Apple Silicon (`arm64`). Conserva juntos todos los archivos de cada ZIP. Cada paquete incluye dos modelos NAM de demostración en `Models`; las IR no se incluyen inicialmente.

En Windows ejecuta `BchoNAMPlayer.exe` y usa **AUDIO SETUP** para elegir interfaz, ASIO/WASAPI, entradas, salidas, frecuencia, buffer y enrutamiento. En macOS abre `BchoNAMPlayer.app`; los paquetes no están firmados ni notarizados. En Linux ejecuta el AppImage después de darle permiso de ejecución.

### Funciones

- Detección automática de NAM A1/A2.
- Cadena arrastrable con COMP, DELAY, CHORUS, FLANGER, PHASER, REVERB, OCTAVER y PITCH.
- Segundo NAM opcional para overdrive/distorsión.
- Gate profesional, tonestack de cuatro bandas, convolución IR y mezcla dry/IR.
- Afinador sobre la señal DI y afinaciones alternativas.
- Salidas MAIN, PRE, DI y WET en el standalone.
- Presets portables `.bnpp` con NAM, IR, orden de efectos y ajustes.
- Listas NAM e IR iguales, con cuatro filas visibles, scroll, flechas de navegación y drag-and-drop.

La ruta MAIN por defecto es neutra; PRE entrega el NAM sin procesamiento del player y DI entrega la señal limpia de entrada. `SHA256SUMS.txt` permite verificar los ZIP.

Consulta el [manual completo en español](docs/USER_MANUAL.es.md) o el [manual completo en inglés](docs/USER_MANUAL.en.md).

## English

Bcho NAM Player is a portable standalone guitar processor built with C++20, JUCE 8 and Neural Amp Modeler Core. It combines NAM A1/A2 model playback, cabinet IRs, studio-oriented effects, flexible routing, a stable tuner and a photorealistic Bcho amplifier interface.

## Download

Download the current packages from [Latest Release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest):

- **Windows x64:** portable ZIP with `BchoNAMPlayer.exe`, ASIO/WASAPI support and all runtime resources.
- **macOS Apple Silicon:** ZIP for `arm64` Macs (M1/M2/M3 and newer).
- **macOS Intel:** ZIP for `x86_64` Macs.
- **Linux x86_64:** ZIP containing a portable AppImage.
- `SHA256SUMS.txt` lets you verify every downloaded ZIP.

Keep the complete contents of each ZIP together. Two demonstration `.nam` models are included in `Models`; add more with **BROWSE NAM** or drag-and-drop. IRs are intentionally not bundled and can be loaded with **BROWSE IR** or drag-and-drop.

## Highlights

- Automatic NAM A1/A2 architecture detection.
- Movable COMP, DELAY, CHORUS, FLANGER, PHASER, REVERB, OCTAVER and PITCH blocks.
- Optional second NAM model as an overdrive/distortion pedal.
- Drag-and-drop routing before PREAMP, in the FX loop/pre-IR position, or after IR.
- Professional gate, four-band tone stack, cabinet IR convolution and dry/IR blend.
- Untouched DI tuner with alternate tunings.
- MAIN, PRE, DI and WET output routes in the standalone Audio Setup panel.
- Portable `.bnpp` presets embedding the selected NAM model, optional NAM pedal, IR, effect order and all settings.
- Settings from the gear icon: temporary skin preview with explicit Apply, installed version, and manual or startup update checks.
- Equal four-row NAM/IR browsers with up/down folder navigation and drag-and-drop loading.

## Installation

### Windows

Extract the ZIP to a writable folder and run `BchoNAMPlayer.exe`. Open **AUDIO SETUP** to choose the audio system, interface, enabled channels, sample rate, buffer and output routing. For ASIO, install the official driver supplied by your audio-interface manufacturer.

### macOS

Extract the ZIP and open `BchoNAMPlayer.app`. The macOS packages are unsigned and not notarized; on first launch, right-click the app and choose **Open** if Gatekeeper asks for confirmation.

### Linux

Extract the ZIP, make the AppImage executable if required, then launch it:

```bash
chmod +x BchoNAMPlayer-*.AppImage
./BchoNAMPlayer-*.AppImage
```

ALSA/JACK availability and real-time audio permissions depend on the Linux distribution and user configuration.

## Signal and output routing

The normal MAIN path is fully processed and is neutral at its default control values. PRE always carries the main NAM result without player processing; DI carries the untouched interface input; WET is useful for recording a dedicated processed branch. Audio-device settings remain local to the standalone application and are not stored inside `.bnpp` presets.

See the [complete Spanish user manual](docs/USER_MANUAL.es.md) or the [complete English user manual](docs/USER_MANUAL.en.md).

## Notes

- Version: 1.0.0
- Windows: x64, Windows 10/11.
- macOS: Apple Silicon `arm64` or Intel `x86_64`, macOS 11 or newer.
- Linux: x86_64 AppImage.
- Bcho NAM Player does not distribute third-party NAM captures. Respect the licence attached to every model and IR you use.

See [third-party notices](THIRD_PARTY_NOTICES.md) for framework and dependency licensing information.
