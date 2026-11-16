# winbtw

> **Bahasa:** [English](README.md) · Bahasa Indonesia

### Pengantar dotfiles/config

**winbtw** adalah kumpulan dotfiles dan file konfigurasi yang mengubah desktop Windows 11 menjadi tampilan yang lebih rapi dan terinspirasi macOS. Isinya meliputi status bar, terminal, tampilan info sistem, dock, gaya jendela, pengganti wallpaper, dan overlay bergaya Dynamic Island.

Windows juga bisa punya tampilan desktop yang bagus, tidak hanya Linux.

Repositori ini berisi:

- `config/fastfetch/`: Tata letak Fastfetch, gambar logo, dan teks ASCII ("kiyo").
- `config/mydockfinder/`: Pengaturan dock MyDockFinder (`config.ini`).
- `config/wezterm/`: Konfigurasi WezTerm (`.wezterm.lua`). Opsional.
- `config/yasb/.config/yasb/`: Konfigurasi, gaya, dan widget wallpaper status bar YASB (`config.yaml`, `styles.css`, `yasb_colors.css`).
- `resource/`: Ikon dan kursor komponen yang dipakai konfigurasi.
- `resource/walls/`: Gambar wallpaper untuk pengganti wallpaper.
- `resource/fonts/`: File font yang dipakai konfigurasi.
- `windhawk.txt`: Pengaturan mod Windhawk yang disalin secara manual.
- `LICENSE`: Lisensi MIT.

### Persiapan

#### Kebutuhan

- **Sistem operasi:** Windows 11 (sudah diuji). Windows 10 mungkin bisa, tetapi belum diuji.
- **Izin:** Akses Administrator mungkin diperlukan untuk beberapa pengaturan Windhawk dan dock.

#### Software wajib

| Software | Tautan | Wajib |
|---|---|:---:|
| MyDockFinder | [Steam store](https://store.steampowered.com/app/1787090/MyDockFinder/) | Ya (berbayar) |
| YASB | [yasb.dev](https://yasb.dev/) | Ya |
| Windhawk | [windhawk.net](https://windhawk.net/) | Ya |
| Fastfetch | [GitHub](https://github.com/fastfetch-cli/fastfetch) | Ya |
| Modul VirtualDesktop (PowerShell) | [PowerShell Gallery](https://www.powershellgallery.com/packages/VirtualDesktop/) | Ya (untuk pengganti wallpaper, khusus Windows 11) |
| WezTerm | [wezterm.org](https://wezterm.org/index.html) | Opsional |

> **Peringatan:** Mohon gunakan lisensi MyDockFinder yang legal dan sudah dibeli. Salinan bajakan tidak didukung dan bisa mengandung malware.

#### Komponen opsional

- WezTerm: Hanya diperlukan jika Anda ingin memakai konfigurasi terminal yang disertakan.
- Font **SF Pro Display**: Dipakai oleh konfigurasi Dynamic Island (`FontFamily`). File font disimpan di `resource/fonts/`. Jika tidak dipasang, overlay akan memakai font lain.
- Shortcut desktop virtual bawaan Windows dipakai untuk workspace (lihat [Cara kerja](#cara-kerja)).

### Instalasi

Ikuti langkah-langkah berikut secara berurutan.

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
   | `resource/walls/` | `C:\Users\<NAMA_USER_ANDA>\walls\` |
   | `resource/` (file lainnya) | Folder pilihan Anda, misalnya `C:\Users\<NAMA_USER_ANDA>\winbtw-resource\` |

4. **Sesuaikan path.** Buka setiap file config dan periksa path yang tertulis langsung (hardcoded), biasanya mengarah ke username atau folder lama. Ganti dengan path Anda sendiri. Ganti setiap `<NAMA_USER_ANDA>` dengan username Windows Anda, misalnya:
   - Path gambar di `config/fastfetch/config.jsonc`
   - Path ikon atau kursor di `config/yasb/.config/yasb/` (`styles.css`, `config.yaml`)
   - Folder wallpaper di `config/yasb/.config/yasb/config.yaml` (lihat [Pengganti wallpaper](#pengganti-wallpaper))
   - Path apa pun di `.wezterm.lua`

   Tips: cari `C:\Users\` atau `resource` di setiap file.

5. **Atur pengganti wallpaper.** Lihat [Pengganti wallpaper](#pengganti-wallpaper) di bawah.

6. **Atur Fastfetch.** Jalankan dengan config-nya:
   ```powershell
   fastfetch -c "$env:USERPROFILE\.config\fastfetch\config.jsonc"
   ```
   Agar selalu aktif, tambahkan perintah tersebut ke profil PowerShell Anda (`$PROFILE`).

7. **Atur MyDockFinder.** Pasang aplikasinya, cari folder instalasinya (misalnya `steamapps\common\mydockfinder\` jika dipasang lewat Steam, atau folder yang Anda pilih), lalu salin `config.ini` ke sana dan timpa file yang ada. Buat cadangan file aslinya terlebih dahulu.

8. **Atur Windhawk.** Ikuti langkah [Windhawk](#windhawk-1) di bawah.

9. **Mulai ulang** YASB, MyDockFinder, dan Windhawk (atau keluar lalu masuk kembali) agar semua perubahan termuat.

#### Pengganti wallpaper

Pengganti wallpaper diatur di config YASB. Ada dua hal yang diperlukan:

1. **Gambar wallpaper.** Salin isi `resource/walls/` ke `C:\Users\<NAMA_USER_ANDA>\walls\`. Ganti `<NAMA_USER_ANDA>` dengan username Windows Anda.
2. **Pasang modul PowerShell VirtualDesktop.** Buka PowerShell dan jalankan:
   ```powershell
   Install-Module VirtualDesktop -Scope CurrentUser
   ```
   Modul ini menyediakan `Set-AllDesktopWallpapers`, yang dipakai pengganti wallpaper untuk mengganti wallpaper. Hanya berfungsi di Windows 11. Tanpa modul ini, pengganti wallpaper akan menampilkan error. `Set-AllDesktopWallpapers` mengganti wallpaper di semua desktop virtual, tidak hanya yang sedang aktif.

Lalu buka `C:\Users\<NAMA_USER_ANDA>\.config\yasb\config.yaml`, cari widget `wallpapers`, dan pastikan `image_path` mengarah ke folder `walls` Anda:

```yaml
  wallpapers:
    type: "yasb.wallpapers.WallpapersWidget"
    options:
      label: "<span>\ue7aa</span>"
      image_path: "C:/Users/<NAMA_USER_ANDA>/walls"
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

Ganti `<NAMA_USER_ANDA>` di `image_path` dengan username Windows Anda. Gunakan garis miring (`/`) pada path ini, seperti ditunjukkan.

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
| **YASB** | Status bar di bagian atas, dengan gaya CSS (`styles.css`, `yasb_colors.css`). Memiliki pencarian cepat dan pengganti wallpaper sendiri. |
| **MyDockFinder** | Dock di bagian bawah layar. |
| **Fastfetch** | Menampilkan info sistem dengan logo "kiyo", misalnya saat membuka sesi terminal baru. |
| **WezTerm** | Terminal opsional, dengan tema dan pengaturannya sendiri. |
| **resource/** | Ikon, gambar kursor, wallpaper (`walls/`), dan font (`fonts/`). |

##### Shortcut keyboard

**Shortcut kustom winbtw:**

| Shortcut | Aksi | Dari |
|---|---|---|
| `Ctrl + Alt + D` | Sembunyikan atau tampilkan Dynamic Island | Windhawk (Dynamic Island) |
| `Ctrl + Alt + Space` | Membuka pencarian cepat Dynamic Island | Windhawk (Dynamic Island) |
| `Alt + Space` | Membuka pencarian cepat YASB (seperti Spotlight di macOS) | YASB |
| `Alt + Shift + W` | Membuka galeri wallpaper (ganti wallpaper dengan cepat) | YASB |

**Shortcut bawaan Windows untuk workspace:**

| Shortcut | Aksi |
|---|---|
| `Win + Ctrl + D` | Membuat desktop virtual baru |
| `Win + Ctrl + ←` / `→` | Berpindah antar desktop virtual |
| `Win + Ctrl + F4` | Menutup desktop virtual yang aktif |
| `Win + Tab` | Membuka Task View |

---

### Lisensi

Proyek ini dilisensikan di bawah **MIT License**. Lihat file [LICENSE](LICENSE) untuk detailnya.
