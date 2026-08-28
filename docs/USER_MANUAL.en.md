# Bcho NAM Player — User Manual

## 1. Overview

Bcho NAM Player is a portable guitar processor for Windows, macOS and Linux. It plays Neural Amp Modeler (`.nam`) models, cabinet impulse responses (`.wav`) and a reorderable effects chain. The standalone edition also owns the audio device; the VST3 receives audio and routing from the DAW.

## 2. Quick installation

Download the package for your system from the [latest release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest) and keep every file in the ZIP together.

- Windows: run `BchoNAMPlayer.exe`.
- macOS: open `BchoNAMPlayer.app`; choose Intel or Apple Silicon.
- Linux: launch the AppImage, making it executable if needed.

NAM models and IRs are not bundled. Load your own files from the centre display. macOS packages are currently unsigned and not notarized.

## 3. Main panel

The head contains the **POWER** switch, input controls, tuner, amplifier controls and meters. The centre display shows the active model, calibrated level, output level, selected IR and load/delete controls.

Drag a knob vertically or horizontally to change it. Double-click any knob to restore its initial value: every control returns to 12 o’clock except **Gate**, which returns to 0 and disables the gate.

### Input and amplifier controls

- **POWER**: enables or mutes the main processing path.
- **Input Gain**: level entering the NAM model.
- **Input Cali (Auto)**: compensates input level when the model provides `input_level_dbu`; otherwise no correction is applied.
- **Gate**: professional noise gate. At 0 it is fully bypassed. Increasing it raises the threshold; the detector uses a smoothed envelope, attack, hold and release to avoid abrupt cuts.
- **Bass, Mid, Treble, Presence**: four-band EQ after the NAM preamp.
- **IR Blend**: mixes the un-convolved signal with the cabinet-IR signal.
- **Master Vol**: main level after the player chain.
- **Output Gain**: final output gain.

At default values, MAIN is neutral and sounds the same as PRE. PRE is an independent reference tap and is unaffected by player controls.

## 4. Tuner

Enable **TUNER**. It always analyses the clean DI signal before gate, NAM and effects. The lights show whether the note is flat, in tune or sharp; the detected note is shown below. Standard and alternate tunings are available. For stable detection, play one isolated string at a useful level and allow noise to decay between notes.

## 5. NAM models and IRs

Click the profile area in the centre display to select a `.nam` file. A1/A2 architecture is detected automatically. Loading another NAM resets the controls and switches to their defaults.

The **IR FILES** list scans `.wav` files in the `IRs` folder beside the executable. Select an IR and press **LOAD IR**. **DELETE** removes the active IR. Mono and stereo IRs are prepared for the selected audio rate.

## 6. Effects rack

The rack opens above the amplifier. Drag blocks to change their order and click a block to enable or bypass it. Double-click opens the advanced editor; it closes with **X**, Escape or a click outside.

The **PREAMP** and **IR** anchors define the electrical position. Before PREAMP is in front of the amp; between PREAMP and IR is the effects loop; after IR is post-cabinet. The tuner is always first and is intentionally not shown in the rack. **NAM FX** adds an optional second NAM model as an overdrive/distortion pedal.

Each block provides three algorithms and six parameters:

| Block | Types | Parameters |
|---|---|---|
| COMPRESSOR | Studio VCA, Optical, FET Punch | Threshold, Ratio, Attack, Release, Makeup, Mix |
| DELAY | Digital Studio, Tape Echo, Analog BBD | Time, Feedback, Mix, Tone, Mod, Level |
| CHORUS | Studio, Ensemble, Tri-Chorus | Rate, Depth, Mix, Delay, Feedback, Level |
| FLANGER | Analog, Through-Zero, Jet | Rate, Depth, Mix, Feedback, Manual, Level |
| PHASER | 4 Stage, 8 Stage, 12 Stage | Rate, Depth, Mix, Feedback, Centre, Level |
| REVERB | Studio Room, Plate, Concert Hall | Size, Damping, Mix, Width, Freeze, Level |
| OCTAVER | Poly Clean, Classic Mono, Organ | Oct Down, Oct Up, Dry, Tone, Tracking, Level |
| PITCH SHIFTER | Studio, Low Latency, Vintage | Semitones, Mix, Window, Feedback, Fine, Level |

Values are displayed with units in each block editor. Bypass, parameter and type changes are smoothed to prevent clicks; delay effects use interpolation and feedback is bounded for stable processing.

## 7. AUDIO SETUP — standalone only

Open **AUDIO SETUP** to select the audio system and driver, including ASIO on Windows; interface; active inputs and outputs; sample rate; buffer size; manufacturer control panel; and output routing.

Available taps are **MAIN** (processed), **PRE** (NAM without player controls or effects), **DI** (clean input) and **WET** (processed post-cab branch). MAIN defaults to outputs 1/2 when enabled. The last device and routing configuration is restored on the next launch. The VST3 does not show this panel because the DAW owns the audio device.

## 8. `.bnpp` presets

**SAVE .BNPP** creates a self-contained portable preset containing the XML state, main NAM, optional NAM pedal, IR, rack order, types, bypass states and all controls. **LOAD .BNPP** extracts its resources to a safe cache and restores the state. Audio-device settings are excluded so presets remain portable across computers and DAWs.

## 9. State and troubleshooting

The application restores the last NAM, IR and preset used. If there is no sound, check POWER, the selected device, active inputs, buffer size and INPUT VU level. If a NAM is silent, verify the file and its licence. For low latency, start with a small ASIO buffer and increase it if clicks occur.

