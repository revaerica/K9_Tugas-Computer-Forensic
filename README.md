# Computer Forensics - Kelompok 9

- **Operating System:** Windows 11 (dijalankan di VirtualBox VM)
- **Disk Image Format:** Raw (.img), dikompres dalam .zip (`kel9_windows.zip`)
- **Image Name:** `kel9_windows.img`
- **Disk Capacity:** 256 MB (satu volume NTFS, label `KASUS-KEL9`)
- **SHA-256 (kel9_windows.img):** `92F4A235B023E0F5912598D327BC1D1A8EF20F5F76DF9958ACA3FD595BAE2F69`
- - **Link:** https://drive.google.com/file/d/11oS3yfCz9Ysj68rrp6DZ2dGgKBNav6qZ/view?usp=drive_link

## Anggota Kelompok 9
| No. | Nama | NRP |
|---:|---|---|
| 1 | Almendo Jekson Darwin Naftali Kambu | 5027221073 |
| 2 | M. Abhinaya Al Faruqi | 5027231011 |
| 3 | Revalina Erica P. | 5027241007 |
| 4 | Salsa Bil Ulla | 5027241052 |
| 5 | Raynard Carlent | 5027241109 |

## Deskripsi Kasus

### Perubahan Harga pada Dokumen Tender

CV Maju Bersama sedang mengikuti tender pengadaan perangkat jaringan. Satu komputer kantor dipakai bergantian oleh dua staf, `budi` dan `titut`, untuk menyiapkan dokumen penawaran. Menjelang batas pengumpulan berkas, angka harga penawaran dicurigai berubah dari versi awal. Selain itu, ada catatan harga yang disimpan dengan cara tidak biasa, dan beberapa berkas yang berkaitan dengan penawaran sudah tidak ada di tempat semula.

Tugas investigator adalah merekonstruksi apa yang terjadi pada komputer tersebut berdasarkan image disk yang berhasil diamankan.

## Target Investigasi
1. Menemukan file yang **terhapus** (termasuk yang sudah dihapus permanen), **tersembunyi**, dan **termodifikasi** dengan keyword `penawaran`.
2. Mengidentifikasi **username** yang melakukan perubahan tersebut, **kapan** hal itu terjadi (timestamp), dan bukti pendukung lain yang dianggap perlu.

## Catatan
- Image dibuat dari komputer Windows 11 yang sebenarnya (VM), bukan hasil rekayasa file system, sehingga artefak Windows (Recycle Bin, atribut file, MFT, dan sebagainya) muncul secara alami.
- Pada root volume terdapat `security_log.evtx`, hasil ekspor Windows Security log selama aktivitas berlangsung. Log ini memuat pencatatan akses file (Event ID 4663) yang dapat dipakai untuk menghubungkan file dengan username dan waktu.
- Tidak semua jejak file bisa dipulihkan isinya. File yang dihapus permanen mungkin hanya meninggalkan jejak berupa nama di log, sehingga perlu dikorelasikan dengan artefak lain.
- Perhatikan zona waktu saat membandingkan timestamp file dengan log (WIB = UTC+7). Event Viewer menampilkan waktu lokal, sedangkan sebagian tool menampilkan UTC.
- Tidak semua file yang mengandung keyword merupakan bukti. Perlu dipilah mana yang relevan.
- Nama dan ekstensi file tidak selalu mencerminkan isinya.

## Tools yang Disarankan
Autopsy, FTK Imager, Sleuth Kit (`fls`, `istat`, `icat`), Event Viewer atau parser evtx (mis. python-evtx, EvtxECmd).
