---
layout: tutorial.njk
title: Deploying Apps dengan Docker & Kubernetes
order: 45
permalink: /tutorial/deploying-docker-kubernetes-python/
---

<img src="/img/tutorial/45-deploying-apps-python.png" alt="Deploying Apps dengan Docker dan Kubernetes" class="w-full rounded-lg shadow-md mb-6" loading="lazy">

Pernahkah Anda mendengar kalimat "Tapi ini jalan di laptop saya!" saat aplikasi Anda error di server produksi?

Masalah ini diselesaikan oleh **Containerization**. Docker membungkus aplikasi Anda beserta semua dependensinya (seperti library Python, OS settings) ke dalam satu wadah ("container") yang bisa berjalan di mana saja.

### Apa itu Docker?
Docker memungkinkan Anda membuat paket aplikasi yang ringan dan portabel.

#### Membuat Dockerfile
Bayangkan kita punya aplikasi Flask sederhana. Buat file bernama `Dockerfile` (tanpa ekstensi):

```dockerfile
# Gunakan base image Python resmi
FROM python:3.9-slim

# Set direktori kerja di dalam container
WORKDIR /app

# Salin file requirements.txt
COPY requirements.txt .

# Install dependensi
RUN pip install --no-cache-dir -r requirements.txt

# Salin seluruh kode aplikasi ke dalam container
COPY . .

# Beritahu port yang digunakan
EXPOSE 5000

# Perintah untuk menjalankan aplikasi
CMD ["python", "app.py"]
```

Build dan jalankan:
```bash
docker build -t aplikasi-python-saya .
docker run -p 5000:5000 aplikasi-python-saya
```

Sekarang aplikasi Anda berjalan dalam container yang terisolasi!

### Apa itu Kubernetes (K8s)?
Jika Docker adalah kapal pengangkut kontainer, maka Kubernetes adalah nahkoda pelabuhan yang mengatur ribuan kapal tersebut.

Kubernetes (K8s) adalah sistem *orchestration* untuk mengelola container dalam skala besar. Jika Anda punya 100 container aplikasi yang harus berjalan di 10 server berbeda, K8s yang akan mengaturnya.

K8s menangani:
1.  **Load Balancing**: Membagi trafik ke beberapa container.
2.  **Self-healing**: Jika container crash, K8s akan otomatis merestartnya.
3.  **Scaling**: Menambah jumlah container saat trafik tinggi (Black Friday sales!).

### Kesimpulan
Untuk aplikasi kecil, Docker (dan Docker Compose) sudah cukup. Namun jika Anda membangun sistem skala perusahaan yang besar dan kompleks, Kubernetes adalah standar industri untuk deployment.

> <a href="https://github.com/devmode-id/belajarpython.com/blob/master/src/tutorial/deploying-docker-kubernetes-python.md" target="_blank" rel="noopener noreferrer">
> Edit tutorial ini
> </a>

<div class="mt-8 flex justify-between gap-x-2 md:gap-x-4">
  <div class="flex justify-start">
    <a href="/tutorial/microservices-python" class="text-primary-300 hover:text-primary-300 flex h-10 md:h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-4 md:px-8 text-sm md:text-base hover:no-underline md:">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Microservices</span>
    </a>
  </div>
  <div class="flex justify-end">
    <a href="/tutorial/devops-ci-cd-python" class=" flex h-10 md:h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-4 md:px-8 text-sm md:text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:">
      <span class="-mt-0.5">DevOps & CI/CD</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
