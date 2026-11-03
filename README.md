# OpenMoHAA

# Medal of Honor  Recompiled + Full 6dof VR

<!-- retcomm-readme-metrics -->
[![GitHub downloads (all assets, all releases)](https://img.shields.io/github/downloads/FractalEngineer/Medal-Of-Honor-PSX-Recomp/total)](https://github.com/FractalEngineer/Medal-Of-Honor-PSX-Recomp/releases)
[![Alpha v0.1.6](https://img.shields.io/badge/alpha-v0.1.6-orange)](https://github.com/FractalEngineer/Medal-Of-Honor-PSX-Recomp/releases/tag/v0.1.6)
<!-- /retcomm-readme-metrics -->

<!-- retcomm-readme-boxart -->
<p align="center">
  <img src="launcher_assets/img/boxart.png" alt="Medal of Honor box art" width="280">
</p>
<!-- /retcomm-readme-boxart -->

Static recompilation of **Medal of Honor** built on
[psxrecomp](https://github.com/mstan/psxrecomp) and
[recomp-ui](https://github.com/RetroPortingToolKit/recomp-ui).

Play the original game on a flat display, or opt into the experimental native
VR alpha with head tracking, per-eye rendering and tracked-weapon controls.
Flat play is the default; VR is enabled through a separate launcher.
Watch the [VR video demo](https://youtu.be/aS8N94uO3M0) for gameplay footage.

The **v0.1.6 Windows native alpha** is available from this fork's
[releases](https://github.com/FractalEngineer/Medal-Of-Honor-PSX-Recomp/releases/tag/v0.1.6).
See [alpha installation and controls](ALPHA_README.md) before testing.

| | |
|---|---|
| Players | 2 |
| Region | USA |
| Publisher | - |
| Year | - |

Scaffolded with the New Project Layout. See
`psxrecomp/docs/GAME_PROJECT_SETUP.md` for the full flow.

<!-- retcomm-readme-launcher -->
## Retro Launcher

You can run this title **standalone** (download the release zip, point it at
your disc, play), or manage installs, updates, and disc/BIOS wiring with
**[Retro Launcher](https://github.com/RetroPortingToolKit/Retro-Launcher)** —
the Retro Compilation Manager hub for self-compiling recomps.

[Downloads](https://github.com/RetroPortingToolKit/Retro-Launcher/releases) ·
[Full README & features](https://github.com/RetroPortingToolKit/Retro-Launcher#readme)

<p align="center">
  <img src="https://raw.githubusercontent.com/RetroPortingToolKit/Retro-Launcher/main/docs/screenshots/hub-and-game-launcher.png" alt="Retro hub with a background build, next to a title’s recomp-ui launcher" width="720">
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/RetroPortingToolKit/Retro-Launcher/main/docs/screenshots/queue-and-background-build.png" alt="Background cmake build with titles queued" width="720">
</p>

Retro checks for updates, installs the prebuilt release zips, and automates
BIOS/ROM/save plumbing so you are not stuck repeating each game’s first run by hand.
<!-- /retcomm-readme-launcher -->

## Legal

You must own the original game. Disc images under `disc/` are gitignored and
must never be committed. Retail BIOS dumps are not redistributed and no C
derived from one may be committed; releases run on the bundled MIT OpenBIOS.

`generated/` (the recompiled game C) **is committed**: releases ship the
compiled game, built by CI from that tree. Regenerate and commit it whenever
seeds or the framework pin change.

Default app icon: `assets/psxrecomp.ico` (and `.png` / `.svg`) — Retro-themed controller mark from `psxrecomp/assets/`. Windows builds embed it via `APP_ICON`.

Optional box art under `launcher_assets/img/` may come from
[libretro-thumbnails](https://github.com/libretro-thumbnails/libretro-thumbnails)
(`Named_Boxarts`); see `BOXART_SOURCE.txt` when present.

## Flat play

Launch `Medal_of_Honor__Recompiled.exe` normally and select your own disc image
in the launcher. No headset is required. The supported disc is **SLUS-00974
(NTSC-U)**; game data is not included.
The Windows release also includes `RunFlat.bat`, which clears VR overrides.

For a local Windows build, launch from the project root in a fresh terminal:

```powershell
.\build-release\Medal_of_Honor__Recompiled.exe --game game.toml --disc "C:\Games\Medal of Honor\medal-of-honor.cue"
```

Replace the example disc path with your own. Add `--no-launcher` to boot
directly. OpenXR support can be compiled into the same executable while ordinary
launches retain flat rendering and normal controller input. VR environment
overrides should be absent for flat play; the VR wrapper restores its process
environment when it exits.

`RunVR-VDXR.bat -Desktop` is a stereo diagnostic mode, not the ordinary flat launch.

## Experimental VR alpha (Windows)

The current [v0.1.6 Alpha](https://github.com/FractalEngineer/Medal-Of-Honor-PSX-Recomp/releases/tag/v0.1.6)
fixes the missing nearby floor and world shakiness during head movement, and
prevents overload shedding from flashing black frames. It retains tracked
weapons, the hand-anchored native HUD, desktop spectator mirror, barrel laser,
and 1080p default. Production builds disable heavyweight debug instrumentation.
The owner considers this build playable on Quest 3 through Virtual Desktop
with **VDXR**; demanding scenes can still slow down.

<p align="center">
  <a href="https://youtu.be/aS8N94uO3M0" title="Watch the Medal of Honor VR alpha gameplay demo">
    <img src="assets/vr-alpha-video-thumbnail.jpg" alt="Medal of Honor VR alpha gameplay demo" width="900">
  </a>
  <br>
  <a href="https://youtu.be/aS8N94uO3M0"><strong>&#9654; WATCH THE VR ALPHA GAMEPLAY DEMO</strong></a>
</p>

### Setup and launch

Download the Windows release and extract the entire ZIP. Connect your headset
and double-click the launcher for your runtime: `RunVR-VDXR.bat` (Virtual
Desktop VDXR), `RunVR-SteamVR.bat` or `RunVR-Oculus.bat` (Meta Quest Link / Air
Link). Each selects that runtime for the launch and leaves the system's active
runtime unchanged. Select your own
**SLUS-00974 (NTSC-U)** CUE/BIN image when prompted; the launcher remembers its
location. Keep the BIN files beside the CUE.

Boot videos, menus and briefing appear on a screen in VR; gameplay switches to
per-eye rendering. No save state, Python installation or development tools are
required. The game runs until you close it, and startup errors remain visible
in the console. Keep your `saves/` folder when updating.

To select a disc explicitly:

```powershell
.\RunVR-VDXR.bat -DiscPath "C:\Games\Medal of Honor\medal-of-honor.cue"
```

Use `RunFlat.bat` for ordinary flat play. See
[ALPHA_README.md](ALPHA_README.md) for further installation details and alpha
limitations.

### Current Touch controls

| Control | Gameplay |
| --- | --- |
| Left stick | Move / strafe |
| Right stick | Smooth turn |
| Right trigger | Fire |
| A | Use |
| B | Cycle weapon |
| X | Reload / use, according to game context |
| Right stick click | Toggle crouch |
| Left stick click | Jump |
| Left Menu button | Pause / Start |
| Right grip | Hold to show the barrel laser (ends on the surface it hits) |
| Left grip | Hold to aim a mounted machine gun with one stick |

In menus, the left stick navigates, A or right trigger confirms, and B goes back.

The barrel laser is a laser sight on the tracked weapon: **hold the right grip**
and the beam runs from the muzzle to whatever it hits, with a dot marking the
impact. It appears for firearms only.

A mounted machine gun aims with a single stick: **hold the left grip** and one
hand covers both traverse and elevation. Let go and normal movement returns.

### Report issues and contribute

Report problems in this fork's
[issue tracker](https://github.com/FractalEngineer/Medal-Of-Honor-PSX-Recomp/issues).
Include the build version, headset, OpenXR runtime, connection method,
mission/location, steps to reproduce, and any relevant captures. Mention whether
the issue also occurs in flat play. Do not attach disc images or retail BIOS dumps.

For development context, start with the
[VR handoff](docs/reverse/VR_HANDOFF.md) and
[alpha todo list](docs/reverse/VR_ALPHA_TODO.md). Game-specific weapons, controls
and HUD changes belong here; generic framework work is tracked in
[the upstream inventory](docs/UPSTREAM_PENDING.md).

## Development build

```bash
git submodule update --init --recursive
./psxrecomp/tools/ci/build_emitters.sh
python3 psxrecomp/psxrecomp_cli.py generate \
  --config game.toml --project-root . --disc disc/<your>.cue
git add generated && git commit -m "Regenerate game C"
cmake -S . -B build-release -G Ninja -DCMAKE_BUILD_TYPE=Release -DPSXRECOMP_BIOS_STEMS=OpenBIOS
cmake --build build-release --target psx-runtime
```

For Windows VR, configure the Release build with `-DPSX_OPENXR=ON`, or use
`RunVR-VDXR.bat -Build` after preparing the build tools and generated game C.
Compiling OpenXR support does not automatically enable VR when launching the
executable.

Releases `v0.1.0` through `v0.1.3` use locally verified Windows alpha packages. CI builds
its platform matrix without replacing those tested assets. Other tags `vX.Y.Z`
(or the *Release builds* workflow) build the
committed `generated/` C on Linux, Windows and macOS and attach
`moh-<version>-<platform>.zip`, the compiled game. Locally:
`scripts/package_release.sh build-release linux-x64`.
Windows packaging requires OpenXR and TCP startup inspection to be enabled
(`-DPSX_OPENXR=ON -DPSX_DEBUG_TOOLS=ON`), and includes both launchers.

## Symbols

Progressive map: `symbols.toml` → `python3 tools/sync_symbols.py` →
`psx_symbols.h` (`PSX_FN_*`). See `psxrecomp/docs/SYMBOLS.md`.

## Framework pins

Submodule gitlinks (`psxrecomp`, optional `recomp-ui`, nested `recomp-net`)
are authoritative. `framework_pins.txt` is an optional scaffold snapshot;
release CI logs SHAs with `record_pins.sh` but builds whatever the gitlinks
resolve to. Bump submodules deliberately — do not float on `main`/`master`
in release CI.

<!-- retcomm-readme-raid -->
---

<p align="center">
  <sub><b>R.A.I.D. — Retro AI Development</b> · a Discord for AI-assisted retro reverse-engineering, decomp &amp; recomp</sub>
</p>

<p align="center">
  <a href="https://discord.gg/Ad9BwSzctP"><img src=".github/raid-discord.png" alt="Join the Retro AI Development (R.A.I.D.) Discord" width="200"></a>
</p>
<!-- /retcomm-readme-raid -->


[![Build](https://github.com/openmoh/openmohaa/actions/workflows/branches-build.yml/badge.svg?branch=main)](https://github.com/openmoh/openmohaa/actions/workflows/branches-build.yml) [![Release](https://img.shields.io/github/v/release/openmoh/openmohaa)](https://github.com/openmoh/openmohaa/releases) [![Downloads](https://img.shields.io/github/downloads/openmoh/openmohaa/total)](https://github.com/openmoh/openmohaa/releases)

![License](https://img.shields.io/github/license/openmoh/openmohaa) ![Commits](https://img.shields.io/github/commit-activity/t/openmoh/openmohaa)

![Discord](https://img.shields.io/discord/596049712579215361?logo=discord&logoColor=white&color=5865F2)

![logo](misc/openmohaa-text-sm.png)

## What is OpenMoHAA?

OpenMoHAA is an open-source project aimed at preserving and enhancing **Medal of Honor: Allied Assault** (including Spearhead and Breakthrough expansions) by providing more features and bugfixes, across modern platforms and architectures.

Powered by [ioquake3](https://github.com/ioquake/ioq3) and the [F.A.K.K SDK](https://code.idtech.space/ritual/fakk2-sdk), OpenMoHAA provides:
- Full compatibility with the original game: assets, scripts and multiplayer
- Better support for modern systems
- Cross-platform support (Linux, Windows, macOS)
- Support for both single-player and multiplayer modes
- Includes all fixes from Spearhead 2.15 and Breakthrough 2.40b
- More fixes and features, such as bots and a ban system

*OpenMoHAA is an independent project and is not affiliated with or endorsed by Electronic Arts.*

## Getting started

- 📦 [Installing OpenMoHAA](docs/markdown/01-intro/01-installation.md)
- ▶️ [How to play: Launching the game, expansions & file locations](docs/markdown/02-running/01-running.md)
- ❓ [FAQ & Troubleshooting](docs/markdown/02-running/03-faq.md)
- 🌐 [Setting up a game server](docs/markdown/02-running/02-running-server.md)

## Reporting Issues

> [!NOTE]
> OpenMoHAA hasn't hit version 1.0.0 yet. Think of it like a beta build from the golden age of LAN parties. Features are being added, bugs are getting squashed, and more things are being tweaked. Things might change, break, or get even better over time.
> 
> If that sounds like your kind of mission, gear up, frag some bots, and help level up OpenMoHAA!

If you encounter a bug or a problem, you can do one of the following:
- Submit an [issue](https://github.com/openmoh/openmohaa/issues) on GitHub (use the template).
- Join the [OpenMoHAA Discord](https://discord.gg/NYtH58R) for a quick help.

## Additional documentation

- 📖 [Documentation](https://openmoh.github.io/openmohaa)
- ⚙️ [Game settings & configuration](docs/markdown/03-configuration/01-configuration.md)
- 📝 [Code & Scripting reference](docs/markdown/04-coding/02-coding.md)
- 📜 [Contributing guidelines](CONTRIBUTING.md)

## Current state

- 🧰 [List of differences](docs/markdown/01-intro/04-differences.md)

### Single-player

The entire single-player campaign should work (Allied Assault, Spearhead and Breakthrough). If you encounter any bug, please create a new [GitHub issue](https://github.com/openmoh/openmohaa/issues) describing them.

### Multiplayer

- Almost fully stable
- All official game modes are supported, including those from Spearhead and Breakthrough:
  - Free-For-All
  - Team-Deathmatch
  - Round-based match
  - Objective match
  - Tug-of-War (Spearhead)
  - Liberation (Breakthrough)
- Popular mods like **Freeze-Tag** are supported
- Built-in bots for offline practice and for testing
  - 🔧 [Setting up bots](docs/markdown/02-running/01-running.md#Playing-with-bots)

You can host your own [OpenMoHAA server](docs/markdown/02-running/02-running-server.md#) or join others using OpenMoHAA.

## Screenshots

|                                                                                   |                                                                            |
|-----------------------------------------------------------------------------------|----------------------------------------------------------------------------|
| ![](docs/assets/images/v0.60.0-x86_64/mohdm1_1.png)                                      | ![](docs/assets/images/v0.60.0-x86_64/training_1.png)                               |
| ![](docs/assets/images/v0.60.0-x86_64/flughafen_1.png)                                   | ![](docs/assets/images/v0.60.0-x86_64/flughafen_2.png)                            |
| ![](docs/assets/images/v0.60.0-x86_64/mohdm2_1.png "Playing Freeze-Tag mode with bots")  | ![](docs/assets/images/v0.60.0-x86_64/training_3.png "Single-Player training")    |

*More screenshots [here](docs/assets/images)*

## Development & Compiling

- 💻 [Building from source](docs/markdown/04-coding/01-compiling.md)

## Third party librairies

The following third party tools and libraries are used by the project

- [Flex](https://github.com/westes/flex)
- [Bison](https://savannah.gnu.org/projects/bison/)
- [SDL](http://www.libsdl.org/)
- [OpenAL](https://www.openal.org/)
- [LibMAD](http://www.underbit.com/products/mad/)
- [cURL](https://curl.se/)
- [Libogg](https://github.com/gcp/libogg)
- [Libvorbis](https://xiph.org/vorbis/)
- [Libopus](https://opus-codec.org/)

## Resources

- 🔗 [GitHub Repository](https://github.com/openmoh/openmohaa/)
- 🌐 [MOH-DB](https://www.moh-db.com/)
- 🕹️ [333networks](https://333networks.com/)
- 📂 [ModDB](https://www.moddb.com/games/medal-of-honor-allied-assault)
- 📂 [GameBanana](https://gamebanana.com/games/720)
- 💬 [Join us on Discord](https://discord.gg/NYtH58R)
