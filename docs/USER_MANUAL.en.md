# Bcho NAM Player 1.8.0 - Standalone User Manual

Complete reference for the standalone application on Windows, macOS and Linux.
This guide covers the controls, file handling, signal paths and session behavior of version 1.8.0. For the VST3 / AU
plug-in see [PLUGIN_MANUAL.en.md](PLUGIN_MANUAL.en.md).

---

## Contents

1. [What Bcho NAM Player is](#1-what-bcho-nam-player-is)
2. [Installing and first launch](#2-installing-and-first-launch)
3. [Map of the window](#3-map-of-the-window)
4. [Quick start: sound in five steps](#4-quick-start-sound-in-five-steps)
5. [Audio Setup: device, latency and routing](#5-audio-setup-device-latency-and-routing)
6. [Signal flow](#6-signal-flow)
   - [IN / DI player and transport](#in--di-choose-the-source-standalone-only)
7. [The rack: blocks, order and the eye](#7-the-rack-blocks-order-and-the-eye)
8. [BLOCK NAM 1 and BLOCK NAM 2](#8-block-nam-1-and-block-nam-2)
9. [Cabinet impulse responses](#9-cabinet-impulse-responses)
10. [Amplifier controls, knob by knob](#10-amplifier-controls-knob-by-knob)
11. [The eight effects in full](#11-the-eight-effects-in-full)
12. [MONO and STEREO: two complete rigs](#12-mono-and-stereo-two-complete-rigs)
13. [Linking effects between L and R](#13-linking-effects-between-l-and-r)
14. [Tuner](#14-tuner)
15. [Input Cali (automatic input calibration)](#15-input-cali-automatic-input-calibration)
16. [TONE3000 inside the player](#16-tone3000-inside-the-player)
17. [Portable .bnpp presets](#17-portable-bnpp-presets)
18. [What is remembered, and where](#18-what-is-remembered-and-where)
19. [Settings, skins, updates and support](#19-settings-skins-updates-and-support)
20. [Meters and animated cones](#20-meters-and-animated-cones)
21. [Mouse and keyboard reference](#21-mouse-and-keyboard-reference)
22. [Troubleshooting](#22-troubleshooting)
23. [Technical specifications](#23-technical-specifications)
24. [Integrity, third-party code and licences](#24-integrity-third-party-code-and-licences)

---

## 1. What Bcho NAM Player is

Bcho NAM Player is a portable standalone guitar processor. It plays Neural Amp
Modeler captures (`.nam`), cabinet impulse responses (`.wav`) and a reorderable
chain of studio effects, and it owns the audio device itself: driver, channels,
sample rate, buffer size and physical output routing are configured inside the
application.

The player has **two complete and independent signal paths**, left and right.
In NORMAL, each path owns its own BLOCK NAM 1, BLOCK NAM 2, cabinet IR, effects rack,
block order, gate, tone stack, master level, IR blend, IR cabinet volume, input
and output gain, power switch, calibration and tuner. In **MONO** only the left
path is audible and the right-hand controls are hidden; in **STEREO** both run
at once. PLUS expands each path into a series lane or two parallel lanes, each limited to two NAMs and two IRs. Standalone DI playback can replace the physical input (chapter 6).

**What is in the package**

| Item | Notes |
| --- | --- |
| `Bcho NAM Player.exe` (or `.app` / AppImage) | The whole application; no installer, no runtime DLLs |
| `Models` | Two demonstration NAM captures. They are **not** loaded automatically |
| `IRs` | The folder the IR browser opens by default. No cabinet IR is bundled |
| `NAM_A2_HEAD.xml` | Appears after the first normal exit: your saved session |
| `tone3000.session` | Appears only after connecting a TONE3000 account (encrypted) |

> The window opens centred at its native 1537 x 1023 size whenever the screen
> allows it. The whole design is responsive - furniture, knobs, lists, meters and
> text scale together - and cannot be made smaller than 50 % of native size, so
> no control or legend can ever leave its plate.

---

## 2. Installing and first launch

Download the package for your system from the
[latest public release](https://github.com/bchosoft/Bcho_NAM_Player/releases/latest),
extract it, and keep every file and folder together.

| System | How to run it |
| --- | --- |
| Windows x64 | Run `Bcho NAM Player.exe`. Install your interface manufacturer's ASIO driver for the lowest latency |
| macOS Apple Silicon | Use the `arm64` ZIP, open `Bcho NAM Player.app` |
| macOS Intel | Use the `x86_64` ZIP, open `Bcho NAM Player.app` |
| Linux x86_64 | Run the AppImage; `chmod +x BchoNAMPlayer-*.AppImage` if it will not start |

macOS builds are ad-hoc signed but **not** notarized. If Gatekeeper blocks the
first launch, right-click the application and choose **Open**.

**What the first launch looks like.** The player starts in MONO, with every
block disabled, no model and no IR loaded, and the audio device set to the
system default. A completely bypassed chain passes your dry signal through - it
does not mute. Your first job is [Audio Setup](#5-audio-setup-device-latency-and-routing)
and then loading a capture.

Every later launch restores the last session you closed normally: controls, both
paths, resources, block order, effects and bypass states. The source always returns to IN and DI playback remains paused.

---

## 3. Map of the window

![The standalone in MONO with a capture, a cabinet and two effects running](manual/img/standalone-mono.jpg)

The window has three pieces of furniture, from top to bottom. The rack also holds NORMAL / PLUS and IN / DI. CONFIG DI and the gold-framed transport appear only in DI mode; PAN appears in STEREO.

**1 - The rack strip.** Preset bay on the left, the reorderable processing
blocks in the middle, the tuner button and display, the tuning selector, and on
the right the MONO / STEREO switch and the settings gear.

**2 - The amplifier head.** Input VU, INPUT GAIN and INPUT CALI on the left;
the seven main knobs and, above them, the NAM and IR selectors; the two file
browsers (NAM models on the left, IR files on the right) with the IR VOL fader
between them and the output column; Output VU, OUTPUT GAIN and the red POWER
switch on the right.

**3 - The speaker cabinet.** The Bcho logo and two cones that move with the real
output level.

![Preset bay, input-mode switch and the first rack blocks](manual/img/zone-preset-bay.jpg)

The caption under **LOAD PRESET** always names what the shared controls are
editing right now - for example `PATH R · NAM 2`, or `MONO · NAM 1`.

---

## 4. Quick start: sound in five steps

1. **Open Audio Setup.** Press the gear (top right of the rack) → **AUDIO
   SETUP**. Choose your driver and interface, pick the input your guitar is
   plugged into, set the sample rate and the buffer size, and make sure
   **MAIN / POST MASTER** points at the outputs your monitors use.
2. **Load an amp capture.** Press **BROWSE LOCAL** under NAM MODELS and pick a
   `.nam` file or a whole folder. The capture loads, BLOCK NAM 2 lights up, and
   the file appears in the list.
3. **Load a cabinet.** Press **BROWSE IR** and pick a `.wav` impulse response.
   The IR block lights up. (Skip this if your capture already includes a
   cabinet - many "amp_cab" captures do.)
4. **Set levels.** Play and watch INPUT VU: aim for the green range with the
   loudest strumming just touching yellow. Use INPUT GAIN to trim. Then set
   MASTER VOL and OUTPUT GAIN for a comfortable monitoring level.
5. **Play.** Add effects by clicking their blocks; double-click a block to open
   its editor.

> Start at a low monitoring level and avoid hearing your guitar twice - through
> the interface's own direct monitoring **and** through the player.

---

## 5. Audio Setup: device, latency and routing

Gear → **AUDIO SETUP**.

![The Audio I/O window: device routing, output routing and the calibration reference](manual/img/dialog-audio-setup.png)

**Device routing (upper half)**

| Control | What it does |
| --- | --- |
| Audio device type | The driver family: ASIO, Windows Audio, DirectSound (Windows); CoreAudio (macOS); ALSA/JACK (Linux). **ASIO gives the lowest latency on Windows** |
| Output | The interface that plays the processed sound |
| Input | The interface your guitar is connected to |
| Active channels | Tick the input channel the guitar uses and the output pair your monitors use |
| Sample rate | 44.1 kHz and up. Higher rates cost more CPU; NAM captures are resampled internally as needed |
| Audio buffer size | The latency/stability trade-off. 128 or 256 samples is a good starting point |
| Control panel / Test | Opens the manufacturer's own panel (ASIO) and plays a test tone |

**Output routing (lower left).** Four independent taps, each assigned to a
physical output pair or switched **Off**:

| Route | Signal it carries | Typical use |
| --- | --- | --- |
| MAIN / POST MASTER | The finished player output | Monitoring and recording the final sound |
| PRE / NEUTRAL NAM | BLOCK NAM 2 before the player's tone stack, effects and cabinet | Re-amping, A/B comparison |
| DI / CLEAN INPUT | The selected input source before amplifier processing (physical input on IN, file playback on DI) | A clean safety track |
| WET / POST CAB | The processed post-cabinet branch | A separate processed recording path |

A pair can only be used by one route: choosing a pair that is already taken
resets that selector to **Off**. MAIN normally uses outputs 1/2. Leave the
routes you do not need switched off so nothing is duplicated.

**Interface input reference / 0 dBFS peak (lower right).** A slider from 0 to 30
dBu, shown in dBu. It tells [Input Cali](#15-input-cali-automatic-input-calibration)
what your interface's maximum input level is. It has no effect while Input Cali
is off.

Everything in this window - device, channels, rate, buffer, reference and the
four routes - is saved per machine and restored on the next launch. It is
deliberately **not** stored in `.bnpp` presets, so a preset can travel between
computers.

---

## 6. Signal flow

### IN / DI: choose the source (standalone only)

The large **IN / DI** lever sits below DUAL MONO / SPLIT L/R. **IN** uses the
configured physical inputs. **DI** replaces them with audio files before the
existing effects, NAMs, IRs and output routing. The application starts on **IN**
at every launch. Source changes use a short ramp to avoid clicks.

Selecting DI opens the DI PLAYER modal. Close it with **CLOSE**, its window
close button or Esc; playback continues. **CONFIG DI** reopens it without
changing source. The cabinet and the main browsers stay clear.

![DI source selector and CONFIG DI](manual/img/zone-di-source.png)

| Processing mode | DI tracks |
| --- | --- |
| MONO | One mono file feeds the active left path |
| STEREO + DUAL MONO | The same mono file feeds both paths |
| STEREO + SPLIT L/R | Two mono files, DI L and DI R, independently feed the two paths |

![The DI player in MONO / DUAL MONO](manual/img/dialog-di-mono.png)
![The DI player in SPLIT L/R](manual/img/dialog-di-split.png)

**Load and remove.** Use **LOAD DI**, **LOAD DI L** or **LOAD DI R**, or drop
a file onto its row. In SPLIT you can drop two files together, one per path.
WAV, AIFF and FLAC are accepted, **mono only**. A stereo or multichannel file
is rejected with a message explaining that each DI must be a mono track; the
previous file stays loaded. Use the red **X** next to a filename to unload that
track from memory. It does not delete the original file. Removing a track
pauses the shared transport and leaves the other track loaded.

Files load in the background and play from memory. Each track may use a different
sample rate; playback automatically resamples to the audio device. No automatic
normalization is applied. The limit is 512 MiB of decoded audio per track.
Each track has its own **-60 to +12 dB** level, initially **0 dB**; double-click
its level slider to reset. INPUT GAIN remains available further down the chain.

### Shared DI transport and loop

The gold-framed transport above the NAM and IR browsers appears only in DI
mode. From left to right: **back 5 seconds, PLAY, PAUSE, STOP, forward 5 seconds**.
PLAY lights while playback is running.

![The DI transport integrated into the gold-trimmed head](manual/img/zone-di-transport.png)

| Control in the DI PLAYER | Action |
| --- | --- |
| PLAY | Play both tracks from the common position |
| PAUSE | Keep the position and send silence into the processing paths; effect tails continue |
| STOP | Pause and return to the beginning |
| Return-to-start button | Go to the beginning without changing play/pause state |
| POSITION | Seek with the slider or enter a time in seconds |
| LOOP | Enable or disable repetition for both tracks |
| LOOP IN / LOOP OUT | Set the common loop boundaries with sliders or numeric times |

The timeline lasts as long as the longest loaded track. A shorter or unloaded
track supplies silence; it never falls back to the physical input. Both tracks
seek and loop together. Closing the modal does not stop the transport.

**Switching sources:** DI to IN pauses DI and smoothly restores the physical
input. Returning to DI recalls its files, gains, position and loop, but **does
not start playback**. Press PLAY when ready. The physical input configuration
and its calibration setting are retained while DI is selected.

**Calibration:** interface-specific INPUT CALI is bypassed in DI mode, as shown
by the player status. It resumes with its previous setting on IN. This bypass
does not alter the per-file DI level or the amplifier's INPUT GAIN.

**Recall:** a normal exit saves file paths, levels, position and loop with the
standalone session. On relaunch the source is IN and DI is paused. Keep the files
in their saved locations or load them again. DI files and transport settings
are excluded from `.bnpp` presets. The plugin has no DI player, source switch,
transport controls, DI parameters or DI playback state; use audio tracks in the DAW.

### Processing order and output taps

Each path processes its own audio in this order:

```
selected source: physical IN or DI file(s)
  → tuner tap (always the untouched DI, before everything)
  → INPUT GAIN (+ Input Cali offset only on physical IN)
  → GATE
  → [ rack blocks, in the order shown on screen ]
        ...effects before BLOCK NAM 2...
        BLOCK NAM 1  (its own BASS/MID/TREBLE/PRESENCE)
        BLOCK NAM 2  (then the main BASS/MID/TREBLE/PRESENCE)
        ...effects between BLOCK NAM 2 and IR...
        IR  (cabinet convolution → IR VOL → IR BLEND)
        ...effects after IR...
  → MASTER VOL
  → OUTPUT GAIN
  → POWER
  → MAIN output
Other taps: DI before processing; PRE is a separate neutral NAM branch; WET is post-cabinet.
```

The diagram describes NORMAL. In PLUS the NAM / IR chain runs at NAM 1's rack position and NAM 2 is skipped; the rack IR stays separate. PRE remains the independent neutral NORMAL NAM 2 branch, not a tap of the PLUS chain.

BLOCK NAM 2 and IR are **anchors**: they cannot be dragged, and no block can be
moved so that IR ends up before BLOCK NAM 2. Everything else is free.

---

## 7. The rack: blocks, order and the eye

![The two rack rows in STEREO: BLOCK NAM 1 (red), BLOCK NAM 2 (gold), an enabled CHOR, and the chain icons that link L and R](manual/img/zone-rack-stereo.jpg)

In NORMAL, eleven blocks per path, shown left to right in processing order. The default
order is COMP · OCT · PITCH · BLOCK NAM 1 · BLOCK NAM 2 · CHOR · FLANG · PHASE ·
IR · DELAY · REVERB.

**Reading a block**

![The parts of a block: name, eye, LED, colour bar and link icon](manual/img/zone-block-icons.jpg)

| Part | Meaning |
| --- | --- |
| Body colour | Lit and tinted = enabled. Flat grey = bypassed |
| Small LED, top-left | Repeats the enabled state |
| Colour bar, bottom | The block's identity colour, lit while enabled |
| Eye, top-right | Chooses which block the shared controls and browsers describe. A viewed block has a green eye |
| Chain, bottom-right | Only in STEREO, only on effects: the L/R link. See [chapter 13](#13-linking-effects-between-l-and-r) |

**What clicking does**

| Action | Result |
| --- | --- |
| Single click on the body | Enables or bypasses the block |
| Double-click on the body | Effects: opens the editor. BLOCK NAM 1 / BLOCK NAM 2: opens the model chooser. IR: opens the IR chooser |
| Click on the eye | Makes that block the one the shared controls edit. A bypassed block cannot be viewed |
| Drag horizontally | Moves the block; the target position is outlined in white |
| Drop a file on a block | Loads it: `.nam` on a NAM block, `.wav` on the IR block; a folder loads its first valid file |
| Hover BLOCK NAM 1 / BLOCK NAM 2 | Shows the capture information card |

A NAM or IR block can only be enabled once it holds a valid file. Clicking an
empty one while its file is still loading means "switch on when ready", not
"invert".

---

## 8. BLOCK NAM 1 and BLOCK NAM 2

Both blocks run any compatible `.nam` capture; the player does not assume what
was captured. BLOCK NAM 1 sits earlier in the chain and is the natural place for
a pedal or preamp capture, BLOCK NAM 2 for an amplifier - but nothing stops you
using them the other way round.

![The two browsers: NAM models on the left with its four selectors, IR files on the right, IR VOL between them](manual/img/zone-browsers.jpg)

**Loading a capture**

| Route | How |
| --- | --- |
| BROWSE LOCAL | Pick one `.nam`, or a folder. A folder adds every capture it contains to the list and selects the first. Tick **DEEP SEARCH** in the file dialog to include subfolders |
| The list | Click any row to load it; the ▲ / ▼ buttons step through the list and grey out at the ends |
| TONE3000 | Opens the online library inside the player - see [chapter 16](#16-tone3000-inside-the-player) |
| Drag and drop | Drop a `.nam` or a folder on the list or directly on the block |
| Double-click the block | Opens the file chooser for that block |

Each block remembers its own folder, its own deep-search setting, its own list
and its own selection, per path. Selecting a capture for BLOCK NAM 2 also resets
that path's controls to safe defaults and switches the block on; the cabinet
selection is left alone.

**Architecture is automatic.** The player identifies NAM A1, A2 Standard and A2
Nano and dispatches A2 models through NAM Core's fast path. There is no manual
switch. If a file is not a valid single-input/single-output NAM, the load is
refused and the block stays as it was.

**The capture information card.** Hovering a NAM block or any row of the NAM
list shows the metadata written into the `.nam` header - title, gear make and
model, who modelled it, gear type, architecture, sample rate and input reference
level - plus artwork when available.

![The capture information card](manual/img/tone-card.png)

Artwork is any image sitting beside the capture with the same base name
(`My Capture.nam` → `My Capture.png`, `.jpg`, `.jpeg` or `.webp`). TONE3000
downloads save it automatically; for your own captures, drop an image next to
the file. Only the header of the file is read, so hovering a long list costs
nothing.

**Loading BLOCK NAM 1.** Choose its NAM selector to target the browser, or double-click its rack block to choose the capture source:

![Choosing the source for BLOCK NAM 1](manual/img/dialog-block-nam1.png)

### NORMAL / PLUS: NAM and IR chains

The lever switch on the left end of the rack chooses between two ways of using
NAM captures:

| Position | What the rack shows |
| --- | --- |
| NORMAL (lever down) | BLOCK NAM 1 and BLOCK NAM 2, exactly as described above |
| PLUS (lever up) | One large **NAM / IR** block, twice as wide, at BLOCK NAM 1's position in the chain |

![PLUS: one double-width NAM / IR block per path, with its chain topology under the name](manual/img/zone-rack-plus.jpg)

The NAM / IR block of PLUS runs a **chain** of NAM and cabinet IR blocks. It switches on and off with
a click and has the eye like any other NAM block; the line under its name shows
the chain, for example `SERIES 2` or `PARALLEL 2 | 1`. **Double-click it** to open
the PLUS CHAIN window:

![The PLUS CHAIN window in parallel: lane A above, lane B below, the + buttons and the A / B MIX](manual/img/dialog-nam-chain.png)

| Element | Use |
| --- | --- |
| Single-line / parallel-lines switch | **SERIES**: one lane from IN to OUT. **PARALLEL**: two lanes, A above and B below, fed by the same input and mixed back together |
| NAM 1A / 2A and IR 1A / 2A (likewise B) | Up to two NAMs and two IRs per lane. Each lane retains one NAM placeholder. Blocks run in the displayed order |
| Click on a block | On / off (an empty block opens the load menu instead) |
| Double-click or right-click | NAM: load a local capture or use TONE3000. IR: load a local WAV, AIFF or FLAC. Remove block is available when allowed |
| Drop a file | Drop `.nam` on a NAM card or + NAM; drop WAV, AIFF or FLAC on an IR card or + IR |
| Eye (NAM cards only) | Select the NAM block edited by BASS, MID, TREBLE, PRESENCE and loaded from the NAM MODELS list or TONE3000 |
| `-` (top right corner) | Remove the block, after confirmation. The last NAM of a lane cannot be removed; all IRs can be removed |
| **+ NAM / + IR** | Add the chosen type; each button becomes unavailable at its two-block limit. New NAMs are inserted before IRs |
| IR level | -24 to +12 dB, initially 0 dB; double-click to reset. WAV, AIFF and FLAC, mono or stereo averaged to mono, up to 8192 source samples, resampled without normalization |
| Drag a block | Reorder it, also into the other lane (if its two-NAM / two-IR limits allow it) |
| MIX A - B (PARALLEL only) | Linear crossfade: centre gives 50% of each lane; the ends give 100% of A or B. Unlike PAN, centre is not full level on both lanes |

Each NAM block keeps its own capture, on/off switch and tone controls, just like
BLOCK NAM 1 and BLOCK NAM 2. In PLUS the NAM selectors above the tone plate and
over the list become one per path, captioned with the block being edited
(`NAM 2A`), and the list shows the NAM models of that block.

The first time PLUS is switched on, loaded NORMAL NAM captures are copied into lane A in rack order, with their bypass and tone settings. An empty NAM placeholder remains if neither capture is loaded. The general rack IR is not copied into a lane. NORMAL and PLUS keep separate settings: going back to
NORMAL finds BLOCK NAM 1 and BLOCK NAM 2 exactly as they were. The switch, the
chains and their captures are saved with the session, in presets (the `.bnpp`
bundle embeds every chain capture and IR) and, in the plug-in, with the DAW project.
Every change of the chain is applied behind a short fade, with a short transition to suppress clicks.
With INPUT CALI on, PLUS calibrates to the first active NAM of lane A; standalone DI playback bypasses interface calibration.

IRs within a lane run in series. To mix two cabinets, put one in each parallel lane and use A/B MIX. The rack IR remains a separate shared block: bypass it when using independent lane cabinets to avoid filtering the signal twice. IR files load in the background, and their level, order and bypass state are saved with the chain. Legacy chains with more than two NAMs per lane restore the first two and show a notice; keep the original preset if you need its older configuration.

---

## 9. Cabinet impulse responses

**BROWSE IR** loads a `.wav` response, or a folder: the player keeps the short
WAV files that are usable as impulse responses, lists them and selects the
first. If nothing suitable is found it reports **IR not found**.

- Mono and stereo responses are accepted; a stereo file is summed to mono.
- Up to 8192 samples are used, resampled to the current device rate.
- **The original gain is preserved - IRs are never normalized.**
- Click the selected row a second time to deselect it: the response is cleared
  and the IR block is bypassed.
- **DELETE** removes the selected response from the IR folder, after asking.
- Loading or changing a response crossfades, so it never clicks.

Two controls shape the cabinet:

![IR VOL, with its own scale and the (L)/(R) caption in STEREO](manual/img/zone-ir-volume.jpg)

- **IR BLEND** mixes the signal without cabinet convolution against the
  convolved signal, 0 - 100 %.
- **IR VOL** (the vertical fader) sets the level of the cabinet branch alone,
  **-24 dB to 0 dB**, default **-12 dB** to leave headroom for hot captures. The
  current value is printed under the scale.

---

## 10. Amplifier controls, knob by knob

![The main control row and the NAM/IR selectors above it](manual/img/zone-tone-controls.jpg)

**Operating a knob**: drag vertically or horizontally; the exact value is
printed underneath. **Double-click restores the default** - 12 o'clock for
everything except GATE, which returns to fully left (OFF).

| Control | Range | Default | Notes |
| --- | --- | --- | --- |
| INPUT GAIN | -12 … +12 dB | 0.0 dB | Level into the NAM chain; Input Cali is added on physical IN; bypassed for DI files |
| GATE | OFF … -80 … 0 dB threshold | OFF | At the far left it is a true bypass. Attack 1.5 ms, hold 35 ms, release 90 ms, 3 dB hysteresis |
| BASS | ±12 dB @ 70 Hz | 0.0 dB | Peaking, Q 0.72 |
| MID | ±12 dB @ 750 Hz | 0.0 dB | Peaking, Q 0.72 |
| TREBLE | ±12 dB @ 4 kHz | 0.0 dB | Peaking, Q 0.72 |
| PRESENCE | ±12 dB @ 6 kHz | 0.0 dB | Peaking, Q 0.72 |
| MASTER VOL | -12 … +12 dB | 0.0 dB | After the chain, before Output Gain |
| IR BLEND | 0 … 100 % | 50 % | Dry against cabinet |
| IR VOL | -24 … 0 dB | -12 dB | Cabinet branch only |
| OUTPUT GAIN | -12 … +12 dB | 0.0 dB | Final level |
| POWER | On / off | On | Mutes the processed path; the switch glows red while on |
| INPUT CALI | On / off | Off | See [chapter 15](#15-input-cali-automatic-input-calibration) |

**The tone stack follows the selected NAM block.** With a **NAM 1** selector
active, BASS / MID / TREBLE / PRESENCE drive BLOCK NAM 1's own four filters;
with a **NAM 2** selector active they drive the main tone stack. Each set keeps
its own values, and switching selectors recalls them. In the plug-in and in
STEREO the plate prints which one you are editing.

![Input column: Input VU, INPUT GAIN and INPUT CALI with its LED](manual/img/zone-input-column.jpg)
![Output column: Output VU, OUTPUT GAIN and POWER](manual/img/zone-output-column.jpg)

---

## 11. The eight effects in full

The eight effects offer **three algorithms** and **six main parameters** each. PITCH also includes the HARMONIZER controls described below. Double-click a
block to open its editor; every knob shows a real unit, and double-clicking a
knob restores its default.

![The effect editor, here for DELAY](manual/img/dialog-effect-editor.png)

The **ACTIVE** switch at the top right of the editor is the same bypass as
clicking the block. **TYPE** chooses the algorithm. Parameter, algorithm and
bypass changes are smoothed, delay-family reads are interpolated and feedback is
bounded, so nothing clicks or runs away.

### COMP - compressor
Algorithms: **Studio VCA**, **Optical**, **FET Punch**.

| Parameter | Range | Default |
| --- | --- | --- |
| Threshold | -55 … -2 dB | -31.2 dB |
| Ratio | 1 … 20 :1 | 7.7:1 |
| Attack | 1 … 100 ms | 15.9 ms |
| Release | 20 … 600 ms | 223 ms |
| Makeup | -12 … +12 dB | 0.0 dB |
| Mix | 0 … 100 % | 100 % |

### DELAY
Algorithms: **Digital Studio**, **Tape Echo**, **Analog BBD**.

| Parameter | Range | Default |
| --- | --- | --- |
| Time | 20 … 1200 ms | 398 ms |
| Feedback | 0 … 92 % | 32 % |
| Mix | 0 … 100 % | 28 % |
| Tone | 0 … 100 % | 65 % |
| Mod | 0 … 100 % | 8 % |
| Level | -12 … +12 dB | 0.0 dB |

### CHOR - chorus
Algorithms: **Studio**, **Ensemble**, **Tri-Chorus**.

| Parameter | Range | Default |
| --- | --- | --- |
| Rate | 0.05 … 5 Hz | 1.24 Hz |
| Depth | 0.5 … 20 ms | 10.3 ms |
| Mix | 0 … 100 % | 35 % |
| Delay | 4 … 30 ms | 11.8 ms |
| Feedback | -65 … +65 % | 0 % |
| Level | -12 … +12 dB | 0.0 dB |

### FLANG - flanger
Algorithms: **Analog**, **Through-Zero**, **Jet**.

| Parameter | Range | Default |
| --- | --- | --- |
| Rate | 0.03 … 2.5 Hz | 0.57 Hz |
| Depth | 0.1 … 9 ms | 5.0 ms |
| Mix | 0 … 100 % | 35 % |
| Feedback | -85 … +85 % | 20 % |
| Manual | 0.2 … 5 ms | 1.4 ms |
| Level | -12 … +12 dB | 0.0 dB |

### PHASE - phaser
Algorithms: **4 Stage**, **8 Stage**, **12 Stage**.

| Parameter | Range | Default |
| --- | --- | --- |
| Rate | 0.03 … 4 Hz | 0.82 Hz |
| Depth | 0 … 100 % | 70 % |
| Mix | 0 … 100 % | 40 % |
| Feedback | -75 … +75 % | 12 % |
| Centre | 180 … 2200 Hz | 887 Hz |
| Level | -12 … +12 dB | 0.0 dB |

### REVERB
Algorithms: **Studio Room**, **Plate**, **Concert Hall**.

| Parameter | Range | Default |
| --- | --- | --- |
| Size | 0 … 100 % | 55 % |
| Damping | 0 … 100 % | 50 % |
| Mix | 0 … 100 % | 25 % |
| Width | 0 … 100 % | 80 % |
| Freeze | OFF / ON | OFF |
| Level | -12 … +12 dB | 0.0 dB |

### OCT - octaver
Algorithms: **Poly Clean**, **Classic Mono**, **Organ**.

| Parameter | Range | Default |
| --- | --- | --- |
| Oct Down | 0 … 100 % | 45 % |
| Oct Up | 0 … 100 % | 0 % |
| Dry | 0 … 100 % | 80 % |
| Tone | 0 … 100 % | 50 % |
| Tracking | 0 … 100 % | 65 % |
| Level | -12 … +12 dB | 0.0 dB |

### PITCH - pitch shifter
Algorithms: **Studio**, **Low Latency**, **Vintage**.

| Parameter | Range | Default |
| --- | --- | --- |
| Semitones | -12 … +12 st | 0.0 st |
| Mix | 0 … 100 % | 100 % |
| Window | 20 … 120 ms | 65 ms |
| Feedback | 0 … 55 % | 0 % |
| Fine | -100 … +100 ct | 0 ct |
| Level | -12 … +12 dB | 0.0 dB |


#### HARMONIZER (scale-aware harmony)

![The PITCH window with the HARMONIZER strip: switch, INTERVAL, KEY, SCALE, TUNING and the live display](manual/img/dialog-harmonizer.png)

The strip at the bottom of the PITCH window turns the block into an intelligent
harmonizer. With **HARMONIZER** on, every note you play gets a second voice a
scale step away, using the selected or detected scale:

| INTERVAL | Harmony voice |
| --- | --- |
| OCTAVE UP / OCTAVE DOWN | Always an octave; needs no key, sounds from the first note and also works on chords |
| THIRD UP / THIRD DOWN | The third of the scale: **major or minor depending on the note**. In C major, C gets E (major third) and D gets F (minor third); in C minor, C gets Eb |
| FIFTH UP / FIFTH DOWN | The fifth of the scale: perfect, or diminished on the seventh degree (B -> F in C major) |

**KEY and SCALE.** With KEY on **AUTO** the key is learned from the notes you play:

- It works on the seven notes in use, which is what decides the harmony. A key is
  told apart from its parallel (C major / C minor) by the notes actually played (E
  or Eb, A or Ab, B or Bb); a key, its relative and its modes (C major, A minor, D
  dorian...) share their notes and therefore their harmony.
- The tonic and the mode are named from where the playing dwells and, above all,
  where phrases come to rest: the display can read `A MINOR`, `D DORIAN`,
  `G MIXOLYDIAN`... Pentatonic playing is read as the natural minor / major until
  other notes say otherwise. **Harmonic minor** is recognised when the raised
  seventh is used throughout (G# and never G in A minor): the dominant then gets
  its major third.
- Two memories run side by side: a long one keeps the key steady and a short one
  follows a real key change within a few seconds. The detector resists short passing notes; fix KEY manually if automatic detection does not match your phrase.
- Until enough notes have been heard the display shows **LISTENING...** and thirds
  and fifths stay silent, until detection has enough confidence. The bar under the key
  shows how sure the detection is.

Choose a tonic in **KEY** to fix the key yourself; **SCALE** then offers major,
minor, the five other modes, harmonic minor and melodic minor.

**TUNING.** **PURE** tunes each interval to the played note with simple ratios (5:4
and 6:5 thirds, 3:2 fifths): the two voices lock together without beating, which
is what keeps a harmony clean through an overdriven amp. **TEMPERED** uses the
piano's equal semitones, to match keyboards exactly.

**The voice.** The harmony is made by a shifter of its own whose splices are
synchronised to the period of the note being played, so it sounds like a second
guitar rather than an effect. It reads the guitar a few milliseconds late - the
natural delay of a second player - and uses that time to know each new note
before it sounds: a note never comes out with the interval of the previous one.
Notes are recognised from low E (and drop tunings) up to the 24th fret, within a
few cents, in about 25 ms (45 ms on the lowest strings). Bends and vibrato are
followed continuously: in a bend from C to D in C major the harmony slides from E
to F. Notes outside the key (a blue note, the G# of A minor) borrow the scale
degree that gives a real third or fifth: G# gets B, Bb in C major gets D.

**Knobs in HARMONIZER mode**: **MIX** balances the harmony against the note you
play, which always stays (100 % = both at the same level, 0 % = no harmony);
**FINE** detunes the harmony slightly for a wider sound; **LEVEL** works as usual.
SEMITONES, WINDOW and FEEDBACK rest. TYPE chooses the character of the voice:
**Studio**, **Low Latency** (a shorter delay; very fast phrases may lose a little
accuracy on low notes) and **Vintage** (darker). The rack block reads **HARMONY**
while the harmonizer is on.

Play single notes: thirds and fifths follow melodies, riffs and solos. For thirds and fifths, use single-note playing. Polyphonic or unclear input can make pitch detection unreliable; the detector may suppress the harmony. Detection uses the clean
guitar signal, before gain, NAM and effects. The HARMONIZER settings are saved
with the PITCH block and follow an L / R link.

---

## 12. MONO and STEREO: two complete rigs

![STEREO with SPLIT L/R: two rack rows, four NAM selectors, two IR selectors and stereo meters](manual/img/standalone-split.jpg)

**MONO / STEREO** (top right of the rack) switches between one and two audible
paths.

![The MONO / STEREO switch and the settings gear](manual/img/zone-mode-switch.jpg)

- **MONO**: the interface input is summed into the left chain, and its result
  feeds both channels of every routed output pair. Right-hand selectors, the
  second rack row and the input-mode switch are hidden.
- **STEREO**: both chains run. Two rack rows appear, the meters split into L and
  R, and the `L` / `R` tabs beside the racks choose which path the shared
  controls edit.

**DUAL MONO / SPLIT L/R** (beside the preset bay, STEREO only):

| Position | Input handling |
| --- | --- |
| DUAL MONO | The summed interface input feeds **both** chains - one guitar through two independent rigs |
| SPLIT L/R | Input channel 1 feeds the left chain, input channel 2 feeds the right chain |

This setting belongs to the application state, not to presets. The table describes physical IN. In DI mode MONO and DUAL MONO use the left file, while SPLIT L/R uses one file per path (chapter 6).

**PAN** (the bar between the two rack rows and the tuner, STEREO only): a
horizontal fader that balances the level of the two paths.

| Position | Result |
| --- | --- |
| Centre (`CENTER`, centre notch, green mark) | L and R play at their full level, exactly as without PAN |
| Towards `L` | The right path fades out progressively; at the left stop (`L 100 %`) only L is heard |
| Towards `R` | The left path fades out progressively; at the right stop (`R 100 %`) only R is heard |

The `L` and `R` letters at the ends are lamps: the one on the side being faded
dims, and the rail lights up from the centre towards the favoured side. Neither
side ever gets louder than it is at the centre. Double-click returns the fader
to the centre; the mouse wheel moves it in fine steps.

In the standalone PAN acts on the main and WET outputs (the PRE and DI taps stay
untouched) and is saved with the application state and in presets.

**The selectors.**

![NAM 1 L · NAM 2 L · NAM 1 R · NAM 2 R and IR L · IR R](manual/img/zone-selectors.jpg)

| Selector | Chooses |
| --- | --- |
| `NAM 1 L` `NAM 2 L` `NAM 1 R` `NAM 2 R` | The NAM block the tone controls and the NAM browser act on |
| `IR L` `IR R` | The cabinet that IR BLEND and IR VOL act on |
| `L` / `R` tabs | The path every other shared control acts on |

**Which control follows what**

| Control | Follows |
| --- | --- |
| INPUT GAIN, GATE, MASTER VOL, OUTPUT GAIN, POWER, INPUT CALI, TUNER | the selected **path** |
| BASS, MID, TREBLE, PRESENCE | the selected **NAM block** of that path (NAM 1 has its own set) |
| IR BLEND, IR VOL | the selected **cabinet** |
| Tuning reference, skin, Audio Setup, routing, updates | the whole application |

In MONO only the two left selectors are shown, and the IR VOL legend drops its
`(L)` / `(R)` suffix.

---

## 13. Linking effects between L and R

In STEREO you can lock an effect of the left chain to the same effect of the
right chain, so you only have to dial it once.

![Linked pairs are green; unlinked pairs are grey. A pair that no longer shares a column shows its icon in the corner of both blocks](manual/img/zone-rack-stereo.jpg)

- **Where the icon is.** When both blocks are in the same column, one chain icon
  sits on the seam between the two rack rows and joins them. If you move one of
  them so the pair no longer shares a column, the icon moves to the
  **lower-right corner of each block** - it still works exactly the same.
- **Colour.** Green = linked. Grey = not linked.
- **Click to link or unlink.**
- **What is shared:** the algorithm and the six parameters. Editing either block
  changes both.
- **What is not shared:** the on/off switch and the position in the chain. The
  two blocks can be both on, both off, or one of each - linking never touches
  them.
- **Linking two blocks that differ** asks which side to keep:

![Choosing which side's settings to keep](manual/img/dialog-link-choice.png)

- **Unlinking** leaves both blocks exactly as they sound at that moment; from
  then on they are edited separately.
- **BLOCK NAM 1, BLOCK NAM 2 and IR cannot be linked.**
- Links are saved with the session and inside two-path `.bnpp` presets.

---

## 14. Tuner

![The tuner row: the TUNER button, the LED display and the tuning selector](manual/img/zone-tuner-row.jpg)

Press **TUNER**; the lettering lights green and the button looks pressed. The
display shows the detected note with a left/right LED indication for flat,
centred or sharp.

- The tuner listens to the **untouched DI**, before the gate, the NAM blocks and
  the effects, and is not part of the draggable order.
- Range roughly **65 - 700 Hz**, at every sample rate from 44.1 to 192 kHz.
- Within **±5 cents** the display reads centred and turns green; beyond about
  40 cents it turns red.
- **TUNING** offers **STANDARD**, **DROP D**, **D STANDARD**, **Eb** and
  **OPEN G**.
- Play one isolated string at a useful level and let the previous note decay.

---

## 15. Input Cali (automatic input calibration)

NAM captures are trained at a known input level. Input Cali matches your
interface to that level so a capture sounds the way it was captured.

With Input Cali on, the player computes:

```
calibration gain (dB) = interface input reference (dBu) - NAM input reference (dBu)
```

- The interface value is the slider in [Audio Setup](#5-audio-setup-device-latency-and-routing).
- The NAM value comes from the capture's `input_level_dbu` metadata.
- When a capture has no metadata, the standard NAM reference of **+12 dBu** is
  assumed.
- The result is clamped to **-24 … +24 dB** and applied before the NAM blocks.
- The small LED beside INPUT CALI is green while it is active. The DI source bypasses interface calibration; returning to IN restores its setting.
- While a replacement capture is still loading, the gain of the running capture
  is held - it never jumps to 0 dB mid-note.

Input Cali changes gain only. It never rewrites or normalizes a model. If your
interface has several input modes (instrument / line / pad), enter the dBu value
of the mode you are actually using, as specified by the interface manufacturer.

---

## 16. TONE3000 inside the player

**TONE3000** (green button above the NAM list) opens the online capture library
in a window of the player.

![Before connecting an account](manual/img/tone3000-connect.png)

**Connecting once.** The first use asks to connect your account. TONE3000 signs
in with an e-mail link, so that opens their sign-in page once; the player then
keeps the returned refresh token, encrypted with a key derived from this
machine, in `tone3000.session` beside the application. Every later listing and
download normally renews the token silently on that
computer while the saved authorization remains valid. If it expires or is revoked, reconnect. **SIGN OUT** deletes the file.

![The library: five lists, artwork, author, model count and paging](manual/img/tone3000-library.png)

**Browsing and auditioning.**

| Element | What it does |
| --- | --- |
| TRENDING · LATEST · FAVOURITES · DOWNLOADED · MINE | The five listings a free-tier integration may read |
| Selecting a row | **Loads the capture into the current NAM block immediately.** The first capture of the tone is fetched and plays as soon as it is on disk; the rest of the tone and its artwork keep downloading in the background |
| Selecting another row | Cancels whatever is still downloading and auditions the new one instead |
| A tone you already downloaded | Loads instantly from your downloads folder |
| Rows marked **IR only - no NAM** | Contain only impulse responses; there is nothing to load into a NAM block, so they are not auditioned |
| RESTORE PREVIOUS MODEL | Puts back the capture the block held **before this window was opened**. Disabled if the block was empty |
| Closing the window | Keeps the last capture you auditioned |
| PREV / NEXT | Paging |
| The turning indicator and the status line | Show progress: *Downloading tone (n / m)*, then *Playing &lt;capture&gt;* |
| SEARCH FULL CATALOGUE | Opens TONE3000's own picker, with search and auditioning, inside the player. When you choose a tone the picker closes by itself and the download starts |
| SIGN OUT | Forgets the account on this computer |

Downloads are saved under your TONE3000 downloads folder, one folder per tone,
with the tone artwork beside each capture so the information card can show it.

**WebView2 (Windows only).** The embedded sign-in and the catalogue picker use
Microsoft WebView2, which ships with Windows 11 and with Edge on Windows 10. If
it is missing or unavailable the player offers an official Microsoft download,
your external browser, or cancelling - **nothing is ever installed
automatically**, and no Microsoft installer is included in the package. Local
audio and local files never need WebView2. macOS uses WKWebView; Linux falls
back to the system browser. External and embedded browsers do not share cookies,
so a session created in an older build may need one sign-in inside the player.

---

## 17. Portable `.bnpp` presets

**SAVE PRESET** writes one self-contained archive holding **both paths**:

- the BLOCK NAM 2 capture of each path;
- the BLOCK NAM 1 capture of each path, when loaded;
- the selected rack IR of each path, when loaded;
- NORMAL / PLUS mode and every PLUS NAM and IR file, lane order, bypass, tone, IR level and A/B mix;
- rack order, algorithms, all effect parameters and every bypass state;
- all amplifier knob, switch and tuner settings (not the DI player);
- the L/R effect links.

Embedded resources are verified with SHA-256 when loaded, extracted to the
application's preset cache and restored. Audio device, interface reference and
physical routing, DI files and DI transport are deliberately excluded so a preset can move between
computers.

**LOAD PRESET** restores it. A preset written by the single-path player, or by
NAM PLAYER DUAL, loads into the **currently selected path**. A preset written
here includes a left-path compatibility representation. Older players cannot reproduce features they do not implement, including the current PLUS chain; use 1.8.0 to recall the full configuration.

> To save from NORMAL, load BLOCK NAM 2 on the left path. PLUS also permits saving with a loaded file in its left-path chain. DI files are never embedded.

---

## 18. What is remembered, and where

**Session state** is written on a normal exit and restored on the next launch:
both paths, all controls, the selected captures and IRs, block order and bypass
states, links, MONO/STEREO, DUAL MONO/SPLIT, skin, audio device, channels, rate,
buffer, interface reference and the four routes. PLUS chains and DI file paths, levels, position and loop are also recalled. The source always starts on IN, with DI paused; switching back to DI never starts playback automatically.

| File | Where | What it holds |
| --- | --- | --- |
| `NAM_A2_HEAD.xml` | Beside the application when that folder is writable, otherwise the per-user data folder | The session |
| `tone3000.session` | Same folder | The encrypted TONE3000 refresh token |
| `Presets` / `PresetCache` | Same folder | Presets you save and the resources extracted from loaded ones |
| Per-user data folder | Windows `%APPDATA%\Bcho\BchoNAMPlayerDual`, macOS `~/Library/Application Support/Bcho/…`, Linux `~/.config/Bcho/…` | Used when the application folder is read-only (macOS bundles, AppImages) |

NAM and IR files are referenced by path, not copied into the session: keep them
where they were when you saved. Presets, by contrast, embed them.

---

## 19. Settings, skins, updates and support

Press the gear to the right of the rack.

![Application settings](manual/img/dialog-settings.png)

| Control | What it does |
| --- | --- |
| FRONT PANEL SKIN | Previews a finish immediately |
| APPLY SKIN | Makes the previewed finish permanent. Closing without applying restores the previous one |
| AUDIO SETUP | Opens [Audio Setup](#5-audio-setup-device-latency-and-routing) |
| CHECK FOR UPDATES | Compares your version with the latest public release |
| AUTO-UPDATES: ON / OFF | Whether that check also runs at startup |
| SUPPORT PROJECT ON KO-FI | Opens `ko-fi.com/bchosoft` in your browser |
| CLOSE | Closes the window |

**The eleven finishes**: Astra / Obsidian · Tribal / Etched Titanium · Skulls /
Bone & Carbon · Hippie / Sunset Paisley · Graffiti / Electric Ink · Purple
Velvet / Amethyst · Stainless Steel / Precision · Ripped Black Denim / Roadworn ·
Blue Denim / Indigo · Spiderwebs / Black Widow · Classic Black / Levant Tolex.
Every finish uses identical geometry, so no control ever moves; only materials,
knob designs and legend contrast change. The plug-in always uses Astra /
Obsidian.

![The update notice](manual/img/dialog-update.png)

Update checking only reports availability and opens the download page if you ask
it to. It never replaces files, models or presets.

---

## 20. Meters and animated cones

**INPUT VU** shows the incoming level and **OUTPUT VU** the final processed
level, from +6 down to -60 dB. In STEREO each meter splits into an L and an R
column.

![The cabinet: both cones follow the real output level](manual/img/zone-cabinet.jpg)

Both cones react to the real final output RMS: louder playing, or a higher
MASTER VOL / OUTPUT GAIN, gives a larger excursion; silence and POWER off return
them smoothly to rest. Only the cone surfaces move - rings, screws, grille,
cabinet and logo stay fixed. The animation runs at 60 frames per second on the
interface thread and never touches, delays or feeds back into the audio.

---

## 21. Mouse and keyboard reference

| Where | Action | Result |
| --- | --- | --- |
| Any knob | Drag up/down or left/right | Change the value |
| Any knob | Double-click | Restore the default (GATE returns to OFF) |
| Rack block | Single click | Enable / bypass |
| Rack block | Double-click | Open its editor or file chooser |
| Rack block | Drag sideways | Reorder (BLOCK NAM 2 and IR are fixed) |
| Rack block | Drop a file or folder | Load it into that block |
| Eye icon | Click | View that block with the shared controls |
| Chain icon | Click | Link / unlink that effect between L and R |
| NAM or IR list | Click a row | Load it |
| IR list | Click the selected row again | Deselect: clears the response and bypasses the IR block |
| NAM or IR list | Drop a file or folder | Load it |
| ▲ / ▼ | Click | Previous / next entry in the list |
| Dialog window | `Esc` | Close |
| Any control | Hover | Tooltip |

---

## 22. Troubleshooting

| Symptom | What to check |
| --- | --- |
| DI is silent | Press PLAY; returning from IN never resumes automatically. Check the loaded file, its gain and whether the playhead has reached its end |
| DI file rejected | Each file must be mono WAV, AIFF or FLAC; export each side separately from your DAW |
| No sound at all | POWER is on; MAIN route points at the outputs you monitor; the right input channel is ticked in Audio Setup; INPUT VU moves when you play |
| Sound, but no amp tone | A capture is loaded and BLOCK NAM 2 is lit; the chain is not entirely bypassed (a bypassed chain passes dry audio) |
| A NAM block will not switch on | Load a valid capture into that block and wait for the load to finish; a valid capture enables it automatically |
| IR block stays bypassed | Load a valid response, and check you have not clicked the selected row a second time (that deselects it) |
| Clicks or dropouts while playing | Raise the audio buffer, use the manufacturer ASIO driver on Windows, and avoid very small buffers with several NAM blocks running, especially PLUS in parallel |
| A folder appears empty | It must contain `.nam` files, or short valid `.wav` responses, directly inside the folder - unless DEEP SEARCH is ticked |
| Level does not match other NAM software | Check the interface reference in Audio Setup and whether Input Cali is on |
| A capture sounds too loud or too quiet | Check IR VOL (-12 dB by default) and Input Cali before changing INPUT GAIN |
| The session did not come back | The player saves on a **normal** exit; after a forced quit the previous session is restored instead |
| Models or IRs went missing | They are referenced by path. Put them back, or load a `.bnpp` preset, which embeds them |
| TONE3000 list is empty | Check the account, the network and - on Windows - WebView2; or use the external browser |
| macOS refuses the first launch | Right-click the application and choose **Open** |
| Linux AppImage will not start | `chmod +x` it and confirm the system has a working x86_64 audio stack |

---

## 23. Technical specifications

| Item | Value |
| --- | --- |
| Signal paths | 2 independent (L / R) |
| NAM blocks | NORMAL: 2 per path. PLUS: 2 per lane, 2 lanes per path (up to 8 across L/R) |
| Cabinet IR | 1 shared rack IR per path; PLUS adds up to 2 per lane (4 per path) |
| DI file player | Standalone only; 1 shared mono file or 2 mono files in SPLIT; WAV / AIFF / FLAC, automatic resampling |
| Effects | 8 per path, 3 algorithms and 6 main parameters each; PITCH adds HARMONIZER |
| Rack positions | NORMAL: 11. PLUS replaces the two NAM tiles with one double-width NAM / IR tile at NAM 1; the general IR stays separate |
| NAM architectures | A1, A2 Standard, A2 Nano - detected automatically |
| Sample rates | Whatever the device offers, 44.1 - 192 kHz |
| Buffer size | Whatever the driver offers; the engine internally uses at least 32 samples and splits oversized host buffers |
| IR length | Up to 8192 samples, resampled to the device rate, never normalized |
| Tuner range | ~65 - 700 Hz, ±5 cents centred |
| Auto Cal range | -24 … +24 dB |
| Start-up fade | 60 ms from silence |
| NAM change fade | 15 ms out, silence until the new capture is installed, 20 ms in (raised-cosine) |
| IR change fade | 12 ms crossfade |
| Native window | 1537 x 1023, responsive, minimum 50 % |
| Interface refresh | 60 fps, entirely off the audio thread |

---

## 24. Integrity, third-party code and licences

Compare downloaded ZIP hashes against `SHA256SUMS.txt`. Bcho NAM Player
includes JUCE and Neural Amp Modeler Core; their notices are in
`THIRD_PARTY_NOTICES.md`.

The application grants no rights over third-party NAM captures or impulse
responses. Follow the licence supplied with each capture or response, including
anything you download through TONE3000 or share inside a `.bnpp` preset.
