# KlatPack — feed update (publik)

Repo ini **hanya** berisi manifest update `latest.json` dan installer KlatPack sebagai
asset release. Kode aplikasi & alat keygen ada di repo private terpisah.

URL yang dibaca aplikasi (lihat `Services/UpdateService.cs`):

```
https://github.com/Brevalda1/klatda-pack-updates/releases/latest/download/latest.json
```

## Cara merilis versi baru

1. Di repo aplikasi:

   ```powershell
   powershell -NoProfile -ExecutionPolicy Bypass -File tools\publish.ps1 `
       -Version 1.0.1 -Notes "Perbaikan tampilan galeri"
   ```

   Hasil: `dist\KlatPack-Setup-1.0.1.exe` + `dist\latest.json` (sudah ditandatangani).

2. Buat release baru di repo ini dengan tag **`v1.0.1`**.
3. Upload **dua** file: `KlatPack-Setup-1.0.1.exe` dan `latest.json`.
4. Publish release. Klien akan mendeteksinya pada pemeriksaan berikutnya
   (otomatis maksimal 1x/24 jam, atau langsung lewat tombol **CEK UPDATE**).

> Jangan ubah `latest.json` secara manual. Tanda tangan ECDSA P-256 di dalamnya
> membuat aplikasi menolak manifest/installer yang tidak ditandatangani `update.key`.
> Kalau `update.key` hilang, klien lama harus diberi installer manual sekali.

## Isi manifest

```json
{
  "version": "1.0.1",
  "url": "https://github.com/.../KlatPack-Setup-1.0.1.exe",
  "sha256": "...",
  "notes": "catatan rilis",
  "mandatory": false,
  "sig": "tanda tangan ECDSA atas version|url|sha256|mandatory"
}
```
