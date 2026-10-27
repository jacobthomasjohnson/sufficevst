# SUFFICE

A six-slot creative performance effect for Windows — VST3 and standalone —
built with JUCE and C++. One **TRANSFORM** knob morphs a chain of up to six
effects from untouched input to fully processed sound.

![SUFFICE main view](Documentation/reference-default.png)

**Version 1.9.20** · Windows x64 · VST3 + Standalone

## What it's for

SUFFICE is built for sound design and live performance: stacking grain,
rhythm, distortion, space and texture into a single playable gesture. Every
slot's Amount follows TRANSFORM, so a full chain can be swept, automated or
played by hand without balancing a dozen controls. Dice and Variation generate
new chains or variations on the current one, and 257 built-in patches
give starting points across many styles.

## Features

**Six reorderable slots, eleven engines**

| Effect | What it does |
| --- | --- |
| Grain | Up to 64 windowed voices over captured audio; per-control randomness, freeze, reverse, morphable envelope |
| Chop | Slices and rearranges audio in swung 16-step phrases; 58 authored patterns plus a generator |
| Pulse | Gain-only rhythmic shaping: tremolo, pumps, gates and 48 morphable shapes |
| Saturate | Soft, asymmetric and fold waveshaping with bias, pre/post filters and auto level |
| Filter | 23 shapes, up to 48 dB/oct, single/series/parallel A/B pairs, LFO and envelope follower |
| Chorus | 1–8 voices with feedback and loop filtering |
| Delay | Standard and ping-pong echoes with wow, ducking and return colour |
| Reverb | Plate and Hall networks, up to 48 s decay |
| Compress | Single-band or three-band multiband with per-band solo/mute and meters |
| Wear | Continuous blend of Legacy, Tape, Vinyl, Digital and Damaged ageing |
| Texture | Procedural and original synthesized loops, or your own sample, ducked or following the input |

**Performance and workflow**

- TRANSFORM macro with per-slot offsets, unlink/relink and global Mix and Output.
- Host-synced timing with straight, triplet and dotted divisions, plus Free
  timing with 1X/4X/8X range multipliers.
- XY editing surfaces and an editable filter response graph.
- Dice (new chain), Variation (same chain, new settings) and per-slot dice, all undoable.
- Module lock and reset from the right-click menu; locked modules are skipped by Dice.
- Solo and power per slot; a PANIC button clears tails without changing settings.

**Presets**

- 257 factory patches: Factory (80), SKIN & CIRCUIT (90), FERAL BLOOM (55) and PRISM RIOT (32).
- `.sufficepreset` user library with a tag-filtered browser; imported texture
  samples are embedded in presets and projects.

**Visuals**

- Each effect has an animated visual that responds to its parameters and the
  processed audio. Visuals vary per instance but never affect the sound.

**Safety**

- A -0.1 dBFS stereo-linked peak guard, fault latching on invalid audio, and
  optional auto makeup gain.
- No allocation, locks or blocking I/O in the audio callback; Compress reports
  its lookahead latency to the host.
- 8–192 kHz, mono or stereo, variable buffer sizes.

## How it was developed

SUFFICE is written in C++17 on [JUCE](https://juce.com) (pinned as a
submodule) with CMake and the Visual Studio toolchain. It was developed in
short iterative releases from a 1.9.0 baseline. Every release is planned and
recorded in the [version logbook](Documentation/Logbook.md), and design notes
for each feature are kept in [`Documentation/`](Documentation/).

AI coding agents did much of the implementation, working under the rules in
[`AGENTS.md`](AGENTS.md). Those rules cover scope limits, a real-time
audio-safety policy and required verification. Verification uses three tiers
run by `scripts/check.ps1`:

1. **Quick:** focused offline checks for UI and documentation changes.
2. **Standard:** the relevant checks plus a Release build.
3. **Full:** the complete offline suite (80 checks), an AddressSanitizer build
   and [pluginval](https://github.com/Tracktion/pluginval) at strictness 10.
   Required for any change that touches the audio path.

See [the development workflow](Documentation/Workflow.md) for details.

## Building

Requirements: Windows 10/11 x64, Visual Studio C++ Build Tools, the Windows SDK
and CMake 3.24 or newer.

```powershell
git clone --recurse-submodules https://github.com/jacobthomasjohnson/suffice.git
cd suffice
./scripts/build.ps1
```

Outputs:

- `build/Suffice_artefacts/Release/VST3/SUFFICE.vst3`
- `build/Suffice_artefacts/Release/Standalone/SUFFICE.exe`

Nothing is installed automatically. See [INSTALL.md](INSTALL.md) for
installation and [VALIDATION.md](VALIDATION.md) for validation.

## Documentation

- [User guide](Documentation/User-guide.md): every control and effect in detail
- [Preset guide](Documentation/Preset-guide.md) and [factory collections](Documentation/Factory-collection.md)
- [Version logbook](Documentation/Logbook.md) and roadmap

## License

JUCE is used under its own license (`vendor/JUCE/LICENSE.md`). All bundled
texture loops are original synthesis; no third-party recordings are included.
