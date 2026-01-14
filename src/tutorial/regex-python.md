---
layout: tutorial.njk
title: Regular Expressions (RegEx) Python
order: 25
permalink: /tutorial/regex-python/
---

Regular Expression atau RegEx adalah urutan karakter yang membentuk pola pencarian. RegEx dapat digunakan untuk memeriksa apakah sebuah string berisi pola pencarian yang ditentukan.

![Illustration Regular Expressions (RegEx)](/img/regex-illustration.png)

Bagi pemula, bayangkan RegEx sebagai fitur "Search" atau "Find" (Ctrl+F) yang jauh lebih canggih. Jika fitur pencarian biasa hanya bisa mencari kata yang persis sama, RegEx memungkinkan Anda mencari pola tertentu, seperti mencari semua nomor telepon, alamat email, atau format tanggal dalam sebuah dokumen yang sangat panjang tanpa harus tahu isi teksnya secara spesifik.

Meskipun pada awalnya RegEx terlihat membingungkan karena penuh dengan simbol-simbol unik, menguasai teknik ini akan sangat membantu Anda dalam mengolah data teks (*text processing*) dan melakukan validasi input pengguna di aplikasi Python Anda dengan jauh lebih efisien.

Python memiliki modul bawaan bernama `re` yang dapat digunakan untuk bekerja dengan Regular Expressions.

### Menggunakan Modul re

Untuk menggunakan RegEx di Python, Anda harus mengimpor modul `re`:

```python
import re
```

### Fungsi-fungsi dalam Modul re

Modul `re` menawarkan sekumpulan fungsi yang memungkinkan kita mencari string untuk kecocokan:

| Fungsi | Deskripsi |
| :--- | :--- |
| `findall` | Mengembalikan daftar yang berisi semua kecocokan |
| `search` | Mengembalikan objek Match jika ada kecocokan di mana saja dalam string |
| `split` | Mengembalikan daftar di mana string telah dipisahkan pada setiap kecocokan |
| `sub` | Mengganti satu atau lebih kecocokan dengan string |

#### Fungsi search()

Fungsi `search()` mencari string untuk kecocokan, dan mengembalikan objek Match jika ada kecocokan. Jika ada lebih dari satu kecocokan, hanya kecocokan pertama yang akan dikembalikan.

```python
import re

txt = "Hujan di Spanyol"
x = re.search("^Hujan.*Spanyol$", txt)

if x:
  print("YA! Kami memiliki kecocokan!")
else:
  print("Tidak ada kecocokan")
```

#### Fungsi findall()

Fungsi `findall()` mengembalikan daftar yang berisi semua kecocokan.

```python
import re

txt = "Hujan di Spanyol"
x = re.findall("ai", txt)
print(x)
```

Daftar berisi kecocokan dalam urutan kemunculannya. Jika tidak ditemukan kecocokan, daftar kosong akan dikembalikan.

#### Fungsi split()

Fungsi `split()` mengembalikan daftar di mana string telah dipisahkan pada setiap kecocokan.

```python
import re

txt = "Hujan di Spanyol"
x = re.split("\s", txt)
print(x)
```

Anda dapat mengontrol jumlah pemisahan dengan menentukan parameter `maxsplit`:

```python
import re

txt = "Hujan di Spanyol"
x = re.split("\s", txt, 1)
print(x)
```

#### Fungsi sub()

Fungsi `sub()` mengganti kecocokan dengan teks pilihan Anda.

```python
import re

txt = "Hujan di Spanyol"
x = re.sub("\s", "9", txt)
print(x)
```

Anda dapat mengontrol jumlah penggantian dengan menentukan parameter `count`:

```python
import re

txt = "Hujan di Spanyol"
x = re.sub("\s", "9", txt, 2)
print(x)
```

### Metakarakter

Metakarakter adalah karakter dengan makna khusus:

| Karakter | Deskripsi | Contoh |
| :--- | :--- | :--- |
| `[]` | Satu set karakter | `"[a-m]"` |
| `\` | Memberi sinyal urutan khusus (bisa juga digunakan untuk escape karakter khusus) | `"\d"` |
| `.` | Karakter apa pun (kecuali karakter baris baru) | `"he..o"` |
| `^` | Dimulai dengan | `"^hello"` |
| `$` | Berakhir dengan | `"world$"` |
| `*` | Nol atau lebih kemunculan | `"aix*"` |
| `+` | Satu atau lebih kemunculan | `"aix+"` |
| `{}` | Persis jumlah kemunculan yang ditentukan | `"al{2}"` |
| `\|` | Salah satu dari | `"falls\|stays"` |
| `()` | Grup | |

### Urutan Khusus (Special Sequences)

Urutan khusus adalah `\` diikuti oleh salah satu karakter dalam daftar di bawah ini, dan memiliki makna khusus:

| Karakter | Deskripsi | Contoh |
| :--- | :--- | :--- |
| `\A` | Mengembalikan kecocokan jika karakter yang ditentukan berada di awal string | `"\AHalo"` |
| `\b` | Mengembalikan kecocokan di mana karakter yang ditentukan berada di awal atau di akhir kata | `r"\bain"` `r"ain\b"` |
| `\B` | Mengembalikan kecocokan di mana karakter yang ditentukan ada, tetapi TIDAK di awal (atau di akhir) kata | `r"\Bain"` `r"ain\B"` |
| `\d` | Mengembalikan kecocokan di mana string berisi digit (angka 0-9) | `"\d"` |
| `\D` | Mengembalikan kecocokan di mana string TIDAK berisi digit | `"\D"` |
| `\s` | Mengembalikan kecocokan di mana string berisi karakter spasi putih | `"\s"` |
| `\S` | Mengembalikan kecocokan di mana string TIDAK berisi karakter spasi putih | `"\S"` |
| `\w` | Mengembalikan kecocokan di mana string berisi karakter kata apa pun (a-z, 0-9, dan underscore) | `"\w"` |
| `\W` | Mengembalikan kecocokan di mana string TIDAK berisi karakter kata | `"\W"` |
| `\Z` | Mengembalikan kecocokan jika karakter yang ditentukan berada di akhir string | `"Spanyol\Z"` |

### Set Karakter

Set adalah sekumpulan karakter di dalam sepasang tanda kurung siku `[]` dengan makna khusus:

| Set | Deskripsi |
| :--- | :--- |
| `[arn]` | Mengembalikan kecocokan di mana salah satu karakter yang ditentukan (`a`, `r`, atau `n`) ada |
| `[a-n]` | Mengembalikan kecocokan untuk karakter huruf kecil apa pun, secara abjad antara `a` dan `n` |
| `[^arn]` | Mengembalikan kecocokan untuk karakter apa pun KECUALI `a`, `r`, dan `n` |
| `[0123]` | Mengembalikan kecocokan di mana salah satu digit yang ditentukan (`0`, `1`, `2`, atau `3`) ada |
| `[0-9]` | Mengembalikan kecocokan untuk digit apa pun antara `0` dan `9` |
| `[0-5][0-9]` | Mengembalikan kecocokan untuk angka dua digit dari `00` hingga `59` |
| `[a-zA-Z]` | Mengembalikan kecocokan untuk karakter apa pun secara abjad antara `a` dan `z`, huruf kecil ATAU huruf besar |
| `[+]` | Dalam set, `+`, `*`, `.`, `\|`, `()`, `$`, `{}` tidak memiliki makna khusus |

### Contoh

```python
import re

# Cari string yang berisi huruf kecil antara a dan n
x = re.findall("[a-n]", txt)
print(x)
```

Jika tidak ditemukan kecocokan, `findall()` akan mengembalikan daftar kosong.


> [Edit tutorial ini](https://github.com/belajarpythoncom/belajarpython.com/blob/master/docs/tutorial/regex-python.md)

<div class="mt-8 inline justify-between gap-x-4 md:flex">
  <div class="flex justify-center mb-4 md:mb-0">
    <a href="/tutorial/pengembangan-web-python" class="text-primary-300 hover:text-primary-300 order-2 flex h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-8 text-base hover:no-underline md:order-1">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Pengembangan Web Python</span>
    </a>
  </div>
  <div class="order-1 flex justify-center">
    <a href="/tutorial/json-python" class="order-1 flex h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-8 text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:order-2">
      <span class="-mt-0.5">JSON Data Python</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
