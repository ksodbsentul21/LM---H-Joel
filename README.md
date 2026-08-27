# Last Mile - H Joel Logistics (GitHub PWA + Google Sheets)

## Isi paket
- `index.html` – aplikasi utama PWA untuk Android/iPhone.
- `manifest.json` + `sw.js` – instalasi PWA.
- `logo.png`, `icon-192.png`, `icon-512.png` – identitas aplikasi.
- `Code.gs` – backend Google Apps Script untuk login, validation, simpan data dan foto.

## Sheet yang digunakan
Spreadsheet ID sudah terpasang di `Code.gs`: `1NHKxvn0TDP_lcVX9RcLM1-IKy6o_5yTvSteZdMo5Fo0`.
Nama tab yang diharapkan:
- `Validation` – Vendor A2:A20 dan Keterangan D4:D9
- `Username` – Username A2:A dan Origin B2:B
- `Outbound`
- `BAST Back`
- `Return`

> Jika nama tab Anda berbeda, ubah konstanta `CONFIG` pada bagian paling atas `Code.gs`.

## 1. Deploy Google Apps Script
1. Buka Google Sheet → Extensions → Apps Script.
2. Hapus kode lama dan tempel seluruh isi `Code.gs`.
3. Project Settings → Time zone: `Asia/Jakarta`.
4. Klik **Deploy → New deployment → Web app**.
5. Execute as: **Me**.
6. Who has access: **Anyone**.
7. Authorize akses Spreadsheet dan Google Drive.
8. Salin URL deployment yang berakhir `/exec`.

## 2. Sambungkan frontend
Buka `index.html`, cari:
`const API_URL = 'PASTE_APPS_SCRIPT_WEB_APP_URL_HERE';`
Ganti dengan URL `/exec` tadi.

## 3. Upload ke GitHub
Upload ke root repository:
`index.html`, `manifest.json`, `sw.js`, `logo.png`, `icon-192.png`, `icon-512.png`.
Aktifkan **Settings → Pages → Deploy from branch → main / root**.

## 4. Install di HP
- Android Chrome: buka GitHub Pages → menu ⋮ → **Install app / Add to Home screen**.
- iPhone Safari: Share → **Add to Home Screen**.

## Catatan Foto SN
Aplikasi mencoba membaca barcode/QR dari foto SN terlebih dahulu. Jika tidak ada barcode, aplikasi menjalankan OCR teks. Hasil SN bisa dikoreksi secara manual bila pembacaan tidak akurat.

## Data yang disimpan
- Outbound: Tanggal, Timestamp, User, Origin, AWB, Driver, Plat, Vendor, Foto Driver, No SN, Foto SN.
- BAST Back: Tanggal, Timestamp, User, Origin, AWB, Driver, Plat, Vendor, Foto Driver.
- Return: Tanggal, Timestamp, User, Origin, AWB, Driver, Plat, Vendor, Keterangan, Reason, Foto SN.

Foto disimpan otomatis ke folder Google Drive `Last Mile - H Joel Photos`, kemudian URL-nya dicatat di Google Sheet.
