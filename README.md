[README.md](https://github.com/user-attachments/files/35482627/README.md)
<div align="center">

# Asura's Wrath — native PC port

**An unofficial port of Asura's Wrath (PS3) to Windows and Linux, made by static recompilation.**
No emulator, no PS3 firmware, at the resolution and frame rate you choose.

[![Release](https://img.shields.io/github/v/release/RecompPort/asura-port)](https://github.com/RecompPort/asura-port/releases/latest)
[![Downloads](https://img.shields.io/github/downloads/RecompPort/asura-port/total)](https://github.com/RecompPort/asura-port/releases)
[![Check](https://github.com/RecompPort/asura-port/actions/workflows/comprobar.yml/badge.svg)](https://github.com/RecompPort/asura-port/actions/workflows/comprobar.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
![Windows](https://img.shields.io/badge/Windows-10%20%7C%2011-0078D6)
![Linux](https://img.shields.io/badge/Linux%20%7C%20Steam%20Deck-experimental-orange)

**[Download](https://github.com/RecompPort/asura-port/releases/latest)** ·
[Install guide](docs/INSTALAR.md) ·
[Linux & Steam Deck](docs/LINUX.md) ·
[Known issues](#known-issues) ·
[Español](README.es.md)

</div>

> [!IMPORTANT]
> **This repository contains nothing from the game.** That means no
> executable, graphics, sounds or text, no official artwork, and no PS3 keys
> or firmware. You build the port on your own machine from **your own copy**
> of Asura's Wrath for PS3 (European, `BLES01227`, or US, `BLUS30721`).
>
> This is a fan project. It is not affiliated with Capcom, CyberConnect2 or
> Sony Interactive Entertainment. Requests, links or files from the game are
> not accepted in issues.

## New in 1.1

- **The US version works too** (`BLUS30721`), besides the European one. Same
  program, one build: you pick which to play in the launcher.
- **In-game options menu** (**F1**, or **SELECT + START** on a gamepad), with
  **keyboard and gamepad remapping**.
- **Mouse camera**, a **VSync** option and **mash QTEs that can be won at any
  frame rate**.
- **Redesigned launcher** with seven sections, save **export and import**, a
  **low-end PC preset**, a **bug report** button and a new-version notice.
- **Update and DLC from RPCS3 in one click** (*Extras → Add from RPCS3*).
- **Smoother and faster:** chapter VI and later run much better, no more
  periodic stutter, and the shader cache survives driver updates.

All the details are in the
[1.1 release notes](https://github.com/RecompPort/asura-port/releases/tag/v1.1)
and in [CHANGELOG.md](CHANGELOG.md).

## What it is

The whole game program (Cell PowerPC code) is translated to C++ and compiled
into a native PC executable. It runs on our own runtime, which plays the part
of the PS3:

- the system (LV2), files and threads;
- the SPUs;
- the RSX graphics, on OpenGL 4.5;
- audio and gamepads.

It is not an emulator: the game's code runs directly on your CPU.

### Features

- **Graphics:** internal resolution from 640 × 360 up to 4K (or your
  screen's). 30, 60, 90 or 120 fps (120 is experimental). Fullscreen or
  windowed. Optional removal of the cutscene letterbox.
- **Controls:** any gamepad SDL recognizes (Xbox, DualShock 4, DualSense,
  Switch Pro…) with rumble, or the keyboard. In-game button prompts can be
  PlayStation, Xbox, Switch, keyboard, or match the connected gamepad.
- **Both versions:** European (`BLES01227`) and US (`BLUS30721`), with one
  build.
- **Content:** update 01.02 and the DLC, if you have them. They are read from
  wherever they are, without copying; what you installed in RPCS3 is found
  automatically.
- **Trophies**, with on-screen pop-ups and a list in the launcher.
- **Save games**, with export and import in the launcher (saves and trophies
  in one `.zip`).
- **Launcher** in 7 languages: English (the default), Spanish, German, Italian,
  French, Japanese and Chinese. It works with mouse, keyboard or gamepad.
- **Windows setup wizard** that does everything for you, and uninstalls like
  any other program.
- **Audio without PS3 firmware:** the port decodes the game's MP3 music and
  voices itself.
- **Low-end PC options:** resolution below the console's, console-sized
  shadows, and profile-guided optimization.

## Status (1.1)

| | Status |
|---|---|
| Windows 10 / 11 | **Playable.** This is the main platform. |
| Linux | Experimental. It builds and runs, but needs more testers. |
| Steam Deck | Experimental. It installs through distrobox; no performance testing yet. |
| European version (`BLES01227`) | Playable. |
| US version (`BLUS30721`) | Supported. It is the same program as the European one; new in 1.1, so less tested. |
| Update 01.02 and DLC | Working, including their episodes and the full list of 53 trophies. |
| 30 / 60 / 90 fps | Stable. |
| 120 fps | Experimental. It can drop below 120 in the heaviest scenes. |

On the test PC (Ryzen 7 5700X, RTX 5060, 1080p) most of the game holds the
chosen frame rate. In the hardest fights the game's own main thread sets the
limit: the toughest fight of episode IV runs at 65–90 fps in 90 fps mode and at
70–115 fps in 120 fps mode.

## Requirements

| | Minimum | Recommended |
|---|---|---|
| OS | 64-bit Windows 10, or Linux with a recent Mesa | Windows 11 |
| CPU | 4 threads | 4 cores / 8 threads or more |
| GPU | OpenGL 4.5 (any recent NVIDIA, AMD or Intel) | Current mid-range |
| Disk | About 6 GB free (MSYS2 and the build) | |

**From your own copy of the game:**

1. **Asura's Wrath, European (`BLES01227`) or US (`BLUS30721`)**, as a
   `PS3_GAME` folder or a **decrypted** ISO (made with 3k3y or PS3Dec). The
   raw encrypted disc ISO won't work.
2. **The decrypted `EBOOT.elf` of that same version.** The disc's `EBOOT.BIN`
   is encrypted, and the port does not decrypt it: that would mean putting
   Sony keys in the repository. The one from the disc or from the update
   works, since they are the same program.
3. **Optional:** the update and the DLC of that same version, already
   installed and decrypted. If you only have the PKG files, install them once
   in RPCS3: the launcher shows the steps and then finds them by itself
   (*Extras → Add from RPCS3*).

**European or US?** Either one. Both executables carry the same program (only
a few bytes of data differ: the title ID, the region and the build date), so
one build of the port plays both. You choose which one to play by choosing
the game in the launcher (*Disc* section). Each keeps its own
`datos\<ID>\EBOOT.elf` and its own saves; trophies are the same list and are
shared. The update and DLC must match the game: US ones only with the US
game, European ones only with the European game.

You need no emulator and no PS3 firmware.

## Installing

### Windows (recommended)

1. Download **`AsurasWrath-PC-v1.1-Setup.exe`** from
   [Releases](https://github.com/RecompPort/asura-port/releases/latest).
2. Run it. It doesn't need administrator rights. The wizard is in English
   (an *Español* link on the first page switches it to Spanish). The installer is
   not signed: if Windows says "Windows protected your PC", choose *More info
   → Run anyway*. You can check it is the original against its sha256 in
   `SHA256SUMS.txt`.
3. Follow the wizard. It:
   - finds your copy and checks the `EBOOT.elf`;
   - picks up any update and DLC you have;
   - installs MSYS2 if needed;
   - builds the port, which takes about 10 minutes on 8 threads;
   - creates the shortcuts.
4. Open **"Asura's Wrath"** from the desktop and press **Play**.

**Why is it built on your PC?** Because the resulting program contains the
game's translated code, and that can't be distributed. What you download is
only the port.

**To update,** run the new version's installer on the same folder. Your saves,
trophies and settings are kept. The full guide, with troubleshooting, is in
[docs/INSTALAR.md](docs/INSTALAR.md) (in Spanish).

### Linux and Steam Deck (experimental)

Download **`AsurasWrath-PC-v1.1-Linux.tar.gz`** from
[Releases](https://github.com/RecompPort/asura-port/releases/latest), then:

```sh
tar xzf AsurasWrath-PC-v1.1-Linux.tar.gz && cd asuras-wrath-pc
./instalar-linux.sh /path/to/PS3_GAME
./jugar.sh
```

The script builds with your system's tools: clang, cmake, ninja, Python 3.10+,
SDL3 and zlib. If they're missing, as on the Steam Deck, it builds inside a
distrobox container and leaves the system untouched. On the Steam Deck it
also sets suitable defaults and creates an entry you can add to Steam for
Game Mode. Messages are in English (`--idioma es` for Spanish). Step by step:
[docs/LINUX.md](docs/LINUX.md) (in Spanish).

## Settings and performance

Everything is set in the launcher, or in game with the **port options menu**
(**F1**, or **SELECT + START** on a gamepad). On Linux, where there is no
launcher, the menu is the easiest way; all settings are also in
`opciones.txt`.

The launcher checks GitHub once a day for a newer release of the port and
shows a button if there is one. It only asks for the latest public release
of `RecompPort/asura-port` and sends nothing about you; turn it off with
*Game → Check for new versions*.

| Setting | Values |
|---|---|
| Frame rate | 30 (like the console), 60, 90, 120 (experimental). **F10** changes it in game. |
| Internal resolution | 0.5x (640 × 360), 0.75x (960 × 540), 1x (1280 × 720, like the PS3), 1.5x, 2x, 3x, or your screen's. |
| Shadows | At the internal resolution, or console-sized (faster). |
| Letterbox | In cutscenes: as on the console, or removed. **F8** in game. |
| Button prompts | PlayStation, Xbox, Switch, keyboard or automatic. |
| Game language | English, Spanish, French, German, Italian or Japanese. |
| VSync | Off (default), on, or adaptive. |
| New shaders | *Balanced* (default: never makes a frame late), wait for them (no flicker) or don't wait. |
| Mash QTEs | Winnable at your frame rate (default: each press counts as fps/30 presses), or at 30 fps like the console. Optional *hold to mash*. Stick QTEs (spin or shake) run at 30 fps while they last. |
| Mute in background | Off (default) or on. |

**If your PC struggles:**

- Press **Low-end PC preset** in the launcher's *Graphics* section, or use
  60 fps, an internal resolution of 1x or lower, and *console* shadows.
- **The first sessions are less smooth.** The game saves the SPU programs it
  uses, and the launcher translates them to native code the next time you
  press *Play*. The more you play, the smoother it gets.
- **Profile-guided optimization (optional):**
  1. Create a `pgo` folder containing an empty file named `MEDIR`, and press
     *Build the port*.
  2. Play for about 10 minutes, ideally with some fights, and close the game.
  3. Build again.

  [docs/INSTALAR.md](docs/INSTALAR.md) explains it in detail.

## Controls

On a gamepad, buttons are mapped by position: the bottom one is ✕. On the
keyboard:

| Keyboard | PS3 | | Keyboard | PS3 |
|---|---|---|---|---|
| W A S D (Shift: half tilt) | left stick | | Q / E | L1 / R1 |
| Arrow keys | right stick | | U / O | L2 / R2 |
| K or Space / L / J / I | ✕ / ○ / □ / △ | | Z / M | L3 / R3 |
| T F G H | D-pad | | Enter / Tab | START / SELECT |

The keys and the gamepad buttons can be changed in game: **F1 → Keyboard
controls** and **F1 → Gamepad buttons**.

**Mouse:** click in the window and the mouse moves the camera (right
stick); left button □, right button △, middle R3. Esc releases it (in
fullscreen it is taken automatically). Sensitivity, inverted Y or turning it
off are in the F1 menu; `raton_izq=` / `raton_der=` in `opciones.txt` change the
buttons.

| Key | What it does |
|---|---|
| F1, or SELECT + START | Port options menu |
| F11 or Alt+Enter | Fullscreen |
| F10 | Frame rate: 30 → 60 → 90 → 120 |
| F8 | Toggle the cutscene letterbox |
| F7 | Trophies earned |
| Esc | Release the mouse |

## Known issues

- **Only the European (`BLES01227`) and US (`BLUS30721`) versions work.**
  Other versions (such as the Japanese one) haven't been checked. If you have
  one, open an issue with the sha1 the installer shows, without any game files.
  The US version is new in 1.1 and has had less testing than the European one.
- **120 fps is experimental.** In the hardest fights the game's own main
  thread doesn't always fit in 8.3 ms per frame: on a Ryzen 7 5700X, the
  toughest fight of episode IV runs at 70–115 fps.
- **The first time an effect appears**, its GPU program has to be compiled.
  With *Balanced* (the default) the game never waits, but the effect may be
  missing for a frame or two. With *Wait* nothing is ever missing, but the game
  pauses for a moment (100–170 ms with an RTX 5060). After that it is cached.
- **The first time you play each area** there may be some stutter, until its
  SPU programs are translated (see above).
- **The installer is not signed**, so Windows SmartScreen warns about it.
- **Linux and the Steam Deck** have had little testing. Reports are very
  welcome.

If you find a bug, open an issue with the *Fallo* (bug) template and attach
the `asura.log` from that session. See [CONTRIBUTING.md](CONTRIBUTING.md).

## FAQ

**Does it download the game or give it to me?**
No. You need your own copy, and the port uses it from wherever it is.

**Why doesn't it decrypt the `EBOOT.BIN`, the update or the DLC?**
That would mean putting Sony's keys and decryption code in the project, and
that won't happen. You need them already decrypted.

**Can I download a prebuilt `asura.exe`?**
No. It contains the game's code, so it isn't published, and sharing it isn't
allowed here.

**Do I need RPCS3?**
No, not to play: you need no emulator of any kind, and no PS3 firmware. The
only case is the update and DLC if you have them as PKG files: those have to
be installed once (RPCS3 does it with your licence), and the launcher then
finds them by itself and shows you the steps.

**Can I play the US and the European version?**
Yes, both, with the same install. Choose the game in the launcher's *Disc*
section; each version needs its own decrypted `EBOOT.elf`, keeps its own saves
and uses update and DLC of its own region only.

**Why OpenGL and not Vulkan?**
OpenGL 4.5 was the most direct way to translate the RSX. Vulkan is on the
list for later.

## For developers

<details>
<summary><b>Building by hand (MSYS2 CLANG64 or Linux)</b></summary>

On Windows you need the MSYS2 CLANG64 terminal:

```sh
pacman -S --needed mingw-w64-clang-x86_64-{clang,cmake,ninja,python,zlib,sdl3}
./setup.sh "/c/path/to/Asura's Wrath/PS3_GAME"     # or the path to the EBOOT.elf
./asura.exe "C:/path/to/Asura's Wrath.iso"          # the decrypted ISO or the PS3_GAME folder
./lanzador.sh                                        # the launcher and its shortcut
```

`setup.sh` checks that the `EBOOT.elf` is exactly the one that was analyzed.
It then generates these in `build/`:

- the map of 47,932 functions (`build/analisis/funciones.tsv`);
- the 292 firmware imports (`imports.tsv`);
- the jump tables;
- the 27 SPU programs;
- the game translated to C++: 189 files, about 48,700 functions.

Nothing in `build/` is ever committed. Afterwards, `tools/compilar.sh`
rebuilds with the saved SPU programs and the `pgo/` profile.

From a clone, `Instalar.cmd` does the same as the installer, in a console
window. The release packages are made by `tools/instalador/compilar.sh`.

</details>

<details>
<summary><b>How it works</b></summary>

- **Analysis** (`tools/analisis/`) reads the PS3 ELF. From it, it gets the
  function map, firmware function names (by NID) and native UnrealScript
  function names, and the SPU programs.
- **Recompiler** (`tools/recomp/`) turns PowerPC64 + VMX into C++, with
  registers kept as local variables. It is tested instruction by
  instruction against `qemu-ppc64` (`tools/pruebas/`).
- **Runtime** (`runtime/`) is the PS3 the game sees:
  - memory, threads and LV2;
  - files and FIOS;
  - cellGcm and the RSX on OpenGL;
  - cellAudio and MultiStream;
  - SPURS (job chains and tasks) and the SPUs, with an interpreter and
    ahead-of-time translation.

  A few of the game's hot functions are rewritten by hand
  (`juego_nativo.cpp`).

Technical documentation (in Spanish):

- [docs/VIABILIDAD.md](docs/VIABILIDAD.md): the analysis and the plan.
- [docs/RECOMPILADOR.md](docs/RECOMPILADOR.md): the recompiler and how it was verified.
- [docs/RUNTIME.md](docs/RUNTIME.md): the runtime, performance, and the debug environment variables.

</details>

<details>
<summary><b>Customizing the launcher with your own art</b></summary>

The launcher's art belongs to the port: the program draws it itself, and it
shows your disc's icon, read from your copy. To use your own, put your
images in the `arte/` folder, which is never committed:

| File | What it's for |
|---|---|
| `logo.png` | Replaces the title. |
| `fondo.png` or `fondo.jpg` | The background. For a panorama, `fondo_x=` in `lanzador.ini` picks which part shows. |
| `icono.ico` | Icon of the launcher and its shortcut. Run `./lanzador.sh` afterwards. |
| `icono.png` | Icon of the game window, and of the Linux shortcut. |
| `icono_juego.png` | Use this if you want a different icon for the game than for the launcher. |

</details>

## Contributing

Issues and pull requests are welcome in English or Spanish. Please read
[CONTRIBUTING.md](CONTRIBUTING.md) first: no game files, ISOs, keys or links,
ever. `tools/comprobar_repo.py` checks this on every push.

## License

The project's code and scripts are under the [MIT](LICENSE) license.
Third-party components (SDL3, zlib, minimp3, stb) and trademarks are listed in
[TERCEROS.md](TERCEROS.md).

Asura's Wrath is a trademark of Capcom Co., Ltd. PlayStation and PS3 are
trademarks of Sony Interactive Entertainment. This project is not affiliated
with either of them.
