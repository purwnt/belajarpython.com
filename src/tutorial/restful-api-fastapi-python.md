---
layout: tutorial.njk
title: Membuat RESTful APIs dengan FastAPI
order: 42
permalink: /tutorial/restful-api-fastapi-python/
---

<img src="/img/tutorial/42-restful-api-fastapi-python.png" alt="Membuat RESTful APIs dengan FastAPI" class="w-full rounded-lg shadow-md mb-6" loading="lazy">

Dalam pengembangan web modern, API (Application Programming Interface) adalah jembatan yang menghubungkan frontend (seperti aplikasi React, Vue, atau Mobile App) dengan backend (server).

Python memiliki banyak framework untuk membuat API, tetapi **FastAPI** adalah bintang yang sedang naik daun. Mengapa? Karena, sesuai namanya, ia **sangat cepat** (setara dengan NodeJS dan Go), mudah digunakan, dan memiliki dokumentasi otomatis yang luar biasa.

### Apa itu RESTful API?
REST (Representational State Transfer) adalah standar arsitektur komunikasi web. API RESTful menggunakan metode HTTP standar:
*   **GET**: Mengambil data.
*   **POST**: Mengirim/membuat data baru.
*   **PUT**: Memperbarui data.
*   **DELETE**: Menghapus data.

### Instalasi FastAPI

Kita butuh `fastapi` dan `uvicorn` (server ASGI untuk menjalankan aplikasi).

```bash
pip install fastapi uvicorn
```

### Membuat API Pertama Anda

Buat file bernama `main.py`:

```python
from fastapi import FastAPI
from pydantic import BaseModel

app = FastAPI()

# Model data menggunakan Pydantic (untuk validasi otomatis)
class Item(BaseModel):
    name: str
    price: float
    is_offer: bool = None

@app.get("/")
def read_root():
    return {"Hello": "World"}

@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}

@app.put("/items/{item_id}")
def update_item(item_id: int, item: Item):
    return {"item_name": item.name, "item_id": item_id}
```

Jalankan server:
```bash
uvicorn main:app --reload
```

Buka browser di `http://127.0.0.1:8000`. Anda akan melihat JSON `{"Hello": "World"}`.

### Keajaiban Dokumentasi Otomatis
Sekarang, coba buka `http://127.0.0.1:8000/docs`.

FastAPI secara otomatis membuat halaman dokumentasi interaktif (Swagger UI) di mana Anda bisa mencoba semua endpoint API Anda langsung dari browser tanpa perlu coding frontend!

### Pydantic: Validasi Data Tanpa Sakit Kepala
Perhatikan kelas `Item` di atas. FastAPI menggunakan **Pydantic** untuk memastikan data yang dikirim user sesuai format.

Jika user mengirim `price` sebagai "gratis" (string) padahal seharusnya float, FastAPI akan otomatis menolak request tersebut dan memberikan pesan error yang jelas. Anda tidak perlu menulis `if` check satu per satu.

### Kesimpulan
FastAPI mengubah cara developer Python membangun backend. Cepat, aman, dan modern. Ini adalah pilihan terbaik untuk memulai proyek API baru di tahun ini.

> <a href="https://github.com/devmode-id/belajarpython.com/blob/master/src/tutorial/restful-api-fastapi-python.md" target="_blank" rel="noopener noreferrer">
> Edit tutorial ini
> </a>

<div class="mt-8 flex justify-between gap-x-2 md:gap-x-4">
  <div class="flex justify-start">
    <a href="/tutorial/cybersecurity-ethical-hacking-python" class="text-primary-300 hover:text-primary-300 flex h-10 md:h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-4 md:px-8 text-sm md:text-base hover:no-underline md:">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Cybersecurity</span>
    </a>
  </div>
  <div class="flex justify-end">
    <a href="/tutorial/fullstack-django-python" class=" flex h-10 md:h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-4 md:px-8 text-sm md:text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:">
      <span class="-mt-0.5">Fullstack App</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
