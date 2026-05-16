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
| T-005 | Build Windows x64 (`.msi`) | done | agent | Sukses lewat GitHub Actions release pipeline |
| T-006 | Verifikasi behavior wajib (login persistence, upload/download, notification, external links, clipboard) | pending | agent | Uji smoke test lintas platform |
| T-007 | Persiapan alur GitHub Releases | done | agent | Pipeline release lintas platform sudah berjalan |
| T-008 | Evaluasi code signing/notarization untuk fase berikutnya | pending | agent | Backlog readiness distribusi publik |
| T-009 | Implementasi workflow GitHub Actions untuk build/release lintas platform | done | agent | Workflow `.github/workflows/release.yml` ditambahkan |
| T-010 | Inisialisasi git repo lokal dan set remote ke GitHub desktop repo | done | agent | Remote `origin` sudah diset ke `chepidvs/kaneo-desktop` |
| T-011 | Tambah README build + release operasional | done | agent | README baseline sudah tersedia |
| T-012 | Tambah `CHANGELOG.md` untuk catatan rilis | done | agent | Versi `1.0.0` sudah dicatat |
