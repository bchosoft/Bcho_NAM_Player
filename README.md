# Bcho NAM Player 1.7.0

[Español](README.es.md) | [Downloads](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest) | [Standalone manual](docs/USER_MANUAL.en.md) | [Plugin manual](docs/PLUGIN_MANUAL.en.md)

![Bcho NAM Player 1.7.0](docs/Caratula_BNAMP.png)

A guitar processor combining Neural Amp Modeler, cabinet IRs and effects. Standalone application and VST3 plugin, with Audio Unit (AU) on macOS.

## New in 1.7.0

- Independent L/R paths, each with BLOCK NAM 1, BLOCK NAM 2, IR and effects rack.
- MONO / STEREO. Standalone DUAL MONO feeds one guitar to both chains; SPLIT L/R processes two inputs separately.
- NAM 1 L, NAM 2 L, NAM 1 R, NAM 2 R and IR L/R selectors. NAM 1 has its own tone controls.
- Two rack rows in stereo, separate NAM/IR lists and per-channel meters.
- Capture information cards with metadata and artwork when available.
- TONE3000 favourites, downloads, trending, latest, your own tones and full-catalogue search. Embedded sign-in and search share a session to avoid unnecessary repeat authentication.
- Windows WebView2 detection. If unavailable, choose an official Microsoft download, the system browser or cancel. Nothing is installed automatically.
- Standalone restores the last session, including bypass. First launch starts in MONO with every block disabled and no automatically loaded models.
- Improved IR VOL scale spacing, unclipped L/R labels and symmetrical plate screw margins.
- Improved plugin state restoration and oversized offline-rendering block handling.

## Sound and controls

Two NAM slots per path, unnormalized IRs, IR BLEND, cabinet level from -24 to 0 dB, gate, tone controls, gains and tuner. Compressor, octaver, pitch shifter, chorus, flanger, phaser, delay and reverb, each with three algorithms and six parameters.

Portable `.bnpp` presets embed resources with SHA-256 checks. Standalone presets save both paths; plugin presets save one path, while DAW projects save both. Keep original NAM/IR files available when reopening DAW projects.

Standalone adds Audio Setup, Windows ASIO, MAIN/PRE/DI/WET routing, interface-reference calibration, eleven skins, animated cones and update checks. Plugins use the DAW audio device and connections with the Astra / Obsidian finish. Standalone device setup and physical-output routing are not included in plugins.

## Packages and quick start

- Windows x64: portable standalone and VST3.
- macOS Intel (`x86_64`) and Apple Silicon (`arm64`): standalone, VST3 and AU.
- Linux x86_64: standalone AppImage and VST3.

Attached release assets show the packages actually available. Match plugin and DAW architectures. AU is macOS-only. macOS packages are ad-hoc signed, not Apple-notarized.

Extract the ZIP. For standalone, open **Bcho NAM Player**, configure AUDIO SETUP and load NAM/IR resources. For plugins, follow the installation paths in the plugin manual, rescan and insert as a DAW audio effect. Start at a low monitoring level: with all blocks disabled, dry audio passes through.

WebView2 is only needed for embedded TONE3000 on Windows, not local audio processing. macOS uses WKWebView; Linux uses the system browser. Obtain audio-interface drivers from their manufacturer.

## Documentation and integrity

ZIPs include English and Spanish standalone and plugin PDF manuals. Read the Markdown versions in [docs](docs). Verify archives against `SHA256SUMS.txt`.

The public repository contains documentation and downloads, **not the application source code**. GitHub's automatic “Source code” archives contain only the public documentation repository.

See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md). Captures and IRs have their own licences; sharing presets does not grant rights to third-party resources.
