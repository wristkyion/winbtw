# Introduction to the dotfiles/config

**winbtw** is a collection of dotfiles and configuration files that turns a Windows 11 desktop into a more polished, macOS-inspired setup. It includes a status bar, a terminal, a system info display, a dock, window styling, and a Dynamic Island-style overlay.

Windows can make a better themed desktop too, not only Linux.

The repository contains:

- `config/fastfetch/`: Fastfetch layout, logo image, and ASCII text ("kiyo").
- `config/mydockfinder/`: MyDockFinder dock settings (`config.ini`).
- `config/wezterm/`: WezTerm configuration (`.wezterm.lua`). Optional.
- `config/yasb/.config/yasb/`: YASB status bar configuration and styles (`config.yaml`, `styles.css`, `yasb_colors.css`).
- `resource/`: Component icons and cursors used by the configs.
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
| WezTerm | [wezterm.org](https://wezterm.org/index.html) | Optional |

> **Warning:** Please use a legal, purchased license for MyDockFinder. Cracked copies are not supported and may contain malware.

#### Optional components

- WezTerm: Only needed if you want the included terminal config.
- **SF Pro Display** font: Used by the Dynamic Island config (`FontFamily`). The font file is stored in `resource/fonts/`. If you do not install it, the overlay falls back to another font.
- Windows default virtual desktop shortcuts are used for workspaces (see [How it works](#how-it-works)).

### Installation

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
   | `resource/` | A folder of your choice, for example `C:\Users\<YOUR_USERNAME>\winbtw-resource\` |

4. **Edit paths.** Open each config file and check for hardcoded paths, usually pointing to a previous username or a previous folder. Replace them with your own paths, for example:
   - Image paths in `config/fastfetch/config.jsonc`
   - Icon or cursor paths in `config/yasb/.config/yasb/` (`styles.css`, `config.yaml`)
   - Any paths in `.wezterm.lua`

   Tip: search for `C:\Users\` or `resource` in each file.

5. **Set up Fastfetch.** Run it with the config:
   ```powershell
   fastfetch -c "$env:USERPROFILE\.config\fastfetch\config.jsonc"
   ```
   To use it every time, add the command to your PowerShell profile (`$PROFILE`).

6. **Set up MyDockFinder.** Install the app, find its install folder (for example `steamapps\common\mydockfinder\` if you installed it through Steam, or the folder you chose), and copy `config.ini` there, replacing the existing file. Back up the original first.

7. **Set up Windhawk.** Follow the [Windhawk](#windhawk) steps below.

8. **Restart** YASB, MyDockFinder, and Windhawk (or sign out and back in) so all changes load.

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
| **YASB** | Top status bar, styled with CSS (`styles.css`, `yasb_colors.css`). Includes its own quick search. |
| **MyDockFinder** | Dock at the bottom of the screen. |
| **Fastfetch** | Shows system info with the "kiyo" logo, for example in new terminal sessions. |
| **WezTerm** | Optional terminal, with its own theme and settings. |
| **resource/** | Component icons and cursor images. |

#### Keybindings

**winbtw custom shortcuts:**

| Shortcut | Action | From |
|---|---|---|
| `Ctrl + Alt + D` | Hide or show the Dynamic Island | Windhawk (Dynamic Island) |
| `Ctrl + Alt + Space` | Open the Dynamic Island quick search | Windhawk (Dynamic Island) |
| `Alt + Space` | Open YASB quick search (like macOS Spotlight) | YASB |
| `Alt + Shift + W` | Quick switch wallpaper | YASB |

**Windows default shortcuts used for workspaces:**

| Shortcut | Action |
|---|---|
| `Win + Ctrl + D` | Create a new virtual desktop |
| `Win + Ctrl + ←` / `→` | Switch between virtual desktops |
| `Win + Ctrl + F4` | Close the current virtual desktop |
| `Win + Tab` | Open Task View |

---

### Bahasa Indonesia

#### Pengantar dotfiles/config

**winbtw** adalah kumpulan dotfiles dan file konfigurasi yang mengubah desktop Windows 11 menjadi tampilan yang lebih rapi dan terinspirasi macOS. Isinya meliputi status bar, terminal, tampilan info sistem, dock, gaya jendela, dan overlay bergaya Dynamic Island.

Windows juga bisa punya tampilan desktop yang bagus, tidak hanya Linux.

Repositori ini berisi:

- `config/fastfetch/`: Tata letak Fastfetch, gambar logo, dan teks ASCII ("kiyo").
- `config/mydockfinder/`: Pengaturan dock MyDockFinder (`config.ini`).
- `config/wezterm/`: Konfigurasi WezTerm (`.wezterm.lua`). Opsional.
- `config/yasb/.config/yasb/`: Konfigurasi dan gaya status bar YASB (`config.yaml`, `styles.css`, `yasb_colors.css`).
- `resource/`: Ikon dan kursor komponen yang dipakai konfigurasi.
- `windhawk.txt`: Pengaturan mod Windhawk yang disalin secara manual.
- `LICENSE`: Lisensi MIT.

#### Persiapan

##### Kebutuhan

- **Sistem operasi:** Windows 11 (sudah diuji). Windows 10 mungkin bisa, tetapi belum diuji.
- **Izin:** Akses Administrator mungkin diperlukan untuk beberapa pengaturan Windhawk dan dock.

##### Software wajib

[mydockfinder](https://store.steampowered.com/app/1787090/MyDockFinder/)
[yasb](https://yasb.dev/)
[WezTerm](https://wezterm.org/index.html)
[fastfetch](https://github.com/fastfetch-cli/fastfetch)
[windhawk](https://windhawk.net/)

> **Peringatan:** Mohon gunakan lisensi MyDockFinder yang legal dan sudah dibeli. Salinan bajakan tidak didukung dan bisa mengandung malware.

##### Komponen opsional

- WezTerm: Hanya diperlukan jika Anda ingin memakai konfigurasi terminal yang disertakan.
- Font **SF Pro Display**: Dipakai oleh konfigurasi Dynamic Island (`FontFamily`). File font disimpan di `resource/fonts/`. Jika tidak dipasang, overlay akan memakai font lain.
- Shortcut desktop virtual bawaan Windows dipakai untuk workspace (lihat [Cara kerja](#cara-kerja)).

#### Instalasi

Ada dua cara untuk memasang winbtw.

##### Opsi A: Otomatis (tidak disarankan)

Cara ini menyalin seluruh folder config ke folder user Anda sekaligus. Prosesnya cepat, tetapi melewati langkah manual yang dibutuhkan beberapa aplikasi, sehingga mungkin ada yang tidak berfungsi dengan benar.

1. Clone repositori:
   ```powershell
   git clone https://github.com/wristkyion/winbtw.git
   ```
2. Salin isi folder `config/` ke `C:\Users\<NAMA_USER_ANDA>\`. Ini akan membuat folder `.config\` dan file terkait di sana.
3. Tetap lakukan langkah manual untuk [Windhawk](#windhawk-1) dan [MyDockFinder](#mydockfinder-1) di bawah. Langkah ini tidak bisa sepenuhnya otomatis.

##### Opsi B: Manual (sangat akurat, direkomendasikan)

1. **Clone repositori:**
   ```powershell
   git clone https://github.com/wristkyion/winbtw.git
   ```
2. **Pasang software wajib** yang tercantum di [Persiapan](#persiapan).
3. **Salin setiap config ke lokasinya:**

   | Sumber (di repo) | Tujuan (di PC Anda) |
   |---|---|
   | `config/yasb/.config/yasb/` | `C:\Users\<NAMA_USER_ANDA>\.config\yasb\` |
   | `config/fastfetch/` | `C:\Users\<NAMA_USER_ANDA>\.config\fastfetch\` |
   | `config/wezterm/.wezterm.lua` | `C:\Users\<NAMA_USER_ANDA>\.wezterm.lua` (opsional) |
   | `config/mydockfinder/config.ini` | Folder instalasi MyDockFinder (lihat di bawah) |
   | `resource/` | Folder pilihan Anda, misalnya `C:\Users\<NAMA_USER_ANDA>\winbtw-resource\` |

4. **Sesuaikan path.** Buka setiap file config dan periksa path yang tertulis langsung (hardcoded), biasanya mengarah ke username atau folder lama. Ganti dengan path Anda sendiri, misalnya:
   - Path gambar di `config/fastfetch/config.jsonc`
   - Path ikon atau kursor di `config/yasb/.config/yasb/` (`styles.css`, `config.yaml`)
   - Path apa pun di `.wezterm.lua`

   Tips: cari `C:\Users\` atau `resource` di setiap file.

5. **Atur Fastfetch.** Jalankan dengan config-nya:
   ```powershell
   fastfetch -c "$env:USERPROFILE\.config\fastfetch\config.jsonc"
   ```
   Agar selalu aktif, tambahkan perintah tersebut ke profil PowerShell Anda (`$PROFILE`).

6. **Atur MyDockFinder.** Pasang aplikasinya, cari folder instalasinya (misalnya `steamapps\common\mydockfinder\` jika dipasang lewat Steam, atau folder yang Anda pilih), lalu salin `config.ini` ke sana dan timpa file yang ada. Buat cadangan file aslinya terlebih dahulu.

7. **Atur Windhawk.** Ikuti langkah [Windhawk](#windhawk-1) di bawah.

8. **Mulai ulang** YASB, MyDockFinder, dan Windhawk (atau keluar lalu masuk kembali) agar semua perubahan termuat.

##### Windhawk

1. Buka Windhawk, lalu masuk ke **Settings > Advanced settings > More advanced settings > Process inclusion list**.
2. Pastikan **`dwm.exe`** ada di daftar. Mod perlu mengait ke `dwm.exe` agar berfungsi.
3. Pasang dan aktifkan mod berikut:
   - **Custom Window Corner Radius**
   - **macOS magnifying cursor**
   - **Dynamic Island for Windows**
4. Buka pengaturan tiap mod, ubah ke **text mode**, lalu tempel pengaturan yang sesuai dari `windhawk.txt`:
   - **Custom Window Corner Radius:** `radius: 15`, `smallRadius: 6`, `tooltipRadius: -1`, `roundMaximizedAndSnapped: none`
   - **macOS magnifying cursor:** `maxScalePercent: 400`, `shakeThreshold: 2500`, `lerpSpeedUpPercent: 40`, `lerpSpeedDownPercent: 15`
   - **Dynamic Island for Windows:** tempel seluruh blok dari `windhawk.txt`.

##### MyDockFinder

- Pasang MyDockFinder dan aktifkan lisensinya.
- Ganti `config.ini`-nya dengan file dari `config/mydockfinder/`, seperti dijelaskan pada langkah instalasi di atas.

---

#### Cara kerja

##### Ringkasan

| Komponen | Fungsi |
|---|---|
| **Windhawk** | Menambahkan efek visual ke Windows (sudut membulat, kursor pembesar, Dynamic Island). Mengait ke `dwm.exe`. |
| **YASB** | Status bar di bagian atas, dengan gaya CSS (`styles.css`, `yasb_colors.css`). Memiliki pencarian cepat sendiri. |
| **MyDockFinder** | Dock di bagian bawah layar. |
| **Fastfetch** | Menampilkan info sistem dengan logo "kiyo", misalnya saat membuka sesi terminal baru. |
| **WezTerm** | Terminal opsional, dengan tema dan pengaturannya sendiri. |
| **resource/** | Ikon dan gambar kursor komponen. |

##### Shortcut keyboard

**Shortcut kustom winbtw:**

| Shortcut | Aksi | Dari |
|---|---|---|
| `Ctrl + Alt + D` | Sembunyikan atau tampilkan Dynamic Island | Windhawk (Dynamic Island) |
| `Ctrl + Alt + Space` | Membuka pencarian cepat Dynamic Island | Windhawk (Dynamic Island) |
| `Alt + Space` | Membuka pencarian cepat YASB (seperti Spotlight di macOS) | YASB |
| `Alt + Shift + W` | Ganti wallpaper dengan cepat | YASB |

**Shortcut bawaan Windows untuk workspace:**

| Shortcut | Aksi |
|---|---|
| `Win + Ctrl + D` | Membuat desktop virtual baru |
| `Win + Ctrl + ←` / `→` | Berpindah antar desktop virtual |
| `Win + Ctrl + F4` | Menutup desktop virtual yang aktif |
| `Win + Tab` | Membuka Task View |

---

## License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

### Footer

Made by **wristkyion** · [github.com/wristkyion/winbtw](https://github.com/wristkyion/winbtw) · MIT License

*Windows can make a better themed desktop too, not only Linux.*