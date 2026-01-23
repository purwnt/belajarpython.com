---
layout: tutorial.njk
title: DevOps & CI/CD untuk Python
order: 46
permalink: /tutorial/devops-ci-cd-python/
---

<img src="/img/tutorial/46-devops-ci-cd-python.png" alt="DevOps dan CI/CD untuk Python" class="w-full rounded-lg shadow-md mb-6" loading="lazy">

**DevOps** adalah budaya yang menggabungkan tim Pengembang (Dev) dan Operasional (Ops) untuk mempercepat pengiriman software. Jantung dari DevOps adalah **CI/CD** (Continuous Integration / Continuous Deployment).

### Apa itu CI/CD?

1.  **Continuous Integration (CI)**: Setiap kali Anda menyimpan kode (git push), server otomatis menjalankan tes (Unit Test). Jika tes gagal, kode ditolak. Ini mencegah "bug" masuk ke kode utama.
2.  **Continuous Deployment (CD)**: Jika semua tes lulus, kode otomatis di-deploy ke server produksi tanpa campur tangan manusia.

### Tools Populer
*   **GitHub Actions**: Gratis dan terintegrasi langsung dengan GitHub.
*   **GitLab CI**: Sangat populer di perusahaan enterprise.
*   **Jenkins**: Tool open-source klasik yang sangat fleksibel.

### Contoh: GitHub Actions untuk Python

Buat file `.github/workflows/python-app.yml` di repository Anda:

```yaml
name: Python Application

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Python 3.10
      uses: actions/setup-python@v3
      with:
        python-version: "3.10"
        
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install pytest
        if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
        
    - name: Test with pytest
      run: |
        pytest
```

Dengan konfigurasi di atas, setiap kali Anda push ke branch `main`, GitHub akan meminjamkan komputer server (runner), menginstal Python, menginstal dependensi Anda, dan menjalankan `pytest`. Jika ada error, Anda akan mendapat email notifikasi "Build Failed".

### Manfaat CI/CD
1.  **Kecepatan**: Tidak perlu copy-paste file manual lewat FTP/SSH.
2.  **Kualitas**: Kode yang error tidak akan pernah sampai ke user.
3.  **Tidur Nyenyak**: Mengurangi risiko "deploy hari Jumat" yang merusak server di akhir pekan.

### Kesimpulan
Mengimplementasikan CI/CD adalah langkah besar menuju profesionalisme. Ini mengubah proses pengembangan dari "seni yang kacau" menjadi "pabrik yang presisi".

> <a href="https://github.com/devmode-id/belajarpython.com/blob/master/src/tutorial/devops-ci-cd-python.md" target="_blank" rel="noopener noreferrer">
> Edit tutorial ini
> </a>

<div class="mt-8 flex justify-between gap-x-2 md:gap-x-4">
  <div class="flex justify-start">
    <a href="/tutorial/deploying-docker-kubernetes-python" class="text-primary-300 hover:text-primary-300 flex h-10 md:h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-4 md:px-8 text-sm md:text-base hover:no-underline md:">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Deploying Apps</span>
    </a>
  </div>
  <div class="flex justify-end">
    <a href="/tutorial/ai-mcp-fastmcp-python" class=" flex h-10 md:h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-4 md:px-8 text-sm md:text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:">
      <span class="-mt-0.5">AI MCP</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
