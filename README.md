# endok-updates

Repo **public** khusus manifest & paket hot-update EnDok Browser.
Source code aplikasi tetap berada di repo private `fizardstudio/EnDok`.

Aplikasi membaca:
`https://raw.githubusercontent.com/fizardstudio/endok-updates/main/update.json`

## Cara rilis versi baru (mis. 1.0.3)
1. Di project EnDok: ubah `version` di `package.json`, lalu `npm run compile`, lalu `.\create_update_zip.ps1`
   → menghasilkan `update-v1.0.3.zip` + mencetak `SHA256CHECKSUM=...`
2. Di repo ini: buat Release dengan tag `v1.0.3`, upload `update-v1.0.3.zip`
3. Edit `update.json`: `version`, `hot_update_url` (ke asset release), `checksum` (huruf kecil/besar bebas)
4. Commit & push ke `main`. Semua laptop akan update otomatis saat launch berikutnya.

Catatan: jika download gagal 2x untuk versi yang sama, aplikasi berhenti mencoba
(`%APPDATA%\endok-browser\updates\failed_update.json`). Perbaiki release, lalu
hapus file itu di laptop (atau rilis versi lebih baru) agar dicoba lagi.
