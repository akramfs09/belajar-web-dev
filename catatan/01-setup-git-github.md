# Panduan Lengkap Setup Git, GitHub CLI & Alur Kerja Web Developer

Dokumen ini adalah rangkuman lengkap dari proses belajar dari nol: mulai dari instalasi, konfigurasi, pengertian perintah (command), solusi error yang dihadapi, hingga alur kerja harian. Menggunakan Windows, VS Code, dan Git Bash (dengan environment Laragon di `C:/laragon/www/`).

## 1. Instalasi Tools (Jika menggunakan laptop baru)
Jika suatu saat harus menginstal ulang Windows, buka terminal dan jalankan:

```bash
# 1. Instal Git
winget install --id Git.Git

# 2. Instal VS Code
winget install --id Microsoft.VisualStudioCode

# 3. Instal GitHub CLI (gh)
winget install --id GitHub.cli