# Decisions Log

Dokumen ini mencatat keputusan penting proyek desktop Kaneo agar perubahan scope dan teknis tetap ter-trace.

## D-001 - Pilih Pake (Tauri-based) sebagai wrapper desktop

- Status: accepted
- Tanggal: 2026-05-16
- Context: Dibutuhkan cara cepat dan ringan untuk mengubah web app Kaneo menjadi aplikasi desktop lintas platform.
- Decision: Menggunakan Pake sebagai basis wrapper desktop.
- Consequences:
  - Build lebih ringan dibanding pendekatan Electron pada umumnya.
  - Konfigurasi desktop shell (window/icon/permission/package) menjadi fokus utama.

## D-002 - Target platform rilis awal

- Status: accepted
- Tanggal: 2026-05-16
- Context: Kebutuhan deployment saat ini fokus ke device tim internal.
- Decision:
  - macOS Apple Silicon
  - Windows x64
- Consequences:
  - Pipeline build difokuskan pada dua target ini.
  - Target lain (Linux, Intel macOS, Windows ARM) di luar scope awal.

## D-003 - Strategi distribusi dan repository

- Status: accepted
- Tanggal: 2026-05-16
- Context: Rilis desktop sebaiknya tidak mengganggu workflow repo web utama.
- Decision:
  - Build lokal lebih dulu.
  - Distribusi melalui internal sharing dan GitHub Releases.
  - Desktop app direkomendasikan berada di repository terpisah.
- Consequences:
  - Versioning artifacts desktop lebih bersih.
  - CI/CD desktop dapat dikelola independen dari web app.

## D-004 - Kebijakan signing fase awal

- Status: accepted
- Tanggal: 2026-05-16
- Context: Belum tersedia Apple Developer certificate dan Windows code-signing certificate.
- Decision: Mengizinkan unsigned build untuk fase validasi internal.
- Consequences:
  - User akan melihat warning keamanan saat install/open aplikasi.
  - Code signing/notarization menjadi backlog untuk readiness distribusi lebih luas.

## D-005 - Strategi update

- Status: accepted
- Tanggal: 2026-05-16
- Context: Aplikasi membungkus URL live sehingga konten berubah dinamis.
- Decision:
  - Tidak mewajibkan auto-update binary di fase awal.
  - Perubahan web tidak memerlukan rilis desktop baru.
- Consequences:
  - Rilis desktop baru hanya saat ada perubahan shell/native/package metadata.

## D-006 - Baseline toolchain dan command build proyek

- Status: accepted
- Tanggal: 2026-05-16
- Context: Diperlukan setup yang repeatable untuk build lokal macOS/Windows.
- Decision:
  - Inisialisasi project Node lokal dengan dependency `pake-cli`.
  - Menyediakan script build di `package.json`:
    - `build:mac` untuk target Apple Silicon
    - `build:windows` untuk target Windows x64
    - `verify:mac` untuk verifikasi minimum build macOS
  - Mengabaikan artifact installer (`*.dmg`, `*.msi`) di `.gitignore`.
- Consequences:
  - Build command menjadi konsisten dan mudah dipakai ulang.
  - Artifact besar tidak ikut ter-commit ke repository.

## D-007 - Hasil verifikasi build awal macOS

- Status: accepted
- Tanggal: 2026-05-16
- Context: Perlu validasi bahwa baseline project bisa menghasilkan installer.
- Decision: Menjalankan verifikasi `npm run verify:mac` dan menerima output unsigned untuk fase awal.
- Consequences:
  - Installer `.dmg` berhasil dihasilkan.
  - Notarization masih dilewati karena kredensial Apple belum tersedia.

## D-008 - Gunakan icon brand lokal untuk build Kaneo App

- Status: accepted
- Tanggal: 2026-05-16
- Context: Branding aplikasi perlu konsisten dengan identitas FRMWRK.
- Decision:
  - Menggunakan file icon lokal `assets/icon.png` pada command build macOS dan Windows.
  - Menjalankan ulang verifikasi build macOS setelah update icon.
- Consequences:
  - Artifact build berikutnya menggunakan icon brand yang disediakan tim.
  - Script build tetap sederhana dan repeatable via `package.json`.

## D-009 - Build Windows tidak dilakukan lokal di host macOS ini

- Status: accepted
- Tanggal: 2026-05-16
- Context: Percobaan `npm run build:windows` dari macOS menghasilkan target `x86_64-apple-darwin` dan gagal karena target Rust terkait belum terpasang, serta bukan jalur ideal untuk menghasilkan `.msi`.
- Decision: Menetapkan build Windows x64 dijalankan pada runner Windows (CI) agar output `.msi` konsisten.
- Consequences:
  - Verifikasi Windows dipindahkan ke GitHub Actions.
  - Build lokal macOS tetap fokus pada output `.dmg`.

## D-010 - Gunakan workflow GitHub Actions untuk artifact lintas platform

- Status: accepted
- Tanggal: 2026-05-16
- Context: Diperlukan pipeline repeatable untuk build macOS + Windows dan publikasi rilis.
- Decision:
  - Menambahkan workflow `.github/workflows/release.yml`.
  - Job macOS menghasilkan `.dmg` pada `macos-14`.
  - Job Windows menghasilkan `.msi` pada `windows-latest`.
  - Saat push tag `v*`, artifact dipublikasikan ke GitHub Release.
- Consequences:
  - Build lintas platform tidak bergantung mesin lokal.
  - Release process menjadi lebih stabil dan mudah diulang.

## D-011 - Inisialisasi repository git dan hubungkan remote GitHub

- Status: accepted
- Tanggal: 2026-05-16
- Context: Repo GitHub desktop sudah dibuat di `https://github.com/chepidvs/kaneo-desktop` dan project lokal perlu dihubungkan.
- Decision:
  - Inisialisasi git di project lokal.
  - Set remote `origin` ke `https://github.com/chepidvs/kaneo-desktop.git`.
- Consequences:
  - Project siap untuk proses commit/push ke repo desktop terpisah.

## D-012 - Tambah README operasional build dan release

- Status: accepted
- Tanggal: 2026-05-16
- Context: Tim membutuhkan panduan cepat untuk build lokal dan publish release.
- Decision: Menambahkan `README.md` berisi prasyarat, command build, dan alur release berbasis tag.
- Consequences:
  - Onboarding lebih cepat.
  - Risiko salah langkah saat release berkurang.
