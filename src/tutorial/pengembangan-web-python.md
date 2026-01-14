---
layout: tutorial.njk
title: Pengembangan Web Python
order: 24
permalink: /tutorial/pengembangan-web-python/
---

Pengembangan web adalah istilah umum untuk membuat konsep, membuat, menyebarkan, dan mengoperasikan aplikasi website dan antarmuka pemrograman aplikasi untuk Website.

### Penggunaan Python dalam Pengembangan Web

Python dapat digunakan untuk membangun aplikasi web sisi server. Sementara kerangka web tidak diperlukan untuk membangun aplikasi web, jarang sekali pengembang tidak akan menggunakan pustaka sumber terbuka yang ada untuk mempercepat kemajuan mereka dalam membuat aplikasi mereka berfungsi.

Python tidak digunakan di browser web. Bahasa yang dijalankan di browser seperti Chrome, Firefox, dan Internet Explorer adalah JavaScript. Proyek seperti pyjs dapat dikompilasi dari Python ke JavaScript. Namun, sebagian besar pengembang Python menulis aplikasi web mereka menggunakan kombinasi Python dan JavaScript. Python dieksekusi di sisi server sementara JavaScript diunduh ke klien dan dijalankan oleh browser web.

Untuk membuat website dengan menggunakan Python sebagai bahasa pemrogramanya, caranya sangat mudah. Tetapi perlu diingat bahwa sebelumnya Anda sudah harus menguasai HTML, CSS dan Javascript.

### Web Framework Python

Framework pengembangan web pada python yang paling populer dan mudah dipelajari ada Django, Flask, dan FastAPI.

#### Flask

Flask adalah sebuah microframework web python yang mudah untuk dipelajari, mudah diinstal dan pengembangan yang sangat simpel.

Berikut adalah beberapa kelebihanya :

- mudah digunakan.
- dibangun di server pengembangan dan debugger
- dukungan pengujian unit terpadu
- Kirim permintaan yang tenang
- menggunakan tempering Jinja2
- dukungan untuk cookie aman (sesi sisi klien)
- 100% WSGI 1.0 compliant
- Berbasis Unicode
- didokumentasikan secara ekstensif

Instalasi Flask
`pip install Flask`

Hello World Web App dengan Flask

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
return "Hello World!"

if __name__ == "__main__":
app.run()
```

Jalankan server dengan perintah:
`python hello.py`

Buka [http://localhost:5000/](http://localhost:5000/) dibrowser anda dan akan muncul `Hello World!`

#### Django

Django adalah kerangka kerja Python Web tingkat tinggi yang menangani banyak kerumitan pengembangan Web, sehingga Anda dapat fokus untuk menulis aplikasi tanpa perlu menemukan kembali roda.

Kelebihan Framework Django dibanding yang lain adalah pada segi skalabilitas. Framework ini cocok untuk pengembangan aplikasi besar.

Untuk menginstal Django jalankan perintah dibawah ini :
`pip install Django`

Setelah terinstal, buat project Django baru:

```bash
django-admin startproject myproject
cd myproject
python manage.py runserver
```

Buka [http://127.0.0.1:8000/](http://127.0.0.1:8000/) di browser dan Anda akan melihat halaman selamat datang Django.

#### FastAPI

FastAPI adalah framework web modern dan cepat (high-performance) untuk membangun API dengan Python 3.7+ berdasarkan standard Python type hints. FastAPI sangat populer di tahun 2025 karena performanya yang tinggi dan kemudahan penggunaannya.

Kelebihan FastAPI:

- Sangat cepat: Performa setara dengan NodeJS dan Go
- Cepat untuk coding: Meningkatkan kecepatan development 2-3x lipat
- Lebih sedikit bugs: Mengurangi sekitar 40% human errors
- Dokumentasi otomatis: Swagger UI dan ReDoc otomatis tersedia
- Berbasis standard: OpenAPI dan JSON Schema

Instalasi FastAPI:
`pip install fastapi uvicorn`

Hello World dengan FastAPI:

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
    return {"Hello": "World"}

@app.get("/items/{item_id}")
def read_item(item_id: int, q: str = None):
    return {"item_id": item_id, "q": q}
```

Jalankan server dengan perintah:
`uvicorn main:app --reload`

Buka [http://127.0.0.1:8000/](http://127.0.0.1:8000/) untuk melihat hasilnya, dan [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) untuk dokumentasi API interaktif.

> [Edit tutorial ini](https://github.com/belajarpythoncom/belajarpython.com/blob/master/docs/tutorial/pengembangan-web-python.md)

<div class="mt-8 inline justify-between gap-x-4 md:flex">
  <div class="flex justify-center mb-4 md:mb-0">
    <a href="/tutorial/networking-python" class="text-primary-300 hover:text-primary-300 order-2 flex h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-8 text-base hover:no-underline md:order-1">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Networking Python</span>
    </a>
  </div>
  <div class="order-1 flex justify-center">
    <a href="/tutorial/regex-python" class="order-1 flex h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-8 text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:order-2">
      <span class="-mt-0.5">RegEx Python</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
