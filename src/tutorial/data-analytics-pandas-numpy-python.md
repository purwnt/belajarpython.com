---
layout: tutorial.njk
title: Data Analytics dengan Pandas & NumPy
order: 38
permalink: /tutorial/data-analytics-pandas-numpy-python/
---

<img src="/img/tutorial/38-data-analytics-pandas-numpy.png" alt="Data Analytics dengan Pandas & NumPy" class="w-full rounded-lg shadow-md mb-6" loading="lazy">

Data adalah minyak baru. Di era digital ini, kemampuan untuk mengolah, menganalisis, dan mengambil wawasan dari data adalah keterampilan yang sangat berharga. Python, dengan ekosistemnya yang kaya, telah menjadi bahasa pemrograman *de facto* untuk Data Science dan Data Analytics.

Dua pustaka (library) yang menjadi fondasi utama dalam analisis data dengan Python adalah **NumPy** dan **Pandas**.

Dalam tutorial ini, kita akan mempelajari dasar-dasar melakukan analisis data menggunakan kedua alat canggih ini.

### Apa itu NumPy dan Pandas?

**1. NumPy (Numerical Python)**
NumPy adalah pustaka dasar untuk komputasi ilmiah di Python. Ia menyediakan dukungan untuk array multidimensi (seperti matriks) yang besar, beserta koleksi fungsi matematika tingkat tinggi untuk mengoperasikan array ini. Keunggulan utamanya adalah **kecepatan** dan **efisiensi memori**.

**2. Pandas (Python Data Analysis Library)**
Dibangun di atas NumPy, Pandas menawarkan struktur data dan alat analisis data yang mudah digunakan, fleksibel, dan ekspresif. Struktur data utamanya, **DataFrame**, memungkinkan Anda menyimpan dan memanipulasi data tabular (seperti spreadsheet Excel atau tabel SQL) dengan sangat mudah.

### Instalasi

Sebelum memulai, pastikan Anda sudah menginstal NumPy dan Pandas. Anda bisa menginstalnya menggunakan `pip`:

```bash
pip install numpy pandas
```

### Menggunakan NumPy

Langkah pertama adalah mengimpor pustaka ini. Kebiasaan umum (convention) di komunitas Python adalah menyingkatnya menjadi `np`.

```python
import numpy as np
```

#### Membuat Array
Perbedaan utama antara list Python biasa dan array NumPy adalah array NumPy harus berisi data dengan tipe yang sama (homogen), yang membuatnya jauh lebih cepat untuk operasi matematika.

```python
# Membuat array dari list
arr = np.array([1, 2, 3, 4, 5])
print(arr)

# Membuat array 2 dimensi (matriks)
matriks = np.array([[1, 2, 3], [4, 5, 6]])
print(matriks)
```

#### Operasi Matematika
Anda bisa melakukan operasi matematika langsung pada seluruh elemen array.

```python
arr = np.array([1, 2, 3])
print(arr + 10) # Menambah 10 ke setiap elemen: [11 12 13]
print(arr * 2)  # Mengalikan setiap elemen dengan 2: [2 4 6]
```

### Menggunakan Pandas

Mari mengimpor Pandas, biasanya disingkat sebagai `pd`.

```python
import pandas as pd
```

#### DataFrame: Jantungnya Pandas
DataFrame adalah tabel data yang terdiri dari baris dan kolom. Anda bisa membayangkannya seperti lembar kerja di Excel.

Mari kita buat DataFrame sederhana dari dictionary:

```python
data = {
    'Nama': ['Budi', 'Siti', 'Agus', 'Dewi'],
    'Usia': [25, 30, 22, 28],
    'Pekerjaan': ['Programmer', 'Data Analyst', 'Desainer', 'Marketer']
}

df = pd.DataFrame(data)
print(df)
```

Output:
```
   Nama  Usia     Pekerjaan
0  Budi    25    Programmer
1  Siti    30  Data Analyst
2  Agus    22      Desainer
3  Dewi    28      Marketer
```

#### Membaca Data
Dalam praktiknya, Anda jarang membuat DataFrame secara manual. Biasanya Anda akan memuat data dari file eksternal seperti CSV atau Excel.

```python
# Membaca file CSV
df = pd.read_csv('data_penjualan.csv')

# Membaca file Excel
# df = pd.read_excel('data_penjualan.xlsx')
```

#### Eksplorasi Data Awal
Setelah data dimuat, hal pertama yang harus dilakukan adalah memahaminya.

*   **`df.head()`**: Melihat 5 baris pertama data.
*   **`df.info()`**: Mendapatkan ringkasan tentang tipe data dan nilai yang hilang (missing values).
*   **`df.describe()`**: Melihat statistik deskriptif (rata-rata, min, max, standar deviasi) untuk kolom numerik.

```python
print(df.head())
print(df.describe())
```

#### Seleksi dan Filter Data

Salah satu kekuatan utama Pandas adalah kemampuannya "mengiris" (slice) dan menyaring data.

**1. Memilih Kolom**
```python
# Mengambil kolom 'Nama' saja
nama = df['Nama']
```

**2. Filter Baris (Query)**
Misalkan kita ingin mencari karyawan yang usianya di atas 25 tahun:

```python
diatas_25 = df[df['Usia'] > 25]
print(diatas_25)
```

**3. Menggunakan `loc` dan `iloc`**
*   `loc`: Seleksi berdasarkan Label (nama baris/kolom).
*   `iloc`: Seleksi berdasarkan Posisi (indeks integer).

```python
# Baris ke-0, kolom 'Pekerjaan'
print(df.loc[0, 'Pekerjaan']) 

# Baris pertama, kolom kedua
print(df.iloc[0, 1]) 
```

### Studi Kasus Sederhana: Analisis Nilai Siswa

Mari kita gabungkan semuanya dalam satu contoh skrip analisis sederhana.

```python
import pandas as pd
import numpy as np

# Simulasi data nilai siswa
data_nilai = {
    'Siswa': ['Ali', 'Budi', 'Cici', 'Dedi', 'Euis'],
    'Matematika': [85, 90, 75, 60, 95],
    'Fisika': [80, 88, 70, 65, 92]
}

df = pd.DataFrame(data_nilai)

# 1. Menghitung Rata-rata Nilai Setiap Siswa
# Axis=1 berarti operasi dilakukan per baris (horizontal)
df['Rata_rata'] = df[['Matematika', 'Fisika']].mean(axis=1)

# 2. Menentukan Status Lulus/Tidak (Kriteri: Rata-rata >= 75)
# Kita menggunakan numpy.where untuk logika if-else cepat
df['Status'] = np.where(df['Rata_rata'] >= 75, 'Lulus', 'Remedial')

print("--- Hasil Analisis Nilai ---")
print(df)

print("\n--- Statistik Kelas ---")
print(f"Nilai Matematika Tertinggi: {df['Matematika'].max()}")
print(f"Rata-rata Kelas (Total): {df['Rata_rata'].mean()}")
```

### Sumber Daya Tambahan (External Resources)

Untuk mendalami lebih lanjut tentang kedua library ini, Anda bisa mengunjungi dokumentasi resminya:

*   **NumPy Official Documentation**: [https://numpy.org/doc/stable/](https://numpy.org/doc/stable/)
*   **Pandas Official Documentation**: [https://pandas.pydata.org/docs/](https://pandas.pydata.org/docs/)
*   **10 Minutes to pandas**: Tutorial singkat resmi dari Pandas untuk pemula. [https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html](https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html)

### Kesimpulan

Data Analytics dengan Python membuka pintu wawasan yang tak terbatas. **NumPy** memberikan fondasi komputasi yang cepat, sementara **Pandas** memberikan kemudahan dalam manipulasi data tabular. Kombinasi keduanya adalah senjata utama bagi setiap Data Scientist.

Di tutorial selanjutnya, kita akan belajar bagaimana memvisualisasikan data ini menjadi grafik yang menarik menggunakan **Matplotlib** dan **Seaborn**.

> <a href="https://github.com/devmode-id/belajarpython.com/blob/master/src/tutorial/data-analytics-pandas-numpy-python.md" target="_blank" rel="noopener noreferrer">
> Edit tutorial ini
> </a>

<div class="mt-8 flex justify-between gap-x-2 md:gap-x-4">
  <div class="flex justify-start">
    <a href="/tutorial/memory-management-python" class="text-primary-300 hover:text-primary-300 flex h-10 md:h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-4 md:px-8 text-sm md:text-base hover:no-underline md:">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Memory Management</span>
    </a>
  </div>
  <div class="flex justify-end">
    <!-- Next link is empty for now as this is the last one implemented -->
  </div>
</div>
