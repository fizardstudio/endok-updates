# endok-updates

Repo khusus manifest & paket hot-update EnDok Browser.
Source code aplikasi tetap berada di repo private `fizardstudio/EnDok`.

> ⚠️ Agar auto-update berjalan, repo ini **harus public**. Kalau masih private,
> `raw.githubusercontent.com` mengembalikan 404 dan aplikasi tidak bisa update.

Aplikasi membaca:
`https://raw.githubusercontent.com/fizardstudio/endok-updates/main/update.json`

## Cara rilis versi baru (mis. 1.0.3)
1. Di project EnDok: ubah `version` di `package.json`, lalu `npm run compile`, lalu `.\create_update_zip.ps1`
   → menghasilkan `update-v1.0.3.zip` + mencetak `SHA256CHECKSUM=...`
2. Di repo ini: letakkan `update-v1.0.3.zip` langsung di root repo (commit ke `main`). Zip kecil (~1 MB) aman di git.
3. Edit `update.json`:
   - `version` → `1.0.3`
   - `hot_update_url` → `https://raw.githubusercontent.com/fizardstudio/endok-updates/main/update-v1.0.3.zip`
   - `checksum` → nilai SHA-256 dari langkah 1 (huruf besar/kecil bebas)
4. Commit & push ke `main`. Semua laptop akan update otomatis saat launch berikutnya.

Zip versi lama boleh dihapus dari repo setelah semua laptop naik versi, biar repo tetap ramping.

## Anti-loop
Jika download/ekstraksi gagal 2x untuk versi yang sama, aplikasi berhenti mencoba
dan mencatatnya di `%APPDATA%\endok-browser\updates\failed_update.json`.
Perbaiki paket lalu rilis versi lebih baru (atau hapus file itu di laptop) agar dicoba lagi.
