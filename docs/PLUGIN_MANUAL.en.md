# Bcho NAM Player 1.7.0 - VST3 / AU Plugin Manual

## 1. Included formats

An audio-effect plugin, not a MIDI instrument. Two L/R paths, each with two NAM blocks, IR and effects rack. VST3 for Windows x64, macOS Intel/Apple Silicon and Linux x86_64. AU is macOS-only. Match the package to your DAW architecture. AAX is not included.

## 2. Installation

Close the DAW before copying. Copy the entire bundle, not only its inner binary.

- Windows: copy Bcho NAM Player.vst3 to C:/Program Files/Common Files/VST3. Administrator permission may be required.
- macOS VST3: copy Bcho NAM Player.vst3 to ~/Library/Audio/Plug-Ins/VST3.
- macOS AU: copy Bcho NAM Player.component to ~/Library/Audio/Plug-Ins/Components.
- Linux: copy Bcho NAM Player.vst3 to ~/.vst3.

Restart the DAW and rescan plugins. The effect appears as Bcho NAM Player. Use VST3 in compatible hosts or AU in an Audio Unit host such as Logic. Match the DAW process architecture: Intel x86_64 or Apple Silicon arm64. macOS builds are ad-hoc signed, not notarized. If blocked, review Privacy & Security and host instructions; do not globally disable system protection.

## 3. Your first track

Insert the plugin as an effect on a mono or stereo audio track. Select the guitar input in your DAW and enable monitoring. Start at low levels and avoid double monitoring through both the interface and DAW.

A new instance starts in MONO with all blocks disabled. Dry audio passes until processing is loaded/enabled. POWER can mute the path. Configure device, driver, sample rate and buffer in the DAW, not the plugin.

MONO processes the L path and feeds the plugin outputs. On a stereo bus, STEREO processes L and R inputs separately. For one guitar through two stereo rigs, duplicate/send it to both channels in the DAW. The standalone DUAL MONO / SPLIT L/R input switch is not present in the plugin.

## 4. Loading models and cabinets

Choose NAM 1 L or NAM 2 L; stereo also exposes NAM 1 R and NAM 2 R. Use BROWSE LOCAL or drop a compatible .nam capture. Loading activates that block. NAM 1 and NAM 2 have independent tone settings.

Choose IR L or IR R and use BROWSE IR for a .wav response. No IR is bundled; source gain is not normalized. IR BLEND mixes dry and cabinet audio. IR VOL adjusts the cabinet branch from -24 to 0 dB, with a separate L/R caption and unobstructed scale. Loading activates the IR; bypass its block to compare.

Demo captures are provided in Models next to the package but are not loaded automatically. Locate them with BROWSE LOCAL. Save or consolidate resources before moving a project.

## 5. Controls and effects

INPUT GAIN and OUTPUT GAIN control levels; GATE controls the gate; MASTER VOL is the main level. BASS, MID, TREBLE and PRESENCE follow the selected NAM. IR BLEND and IR VOL follow the IR selector. Watch the input/output meters.

Each path has compressor, octaver, pitch shifter, chorus, flanger, phaser, delay and reverb. Click to enable/bypass, double-click for editing/loading and drag to reorder around the NAM 2 and IR anchors. Each conventional effect offers three algorithms and six parameters. Smoothed changes reduce abrupt transitions but do not replace sensible gain staging.

TUNER analyses DI; play one isolated string. INPUT CALI uses the engine reference and model metadata; the plugin does not expose the standalone Audio Setup interface-reference setting. For a specific interface calibration, adjust gain externally or use standalone.

## 6. Saving and automation

Save the DAW project to retain both paths, parameters, file references and rack states/order. DAW state references NAM/IR files on disk; it does NOT automatically embed them. Keep them available when reopening or moving projects.

SAVE PRESET writes a .bnpp for the selected path with NAM 1, NAM 2, IR and settings. LOAD PRESET replaces that path. Share both paths as two presets; use the DAW project to recall the full instance. Importing a two-path standalone preset uses its backwards-compatible left-path representation in the selected plugin path.

The host can automate published parameters, including gains, tone, blend, IR VOL, power, calibration, tuner and MONO/STEREO. Not every rack control is a host automation parameter: order, algorithms and internal settings are saved in state. File changes involve loading and are not continuous automation.

## 7. TONE3000 and WebView2

TONE3000 provides favourites, downloads, latest, trending and your own captures. Connect your account, then use SEARCH FULL CATALOGUE for the official picker. Embedded login and search share a session; service-side expiry can still require authentication.

On Windows, missing/unavailable WebView2 offers an official Microsoft download, external browser or cancel. No automatic installation and no Microsoft installer in the ZIP. Install from Microsoft, then reopen TONE3000. Local audio does not need WebView2. macOS uses WKWebView and Linux the external browser. Network, account and catalogue availability depend on the external service.

## 8. Differences from standalone

Plugins use Astra / Obsidian, without standalone's eleven selectable skins, device setup, physical MAIN/PRE/DI/WET output routing or dual input-mode switch. Configure routing in the DAW. A new instance does not inherit the last standalone session; saved instances restore from their host project.

## 9. Troubleshooting

- Not listed: check folder, format and architecture, then rescan.
- No audio: check track input, monitoring, POWER and DAW routes.
- One silent side: in STEREO ensure the DAW feeds both channels.
- Missing files: restore resource locations or load your .bnpp presets.
- Dropouts: increase the buffer and reduce CPU load; four NAM slots across two paths may be demanding.
- Empty TONE3000: check account/network/WebView2 or use the external browser.
- macOS host rejection: review host validation and system permissions. Ad-hoc signing is not notarization.

## 10. Integrity and licences

Check ZIP hashes against SHA256SUMS.txt and read THIRD_PARTY_NOTICES.md. Respect the licences of captures and IRs shared in presets. These manuals do not imply certification in every DAW; host/system combinations need practical validation.
