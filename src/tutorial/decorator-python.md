---
layout: tutorial.njk
title: Decorator Python
order: 28
permalink: /tutorial/decorator-python/
---

Decorator adalah fitur powerful di Python yang memungkinkan Anda memodifikasi atau memperluas perilaku fungsi atau class tanpa mengubah kode aslinya. Decorator banyak digunakan di framework modern seperti Flask, Django, dan FastAPI.

### Konsep Dasar

Di Python, fungsi adalah **first-class objects**, artinya fungsi bisa:
- Disimpan dalam variabel
- Dikirim sebagai argumen ke fungsi lain
- Dikembalikan dari fungsi lain

```python
# Fungsi sebagai objek
def salam():
    return "Halo!"

# Menyimpan fungsi ke variabel
ucapan = salam
print(ucapan())  # Output: Halo!

# Fungsi sebagai argumen
def panggil_fungsi(func):
    return func()

print(panggil_fungsi(salam))  # Output: Halo!
```

### Decorator Sederhana

Decorator adalah fungsi yang menerima fungsi lain sebagai argumen dan mengembalikan fungsi baru:

```python
def decorator_saya(func):
    def wrapper():
        print("Sebelum fungsi dipanggil")
        func()
        print("Setelah fungsi dipanggil")
    return wrapper

# Menggunakan decorator
@decorator_saya
def say_hello():
    print("Hello!")

# Memanggil fungsi yang sudah di-decorate
say_hello()
# Output:
# Sebelum fungsi dipanggil
# Hello!
# Setelah fungsi dipanggil
```

Sintaks `@decorator_saya` adalah shorthand untuk:
```python
say_hello = decorator_saya(say_hello)
```

### Decorator dengan Argumen Fungsi

Untuk decorator yang bekerja dengan fungsi berargumen, gunakan `*args` dan `**kwargs`:

```python
def log_fungsi(func):
    def wrapper(*args, **kwargs):
        print(f"Memanggil {func.__name__} dengan args={args}, kwargs={kwargs}")
        hasil = func(*args, **kwargs)
        print(f"Hasil: {hasil}")
        return hasil
    return wrapper

@log_fungsi
def tambah(a, b):
    return a + b

@log_fungsi
def sapa(nama, formal=False):
    if formal:
        return f"Selamat pagi, {nama}"
    return f"Halo, {nama}!"

tambah(3, 5)
# Output:
# Memanggil tambah dengan args=(3, 5), kwargs={}
# Hasil: 8

sapa("Budi", formal=True)
# Output:
# Memanggil sapa dengan args=('Budi',), kwargs={'formal': True}
# Hasil: Selamat pagi, Budi
```

### Menjaga Metadata Fungsi dengan @wraps

Saat menggunakan decorator, metadata fungsi asli (seperti `__name__` dan `__doc__`) akan hilang. Gunakan `@wraps` dari `functools` untuk menjaganya:

```python
from functools import wraps

def decorator_baik(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        """Ini wrapper"""
        return func(*args, **kwargs)
    return wrapper

@decorator_baik
def contoh():
    """Ini dokumentasi fungsi contoh"""
    pass

print(contoh.__name__)  # Output: contoh (bukan 'wrapper')
print(contoh.__doc__)   # Output: Ini dokumentasi fungsi contoh
```

### Decorator dengan Parameter

Jika decorator membutuhkan parameter sendiri, gunakan nested function:

```python
from functools import wraps

def ulangi(kali):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(kali):
                hasil = func(*args, **kwargs)
            return hasil
        return wrapper
    return decorator

@ulangi(kali=3)
def sapa(nama):
    print(f"Halo, {nama}!")

sapa("Andi")
# Output:
# Halo, Andi!
# Halo, Andi!
# Halo, Andi!
```

### Contoh Praktis Decorator

#### 1. Timer Decorator

```python
import time
from functools import wraps

def timer(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.time()
        hasil = func(*args, **kwargs)
        end = time.time()
        print(f"{func.__name__} selesai dalam {end - start:.4f} detik")
        return hasil
    return wrapper

@timer
def proses_lama():
    time.sleep(1)
    return "Selesai"

proses_lama()
# Output: proses_lama selesai dalam 1.0012 detik
```

#### 2. Retry Decorator

```python
import time
from functools import wraps

def retry(max_attempts=3, delay=1):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            attempts = 0
            while attempts < max_attempts:
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    attempts += 1
                    print(f"Percobaan {attempts} gagal: {e}")
                    if attempts < max_attempts:
                        time.sleep(delay)
            raise Exception(f"Gagal setelah {max_attempts} percobaan")
        return wrapper
    return decorator

@retry(max_attempts=3, delay=1)
def koneksi_api():
    # Simulasi koneksi yang mungkin gagal
    import random
    if random.random() < 0.7:
        raise ConnectionError("Koneksi gagal")
    return "Sukses!"
```

#### 3. Cache/Memoization Decorator

```python
from functools import wraps

def cache(func):
    memo = {}
    @wraps(func)
    def wrapper(*args):
        if args not in memo:
            memo[args] = func(*args)
        return memo[args]
    return wrapper

@cache
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(100))  # Sangat cepat dengan cache!
```

**Catatan:** Python sudah menyediakan `@lru_cache` dari `functools`:

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

#### 4. Validasi Decorator

```python
from functools import wraps

def validasi_positif(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        for arg in args:
            if isinstance(arg, (int, float)) and arg < 0:
                raise ValueError(f"Argumen harus positif, ditemukan: {arg}")
        return func(*args, **kwargs)
    return wrapper

@validasi_positif
def hitung_luas(panjang, lebar):
    return panjang * lebar

print(hitung_luas(5, 3))    # Output: 15
print(hitung_luas(-5, 3))   # Raise ValueError
```

### Multiple Decorators

Anda bisa menerapkan beberapa decorator pada satu fungsi:

```python
@decorator1
@decorator2
@decorator3
def fungsi():
    pass

# Sama dengan:
# fungsi = decorator1(decorator2(decorator3(fungsi)))
```

Urutan penting! Decorator paling bawah dieksekusi pertama.

### Class Decorator

Decorator juga bisa diterapkan pada class:

```python
def singleton(cls):
    instances = {}
    @wraps(cls)
    def get_instance(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]
    return get_instance

@singleton
class Database:
    def __init__(self):
        print("Membuat koneksi database...")

# Hanya satu instance yang dibuat
db1 = Database()  # Output: Membuat koneksi database...
db2 = Database()  # Tidak ada output, menggunakan instance yang sama
print(db1 is db2)  # Output: True
```

### Decorator di Framework Populer

Decorator sangat umum digunakan di framework Python:

```python
# Flask
@app.route("/")
def home():
    return "Hello!"

# FastAPI
@app.get("/items/{item_id}")
def read_item(item_id: int):
    return {"item_id": item_id}

# Django
@login_required
def dashboard(request):
    return render(request, "dashboard.html")

# pytest
@pytest.fixture
def sample_data():
    return [1, 2, 3]
```

---

> [Edit tutorial ini](https://github.com/belajarpythoncom/belajarpython.com/blob/master/src/tutorial/decorator-python.md)

<div class="mt-8 inline justify-between gap-x-4 md:flex">
  <div class="flex justify-center mb-4 md:mb-0">
    <a href="/tutorial/list-comprehension-python" class="text-primary-300 hover:text-primary-300 order-2 flex h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-8 text-base hover:no-underline md:order-1">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">List Comprehension</span>
    </a>
  </div>
  <div class="order-1 flex justify-center">
    <a href="/tutorial/type-hints-python" class="order-1 flex h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-8 text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:order-2">
      <span class="-mt-0.5">Type Hints Python</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
