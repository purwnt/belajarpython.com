---
layout: tutorial.njk
title: Microservices dengan Python
order: 44
permalink: /tutorial/microservices-python/
---

<img src="/img/tutorial/44-microservices-python.png" alt="Microservices dengan Python" class="w-full rounded-lg shadow-md mb-6" loading="lazy">

Dahulu, aplikasi dibangun sebagai satu kesatuan raksasa (**Monolith**). Jika satu bagian rusak, seluruh aplikasi bisa mati. Jika ingin update satu fitur kecil, seluruh aplikasi harus di-deploy ulang.

**Microservices** memecahkan masalah ini dengan memecah aplikasi menjadi layanan-layanan kecil yang independen. Setiap layanan menjalankan prosesnya sendiri dan berkomunikasi melalui mekanisme ringan, biasanya HTTP API.

### Karakteristik Microservices
1.  **Independen**: Bisa di-deploy, di-update, dan di-scale secara terpisah.
2.  **Terdesentralisasi**: Setiap service boleh menggunakan teknologi/database yang berbeda (Polyglot).
3.  **Resilien**: Kegagalan satu service tidak mematikan sistem secara keseluruhan.

### Python untuk Microservices
Python sangat cocok untuk microservices karena:
*   **Ringan**: Framework seperti Flask, FastAPI, dan Nameko sangat ringan.
*   **Cepat**: Waktu pengembangan yang cepat.

### Contoh Arsitektur Sederhana

Bayangkan Toko Online. Alih-alih satu kode besar, kita membaginya menjadi 3 service:
1.  **User Service**: Mengelola login dan profil.
2.  **Product Service**: Katalog barang.
3.  **Order Service**: Transaksi.

Masing-masing service bisa jadi adalah proyek FastAPI yang terpisah, berjalan di port yang berbeda.

#### Komunikasi Antar Service (HTTP Request)

Misalkan `Order Service` butuh data user. Ia akan "menelpon" `User Service`.

```python
# Di dalam Order Service
import requests

def get_user_info(user_id):
    # Memanggil User Service yang berjalan di port 8001
    response = requests.get(f"http://user-service:8001/users/{user_id}")
    return response.json()
```

### Tantangan Microservices
"With great power comes great responsibility." Microservices juga menambah kompleksitas:
*   **Monitoring**: Bagaimana melacak error di antara puluhan service?
*   **Latency**: Komunikasi jaringan lebih lambat daripada pemanggilan fungsi lokal.
*   **Data Consistency**: Menjaga data tetap sinkron antar database yang berbeda.

### Nameko: Framework Khusus Microservices
Selain HTTP, microservices sering berkomunikasi lewat *Message Broker* (seperti RabbitMQ). Framework **Nameko** di Python memudahkan ini.

```python
from nameko.rpc import rpc

class GreetingService:
    name = "greeting_service"

    @rpc
    def hello(self, name):
        return "Hello, {}!".format(name)
```

### Kesimpulan
Microservices adalah arsitektur pilihan untuk sistem skala besar seperti Netflix atau Uber. Namun untuk startup tahap awal, Monolith seringkali lebih efisien. Mulailah dengan Monolith, lalu pecah menjadi Microservices saat sistem Anda mulai terlalu besar untuk ditangani.

> <a href="https://github.com/devmode-id/belajarpython.com/blob/master/src/tutorial/microservices-python.md" target="_blank" rel="noopener noreferrer">
> Edit tutorial ini
> </a>

<div class="mt-8 flex justify-between gap-x-2 md:gap-x-4">
  <div class="flex justify-start">
    <a href="/tutorial/fullstack-django-python" class="text-primary-300 hover:text-primary-300 flex h-10 md:h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-4 md:px-8 text-sm md:text-base hover:no-underline md:">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Fullstack Web App</span>
    </a>
  </div>
  <div class="flex justify-end">
    <a href="/tutorial/deploying-docker-kubernetes-python" class=" flex h-10 md:h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-4 md:px-8 text-sm md:text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:">
      <span class="-mt-0.5">Deploying Apps</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
