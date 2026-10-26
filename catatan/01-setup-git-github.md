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
```
*(Setelah instalasi, tutup dan buka kembali VS Code agar semua perintah dikenali).*

## 2. Konfigurasi Awal (Sekali Seumur Hidup)
Buka **Git Bash** di VS Code (Pilih Git Bash sebagai default terminal).

**A. Atur Identitas Git:**
```bash
git config --global user.name "Akram"
git config --global user.email "akramsuwandi@students.amikom.ac.id"
```
*(Cek dengan `git config --global user.name` untuk memastikan).*

**B. Login ke GitHub via Terminal:**
```bash
gh auth login
```
*Panduan menjawab pertanyaan di terminal:*
1. Where do you use GitHub? -> Pilih **GitHub.com**
2. Preferred protocol? -> Pilih **HTTPS**
3. Authenticate Git with credentials? -> Pilih **Yes**
4. How would you like to authenticate? -> Pilih **Login with a web browser**
5. Copy kode (contoh: `A430-C008`). Jika browser tidak terbuka otomatis, buka browser manual ke `https://github.com/login/device`, paste kode, lalu Authorize.
6. Jika muncul `✓ Logged in as akramfs09`, login berhasil.

---

## 3. Kamus Lengkap Command (Cheat Sheet)

### A. Perintah Navigasi Terminal (Git Bash)
* `ls` : *List*. Melihat isi folder.
* `cd /d/belajar-web-dev` : *Change Directory*. Pindah folder (di Git Bash, drive D ditulis `/d/`).
* `rm -rf .git` : Menghapus folder `.git` secara paksa untuk memulai ulang repositori Git dari nol (file kodemu tetap aman).

### B. Perintah Inti Git (Lokal)
* `git init` : Membuat repositori Git baru di folder saat ini (membuat folder tersembunyi `.git`).
* `git status` : Melihat status file (merah = belum di-track, hijau = siap di-commit).
* `git add .` : Memasukkan **semua** file yang berubah ke *Staging Area* (keranjang persiapan).
* `git commit -m "pesan"` : Menyimpan perubahan secara permanen di laptop sebagai satu *snapshot* dengan pesan tertentu.
* `git branch -M main` : Mengubah nama *branch* utama dari `master` menjadi `main` (standar GitHub).

### C. Perintah Remote (Menghubungkan ke GitHub)
* `git remote add origin <URL>` : Menghubungkan folder lokal ke repositori GitHub.
* `git remote -v` : Melihat daftar URL remote yang terhubung.
* `git remote remove origin` : Memutuskan hubungan dengan remote.
* `git remote set-url origin <URL_BARU>` : Mengganti URL remote yang sudah ada.
* `git push -u origin main` : Mengirim commit lokal ke GitHub. `-u` (upstream) menyimpan pengaturan agar selanjutnya cukup ketik `git push`.
* `git pull origin main` : Menarik file terbaru dari GitHub ke laptop.

### D. Perintah Sakti GitHub CLI (`gh`)
* `gh repo create belajar-web-dev --public --source=. --remote=origin --push`
  *Penjelasan:*
  * `gh repo create`: Membuat repo baru di GitHub.
  * `--public`: Repo bisa dilihat publik (bisa diganti `--private`).
  * `--source=.`: Mengambil kode dari folder saat ini (titik = folder ini).
  * `--remote=origin`: Mengatur remote dengan nama `origin`.
  * `--push`: Langsung unggah file ke GitHub setelah dibuat.

---

## 4. Troubleshooting (Error yang Pernah Dihadapi)

* **`warning: in the working copy of 'README.md', LF will be replaced by CRLF`**
  * *Penyebab*: Perbedaan format baris baru (Enter) antara Windows (CRLF) dan Linux/Mac (LF).
  * *Solusi*: Abaikan saja. Ini normal dan tidak berbahaya.
* **`fatal: not a git repository`**
  * *Penyebab*: Folder saat ini belum di-`git init` atau folder `.git` sudah terhapus.
  * *Solusi*: Jalankan `git init` jika ingin memulai baru.
* **`error: remote origin already exists`**
  * *Penyebab*: Kamu mencoba `git remote add` tapi remote `origin` sudah ada.
  * *Solusi*: Ganti dengan `git remote set-url origin <URL_BARU>` atau hapus dulu dengan `git remote remove origin`.
* **`! [rejected] main -> main (fetch first)`**
  * *Penyebab*: Repo di GitHub sudah memiliki isi (misal tercentang "Add a README file" saat dibuat), sedangkan di laptop juga ada.
  * *Solusi 1 (Aman)*: Tarik dulu file GitHub `git pull origin main --allow-unrelated-histories --no-edit`, lalu `git push`.
  * *Solusi 2 (Paksa)*: `git push -u origin main --force` (Gunakan jika yakin file lokal paling benar).

---

## 5. Alur Kerja (Workflow) Developer

### A. Membuat Proyek Baru dari Nol (Full Command)
Jika punya folder baru dan ingin langsung membuat repo di GitHub tanpa buka browser:
```bash
git init
git add .
git commit -m "init: proyek baru"
git branch -M main
gh repo create nama-proyek --public --source=. --remote=origin --push
```

### B. Siklus Harian (The Holy Trinity)
Setiap kali selesai belajar, mengedit file, atau menulis catatan, cukup ingat dan jalankan 3 perintah ini secara berurutan:
```bash
git add .                              # 1. Kumpulkan perubahan
git commit -m "update: catatan hari ini" # 2. Simpan sebagai snapshot
git push                               # 3. Kirim ke GitHub
```