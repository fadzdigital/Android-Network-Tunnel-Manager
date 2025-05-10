# Android Network Tunnel Manager

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Android-brightgreen.svg" alt="Platform">
  <img src="https://img.shields.io/badge/Requires-Magisk-red.svg" alt="Requires">
  <img src="https://img.shields.io/badge/Version-1.0.0-blue.svg" alt="Version">
  <img src="https://img.shields.io/badge/License-MIT-orange.svg" alt="License">
</p>

<p align="center">
  <img src="https://i.imgur.com/EjXoOFH.png" alt="Logo" width="200">
</p>

## 📱 Tentang Modul

Android Network Tunnel Manager adalah modul Magisk yang memungkinkan Anda mengelola tunnel jaringan dan routing dengan mudah pada perangkat Android yang sudah di-root. Modul ini secara otomatis mengatur iptables, routing, dan DNS forwarding untuk memastikan koneksi jaringan berjalan melalui tunnel yang ditentukan.

### 🎯 Fitur Utama

- **Otomatis Saat Boot**: Konfigurasi jaringan dilakukan secara otomatis saat boot
- **Pengaturan Tunnel**: Mengelola interface tunnel (tun0) dan aturan routing terkait
- **Konfigurasi Firewall**: Mengatur iptables untuk mengontrol aliran traffic
- **Pengalihan DNS**: Mengarahkan permintaan DNS ke server Cloudflare (1.1.1.1)
- **Pencegahan Kebocoran Data**: Menangani traffic IPv6 untuk mencegah kebocoran data
- **Pemantauan Jaringan**: Menyesuaikan konfigurasi secara otomatis saat terjadi perubahan jaringan
- **Optimasi Hotspot**: Mendukung tethering/hotspot melalui tunnel yang dikonfigurasi
- **Logging**: Mencatat aktivitas untuk memudahkan pemecahan masalah

## ⚙️ Cara Kerja

Modul ini menggunakan teknik routing canggih untuk:

1. **Membuat Koneksi Terisolasi**: Membuat jalur khusus untuk traffic jaringan
2. **Mengarahkan Lalu Lintas**: Mengalihkan semua traffic melalui tunnel yang ditentukan
3. **Mengontrol DNS**: Mengelola permintaan DNS untuk mencegah kebocoran data
4. **Monitoring Perubahan**: Menyesuaikan konfigurasi secara otomatis saat jaringan berubah

## 📋 Persyaratan

- Android 7.0+
- Magisk 20.4+
- Perangkat sudah di-root

## 🚀 Cara Instalasi

### Metode 1: Instalasi Melalui Magisk Manager

1. Unduh file zip modul dari [Releases](https://github.com/YourUsername/android-tunnel-manager/releases)
2. Buka aplikasi **Magisk Manager**
3. Tap pada tab **Modules**
4. Tap pada tombol **+** di bagian bawah
5. Pilih file zip modul yang telah diunduh
6. Tunggu hingga proses instalasi selesai
7. Tap **Reboot** ketika diminta

### Metode 2: Instalasi Melalui TWRP Recovery

1. Unduh file zip modul dari [Releases](https://github.com/YourUsername/android-tunnel-manager/releases)
2. Boot perangkat ke TWRP Recovery
3. Tap **Install**
4. Pilih file zip modul yang telah diunduh
5. Geser slider untuk konfirmasi instalasi
6. Tap **Reboot System** setelah instalasi selesai

## 📱 Penggunaan

Setelah instalasi dan restart, modul akan berjalan secara otomatis di latar belakang. Tidak diperlukan konfigurasi tambahan. Modul akan:

1. Melakukan setup tunnel saat boot
2. Memantau perubahan jaringan secara real-time
3. Menyesuaikan konfigurasi secara otomatis

### Konfigurasi Tambahan (Opsional)

Jika Anda ingin mengubah konfigurasi default:

1. Gunakan aplikasi root file manager untuk mengakses:
   ```
   /data/adb/modules/androidtunnelmanager/system/bin/tunnel_manager.sh
   ```

2. Edit parameter sesuai kebutuhan:
   - `TUN_NAME`: Nama interface tunnel (default: tun0)
   - DNS Server: Alamat DNS yang digunakan (default: 1.1.1.1)

3. Simpan perubahan dan restart perangkat

## 📊 Monitoring & Troubleshooting

### Melihat Log

Modul menyimpan log aktivitas di:
```
/sdcard/tunnel_manager.log
```

Anda dapat melihat log ini untuk memantau aktivitas modul atau mendiagnosis masalah.

### Perintah Debugging

Untuk memeriksa status tunnel:
```bash
su -c "ip addr show tun0"
```

Untuk memeriksa aturan routing:
```bash
su -c "ip rule list"
```

Untuk memeriksa aturan iptables:
```bash
su -c "iptables -L -n -v"
```

### Masalah Umum

| Masalah | Solusi |
|---------|--------|
| Modul tidak aktif setelah boot | Pastikan Magisk sudah versi terbaru dan coba instalasi ulang modul |
| Koneksi internet tidak berfungsi | Periksa log untuk error dan pastikan interface tun0 aktif |
| Hotspot tidak berfungsi | Pastikan IP forwarding diaktifkan dan tidak ada firewall yang memblokir |
| Konflik dengan aplikasi VPN | Nonaktifkan aplikasi VPN lain terlebih dahulu |

## 🔄 Pembaharuan

Untuk memperbarui modul:

1. Unduh versi terbaru dari [Releases](https://github.com/YourUsername/android-tunnel-manager/releases)
2. Ikuti langkah instalasi seperti di atas
3. Modul lama akan otomatis digantikan dengan versi baru

## 🛠️ Pengembangan & Kontribusi

Jika Anda ingin berkontribusi pada pengembangan modul:

1. Fork repositori ini
2. Buat branch baru untuk fitur Anda
3. Commit perubahan Anda
4. Push ke branch Anda
5. Buat Pull Request

### Struktur Modul

```
NetworkTunnelModule/
├── META-INF/                    # Instalasi Magisk
│   └── com/google/android/      
│       └── update-binary        # Installer
│       └── updater-script       # Identifier
├── common/                      # Script umum
│   ├── service.sh               # Dijalankan saat boot
│   └── post-fs-data.sh          # Dijalankan saat early-boot
├── module.prop                  # Metadata modul
├── system/                      # File sistem
│   └── bin/                     
│       └── tunnel_manager.sh    # Script utama
├── config.sh                    # Konfigurasi modul
└── uninstall.sh                 # Untuk uninstall
```

## ⚠️ Peringatan

**PENTING**: Penggunaan modul ini dapat melanggar Ketentuan Layanan dari penyedia layanan telekomunikasi Anda. Modul ini disediakan hanya untuk tujuan pendidikan dan pengembangan. Penulis dan kontributor tidak bertanggung jawab atas penyalahgunaan atau konsekuensi dari penggunaan modul ini. Gunakan dengan risiko Anda sendiri.

## ❓ FAQ

<details>
<summary><b>Apakah modul ini akan membuat baterai lebih cepat habis?</b></summary>
<p>
Modul ini dirancang untuk efisien dan memiliki dampak minimal pada baterai. Namun, karena modul ini menangani routing jaringan secara aktif, ada kemungkinan terjadi peningkatan konsumsi baterai yang sedikit.
</p>
</details>

<details>
<summary><b>Apakah modul ini kompatibel dengan ROM custom?</b></summary>
<p>
Ya, modul ini kompatibel dengan sebagian besar ROM custom selama ROM tersebut mendukung Magisk dan perangkat sudah di-root.
</p>
</details>

<details>
<summary><b>Apakah modul ini dapat menyebabkan bootloop?</b></summary>
<p>
Risiko bootloop minimal karena modul ini hanya aktif setelah sistem boot selesai. Namun, jika terjadi masalah, Anda dapat menonaktifkan modul melalui Magisk Manager di safe mode.
</p>
</details>

<details>
<summary><b>Bagaimana cara menonaktifkan modul ini sementara?</b></summary>
<p>
Buka Magisk Manager, masuk ke tab Modules, dan nonaktifkan modul ini. Restart perangkat untuk menerapkan perubahan.
</p>
</details>

<details>
<summary><b>Apakah modul ini bekerja dengan semua aplikasi VPN?</b></summary>
<p>
Modul ini dirancang untuk bekerja dengan aplikasi VPN yang menggunakan interface tun0. Mungkin terjadi konflik dengan beberapa aplikasi VPN tertentu.
</p>
</details>

## 📜 Lisensi

```
MIT License

Copyright (c) 2025 YourUsername

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

## 🤝 Ucapan Terima Kasih

Terima kasih kepada:
- Komunitas Magisk atas framework yang luar biasa
- Semua kontributor dan penguji yang telah membantu pengembangan modul ini
- Anda yang telah menggunakan dan memberikan masukan untuk modul ini

---

<p align="center">
  <b>Jika Anda menyukai modul ini, berikan bintang di GitHub!</b>
  <br>
  <a href="https://github.com/YourUsername/android-tunnel-manager">
    <img src="https://img.shields.io/github/stars/YourUsername/android-tunnel-manager?style=social" alt="GitHub stars">
  </a>
</p>
