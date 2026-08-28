# Bcho NAM Player

[Español](README.es.md)

![Bcho NAM Player](docs/Caratula_BNAMP.png)

Bcho NAM Player is a portable standalone guitar processor built with C++20, JUCE 8 and Neural Amp Modeler Core. It combines NAM A1/A2 model playback, cabinet IRs, studio-oriented effects, flexible routing, a stable tuner and a photorealistic Bcho amplifier interface.

## Download

Download the current packages from [Latest Release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest):

- **Windows x64:** portable ZIP with `BchoNAMPlayer.exe`, ASIO/WASAPI support and all runtime resources.
- **macOS Universal 2:** ZIP containing `BchoNAMPlayer.app` for Apple Silicon and Intel Macs.
- **Linux x86_64:** ZIP containing a portable AppImage.
- `SHA256SUMS.txt` lets you verify every downloaded ZIP.

Keep the complete contents of each ZIP together. NAM models are not bundled; load your own `.nam` files from the centre display.

## Highlights

- Automatic NAM A1/A2 architecture detection.
- Movable COMP, DELAY, CHORUS, FLANGER, PHASER, REVERB, OCTAVER and PITCH blocks.
- Optional second NAM model as an overdrive/distortion pedal.
- Drag-and-drop routing before PREAMP, in the FX loop/pre-IR position, or after IR.
- Professional gate, four-band tone stack, cabinet IR convolution and dry/IR blend.
- Untouched DI tuner with alternate tunings.
- MAIN, PRE, DI and WET output routes in the standalone Audio Setup panel.
- Portable `.bnpp` presets embedding the selected NAM model, optional NAM pedal, IR, effect order and all settings.

## Installation

### Windows

Extract the ZIP to a writable folder and run `BchoNAMPlayer.exe`. Open **AUDIO SETUP** to choose the audio system, interface, enabled channels, sample rate, buffer and output routing. For ASIO, install the official driver supplied by your audio-interface manufacturer.

### macOS

Extract the ZIP and open `BchoNAMPlayer.app`. The current automated build is Universal 2 but unsigned and not notarized; on first launch, right-click the app and choose **Open** if Gatekeeper asks for confirmation.

### Linux

Extract the ZIP, make the AppImage executable if required, then launch it:

```bash
chmod +x BchoNAMPlayer-*.AppImage
./BchoNAMPlayer-*.AppImage
```

ALSA/JACK availability and real-time audio permissions depend on the Linux distribution and user configuration.

## Signal and output routing

The normal MAIN path is fully processed and is neutral at its default control values. PRE always carries the main NAM result without player processing; DI carries the untouched interface input; WET is useful for recording a dedicated processed branch. Audio-device settings remain local to the standalone application and are not stored inside `.bnpp` presets.

## Notes

- Version: 0.3.0
- Windows: x64, Windows 10/11.
- macOS: Universal 2, macOS 11 or newer.
- Linux: x86_64 AppImage.
- Bcho NAM Player does not distribute third-party NAM captures. Respect the licence attached to every model and IR you use.

See [third-party notices](THIRD_PARTY_NOTICES.md) for framework and dependency licensing information.

