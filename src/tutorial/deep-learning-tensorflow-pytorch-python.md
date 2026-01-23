---
layout: tutorial.njk
title: Deep Learning dengan TensorFlow & PyTorch
order: 40
permalink: /tutorial/deep-learning-tensorflow-pytorch-python/
---

<img src="/img/tutorial/40-deep-learning-python.png" alt="Deep Learning dengan TensorFlow dan PyTorch" class="w-full rounded-lg shadow-md mb-6" loading="lazy">

Jika Machine Learning adalah mesin mobil, maka Deep Learning adalah mesin jet. Deep Learning adalah subset dari Machine Learning yang meniru cara kerja otak manusia menggunakan **Artificial Neural Networks (ANN)** yang bertingkat-tingkat ("deep").

Teknologi ini adalah otak di balik *self-driving cars*, ChatGPT, pengenalan wajah di HP Anda, dan generator gambar AI. Dua raksasa utama dalam dunia Deep Learning saat ini adalah **TensorFlow** (Google) dan **PyTorch** (Meta/Facebook).

### Apa itu Neural Network?
Bayangkan jaringan neuron di otak. Setiap neuron menerima sinyal, memprosesnya, dan meneruskannya. Dalam Deep Learning:
1.  **Input Layer**: Menerima data mentah (misalnya piksel gambar).
2.  **Hidden Layers**: Lapisan di tengah yang mengekstraksi fitur-fitur kompleks. Semakin banyak lapisannya, semakin "dalam" (deep) jaringannya.
3.  **Output Layer**: Memberikan hasil prediksi (misalnya "Kucing" atau "Anjing").

### TensorFlow vs PyTorch
*   **TensorFlow / Keras**: Sangat populer di industri, mudah digunakan (dengan Keras API), dan bagus untuk deployment produksi.
*   **PyTorch**: Sangat populer di kalangan peneliti (researchers), lebih fleksibel, dan "Pythonic".

Dalam tutorial ini, kita akan menggunakan **TensorFlow dengan Keras** karena sintaksnya yang sangat ramah pemula.

### Studi Kasus: Mengenali Angka Tulisan Tangan (MNIST)

Kita akan melatih komputer untuk membaca tulisan tangan angka 0-9.

#### 1. Instalasi

```bash
pip install tensorflow
```

#### 2. Memuat Data

```python
import tensorflow as tf
import matplotlib.pyplot as plt

# Memuat dataset MNIST (dataset "Hello World" di Deep Learning)
mnist = tf.keras.datasets.mnist
(x_train, y_train), (x_test, y_test) = mnist.load_data()

# Normalisasi data (mengubah nilai piksel dari 0-255 menjadi 0-1)
# Ini membantu Neural Network belajar lebih cepat
x_train, x_test = x_train / 255.0, x_test / 255.0

print(f"Ukuran data latih: {x_train.shape}") # (60000, 28, 28)
```

#### 3. Membangun Model Neural Network

Kita akan membuat model sekuensial sederhana.

```python
model = tf.keras.models.Sequential([
  # Flatten: Mengubah gambar 2D (28x28) menjadi baris 1D (784 piksel)
  tf.keras.layers.Flatten(input_shape=(28, 28)),
  
  # Dense Layer: Lapisan tersembunyi dengan 128 neuron dan fungsi aktivasi ReLU
  tf.keras.layers.Dense(128, activation='relu'),
  
  # Dropout: Mematikan 20% neuron secara acak saat latihan untuk mencegah overfitting
  tf.keras.layers.Dropout(0.2),
  
  # Output Layer: 10 neuron (untuk angka 0-9) dengan aktivasi Softmax (probabilitas)
  tf.keras.layers.Dense(10, activation='softmax')
])
```

#### 4. Kompilasi dan Pelatihan

```python
# Menentukan optimizer dan loss function
model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])

# Melatih model (Epochs = berapa kali model melihat seluruh data)
print("Mulai melatih model...")
model.fit(x_train, y_train, epochs=5)
```

Output akan menunjukkan akurasi yang meningkat di setiap epoch. Biasanya mencapai **97-98%** dalam waktu kurang dari 1 menit!

#### 5. Evaluasi

```python
loss, accuracy = model.evaluate(x_test, y_test)
print(f"Akurasi pada data uji: {accuracy * 100:.2f}%")
```

### Sumber Daya Tambahan (External Resources)

*   **TensorFlow Tutorials**: [https://www.tensorflow.org/tutorials](https://www.tensorflow.org/tutorials)
*   **PyTorch Tutorials**: [https://pytorch.org/tutorials/](https://pytorch.org/tutorials/)
*   **Fast.ai**: Kursus Deep Learning gratis yang sangat bagus. [https://www.fast.ai/](https://www.fast.ai/)

### Kesimpulan

Anda baru saja membuat jaringan saraf tiruan yang bisa melihat! Deep Learning adalah bidang yang luas. Setelah ini, Anda bisa mempelajari **CNN (Convolutional Neural Network)** untuk pemrosesan gambar yang lebih canggih, atau **RNN/Transformers** untuk pemrosesan teks (NLP).

> <a href="https://github.com/devmode-id/belajarpython.com/blob/master/src/tutorial/deep-learning-tensorflow-pytorch-python.md" target="_blank" rel="noopener noreferrer">
> Edit tutorial ini
> </a>

<div class="mt-8 flex justify-between gap-x-2 md:gap-x-4">
  <div class="flex justify-start">
    <a href="/tutorial/implementasi-machine-learning-python" class="text-primary-300 hover:text-primary-300 flex h-10 md:h-12 items-center rounded-full bg-blue-500 bg-opacity-20 px-4 md:px-8 text-sm md:text-base hover:no-underline md:">
      <svg xmlns="http://www.w3.org/2000/svg" class="mr-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm.707-10.293a1 1 0 00-1.414-1.414l-3 3a1 1 0 000 1.414l3 3a1 1 0 001.414-1.414L9.414 11H13a1 1 0 100-2H9.414l1.293-1.293z" clip-rule="evenodd" />
      </svg>
      <span class="-mt-0.5">Machine Learning</span>
    </a>
  </div>
  <div class="flex justify-end">
    <a href="/tutorial/cybersecurity-ethical-hacking-python" class=" flex h-10 md:h-12 items-center rounded-full bg-gradient-to-l from-yellow-500 to-yellow-400 px-4 md:px-8 text-sm md:text-base text-black shadow-xl hover:text-black hover:no-underline hover:shadow md:">
      <span class="-mt-0.5">Cybersecurity</span>
      <svg xmlns="http://www.w3.org/2000/svg" class="ml-1 h-4 w-4 md:h-5 md:w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zm3.707-8.707l-3-3a1 1 0 00-1.414 1.414L10.586 9H7a1 1 0 100 2h3.586l-1.293 1.293a1 1 0 101.414 1.414l3-3a1 1 0 000-1.414z" clip-rule="evenodd" />
      </svg>
    </a>
  </div>
</div>
