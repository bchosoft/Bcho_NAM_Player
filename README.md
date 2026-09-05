# Bcho NAM Player 1.6.0

[Español](README.es.md) | [Latest release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest) | [English manual](docs/USER_MANUAL.en.md)

![Bcho NAM Player 1.6.0](docs/Caratula_BNAMP.png)

Bcho NAM Player is a portable standalone guitar processor for Windows, macOS and Linux. It combines Neural Amp Modeler playback, cabinet IRs, a reorderable effects rack, automatic input calibration, a DI tuner, portable presets, flexible output routing and a responsive photorealistic interface.

## What is new in 1.6.0

- Settings and Audio I/O dialogs now scale proportionally to the available screen area, including their controls, margins and typography, so the lower routing and calibration sections remain visible on laptop resolutions such as 1366 x 768.
- Completely redesigned 1537 x 1023 front panel with proportional controls and typography.
- Responsive resizing down to 50 percent of the native size.
- Separate, larger NAM and IR browsers with four visible rows, scrollbars and navigation arrows.
- Symmetrical colour LED input/output meters and a cleaner rack/tuner layout.
- Visual speaker-cone movement driven by the real final output level. It changes only the graphics and never the sound.
- Eleven geometry-locked skins with English names: Astra / Obsidian, Tribal / Etched Titanium, Skulls / Bone & Carbon, Hippie / Sunset Paisley, Graffiti / Electric Ink, Purple Velvet / Amethyst, Stainless Steel / Precision, Ripped Black Denim / Roadworn, Blue Denim / Indigo, Spiderwebs / Black Widow and Classic Black / Levant Tolex.
- Coordinated exposed-material panels, screen plates, metal corners and lower rack feet preserve the physical stacking of rack, head and cabinet.
- Independent vertical IR Cabinet Volume fader with aligned dB scale, plus a full-window rock-stage backstage background and per-skin control finishes.
- Polished stainless-steel Bcho cabinet logo.
- Anti-click startup restoration and smooth NAM/IR changes.

## Download

The [latest release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest) provides:

- `BchoNAMPlayer-v1.6.0-Windows-x64.zip`
- `BchoNAMPlayer-v1.6.0-macOS-arm64.zip`
- `BchoNAMPlayer-v1.6.0-macOS-x86_64.zip`
- `BchoNAMPlayer-v1.6.0-Linux-x86_64.zip`
- English and Spanish PDF manuals.
- `SHA256SUMS.txt` for integrity verification.

Every ZIP is self-contained. Keep all included files and folders together. Two demonstration NAM models are supplied in `Models`; no IR is bundled, so the IR block initially starts bypassed.

## Main features

- Automatic NAM A1, A2 Standard and A2 Nano detection.
- Two independent generic slots, **BLOCK NAM 1** and **BLOCK NAM 2**, each accepting any compatible `.nam` model.
- Reorderable COMP, OCT, PITCH, BLOCK NAM 1, CHOR, FLANG, PHASE, DELAY and REVERB blocks around the BLOCK NAM 2 and IR anchors.
- Three types and six advanced parameters per conventional effect.
- Individual-file, folder and drag-and-drop loading for both NAM blocks and IR.
- Clear **NAM file not found** and **IR not found** messages.
- TONE3000 model browser.
- Cabinet IR convolution without normalization; clicking the selected IR again deselects it.
- Professional gate, Bass, Mid, Treble, Presence, Master Volume, IR Blend and independent IR Cabinet Volume.
- Stable tuner that reads untouched DI and supports alternate tunings.
- MAIN, PRE, DI and WET output routes.
- Self-contained `.bnpp` presets with embedded audio resources and verified hashes.
- Safe single-click bypass and separate double-click editing/loading.

## Quick installation

### Windows

Extract the Windows ZIP to a writable folder and run `BchoNAMPlayer.exe`. Open the gear, choose **AUDIO SETUP**, then select ASIO/WASAPI, your interface, active channels, sample rate, buffer and output route. Install the manufacturer's ASIO driver when available.

### macOS

Choose the ZIP matching Apple Silicon (`arm64`) or Intel (`x86_64`), extract it and open `BchoNAMPlayer.app`. The app is ad-hoc signed but not notarized. On first launch, right-click it and select **Open** if Gatekeeper requests confirmation.

### Linux

Extract the ZIP and launch its x86_64 AppImage. If required:

```bash
chmod +x BchoNAMPlayer-*.AppImage
./BchoNAMPlayer-*.AppImage
```

## Loading NAM models and IRs

**BROWSE LOCAL** accepts a `.nam` file or folder for the active NAM tab. BLOCK NAM 1 and BLOCK NAM 2 retain independent folders, lists and selections. Optional **DEEP SEARCH** includes subfolders and is disabled each time the browser opens. Folder selection automatically loads the first model. **BROWSE IR** accepts a suitable `.wav` response or folder. Drag-and-drop works on both NAM tabs/lists and on the BLOCK NAM 1, BLOCK NAM 2 and IR rack blocks.

NAM and IR transitions use output fades to prevent clicks. IRs are resampled to the active device rate without normalizing their original gain. The vertical **IR Cabinet Volume** fader provides independent wet-cabinet gain from -24 dB to 0 dB before IR Blend and defaults to -12 dB. Clicking the active IR entry again clears the selection and bypasses the block.

## Input Cali

Set the interface reference in **Settings > Audio Setup > Interface Input Reference / 0 dBFS Peak**. Input Cali subtracts the NAM input reference from the interface reference. It prefers the model's `input_level_dbu` metadata and otherwise assumes +12 dBu; the correction is limited to -24/+24 dB. Use +10 dBu for a PreSonus Studio 24c. A green LED indicates that calibration is active.

## Rack, presets and settings

Drag rack blocks to place effects before the amp, in the loop/pre-IR section or after the cabinet. A single click changes bypass; a double-click opens the editor or model loader without producing a false toggle.

**SAVE .BNPP** stores both NAM block models, optional IR, effect order, algorithms, bypass states and controls in one portable file. Audio-device settings remain local to the computer.

The gear contains Audio Setup, skin preview/application, version information and manual or startup update checks. A preview becomes permanent only after **APPLY SKIN**.

See the [complete English manual](docs/USER_MANUAL.en.md), the [Spanish manual](docs/USER_MANUAL.es.md) and [third-party notices](THIRD_PARTY_NOTICES.md).

The public repository distributes documentation and compiled packages only. The source code remains in the private development repository.
