---
layout: tutorial.njk
title: Decorators & Closures Python
order: 29
permalink: /tutorial/decorator-python/
---

Decorators dan Closures adalah dua konsep tingkat lanjut di Python yang sangat *powerful*. Meskipun terdengar mengintimidasi, keduanya adalah fondasi dari banyak "sihir" yang terjadi di dalam framework populer seperti Django, Flask, dan FastAPI.

Bayangkan Anda memiliki sebuah kado (fungsi). Anda ingin membungkus kado tersebut dengan kertas kado yang indah (decorator) sebelum memberikannya kepada orang lain. Anda tidak mengubah isi kadonya, tetapi Anda "mempercantik" atau menambah fitur pada kado tersebut dari luar. Itulah inti dari Decorator: memodifikasi perilaku fungsi tanpa mengubah kode aslinya.

Sebelum masuk ke Decorator, kita perlu memahami konsep **Closures** terlebih dahulu.

### 1. Closures

Closure adalah fungsi yang "mengingat" variabel dari lingkup (scope) tempat ia dibuat, bahkan setelah lingkup tersebut selesai dieksekusi.

#### Konsep Nested Function
Di Python, kita bisa membuat fungsi di dalam fungsi:

```python
def luar(x):
    def dalam(y):
        return x + y
    return dalam
```

#### Membuat Closure
Perhatikan contoh ini:

```python
def pembuat_pengali(n):
    def pengali(x):
        return x * n
    return pengali

# Membuat closure
kali_tiga = pembuat_pengali(3)
kali_lima = pembuat_pengali(5)

print(kali_tiga(10))  # Output: 30
print(kali_lima(10))  # Output: 50
```

Di sini, fungsi `kali_tiga` masih "mengingat" bahwa nilai `n` adalah 3, meskipun fungsi `pembuat_pengali` sudah selesai dijalankan. Inilah Closure.

### 2. Decorators

Decorator pada dasarnya adalah Closure yang menerima fungsi sebagai argumen dan mengembalikan fungsi pengganti (wrapper).

#### Decorator Sederhana
```python
def decorator_saya(func):
    def wrapper():
        print("Sebelum fungsi dipanggil")
        func()
        print("Setelah fungsi dipanggil")
    return wrapper

@decorator_saya
def say_hello():
    print("Hello World!")

say_hello()
```

#### Output:
```
Sebelum fungsi dipanggil
Hello World!
Setelah fungsi dipanggil
```

### 3. Decorator dengan Argumen (`*args`, `**kwargs`)

Agar decorator bisa bekerja dengan fungsi apa pun (yang memiliki parameter berapapun), gunakan `*args` dan `**kwargs`.

```python
def log_fungsi(func):
    def wrapper(*args, **kwargs):
        print(f"Panggilan fungsi: {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@log_fungsi
def tambah(a, b):
    return a + b

print(tambah(3, 5)) 
# Output:
# Panggilan fungsi: tambah
# 8
```

### 4. Real World Examples

#### Timer Decorator (Mengukur Waktu Eksekusi)
Sangat berguna untuk optimasi performa.

```python
import time
from functools import wraps

def timer(func):
    @wraps(func)  # Praktik terbaik: menjaga metadata fungsi asli
    def wrapper(*args, **kwargs):
        start = time.time()
        hasil = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} berjalan selama {end - start:.4f} detik")
        return hasil
    return wrapper

@timer
def proses_berat():
    time.sleep(1)
    return "Selesai"

proses_berat()
```

#### Authentication Decorator (Contoh Flask)
Memastikan user sudah login sebelum mengakses halaman tertentu.

```python
def login_required(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        if not current_user.is_authenticated:
            return redirect('/login')
        return func(*args, **kwargs)
    return wrapper

@app.route('/dashboard')
@login_required
def dashboard():
    return "Halaman Dashboard"
```

### Kesimpulan
- **Closure**: Fungsi yang mengingat state dari lingkup luarnya.
- **Decorator**: Cara elegan menggunakan Closure untuk memodifikasi fungsi.

> [Edit tutorial ini](https://github.com/belajarpythoncom/belajarpython.com/blob/master/src/tutorial/decorator-python.md)

<div class="mt-8 inline justify-between gap-x-4 md:flex">
  <div class="flex justify-center mb-4 md:mb-0">
    <a href="/tutorial/pip-package-python" class="text-primary-300 hover:text-primary-300 order-2 flex h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-8 text-base hover:no-underline md:order-1">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Pip & Package</span>
    </a>
  </div>
  <div class="order-1 flex justify-center">
    <a href="/tutorial/iterators-generators-python" class="order-1 flex h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-8 text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:order-2">
      <span class="-mt-0.5">Iterators & Generators</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
