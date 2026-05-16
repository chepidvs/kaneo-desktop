# Changelog

Semua perubahan penting pada proyek ini dicatat di file ini.

Format mengacu pada prinsip Keep a Changelog, dan versi mengikuti Semantic Versioning sejauh relevan untuk fase proyek saat ini.

## [1.0.0] - 2026-05-16

### Added

- Inisialisasi project desktop `Kaneo App` berbasis Pake (`pake-cli`) dengan target URL `https://kaneo.frmwrk.my.id/`.
- Script build lokal untuk macOS Apple Silicon dan Windows x64 pada `package.json`.
- Konfigurasi build baseline: app name, title, ukuran default, minimum size, dan icon brand `assets/icon.png`.
- Workflow GitHub Actions untuk build lintas platform dan publish asset ke GitHub Releases saat push tag `v*`.
- Dokumen operasional dan governance proyek:
  - `AGENTS.md`
  - `docs/context.md`
  - `docs/decisions.md`
  - `docs/todo.md`
  - `README.md`

### Changed

- Strategi build Windows dialihkan dari local macOS ke runner Windows pada CI untuk hasil `.msi` yang konsisten.

### Notes

- Build saat ini masih unsigned (tanpa code signing/notarization), sehingga warning keamanan OS dapat muncul saat instalasi.
