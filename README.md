# hdslave MPC Sample Synths and Drum Machines

The hdslave synthesizers and drum machines for the Akai MPC Sample, and hdslaveOS, the build of Melodee they are
made for, in one place. Each lives in its own repository. This repository holds each of them as a submodule: a folder
pinned to a commit of that repository, so one clone fetches them all.

## Get them all

```sh
git clone --recurse-submodules https://github.com/hdslave/hdslave-MPCSample-Synths-and-Drum-Machines.git
```

If you cloned without `--recurse-submodules`, the folders are empty: run `git submodule update --init` inside the
clone.

## hdslaveOS

[hdslaveOS](https://github.com/hdslave/hdslaveOS) (first called melodee-hdslave) is hdslave's fork of
[Melodee](https://github.com/keremimo/melodee-sample) by Kerem Kiliç (Ellic Studio), the groovebox that runs on the
MPC Sample and hosts the plug-ins below. It gives the MPC's processor less wasted work and plays
the same, to the bit; it adds CPU speed, Refresh, Dim after and Pad brightness settings, the MONO and HDSLAVE
palettes (HDSLAVE is the one a new card starts in), and a screen page a CLAP plug-in can draw itself, which Anvil,
TB-MPC-3-P-0, Machine, Cortex Filter, Necronomicon, MoonBass and Psychic use. It wakes a sleeping plug-in when one of its knobs is turned,
and its master compressor's Sidechain can be keyed by a plug-in's second output (Foundry's SC Key: the kick alone).

Build it with its own `./build.sh` (its README has the details). Its packages are unsigned and are installed by
hand: it keeps Melodee's folders on the card (`autorun/melodee`, and `Melodee/` for projects, samples and
plug-ins). It is AGPL-3.0, as Melodee is.

## Synthesizers

| Plug-in | What it is |
| --- | --- |
| [TB-MPC-3-P-0](https://github.com/hdslave/TB-MPC-3-P-0-Synthesizer) | A 303-style bass synthesizer played by a port of TB-3PO, the random acid-pattern sequencer of the Ornament & Crime Hemisphere firmware |
| [Psychic](https://github.com/hdslave/hdslave-Psychic-Synth) | A generative analog-style synthesizer (Labyrinth panel and flow) with two corruptible 8-bit sequencers. Its Contact Sheet screen compares saved and live steps and lets you edit each gate and voltage. |
| [Machine](https://github.com/hdslave/hdslave-Machine) | A multi-machine synthesizer in the style of Elektron's machines: a four-operator FM voice, seven drum machines, an eight-slot KIT, eight stranger voices and a resonator kick, with its own page on the MPC's screen |
| [Necronomicon](https://github.com/hdslave/hdslave-Necronomicon-Synth) | A polyrhythmic subharmonic synthesizer (Subharmonicon panel and flow) with two VCOs, two subharmonics per VCO and two 4-step sequencers. Its Liquid Light screen shows the phase and routing of all four rhythm generators. |

## Drums and percussion

| Plug-in | What it is |
| --- | --- |
| [Foundry](https://github.com/hdslave/hdslave-Foundry-Drum-Machine) | A sixteen-voice drum machine in the style of the 808, 909 and 606: TR-1000-style controls per voice, 606 mod controls, kick side chain, reverb, delay and bus compressor |
| [Anvil](https://github.com/hdslave/hdslave-Anvil-Synth) | An 8-step analog-style percussion synthesizer (DFAM/Edge panel and flow) with one new control, VCO EG > FM 1-2 Amt |
| [MoonBass](https://github.com/hdslave/hdslave-MoonBass-Synth) | An analog-style kick drum synthesizer (ModBase 09 Mk I/II and MBase 11 style), every parameter on Melodee's Edit pages, with its own Orbital Impact page in hdslaveOS |

## Effects

| Plug-in | What it is |
| --- | --- |
| [Cortex Filter](https://github.com/hdslave/hdslave-Cortex-Filter) | A stereo 3D morphing filter in the style of the filter-cube morphing filters, with the cube and its response drawn in 3D on the MPC's screen |

Each folder's README covers that plug-in's controls, presets, sources, tests and cost.

## On the MPC

Each plug-in is one `.clap` file. Copy it to the card as `Melodee/Plugins/hdslave NAME/hdslave NAME.clap` (for
example `Melodee/Plugins/hdslave Anvil/hdslave Anvil.clap`), then pick it on an empty track: Stage, Plugin,
hdslave NAME. They load in any Melodee. In hdslaveOS, Anvil, TB-MPC-3-P-0, Machine, Cortex Filter, Necronomicon,
MoonBass and Psychic draw their own page in place of the parameter list, and a sleeping plug-in hears a knob turned on the MPC.

## Build

Each plug-in, and hdslaveOS, builds and tests itself with its own `./build.sh`, which needs Docker with a Linux arm64 context
(Melodee's `colima-melodee` and its `melodee-builder` image by default). For example:

```sh
cd Anvil && ./build.sh
```

## Keeping it current

The folders stay at the commits this repository pins until it is updated. `tools/update.sh` moves every folder to
the newest commit on its repository's branch (`main`, and `hdslave` for hdslaveOS) and commits that; `git push` then
publishes it. Work on a plug-in or on hdslaveOS itself is committed and pushed in its own repository.

## Trademarks

Product names mentioned here are trademarks of their owners (Roland, Moog Music, Behringer, Jomox, Elektron, Korg,
E-mu, Rossum Electro-Music, inMusic Brands).
These projects are not affiliated with any of them, nor are they official Melodee releases.
