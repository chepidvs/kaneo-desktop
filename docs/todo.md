# Task Tracker

Dokumen ini melacak pekerjaan proyek desktop Kaneo.

Status yang dipakai:

- `pending`
- `in_progress`
- `done`

## Active Tasks

| ID | Task | Status | Owner | Notes |
| --- | --- | --- | --- | --- |
| T-001 | Inisialisasi dokumen baseline (`AGENTS.md`, `docs/context.md`, `docs/decisions.md`, `docs/todo.md`) | done | agent | Baseline docs selesai dibuat |
| T-002 | Setup struktur project desktop Kaneo berbasis Pake | done | agent | `npm init` + `pake-cli` + script build berhasil dibuat |
| T-003 | Konfigurasi metadata app (name, icon, publisher FRMWRK, target URL) | done | agent | Name/URL/window baseline + icon `assets/icon.png` sudah diterapkan |
| T-004 | Build lokal macOS Apple Silicon (`.dmg`) | done | agent | Verifikasi `npm run verify:mac` sukses |
| T-005 | Build Windows x64 (`.msi`) | in_progress | agent | Build lokal macOS gagal; dialihkan ke CI Windows runner |
| T-006 | Verifikasi behavior wajib (login persistence, upload/download, notification, external links, clipboard) | pending | agent | Uji smoke test lintas platform |
| T-007 | Persiapan alur GitHub Releases | pending | agent | Disarankan repo terpisah |
| T-008 | Evaluasi code signing/notarization untuk fase berikutnya | pending | agent | Backlog readiness distribusi publik |
| T-009 | Implementasi workflow GitHub Actions untuk build/release lintas platform | done | agent | Workflow `.github/workflows/release.yml` ditambahkan |
| T-010 | Inisialisasi git repo lokal dan set remote ke GitHub desktop repo | done | agent | Remote `origin` sudah diset ke `chepidvs/kaneo-desktop` |
| T-011 | Tambah README build + release operasional | done | agent | README baseline sudah tersedia |
