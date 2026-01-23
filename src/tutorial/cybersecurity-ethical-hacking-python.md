---
layout: tutorial.njk
title: Cybersecurity & Ethical Hacking dengan Python
order: 41
permalink: /tutorial/cybersecurity-ethical-hacking-python/
---

<img src="/img/tutorial/41-cybersecurity-python.png" alt="Cybersecurity dan Ethical Hacking dengan Python" class="w-full rounded-lg shadow-md mb-6" loading="lazy">

Python sering disebut sebagai "bahasa hacker". Mengapa? Karena Python memiliki ribuan pustaka keamanan yang kuat dan sintaks yang memungkinkan penulisan skrip serangan atau pertahanan (automasi) dengan sangat cepat. Profesional keamanan siber menggunakan Python untuk segala hal, mulai dari **Penetration Testing**, **Analisis Malware**, hingga **Forensik Digital**.

*Disclaimer: Tutorial ini ditujukan semata-mata untuk tujuan pendidikan (Ethical Hacking). Jangan gunakan ilmu ini untuk menyerang sistem tanpa izin. Itu ilegal.*

### Pustaka Python untuk Security

Berikut beberapa library "wajib tau" bagi seorang Ethical Hacker:

1.  **Requests**: Untuk berinteraksi dengan HTTP (Web Scraping, API Fuzzing).
2.  **Scapy**: "Pisau Swiss Army" untuk manipulasi paket jaringan. Bisa membuat, membaca, dan memalsukan paket di level rendah.
3.  **Socket**: Untuk komunikasi jaringan dasar (membuat Port Scanner, Backdoor sederhana).
4.  **Hashlib**: Untuk enkripsi dan hashing password.

### Studi Kasus: Membuat Port Scanner Sederhana

Salah satu langkah pertama dalam *Reconnaissance* (pengumpulan informasi) adalah mengetahui port mana yang terbuka pada target. Mari kita buat alat pemindai port sederhana menggunakan modul bawaan `socket`.

```python
import socket
import datetime

# Tentukan target (IP Address)
target = "127.0.0.1" # GANTI dengan IP target Anda sendiri (atau localhost)

def port_scan(target_ip):
    print(f"--- Memulai scan pada host: {target_ip} ---")
    print(f"Waktu mulai: {datetime.datetime.now()}")
    
    try:
        # Scan port dari 20 sampai 80 (Port umum)
        for port in range(20, 81):  
            s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
            socket.setdefaulttimeout(1) # Timeout 1 detik jika tidak ada respon
            
            # Jika connect mengembalikan 0, berarti koneksi berhasil (Port Terbuka)
            result = s.connect_ex((target_ip, port))
            if result == 0:
                print(f"[+] Port {port} TERBUKA")
            
            s.close()
            
    except KeyboardInterrupt:
        print("\nScan dihentikan oleh pengguna.")
    except socket.gaierror:
        print("Hostname tidak dapat di-resolve.")
    except socket.error:
        print("Tidak bisa terhubung ke server.")

# Menjalankan scanner
# Pastikan Anda memiliki izin untuk scan target!
# port_scan(target) 
```

### Studi Kasus: Hashing Password (Defense)

Dalam pertahanan (Blue Team), kita belajar bahwa password tidak boleh disimpan dalam teks biasa. Kita harus menyimpannya sebagai hash.

```python
import hashlib

def hash_password(password):
    # Menggunakan algoritma SHA-256
    # Encode string ke bytes sebelum di-hash
    hashed_pass = hashlib.sha256(password.encode()).hexdigest()
    return hashed_pass

password_saya = "Rahasia123"
hash_saya = hash_password(password_saya)

print(f"Password Asli: {password_saya}")
print(f"Password Hash (SHA-256): {hash_saya}")

# Verifikasi
input_user = "Rahasia123"
if hash_password(input_user) == hash_saya:
    print("Login Berhasil!")
else:
    print("Password Salah!")
```

### Tips Keamanan Python:
1.  **Input Validation**: Selalu validasi input pengguna untuk mencegah **SQL Injection** atau **Command Injection**.
2.  **Update Library**: Gunakan `pip list --outdated` untuk memeriksa library yang rentan.
3.  **Virtual Environments**: Isolasi environment Anda agar malware yang mungkin Anda analisis tidak menginfeksi sistem utama.

### Sumber Daya Tambahan (External Resources)

*   **Black Hat Python**: Buku legendaris untuk belajar Python Security.
*   **OWASP**: Organisasi standar keamanan web. [https://owasp.org/](https://owasp.org/)
*   **Scapy Documentation**: [https://scapy.net/](https://scapy.net/)

### Kesimpulan

Python memberikan kekuatan besar di tangan praktisi keamanan. Dengan skrip beberapa baris, Anda bisa mengotomatisasi tugas keamanan yang kompleks. Namun, ingatlah etika "White Hat": Gunakan kemampuan Anda untuk mengamankan dan melindungi sistem, bukan merusaknya.

> <a href="https://github.com/devmode-id/belajarpython.com/blob/master/src/tutorial/cybersecurity-ethical-hacking-python.md" target="_blank" rel="noopener noreferrer">
> Edit tutorial ini
> </a>

<div class="mt-8 flex justify-between gap-x-2 md:gap-x-4">
  <div class="flex justify-start">
    <a href="/tutorial/deep-learning-tensorflow-pytorch-python" class="text-primary-300 hover:text-primary-300 flex h-10 md:h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-4 md:px-8 text-sm md:text-base hover:no-underline md:">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Deep Learning</span>
    </a>
  </div>
  <div class="flex justify-end">
    <a href="/tutorial/restful-api-fastapi-python" class=" flex h-10 md:h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-4 md:px-8 text-sm md:text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:">
      <span class="-mt-0.5">RESTful APIs</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
