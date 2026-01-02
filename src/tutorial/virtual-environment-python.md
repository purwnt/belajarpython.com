---
layout: tutorial.njk
title: Virtual Environment Python
order: 25
permalink: /tutorial/virtual-environment-python/
---

Virtual Environment adalah salah satu konsep penting dalam pengembangan Python modern. Virtual environment memungkinkan Anda membuat lingkungan Python yang terisolasi untuk setiap proyek, sehingga dependensi antar proyek tidak saling bentrok.

### Mengapa Menggunakan Virtual Environment?

Bayangkan Anda memiliki dua proyek:
- Proyek A membutuhkan Django versi 3.2
- Proyek B membutuhkan Django versi 5.0

Tanpa virtual environment, Anda hanya bisa menginstal satu versi Django di sistem. Dengan virtual environment, setiap proyek bisa memiliki versi dependensi yang berbeda.

Keuntungan menggunakan virtual environment:
- **Isolasi dependensi** - Setiap proyek memiliki paket tersendiri
- **Mencegah konflik versi** - Berbagai proyek bisa menggunakan versi library berbeda
- **Reproduksi lingkungan** - Memudahkan berbagi proyek dengan developer lain
- **Keamanan** - Tidak mempengaruhi instalasi Python sistem

### Membuat Virtual Environment

Python 3 sudah menyertakan modul `venv` secara default untuk membuat virtual environment.

```python
# Membuat virtual environment baru bernama "myenv"
python -m venv myenv

# Di Windows
python -m venv myenv

# Di Linux/Mac
python3 -m venv myenv
```

Perintah di atas akan membuat folder `myenv` yang berisi:
- Salinan interpreter Python
- Pip (package manager)
- Folder untuk menyimpan paket yang diinstal

### Mengaktifkan Virtual Environment

Sebelum menggunakan virtual environment, Anda harus mengaktifkannya terlebih dahulu:

```bash
# Windows (Command Prompt)
myenv\Scripts\activate

# Windows (PowerShell)
myenv\Scripts\Activate.ps1

# Linux/Mac
source myenv/bin/activate
```

Setelah aktif, Anda akan melihat nama virtual environment di awal prompt:

```bash
(myenv) C:\Users\nama\proyek>
```

### Menginstal Paket dalam Virtual Environment

Setelah virtual environment aktif, Anda bisa menginstal paket menggunakan pip:

```bash
# Install paket
pip install requests
pip install django==5.0

# Install dari file requirements.txt
pip install -r requirements.txt
```

### Menyimpan Daftar Dependensi

Untuk menyimpan daftar paket yang terinstal (berguna untuk berbagi proyek):

```bash
# Menyimpan daftar paket ke requirements.txt
pip freeze > requirements.txt
```

File `requirements.txt` akan berisi daftar paket beserta versinya:

```
Django==5.0
requests==2.31.0
numpy==1.26.0
```

### Menonaktifkan Virtual Environment

Untuk keluar dari virtual environment:

```bash
deactivate
```

### Menghapus Virtual Environment

Untuk menghapus virtual environment, cukup hapus foldernya:

```bash
# Windows
rmdir /s /q myenv

# Linux/Mac
rm -rf myenv
```

### Best Practices

1. **Selalu gunakan virtual environment** untuk setiap proyek Python
2. **Jangan commit folder virtual environment** ke Git (tambahkan ke `.gitignore`)
3. **Selalu buat `requirements.txt`** untuk mendokumentasikan dependensi
4. **Gunakan nama yang jelas** untuk virtual environment (misalnya `venv` atau `.venv`)

Contoh `.gitignore`:

```
# Virtual Environment
venv/
.venv/
myenv/
env/

# Python
__pycache__/
*.pyc
```

### Alternatif: Poetry dan Pipenv

Untuk manajemen dependensi yang lebih canggih, Anda bisa menggunakan tools seperti:

- **Poetry** - Modern dependency management dengan fitur lengkap
- **Pipenv** - Kombinasi pip dan virtualenv dengan Pipfile

```bash
# Menggunakan Poetry
pip install poetry
poetry new myproject
poetry add django

# Menggunakan Pipenv  
pip install pipenv
pipenv install django
pipenv shell
```

---

> [Edit tutorial ini](https://github.com/belajarpythoncom/belajarpython.com/blob/master/src/tutorial/virtual-environment-python.md)

<div class="mt-8 inline justify-between gap-x-4 md:flex">
  <div class="flex justify-center mb-4 md:mb-0">
    <a href="/tutorial/pengembangan-web-python" class="text-primary-300 hover:text-primary-300 order-2 flex h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-8 text-base hover:no-underline md:order-1">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Pengembangan Web</span>
    </a>
  </div>
  <div class="order-1 flex justify-center">
    <a href="/tutorial/f-string-python" class="order-1 flex h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-8 text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:order-2">
      <span class="-mt-0.5">F-String Python</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
