# Bcho NAM Player - User Manual

## 1. Overview

Bcho NAM Player 1.5 is a portable standalone guitar processor for Windows, macOS and Linux. It plays Neural Amp Modeler (`.nam`) captures, cabinet impulse responses (`.wav`) and a reorderable chain of studio effects. The standalone application owns the audio device, routing and latency configuration.

The initial window uses the native 1537 x 1023 interface size whenever the available screen area permits it and opens centred. The complete design is responsive: furniture, controls, lists, meters and text scale together. The window cannot be reduced below 50 percent of its native size, preventing controls or labels from leaving their intended areas.

## 2. Installation

Download the package for your system from the [latest public release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest), extract it and keep every included file and folder together.

- **Windows x64**: run `BchoNAMPlayer.exe`. Install the official ASIO driver supplied by the audio-interface manufacturer when available.
- **macOS Apple Silicon**: use the `arm64` ZIP and open `BchoNAMPlayer.app`.
- **macOS Intel**: use the `x86_64` ZIP and open `BchoNAMPlayer.app`.
- **Linux x86_64**: run the included AppImage. Use `chmod +x BchoNAMPlayer-*.AppImage` if execution permission is missing.

The macOS applications use ad-hoc signing but are not notarized. On first launch, right-click the app and choose **Open** if Gatekeeper asks for confirmation.

Two demonstration NAM models are included in `Models`. No cabinet IR is bundled. The IR block therefore starts bypassed until a response is loaded.

## 3. Front panel

The upper rack contains preset buttons, reorderable processing blocks, the tuner button/display and tuning selector. The amplifier head contains seven main controls, symmetrical vertical LED meters, input/output gain controls, Input Cali, separate NAM and IR browsers, Settings and the red power switch. The speaker cabinet contains the Bcho logo and two animated cones.

### Knob operation

Drag a knob vertically or horizontally to change its value. Its exact value appears below it. Double-click to restore the default: normal controls return to 12 o'clock and Gate returns fully left to **OFF**.

### Main controls

- **POWER**: enables or mutes the main processing path. The switch is illuminated red while on.
- **INPUT GAIN**: adjusts the signal entering the main NAM model.
- **GATE**: professional noise gate. At 0 it is completely bypassed. Increasing it raises the threshold; attack, hold and release smoothing prevent abrupt cuts.
- **BASS, MID, TREBLE, PRESENCE**: four-band tone shaping after the main NAM stage.
- **MASTER VOL**: main post-processing level.
- **IR BLEND**: mixes the signal without cabinet convolution and the IR-processed signal.
- **OUTPUT GAIN**: final output level.
- **INPUT VU / OUTPUT VU**: symmetrical colour LED meters for incoming and final processed levels.

The player applies a short protective fade when restoring the startup state and when loading a new NAM or IR. This prevents the loading transition from producing a click or crackle.

## 4. Animated speaker cones

Both speaker cones react visually to the real final output RMS level. Louder playing and higher Master Volume or Output Gain produce a greater excursion; silence and POWER off return the cones smoothly to rest.

Only the cone surfaces move. Metal rings, screws, grille, cabinet and Bcho logo remain fixed. Animation is calculated at 60 frames per second on the interface thread and never changes, delays or feeds data back into the audio signal.

## 5. Loading NAM models

Use **BROWSE NAM** to select either one `.nam` file or a folder. When a folder is selected, all NAM files in that folder are added to the list and the first is selected automatically. If none is found, the application displays **NAM file not found**.

The NAM list shows four rows at the native size, adds a scrollbar when required and uses the arrow buttons to select the previous or next entry. An arrow is disabled at its corresponding end of the list. **TONE3000** opens the online model browser and loads a downloaded model with its descriptive name.

The application automatically identifies NAM A1, A2 Standard and A2 Nano models. There is no manual architecture switch. Loading a new main model resets the front-panel and rack settings to safe defaults, activates the NAM AMP block and uses an anti-click output fade.

### Drag-and-drop

Drop a `.nam` file or folder on the NAM list or the **NAM AMP** rack block. The same folder scanning and missing-file messages used by BROWSE NAM are applied.

## 6. NAM STOMP

**NAM STOMP** loads a second `.nam` as an overdrive, distortion or other pedal capture. Use **+ NAM STOMP**, double-click the NAM STOMP block, or drop a file/folder onto that block. The source can be local or TONE3000. Loading a valid model activates the block.

NAM AMP and NAM STOMP are independent. Bypassing NAM AMP lets the remaining effects process clean DI; bypassing NAM STOMP removes only the pedal capture.

## 7. Loading cabinet IRs

Use **BROWSE IR** to select a `.wav` file or folder. Folder selection filters short WAV files suitable for impulse-response use, lists the valid responses and selects the first. If none is found, the application displays **IR not found**.

The IR list has the same size and navigation behaviour as the NAM list. Drop a WAV or folder on the IR list or the **IR** rack block to use the same loader. Mono and stereo responses are prepared for the active device sample rate. Their original gain is preserved: Bcho NAM Player does not normalize IRs.

Click the selected IR entry again to deselect it. This clears the active response and bypasses the IR block. Loading or changing a response uses an anti-click transition.

## 8. Rack and signal order

Drag blocks horizontally to reorder them. **NAM AMP** and **IR** act as electrical anchors:

- Before **NAM AMP**: pedals in front of the amplifier.
- Between **NAM AMP** and **IR**: effects loop or pre-cabinet processing.
- After **IR**: post-cabinet processing.

The tuner is always first on untouched DI and is not part of the draggable order. A single click enables or bypasses a block. A double-click opens its editor or loader without interpreting the first click as a bypass command.

Each conventional effect provides three algorithms and six parameters:

| Block | Algorithms | Parameters |
|---|---|---|
| COMP | Studio VCA, Optical, FET Punch | Threshold, Ratio, Attack, Release, Makeup, Mix |
| DELAY | Digital Studio, Tape Echo, Analog BBD | Time, Feedback, Mix, Tone, Mod, Level |
| CHOR | Studio, Ensemble, Tri-Chorus | Rate, Depth, Mix, Delay, Feedback, Level |
| FLANG | Analog, Through-Zero, Jet | Rate, Depth, Mix, Feedback, Manual, Level |
| PHASE | 4 Stage, 8 Stage, 12 Stage | Rate, Depth, Mix, Feedback, Centre, Level |
| REVERB | Studio Room, Plate, Concert Hall | Size, Damping, Mix, Width, Freeze, Level |
| OCT | Poly Clean, Classic Mono, Organ | Oct Down, Oct Up, Dry, Tone, Tracking, Level |
| PITCH | Studio, Low Latency, Vintage | Semitones, Mix, Window, Feedback, Fine, Level |

Parameter, type and bypass changes are smoothed. Delay-family reads are interpolated and feedback is bounded for stable processing.

## 9. Tuner

Press **TUNER** to enable it. The button lettering lights green and appears pressed while active. The display shows the detected note and a left/right LED indication for flat, centred or sharp pitch.

The tuner analyses untouched DI before Gate, NAM and effects. It supports approximately 65 to 700 Hz at common sample rates from 44.1 to 192 kHz. Available tuning references are Standard, Drop D, D Standard, Eb and Open G. Play one isolated string at a useful input level and allow noise to decay between notes.

## 10. Input Cali

Input Cali compensates for the relationship between the interface's maximum input level and the reference used to train the NAM model.

Set **Interface Input Reference / 0 dBFS Peak** in Audio Setup. When Input Cali is on, the application calculates:

`calibration gain in dB = interface reference dBu - NAM input reference dBu`

- If the NAM contains `input_level_dbu`, that metadata is used.
- If it has no metadata, the likely standard NAM reference of +12 dBu is used.
- The correction is limited to -24/+24 dB.
- For a PreSonus Studio 24c, enter +10 dBu.
- The small LED beside INPUT CALI is green while enabled and dark while disabled.

Input Cali changes gain before the NAM; it does not rewrite or normalize the model. If an interface offers several gain modes, use the dBu value corresponding to the physical input mode in use.

## 11. Audio Setup and routing

Open the gear and choose **AUDIO SETUP**. The panel controls:

- audio system and driver, including ASIO on Windows;
- input/output interface;
- active input and output channels;
- sample rate and buffer size;
- manufacturer control panel when supplied by the driver;
- interface input reference for Input Cali;
- physical destinations for MAIN, PRE, DI and WET.

| Route | Signal | Typical use |
|---|---|---|
| MAIN | Complete processed player output | Monitoring or recording the final sound |
| PRE | Main NAM reference before player tone/effects/cab | Re-amping or comparison |
| DI | Untouched interface input | Recording a clean safety track |
| WET | Processed post-cabinet branch | Separate processed recording path |

MAIN normally uses outputs 1/2. Set an unused route to disabled to prevent duplicate output. The selected device, channels, rate, buffer, interface reference and routes are restored on the next launch.

## 12. Portable `.bnpp` presets

**SAVE .BNPP** creates one self-contained preset containing:

- main NAM model;
- optional NAM STOMP model;
- optional selected IR;
- rack order, algorithms, advanced parameters and bypass states;
- front-panel knob, switch and tuner settings.

Embedded resources are checked with SHA-256 when loaded. **LOAD .BNPP** extracts them to the application cache and restores the saved sound. Audio-device, interface and physical output settings are intentionally excluded so the preset can move between computers.

A main NAM must be loaded before a `.bnpp` can be saved.

## 13. Settings, skins and updates

Press the gear to open **APPLICATION SETTINGS**. It contains Audio Setup, skin selection, installed version, manual update checking and automatic startup checking.

Available skins are **Default**, **Tribal**, **Skulls**, **Hippie**, **Graffiti**, **Purple Velvet**, **Stainless Steel**, **Ripped Black Denim**, **Blue Denim** and **Spiderwebs**. Every skin has identical control geometry. Selecting one previews it immediately; it becomes permanent only after pressing **APPLY SKIN**. Closing without applying restores the previous skin.

**CHECK FOR UPDATES** compares the installed version with the latest public release. Startup checks can be enabled or disabled. Update checking only reports availability and never replaces files, models or presets without the user opening the download page.

## 14. State and file locations

The application restores the last selected NAM, IR, preset values, skin, audio device and routing. Writable portable folders keep state beside the executable. macOS bundles and read-only Linux AppImages use the per-user `Bcho/BchoNAMPlayer` application-data directory.

Keep the two demonstration files in `Models` if they should remain available. User IRs are not included in the distributed package.

## 15. Troubleshooting

- **No sound**: check POWER, MAIN routing, the active interface input/output, INPUT VU, model selection and buffer configuration.
- **NAM AMP cannot be enabled**: load a valid NAM and wait for loading to complete; a successfully selected model activates the block automatically.
- **IR block is bypassed**: load a valid IR and make sure the selected entry has not been clicked a second time.
- **Clicks or dropouts while playing**: increase the audio buffer, use the official ASIO driver on Windows and avoid overloading the CPU with very small buffers.
- **NAM or IR folder appears empty**: confirm that it contains `.nam` files or short valid `.wav` responses directly inside the selected folder.
- **Input level does not match other NAM software**: verify the interface 0 dBFS reference and the active Input Cali state.
- **macOS refuses first launch**: right-click the app, select **Open** and approve the unsigned application.
- **Linux AppImage does not start**: grant execute permission and verify that the system provides a compatible x86_64 audio stack.

## 16. Package integrity and licences

Compare downloaded ZIP hashes with `SHA256SUMS.txt`. Bcho NAM Player includes JUCE and Neural Amp Modeler Core; their notices are in `THIRD_PARTY_NOTICES.md`. The application does not grant rights to third-party NAM captures or IR files. Follow the licence supplied by each model or response.
