# winbtw

> **Language:** English · [Bahasa Indonesia](README_ID.md)

### Introduction to the dotfiles/config

**winbtw** is a collection of dotfiles and configuration files that turns a Windows 11 desktop into a more polished, macOS-inspired setup. It includes a status bar, a terminal, a system info display, a dock, window styling, a wallpaper switcher, and a Dynamic Island-style overlay.

Windows can make a better themed desktop too, not only Linux.

The repository contains:

- `config/fastfetch/`: Fastfetch layout, logo image, and ASCII text ("kiyo").
- `config/mydockfinder/`: MyDockFinder dock settings (`config.ini`).
- `config/wezterm/`: WezTerm configuration (`.wezterm.lua`). Optional.
- `config/yasb/.config/yasb/`: YASB status bar configuration, styles, and wallpaper widget (`config.yaml`, `styles.css`, `yasb_colors.css`).
- `resource/`: Component icons and cursors used by the configs.
- `resource/walls/`: Wallpaper images for the wallpaper switcher.
- `resource/fonts/`: Font files used by the configs.
- `windhawk.txt`: Windhawk mod settings to copy in manually.
- `LICENSE`: MIT License.

### Getting started

#### Requirements

- **Operating system:** Windows 11 (tested). Windows 10 may work, but it has not been tested.
- **Permissions:** Administrator access may be needed for some Windhawk and dock settings.

#### Required software

| Software | Link | Required |
|---|---|:---:|
| MyDockFinder | [Steam store](https://store.steampowered.com/app/1787090/MyDockFinder/) | Yes (paid) |
| YASB | [yasb.dev](https://yasb.dev/) | Yes |
| Windhawk | [windhawk.net](https://windhawk.net/) | Yes |
| Fastfetch | [GitHub](https://github.com/fastfetch-cli/fastfetch) | Yes |
| VirtualDesktop (PowerShell module) | [PowerShell Gallery](https://www.powershellgallery.com/packages/VirtualDesktop/) | Yes (for the wallpaper switcher, Windows 11 only) |
| WezTerm | [wezterm.org](https://wezterm.org/index.html) | Optional |

> **Warning:** Please use a legal, purchased license for MyDockFinder. Cracked copies are not supported and may contain malware.

#### Optional components

- WezTerm: Only needed if you want the included terminal config.
- **SF Pro Display** font: Used by the Dynamic Island config (`FontFamily`). The font file is stored in `resource/fonts/`. If you do not install it, the overlay falls back to another font.
- Windows default virtual desktop shortcuts are used for workspaces (see [How it works](#how-it-works)).

### Installation

Follow these steps in order.

1. **Clone the repository:**
   ```powershell
   git clone https://github.com/wristkyion/winbtw.git
   ```
2. **Install the required software** listed in [Getting started](#getting-started).
3. **Copy each config to its place:**

   | Source (in repo) | Destination (on your PC) |
   |---|---|
   | `config/yasb/.config/yasb/` | `C:\Users\<YOUR_USERNAME>\.config\yasb\` |
   | `config/fastfetch/` | `C:\Users\<YOUR_USERNAME>\.config\fastfetch\` |
   | `config/wezterm/.wezterm.lua` | `C:\Users\<YOUR_USERNAME>\.wezterm.lua` (optional) |
   | `config/mydockfinder/config.ini` | MyDockFinder's install folder (see below) |
   | `resource/walls/` | `C:\Users\<YOUR_USERNAME>\walls\` |
   | `resource/` (other files) | A folder of your choice, for example `C:\Users\<YOUR_USERNAME>\winbtw-resource\` |

4. **Edit paths.** Open each config file and check for hardcoded paths, usually pointing to a previous username or a previous folder. Replace them with your own paths. Replace every `<YOUR_USERNAME>` with your Windows username, for example:
   - Image paths in `config/fastfetch/config.jsonc`
   - Icon or cursor paths in `config/yasb/.config/yasb/` (`styles.css`, `config.yaml`)
   - The wallpaper folder in `config/yasb/.config/yasb/config.yaml` (see [Wallpaper switcher](#wallpaper-switcher))
   - Any paths in `.wezterm.lua`

   Tip: search for `C:\Users\` or `resource` in each file.

5. **Set up the wallpaper switcher.** See [Wallpaper switcher](#wallpaper-switcher) below.

6. **Set up Fastfetch.** Run it with the config:
   ```powershell
   fastfetch -c "$env:USERPROFILE\.config\fastfetch\config.jsonc"
   ```
   To use it every time, add the command to your PowerShell profile (`$PROFILE`).

7. **Set up MyDockFinder.** Install the app, find its install folder (for example `steamapps\common\mydockfinder\` if you installed it through Steam, or the folder you chose), and copy `config.ini` there, replacing the existing file. Back up the original first.

8. **Set up Windhawk.** Follow the [Windhawk](#windhawk) steps below.

9. **Restart** YASB, MyDockFinder, and Windhawk (or sign out and back in) so all changes load.

#### Wallpaper switcher

The wallpaper switcher is set up in the YASB config. It needs two things:

1. **Wallpaper images.** Copy the contents of `resource/walls/` to `C:\Users\<YOUR_USERNAME>\walls\`. Replace `<YOUR_USERNAME>` with your Windows username.
2. **Install the VirtualDesktop PowerShell module.** Open PowerShell and run:
   ```powershell
   Install-Module VirtualDesktop -Scope CurrentUser
   ```
   This module provides `Set-AllDesktopWallpapers`, which the switcher uses to change the wallpaper. It works on Windows 11 only. Without it, the switcher will show an error. `Set-AllDesktopWallpapers` replaces the wallpaper on all virtual desktops, not only the current one.

Then open `C:\Users\<YOUR_USERNAME>\.config\yasb\config.yaml`, find the `wallpapers` widget, and make sure `image_path` points to your `walls` folder:

```yaml
  wallpapers:
    type: "yasb.wallpapers.WallpapersWidget"
    options:
      label: "<span>\ue7aa</span>"
      image_path: "C:/Users/<YOUR_USERNAME>/walls"
      run_after:
            - 'powershell -NoProfile -WindowStyle Hidden -Command "Set-AllDesktopWallpapers ''{image}''"'
      engine:
        enabled: true
        animation: slide_top
      gallery:
        type: "strip"
        image_width: 240
        accent_color: "#fff"
        orientation: "portrait"
        image_corner_radius: 0
      keybindings:
      - keys: alt+shift+w
        action: toggle_gallery
        screen: cursor
```

Replace `<YOUR_USERNAME>` in `image_path` with your Windows username. Use forward slashes (`/`) in this path, as shown.

#### Windhawk

1. Open Windhawk, then go to **Settings > Advanced settings > More advanced settings > Process inclusion list**.
2. Make sure **`dwm.exe`** is in the list. The mods need to hook into `dwm.exe` to work.
3. Install and enable these mods:
   - **Custom Window Corner Radius**
   - **macOS magnifying cursor**
   - **Dynamic Island for Windows**
4. Open each mod's settings, switch to **text mode**, and paste the matching settings from `windhawk.txt`:
   - **Custom Window Corner Radius:** `radius: 15`, `smallRadius: 6`, `tooltipRadius: -1`, `roundMaximizedAndSnapped: none`
   - **macOS magnifying cursor:** `maxScalePercent: 400`, `shakeThreshold: 2500`, `lerpSpeedUpPercent: 40`, `lerpSpeedDownPercent: 15`
   - **Dynamic Island for Windows:** paste the full block from `windhawk.txt`.

#### MyDockFinder

- Install MyDockFinder and activate your license.
- Replace its `config.ini` with the one from `config/mydockfinder/`, as described in the installation steps above.

---

### How it works

#### Overview

| Component | Role |
|---|---|
| **Windhawk** | Adds visual tweaks to Windows (rounded corners, magnifying cursor, Dynamic Island). Hooks into `dwm.exe`. |
| **YASB** | Top status bar, styled with CSS (`styles.css`, `yasb_colors.css`). Includes its own quick search and wallpaper switcher. |
| **MyDockFinder** | Dock at the bottom of the screen. |
| **Fastfetch** | Shows system info with the "kiyo" logo, for example in new terminal sessions. |
| **WezTerm** | Optional terminal, with its own theme and settings. |
| **resource/** | Component icons, cursor images, wallpapers (`walls/`), and fonts (`fonts/`). |

#### Keybindings

**winbtw custom shortcuts:**

| Shortcut | Action | From |
|---|---|---|
| `Ctrl + Alt + D` | Hide or show the Dynamic Island | Windhawk (Dynamic Island) |
| `Ctrl + Alt + Space` | Open the Dynamic Island quick search | Windhawk (Dynamic Island) |
| `Alt + Space` | Open YASB quick search (like macOS Spotlight) | YASB |
| `Alt + Shift + W` | Open the wallpaper gallery (quick switch wallpaper) | YASB |

**Windows default shortcuts used for workspaces:**

| Shortcut | Action |
|---|---|
| `Win + Ctrl + D` | Create a new virtual desktop |
| `Win + Ctrl + ←` / `→` | Switch between virtual desktops |
| `Win + Ctrl + F4` | Close the current virtual desktop |
| `Win + Tab` | Open Task View |

---

### License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

### Footer

Made by **wristkyion** · [github.com/wristkyion/winbtw](https://github.com/wristkyion/winbtw) · MIT License

*Windows can make a better themed desktop too, not only Linux.*