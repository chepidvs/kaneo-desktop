# Kaneo App Desktop Context

## Tujuan Utama

Membuat aplikasi desktop `Kaneo App` untuk macOS dan Windows dengan membungkus web app `https://kaneo.frmwrk.my.id/` menggunakan pendekatan Pake (Tauri), dengan fokus pada distribusi internal dan GitHub Releases.

## Ringkasan Scope

- App name: `Kaneo App`
- URL utama: `https://kaneo.frmwrk.my.id/`
- Platform target:
  - macOS Apple Silicon
  - Windows x64
- Packaging target:
  - macOS `.dmg`
  - Windows `.msi`
- Publisher/company metadata: `FRMWRK`

## Preferensi Delivery

- Alur awal: local build terlebih dulu, kemudian publish ke GitHub Releases.
- Distribusi internal tetap didukung melalui installer sharing.
- Direkomendasikan menggunakan repo desktop terpisah dari repo web Kaneo.

## Behavior Aplikasi yang Diharapkan

- Window default desktop-style, normal title bar, dan resizable.
- Session login stabil; prefer mempertahankan login (remember login) selama aman.
- Fitur native minimum yang harus jalan:
  - desktop notification
  - upload/download file
  - open external links ke browser default
  - clipboard access

## Catatan Update dan Rilis

- Perubahan konten web akan otomatis terlihat di app (karena URL live).
- Rebuild app dibutuhkan hanya jika ada perubahan shell desktop:
  - icon/branding
  - permission/native behavior
  - packaging/metadata
- Fase awal belum mewajibkan auto-update binary.

## Risiko yang Sudah Diketahui

- Build unsigned masih bisa di-install untuk macOS/Windows, tetapi akan memunculkan warning keamanan (Gatekeeper/SmartScreen).
- Jika nanti dibutuhkan distribusi luas ke user non-teknis, code signing dan notarization perlu diprioritaskan.

## Baseline Implementasi Saat Ini

- Project sudah diinisialisasi dengan `pake-cli` sebagai dependency development.
- Script build sudah tersedia di `package.json`:
  - `build:mac` (target `apple`)
  - `build:windows` (target `x64`)
  - `verify:mac`
- Verifikasi build macOS Apple Silicon sudah berhasil menghasilkan `.dmg` unsigned.
