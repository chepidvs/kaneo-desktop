# Kaneo Desktop App

Desktop wrapper untuk `https://kaneo.frmwrk.my.id/` menggunakan Pake (Tauri).

## Stack

- Pake CLI (`pake-cli`)
- Tauri (dibawa oleh Pake)

## Prasyarat

- Node.js 22+
- npm

## Build Lokal

Install dependency:

```bash
npm ci
```

Build macOS Apple Silicon (`.dmg`):

```bash
npm run build:mac
```

Build Windows x64 (`.msi`):

```bash
npm run build:windows
```

Catatan: build Windows sebaiknya dijalankan di runner Windows (GitHub Actions) untuk hasil `.msi` yang konsisten.

## Release GitHub

Workflow release ada di `.github/workflows/release.yml`.

Trigger:

- Manual (`workflow_dispatch`)
- Otomatis saat push tag `v*` (contoh `v1.0.0`)

Contoh rilis:

```bash
git tag v1.0.0
git push origin v1.0.0
```

Workflow akan build:

- macOS `.dmg`
- Windows `.msi`

Lalu upload keduanya ke GitHub Release.
