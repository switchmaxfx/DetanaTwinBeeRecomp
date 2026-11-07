# Detana TwinBee Yahho! Deluxe Pack Recompiled

> **Preview build.** This is an in-progress port, not a finished one. Expect
> rough edges. Bug reports, test results and pull requests are welcome.

[![Latest release](https://img.shields.io/github/v/release/switchmaxfx/DetanaTwinBeeRecomp?include_prereleases&label=release)](https://github.com/switchmaxfx/DetanaTwinBeeRecomp/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/switchmaxfx/DetanaTwinBeeRecomp/total)](https://github.com/switchmaxfx/DetanaTwinBeeRecomp/releases)

A static recompilation of the Japanese PlayStation release of **Detana TwinBee
Yahho! Deluxe Pack** (SLPS-00100) into a native Windows executable, built on
[PSXRecomp](https://github.com/RetroPortingToolKit/psxrecomp) and
[recomp-ui](https://github.com/RetroPortingToolKit/recomp-ui).

You need your own copy of the game. This repository contains no disc images,
no BIOS and no game assets.

| | |
|---|---|
| **Players** | 1–2 |
| **Region** | Japan (NTSC-J) |
| **Serial** | SLPS-00100 |
| **Developer / Publisher** | Konami |
| **Original release** | September 29, 1995 (PlayStation & Sega Saturn) |
| **Genre** | Vertical-scrolling shooter ("cute 'em up") compilation |

## About the game

*Detana TwinBee Yahho! Deluxe Pack* (出たなツインビーヤッホー! DELUXE PACK) is
Konami's two-in-one compilation of TwinBee arcade shooters, released in Japan
only for the PlayStation and Sega Saturn. It came out the year of the series'
10th anniversary and was later reissued on PlayStation as a *PlayStation the
Best* (SLPM-86054) and *PSone Books* (SLPM-87322) budget title.

It includes:

- **Detana!! TwinBee** (1991 arcade). Released in Europe as *Bells &
  Whistles*. Pilot TwinBee and WinBee, shoot clouds to juggle bells, and
  collect them for power-ups. The home versions don't support the arcade's
  vertical (TATE) screen orientation.
- **TwinBee Yahho! Fushigi no Kuni de Ōabare!!** (1995 arcade). The direct
  sequel, which hit Japanese arcades only months before this disc. This
  compilation was its first home release, and the console versions add extra
  voice acting. A US arcade version was planned as *Magical TwinBee* but never
  released.

Both games support two-player simultaneous co-op.

## Status

| Area | State |
|---|---|
| Boot (bundled OpenBIOS) | Working |
| Compilation menu | Working |
| Detana!! TwinBee | Playable |
| TwinBee Yahho! | Playable |
| Controller (digital / D-pad mode) | Working |
| Controller (analog mode) | Not supported by the game, see below |
| Saves / memory cards | Untested |
| Two-player | Untested |

**Latest release:** none yet.

## Setup

### Release package (recommended)

1. Download the latest Windows zip from
   [Releases](https://github.com/switchmaxfx/DetanaTwinBeeRecomp/releases) and
   extract it anywhere.
2. Run `DetanaTwinBee_Recompiled.exe`. The launcher opens.
3. Point it at your own disc image. Use a `.cue` with all its `.bin` files
   next to it (`.chd` and `.iso` also work).
4. In the launcher's controller settings, set your controller to
   **D-pad (digital)** mode.
5. Start the game.

A retail BIOS is optional. The bundled open-source OpenBIOS boots the game.

### Controllers

Keyboard and Xbox-style controllers work out of the box. F11 or Alt+Enter
toggles fullscreen.

> **Use D-pad (digital) mode.** This 1995 disc predates analog controllers,
> so if the pad is set to analog, the game sees an unknown controller and
> ignores all input. In digital mode the left stick works as the D-pad too.

Default keyboard layout:

| PlayStation | Keyboard |
|---|---|
| D-pad | Arrow keys |
| Cross / Circle / Square / Triangle | X / S / Z / A |
| L1 / R1 / L2 / R2 | Q / W / E / R |
| Start / Select | Enter / Right Shift |

## What this repository is

The game config, analysis seeds, build glue and generated C for this title.
It does **not** contain the disc image, a BIOS, or any game assets.

| Path | Purpose |
|---|---|
| `game.toml` | Recompiler config for SLPS-00100 |
| `seeds/`, `symbols.toml` | Function seeds and symbols for the boot EXE |
| `generated/` | Recompiled game C (produced from the disc by `psxrecomp-game`) |
| `psxrecomp/` | PSXRecomp framework (git submodule) |
| `recomp-ui/` | Launcher UI (git submodule) |
| `packaging/` | Release packaging config |

## Building from source

On Windows, using the
[cmake-clang toolchain](https://github.com/RetroPortingToolKit/RetroPorting-Toolchains/releases/latest)
and your own disc:

```sh
git clone --recurse-submodules https://github.com/switchmaxfx/DetanaTwinBeeRecomp.git
cd DetanaTwinBeeRecomp
./psxrecomp/tools/ci/build_emitters.sh
python psxrecomp/psxrecomp_cli.py generate --config game.toml --project-root . --disc <path to your .cue>
python psxrecomp/psxrecomp_cli.py rebuild --config game.toml --project-root . --build-dir build-release --no-pgo
```

See [psxrecomp/docs/BUILDING.md](https://github.com/RetroPortingToolKit/psxrecomp/blob/master/docs/BUILDING.md)
and [GETTING_STARTED.md](https://github.com/RetroPortingToolKit/psxrecomp/blob/master/docs/GETTING_STARTED.md)
for toolchain setup.

## Legal

- You must own the original game. Disc images and retail BIOS dumps are never
  committed or redistributed.
- Releases run on the bundled MIT-licensed
  [OpenBIOS](https://github.com/grumpycoders/pcsx-redux/tree/main/src/mips/openbios).
- Don't share `overlay_captures.json` publicly. It contains code captured from
  the disc.
- *TwinBee* and all related titles, characters and assets are trademarks and
  copyrights of Konami. This is an unofficial fan project, not affiliated with
  or endorsed by Konami.
- The PSXRecomp framework is licensed under PolyForm Noncommercial 1.0.0. See
  the framework's `LICENSE` and `THIRD_PARTY_ATTRIBUTION.md`.

## Credits

- **Konami**: the original games.
- **[PSXRecomp](https://github.com/RetroPortingToolKit/psxrecomp)** and
  **[recomp-ui](https://github.com/RetroPortingToolKit/recomp-ui)**: the
  RetroPortingToolKit recompilation framework and launcher.
- **OpenBIOS** from the PCSX-Redux project.

---

<p align="center">
  <sub><b>R.A.I.D. - Retro AI Development</b> | a Discord for AI-assisted retro reverse-engineering, decomp &amp; recomp</sub>
</p>

<p align="center">
  <a href="https://discord.gg/Ad9BwSzctP"><img src=".github/raid-discord.png" alt="Join the Retro AI Development (R.A.I.D.) Discord" width="200"></a>
</p>
<!-- /retcomm-readme-raid -->
