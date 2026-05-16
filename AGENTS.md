# AGENTS.md

Dokumen ini adalah pedoman kerja agent untuk proyek desktop `Kaneo App` berbasis web wrapper (Pake/Tauri).

## Project Identity

- App name: `Kaneo App`
- Target URL: `https://kaneo.frmwrk.my.id/`
- Platform target:
  - macOS Apple Silicon
  - Windows x64
- Publisher/Company: `FRMWRK`

## Delivery Goals

- Build lokal terlebih dulu, lalu distribusi via GitHub Releases.
- Distribusi internal tetap didukung (manual installer sharing).
- Repositori desktop disarankan terpisah dari repo web Kaneo utama agar rilis, CI, dan artifacts lebih terkontrol.

## Product Behavior Requirements

- Window default desktop-style (normal title bar, resizable).
- Session login harus stabil dan mempertahankan login (remember login) selama aman.
- Native capability minimum:
  - desktop notification
  - upload/download file
  - open external links ke browser default
  - clipboard access

## Packaging and Release Baseline

- macOS package: `.dmg`
- Windows package: `.msi`
- Fase awal: unsigned build diperbolehkan untuk validasi produk internal.
- Catatan: unsigned installer mungkin memunculkan warning keamanan (Gatekeeper/SmartScreen).

## Update Strategy

- Konten web berubah -> app otomatis mengikuti (karena app membungkus URL live).
- Rebuild app hanya untuk perubahan shell desktop (ikon, permission, native behavior, packaging, metadata).
- Auto-update binary lintas versi desktop belum diwajibkan di fase awal.

## RTK Mandatory

RTK di konteks proyek ini mengacu ke: `https://github.com/rtk-ai/rtk`.

Setiap agent WAJIB menjalankan aturan berikut pada tiap task:

1. Tulis tujuan task + acceptance criteria sebelum implementasi.
2. Lakukan risk/security impact check sebelum eksekusi.
3. Setelah perubahan, lakukan verifikasi minimum (build/test yang relevan).
4. Jika ada keputusan baru, update `docs/decisions.md`.
5. Update status task pada `docs/todo.md` dengan status `pending`, `in_progress`, atau `done`.

Tambahan praktik RTK:

- Gunakan pendekatan hemat konteks saat eksekusi command-line.
- Jika RTK tersedia di environment, prioritaskan command RTK (`rtk git status`, `rtk git diff`, dll.) untuk output yang lebih ringkas.
- Jika RTK belum tersedia, lanjutkan dengan command standar namun tetap ringkas dalam pelaporan hasil.

## Working Rules

- Jangan menyimpan secret di repo.
- Gunakan keputusan yang sudah tercatat di `docs/decisions.md` sebagai sumber kebenaran.
- Jangan ubah scope utama tanpa menulis decision baru.
- Pastikan semua pekerjaan ter-trace di `docs/todo.md`.
