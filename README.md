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
palettes (HDSLAVE is the one a new card starts in), and a screen extension that all ten plug-ins below use to draw
their own pages. It wakes a sleeping plug-in when one of its knobs is turned,
and its master compressor's Sidechain can be keyed by a plug-in's second output (Foundry's SC Key: the kick alone).

Build it with its own `./build.sh` (its README has the details). Its packages are unsigned and are installed by
hand: it keeps Melodee's folders on the card (`autorun/melodee`, and `Melodee/` for projects, samples and
plug-ins). It is AGPL-3.0, as Melodee is.

## Synthesizers

| Plug-in | What it is |
| --- | --- |
| [TB-MPC-3-P-0](https://github.com/hdslave/TB-MPC-3-P-0-Synthesizer) | A 303-style bass synthesizer played by a port of TB-3PO, the random acid-pattern sequencer of the Ornament & Crime Hemisphere firmware. Its Press Plate screen shows each step's note, gate, accent and slide, with a Blacklight Transfer theme one press away. |
| [Psychic](https://github.com/hdslave/hdslave-Psychic-Synth) | A generative analog-style synthesizer (Labyrinth panel and flow) with two corruptible 8-bit sequencers. Its Contact Sheet screen compares saved and live steps and lets you edit each gate and voltage. |
| [Machine](https://github.com/hdslave/hdslave-Machine) | A multi-machine synthesizer in the style of Elektron's machines: a four-operator FM voice, seven drum machines, an eight-slot KIT, eight stranger voices and a resonator kick, with its own page on the MPC's screen |
| [Nexus](https://github.com/hdslave/hdslave-Nexus-Synth) | Mutable Instruments Plaits' 24 macro-oscillator models (its own open-source code) as an eight-voice polyphonic synthesizer: mono, poly and legato with unison, two ADSRs, a retrigger rate, two LFOs, a cycling envelope, a random source, a filter, fixed modulation routes and a 4 x 4 assign matrix, with Melodee's Slide and Tie. Its seven acid-rave pages pair the model banks with a live scope and show voice activity, filter response, envelopes, LFOs and both modulation matrices. [Watch the screen tour](https://github.com/hdslave/hdslave-Nexus-Synth/blob/63c5e6b3245136e8663908a4c1fae78ee22acaf2/docs/nexus-pages.gif). |
| [Necronomicon](https://github.com/hdslave/hdslave-Necronomicon-Synth) | A polyrhythmic subharmonic synthesizer (Subharmonicon panel and flow) with two VCOs, two subharmonics per VCO and two 4-step sequencers. Its Liquid Light screen shows the phase and routing of all four rhythm generators. |

## Drums and percussion

| Plug-in | What it is |
| --- | --- |
| [Foundry](https://github.com/hdslave/hdslave-Foundry-Drum-Machine) | A sixteen-voice drum machine in the style of the 808, 909 and 606, with TR-1000-style controls per voice, 606 mod controls, kick side chain, reverb, delay and bus compressor. Its X0X Drum Works page shows the pad layout and the last two seconds of drum hits. |
| [Anvil](https://github.com/hdslave/hdslave-Anvil-Synth) | An 8-step analog-style percussion synthesizer (DFAM/Edge panel and flow) with one new control, VCO EG > FM 1-2 Amt |
| [MoonBass](https://github.com/hdslave/hdslave-MoonBass-Synth) | An analog-style kick drum synthesizer (ModBase 09 Mk I/II and MBase 11 style), every parameter on Melodee's Edit pages, with its own Orbital Impact page in hdslaveOS |
| [Mystik](https://github.com/hdslave/hdslave-Mystik-Synth) | A west-coast hand drum: a membrane of nine bodies (tabla to iron bell) and a complex oscillator, struck by a hand with eight strokes through a modelled Buchla-style vactrol low-pass gate, played by its own six-mode sequencer (Pattern, Euclid, Turing, Automaton, Bounce and 14 traditional Rhythm timelines) with 303-style accents and slides, through four very cheap effects. Its own pages show the vactrol's light as an orb, the ring of steps and a phosphor scope, with an editor for each step and a view of each sequencer mode at work. |

## Effects

| Plug-in | What it is |
| --- | --- |
| [Cortex Filter](https://github.com/hdslave/hdslave-Cortex-Filter) | A stereo 3D morphing filter in the style of the filter-cube morphing filter modules: a bank of 64 filters (a cube with its own offsets, gains, fades, levels and distortion) and a filter sequencer stepped by clocks on the song's grid, the input's envelope or the page. The cube and its response are drawn in 3D on the MPC's screen, with pages to edit filters and program sequences. |

Each folder's README covers that plug-in's controls, presets, sources, tests and cost.

## On the MPC

Each plug-in is one `.clap` file. Copy it to the card as `Melodee/Plugins/hdslave NAME/hdslave NAME.clap` (for
example `Melodee/Plugins/hdslave Anvil/hdslave Anvil.clap`), then pick it on an empty track: Stage, Plugin,
hdslave NAME. They load in any Melodee. In hdslaveOS, open Edit or Stage's plug-in page to see the instrument or
effect's own screen. Turning a knob on the MPC wakes a sleeping plug-in.

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
E-mu, Rossum Electro-Music, Mutable Instruments, inMusic Brands).
These projects are not affiliated with any of them, nor are they official Melodee releases.
