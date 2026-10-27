<div align="center">

# Vita3K &middot; Android Layout Editor Fork

**An experimental PlayStation Vita emulator for Windows, Linux, macOS and Android,**
**with a fully customizable on-screen controller for Android.**

<br>

[![Platform: Android](https://img.shields.io/badge/Platform-Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#downloads)
[![License: GPLv2](https://img.shields.io/badge/License-GPLv2-2F6FEB?style=for-the-badge)](#license)
[![Upstream sync: weekly](https://img.shields.io/badge/Upstream_sync-weekly-8957E5?style=for-the-badge)](#base-version)
[![Discord](https://img.shields.io/badge/Discord-Join-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/MaWhJVH)

<br>

[Website](https://vita3k.org/) &nbsp;&middot;&nbsp;
[Wiki](https://github.com/Vita3K/Vita3K/wiki) &nbsp;&middot;&nbsp;
[Discord](https://discord.gg/MaWhJVH) &nbsp;&middot;&nbsp;
[Compatibility](#compatibility) &nbsp;&middot;&nbsp;
[Downloads](#downloads) &nbsp;&middot;&nbsp;
[Building](./building.md)

</div>

<br>

> [!NOTE]
> **This fork is temporary.** It will be maintained until the [main Vita3K repository](https://github.com/Vita3K/Vita3K) ships an improved Android layout editor. Once upstream includes an equivalent or better editor, this fork may no longer be actively maintained.
> I aim to catch up with upstream **every week** so this Android-focused fork stays close to `master`.

---

## Contents

| | |
| :-- | :-- |
| [Introduction](#introduction) | [Android layout editor](#android-layout-editor-improvements) |
| [What is in this update](#what-is-in-this-update) | [Compatibility](#compatibility) |
| [Gallery](#gallery) | [Downloads](#downloads) |
| [Building and running](#building-and-running) | [Bugs and issues](#bugs-and-issues) |

---

## Introduction

Vita3K is an experimental PlayStation Vita emulator for Windows, Linux, macOS and Android.

| Resource | For | Link |
| :-- | :-- | :-- |
| **Website** | Users | [vita3k.org](https://vita3k.org/) |
| **Wiki** | Developers | [Vita3K Wiki](https://github.com/Vita3K/Vita3K/wiki) |
| **Discord** | Community and support (recommended) | [Join the server](https://discord.gg/MaWhJVH) |

---

## What is in this update

This fork combines the latest upstream Vita3K code with Android-focused layout editor improvements and control customization features.

### Base version

| | Commit | Message |
| :-- | :-- | :-- |
| **Started from** | `99ec7cad` | `kernel: share one wait loop between sync objects` |
| **Synced through** | `6ec8e6ce` | `overlay: use existing bold CJK firmware fonts` |

The Android overlay work described below is retained on top of upstream `master`.

### Upstream Vita3K changes included

<details open>
<summary><b>Kernel, memory and CPU</b></summary>

<br>

| Area | Change |
| :-- | :-- |
| **Synchronization** | Shares a wait loop between synchronization objects. |
| **Synchronization callbacks** | Runs callbacks notified during a wait before the wait returns. |
| **System memory** | Enforces the Vita user-memory budget in `sceKernelAllocMemBlock`. |
| **Kernel timers** | Adds kernel timer event support. |
| **CPU execution** | Fixes handling of a guest function executing in the first memory page. |
| **CPU diagnostics** | Logs invalid guest accesses in full only when `LOG_INVALID_ACCESS` is enabled. |

</details>

<details open>
<summary><b>Graphics, audio and input</b></summary>

<br>

| Area | Change |
| :-- | :-- |
| **Shader output** | Clamps vertex `COLOR0` and `COLOR1` outputs to the `[0, 1]` range. |
| **OpenGL compatibility** | Adds a workaround for AMD integrated GPUs. |
| **PVRTC textures** | Decodes PVRTC textures before Vulkan RGBA8 uploads. |
| **Vulkan portability** | Negotiates Vulkan portability enumeration when available. |
| **NGS player buffers** | Advances to the next populated player buffer when the current slot is unavailable or empty. |
| **SDL input** | Forwards mouse and keyboard input correctly through the SDL frontend. |
| **CJK firmware fonts** | Uses available bold firmware fonts when the preferred Japanese, Chinese, or Korean font files are unavailable. |

</details>

<details open>
<summary><b>Build, logging and code health</b></summary>

<br>

| Area | Change |
| :-- | :-- |
| **Build requirements** | Raises the minimum Boost version to **1.82**. |
| **C++ cleanup** | Modernizes C++ patterns for readability across core, Android JNI, and other platform code. |
| **Logging** | Installs the termination handler only once. |

</details>

---

## Android layout editor improvements

Edit your on-screen controls directly, without leaving the game.

<table>
  <tr>
    <td width="50%" valign="top">

**Selecting and editing**

- Tap a control in the overlay to select it, or use the navigation controls instead.
- Hidden controls stay visible but dimmed while editing, so you can select and re-enable them.
- Adjust **visibility**, **size** and **opacity** per control.

  </td>
    <td width="50%" valign="top">

**Polish and integration**

- Style changes apply to the live overlay drawables.
- Better edit-pointer tracking avoids unnecessary drawable recreation and reduces pointer-related edit problems.
- Higher editor text contrast.
- Connected to the pause-menu and settings layout flows.

  </td>
  </tr>
</table>

### Per-stick sensitivity

Each thumb stick has its own sensitivity setting.

| Property | Behavior |
| :-- | :-- |
| **Scope** | Left and right sticks are stored separately. |
| **Range** | 10% to 200%. |
| **Default** | 100% keeps the normal response. |
| **How it works** | The multiplier is applied to the stick's X/Y output and clamped to the valid axis range. |
| **Persistence** | Saved with the overlay layout. Existing layouts without a saved value default to 100%. |

---

## Compatibility

The emulator currently runs most homebrew programs and commercial games.

| Catalog | Link |
| :-- | :-- |
| **Homebrew** | [Compatibility list](https://vita3k.org/compatibility-homebrew.html) |
| **Commercial** | [Compatibility list](https://vita3k.org/compatibility.html) |

---

## Gallery

<div align="center">

<table>
  <tr>
    <td align="center" width="50%">
      <img src="./_readme/screenshots/P4G.png" alt="Persona 4 Golden running in Vita3K" width="100%"><br>
      <b>Persona 4 Golden</b><br><sub>Atlus</sub>
    </td>
    <td align="center" width="50%">
      <img src="./_readme/screenshots/A%20Rose%20in%20the%20Twilight.png" alt="A Rose in the Twilight running in Vita3K" width="100%"><br>
      <b>A Rose in the Twilight</b><br><sub>Nippon Ichi Software</sub>
    </td>
  </tr>
  <tr>
    <td align="center" width="50%">
      <img src="./_readme/screenshots/Alone%20With%20You.png" alt="Alone with You running in Vita3K" width="100%"><br>
      <b>Alone with You</b><br><sub>Benjamin Rivers</sub>
    </td>
    <td align="center" width="50%">
      <img src="./_readme/screenshots/VA-11%20HALL-A.png" alt="VA-11 HALL-A running in Vita3K" width="100%"><br>
      <b>VA-11 HALL-A</b><br><sub>Sukeban Games</sub>
    </td>
  </tr>
  <tr>
    <td align="center" width="50%">
      <img src="./_readme/screenshots/Fruit%20Ninja.png" alt="Fruit Ninja running in Vita3K" width="100%"><br>
      <b>Fruit Ninja</b><br><sub>Halfbrick Studios</sub>
    </td>
    <td align="center" width="50%">
      <img src="./_readme/screenshots/Jetpack%20Joyride.png" alt="Jetpack Joyride running in Vita3K" width="100%"><br>
      <b>Jetpack Joyride</b><br><sub>Halfbrick Studios</sub>
    </td>
  </tr>
</table>

</div>

---

## Downloads

This fork focuses on Android builds and Android layout-editor development.

| Platform | Where to get it |
| :-- | :-- |
| **Android** | [Vita3K Android Layout Editor Update](https://github.com/Amarthya-sg/Vita3K/releases/tag/Updates) · [Adreno drivers](https://github.com/K11MCH1/AdrenoToolsDrivers/releases/) |
| **Windows, Linux and others** | [Main Vita3K repository](https://github.com/Vita3K/Vita3K.git) |

---

## Building and running

**Building:** see [`building.md`](./building.md).

**Running:** check the [quickstart guide](https://vita3k.org/quickstart) to make sure your device meets the minimum requirements.

<details>
<summary><b>Build validation</b></summary>

<br>

- The Android `assembleReldebug` build completed successfully after the original upstream updates and local Android changes were combined.
- The resulting APK was verified as a readable APK archive with **one signer**.
- A post-sync rebuild was **not** run in the current sandbox because no Android SDK is configured.
- Gameplay behavior was **not** tested on a physical device.

</details>

<details>
<summary><b>Source package note</b></summary>

<br>

The Android-only source archive contains:

- the Gradle Android project (`android/`)
- the Vita3K Android JNI bridge (`vita3k/android/`)

It intentionally excludes the shared Vita3K native core and other platform modules to keep the archive smaller, so it is **not a standalone build tree**. To compile the full Android app, use the complete Vita3K source checkout with its required submodules and dependencies.

</details>

---

## Bugs and issues

> [!WARNING]
> The project is in an early stage, so please be mindful when opening new issues. Expect crashes, glitches, low compatibility and poor performance.

---

## License

Vita3K is licensed under the **GPLv2** license. This is largely dictated by external dependencies, most notably Unicorn.

## Thanks

Special thanks to the maintainers and contributors of the [main Vita3K repository](https://github.com/Vita3K/Vita3K) for their continued work on the emulator and its Android support. This fork builds on their upstream code while focusing on Android layout editor improvements.

---

## Legal note

The purpose of this emulator is not to enable illegal activity. You can dump games from a Vita by using [NoNpDrm](https://github.com/TheOfficialFloW/NoNpDrm) or [FAGDec](https://github.com/CelesteBlue-dev/PSVita-RE-tools/tree/master/FAGDec/build). You can get homebrew programs from [VitaDB](https://www.rinnegatamante.eu/vitadb/#/).

<sub>PlayStation, PlayStation Vita and PlayStation Network are all registered trademarks of Sony Interactive Entertainment Inc. This emulator is not related to or endorsed by Sony, or derived from confidential materials belonging to Sony.</sub>
