---
layout: tutorial.njk
title: Fullstack Web App dengan Django
order: 43
permalink: /tutorial/fullstack-django-python/
---

<img src="/img/tutorial/43-fullstack-django-python.png" alt="Fullstack Web App dengan Django" class="w-full rounded-lg shadow-md mb-6" loading="lazy">

Jika Anda ingin membangun aplikasi web yang kompleks dan kaya fitur (seperti E-commerce, CMS, atau Sosial Media) dengan cepat, **Django** adalah jawabannya.

Django adalah framework "batteries-included". Artinya, ia sudah menyediakan semua yang Anda butuhkan: otentikasi user, panel admin, ORM (database), form handling, dan keamanan. Anda tidak perlu merakit roda dari awal.

### Konsep MVT (Model-View-Template)
Django menggunakan pola desain MVT:
1.  **Model**: Struktur data (database).
2.  **View**: Logika bisnis (apa yang ditampilkan).
3.  **Template**: Tampilan HTML (bagaimana menampilkannya).

### Memulai Proyek Django

```bash
pip install django
django-admin startproject myproject
cd myproject
python manage.py runserver
```

### 1. Model (Database)
Di Django, Anda mendefinisikan tabel database sebagai class Python.

```python
# models.py
from django.db import models

class Artikel(models.Model):
    judul = models.CharField(max_length=200)
    konten = models.TextField()
    tanggal_dibuat = models.DateTimeField(auto_now_add=True)

    def __str__(self):
        return self.judul
```

Setelah membuat model, jalankan migrasi untuk membuat tabel di database secara otomatis:
```bash
python manage.py makemigrations
python manage.py migrate
```

### 2. Admin Panel (Fitur Killer Django)
Hanya dengan mendaftarkan model Anda, Django memberikan dashboard admin yang siap pakai untuk mengelola data.

```python
# admin.py
from django.contrib import admin
from .models import Artikel

admin.site.register(Artikel)
```
Buka `/admin`, login, dan boom! Anda punya CMS instan.

### 3. View (Logika)
```python
# views.py
from django.shortcuts import render
from .models import Artikel

def daftar_artikel(request):
    semua_artikel = Artikel.objects.all() # Query database
    return render(request, 'blog/daftar_artikel.html', {'artikel': semua_artikel})
```

### 4. Template (HTML)
Django Template Language (DTL) memungkinkan kita menyisipkan logika Python ke dalam HTML.

```html
<!-- daftar_artikel.html -->
{% for a in artikel %}
  <h2>{{ a.judul }}</h2>
  <p>{{ a.konten }}</p>
  <small>{{ a.tanggal_dibuat }}</small>
{% endfor %}
```

### Mengapa Django?
*   **Keamanan**: Django melindungi Anda dari serangan umum seperti SQL Injection dan XSS secara default.
*   **Skalabilitas**: Digunakan oleh raksasa seperti Instagram, Pinterest, dan Spotify.
*   **Komunitas**: Ribuan paket pihak ketiga tersedia (Django REST Framework, Wagtail CMS, dll).

### Kesimpulan
Django adalah pilihan tepat untuk startup dan perusahaan yang ingin bergerak cepat ("The web framework for perfectionists with deadlines"). Meskipun kurva belajarnya sedikit lebih curam daripada Flask/FastAPI, produktivitas yang ditawarkannya tak tertandingi.

> <a href="https://github.com/devmode-id/belajarpython.com/blob/master/src/tutorial/fullstack-django-python.md" target="_blank" rel="noopener noreferrer">
> Edit tutorial ini
> </a>

<div class="mt-8 flex justify-between gap-x-2 md:gap-x-4">
  <div class="flex justify-start">
    <a href="/tutorial/restful-api-fastapi-python" class="text-primary-300 hover:text-primary-300 flex h-10 md:h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-4 md:px-8 text-sm md:text-base hover:no-underline md:">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">RESTful APIs</span>
    </a>
  </div>
  <div class="flex justify-end">
    <a href="/tutorial/microservices-python" class=" flex h-10 md:h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-4 md:px-8 text-sm md:text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:">
      <span class="-mt-0.5">Microservices</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
