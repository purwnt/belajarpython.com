---
layout: tutorial.njk
title: Model Context Protocol (MCP) dengan FastMCP
order: 47
permalink: /tutorial/ai-mcp-fastmcp-python/
---

<img src="/img/tutorial/47-ai-mcp-python.png" alt="Model Context Protocol (MCP) dengan FastMCP" class="w-full rounded-lg shadow-md mb-6" loading="lazy">

**Model Context Protocol (MCP)** adalah standar baru yang revolusioner yang memungkinkan asisten AI (seperti Claude, ChatGPT) untuk terhubung dengan sistem data eksternal Anda (database, file lokal, API) secara aman dan terstandarisasi.

Bayangkan MCP sebagai "USB port" untuk AI. Dulu, setiap integrasi AI harus dibuat custom. Dengan MCP, kita bisa membuat satu "server" yang bisa dibaca oleh berbagai klien AI.

### Mengapa MCP Penting?
Tanpa MCP, AI hanyalah chatbot pintar yang terisolasi. Dengan MCP, AI menjadi **Agen** yang bisa:
1.  Membaca file di komputer Anda.
2.  Mengakses database PostgreSQL perusahaan.
3.  Menjalankan perintah terminal.

### FastMCP: Cara Tercepat Membuat MCP Server
Kita akan menggunakan library **FastMCP** (mirip FastAPI tapi untuk MCP) untuk membuat server MCP sederhana.

#### Instalasi
```bash
pip install fastmcp
```

#### Membuat Server MCP Pertama
Kita akan membuat "tool" sederhana yang memungkinkan AI menghitung jumlah kata dalam teks (sesuatu yang seringkali salah dilakukan oleh LLM).

```python
from fastmcp import FastMCP

# Inisialisasi Server
mcp = FastMCP("My First Demo Tools")

# Definisi Tool
# Decorator @mcp.tool mengubah fungsi Python biasa menjadi tool yang bisa dipanggil AI
@mcp.tool()
def hitung_kata(teks: str) -> int:
    """Menghitung jumlah kata dalam sebuah teks dengan akurat."""
    if not teks:
        return 0
    return len(teks.split())

# Menjalankan Server
if __name__ == "__main__":
    mcp.run()
```

### Cara Kerja
1.  Anda menjalankan skrip di atas.
2.  Anda menghubungkan Claude Desktop App (atau klien MCP lain) ke server lokal ini.
3.  Saat Anda bertanya ke Claude: *"Tolong hitung kata di paragraf ini..."*, Claude akan melihat bahwa ia punya tool `hitung_kata`.
4.  Claude mengirim teks ke skrip Python Anda.
5.  Skrip Anda menghitungnya dan mengembalikan angka.
6.  Claude menjawab: *"Teks tersebut memiliki 45 kata."*

### Masa Depan AI Agent
MCP adalah fondasi masa depan di mana AI bukan hanya sekadar chatbot, tapi asisten yang benar-benar bisa bekerja dan berinteraksi dengan dunia digital Anda. Sebagai Python Developer, menguasai MCP menempatkan Anda di garis depan revolusi AI.

> <a href="https://github.com/devmode-id/belajarpython.com/blob/master/src/tutorial/ai-mcp-fastmcp-python.md" target="_blank" rel="noopener noreferrer">
> Edit tutorial ini
> </a>

<div class="mt-8 flex justify-between gap-x-2 md:gap-x-4">
  <div class="flex justify-start">
    <a href="/tutorial/devops-ci-cd-python" class="text-primary-300 hover:text-primary-300 flex h-10 md:h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-4 md:px-8 text-sm md:text-base hover:no-underline md:">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">DevOps & CI/CD</span>
    </a>
  </div>
  <div class="flex justify-end">
    <!-- End of Series -->
  </div>
</div>
