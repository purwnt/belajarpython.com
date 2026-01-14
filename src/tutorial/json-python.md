---
layout: tutorial.njk
title: Bekerja dengan JSON Data di Python
order: 26
permalink: /tutorial/json-python/
---

JSON (JavaScript Object Notation) adalah format populer yang digunakan untuk menyimpan dan memindahkan data. Dalam dunia pemrograman, JSON sering digunakan saat Anda mengambil data dari internet (API) atau saat aplikasi saling bertukar informasi.

Bagi pemula, bayangkan JSON seperti "daftar belanja" yang sangat rapi dan mudah dibaca baik oleh manusia maupun komputer. Karena bentuknya yang mirip dengan *Dictionary* di Python, mempelajari JSON akan terasa familiar dan sangat berguna ketika Anda mulai membangun aplikasi yang terhubung dengan layanan web atau menyimpan konfigurasi aplikasi.

Dibawah ini adalah struktur dan penjelasan singkat tentang objek JSON:

![Illustration Penjelasan Struktur JSON](/img/belajar-json-pada-python.jpg)


Python memiliki paket bawaan bernama `json`, yang dapat digunakan untuk bekerja dengan data JSON.

### Mengimpor Modul JSON

Untuk menggunakan JSON di Python, Anda harus mengimpor modul `json`:

```python
import json
```

### Parsing JSON - Mengubah JSON ke Python

Jika Anda memiliki string JSON, Anda dapat mem-parsingnya dengan menggunakan metode `json.loads()`. Hasilnya akan berupa dictionary Python.

```python
import json

# contoh JSON:
x =  '{ "nama":"Budi", "umur":30, "kota":"Jakarta"}'

# parsing x:
y = json.loads(x)

# hasilnya adalah dictionary Python:
print(y["umur"])
```

### Mengubah Python ke JSON

Jika Anda memiliki objek Python, Anda dapat mengubahnya menjadi string JSON dengan menggunakan metode `json.dumps()`.

```python
import json

# objek Python (dictionary):
x = {
  "nama": "Budi",
  "umur": 30,
  "kota": "Jakarta"
}

# ubah ke JSON:
y = json.dumps(x)

# hasilnya adalah string JSON:
print(y)
```

Anda dapat mengubah objek Python berikut menjadi string JSON:
* dict
* list
* tuple
* string
* int
* float
* True
* False
* None

### Memformat Hasil JSON

Contoh di atas mencetak string JSON, tetapi tidak terlalu mudah dibaca (tanpa indentasi). Metode `json.dumps()` memiliki parameter untuk memudahkan pembacaan hasil:

```python
import json

x = {
  "nama": "Budi",
  "umur": 30,
  "menikah": True,
  "anak": ("Rani","Dodi"),
  "peliharaan": None,
  "mobil": [
    {"model": "Toyota Avanza", "tahun": 2020},
    {"model": "Honda Civic", "tahun": 2021}
  ]
}

# gunakan parameter indent untuk menentukan jumlah indentasi:
print(json.dumps(x, indent=4))
```

Anda juga dapat memberikan parameter tambahan untuk mengatur format output:

```python
import json

x = {
  "nama": "Budi",
  "umur": 30,
  "menikah": True,
  "anak": ("Rani","Dodi"),
  "peliharaan": None,
  "mobil": [
    {"model": "Toyota Avanza", "tahun": 2020},
    {"model": "Honda Civic", "tahun": 2021}
  ]
}

# gunakan parameter indent untuk menentukan jumlah indentasi:
print(json.dumps(x, indent=4, sort_keys=True))
```

JSON ini sangat sering digunakan saat Anda mengambil data dari internet (API) atau saat aplikasi saling bertukar informasi. Jadi, penting untuk memahami bagaimana bekerja dengan JSON di Python.

> [Edit tutorial ini](https://github.com/belajarpythoncom/belajarpython.com/blob/master/docs/tutorial/json-python.md)

<div class="mt-8 inline justify-between gap-x-4 md:flex">
  <div class="flex justify-center mb-4 md:mb-0">
    <a href="/tutorial/regex-python" class="text-primary-300 hover:text-primary-300 order-2 flex h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-8 text-base hover:no-underline md:order-1">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">RegEx Python</span>
    </a>
  </div>
  <div class="order-1 flex justify-center">
    <a href="/tutorial/virtual-environment-python" class="order-1 flex h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-8 text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:order-2">
      <span class="-mt-0.5">Virtual Environment</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
