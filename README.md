## AI Model Experiment & Evaluation

### Deskripsi

Di tugas ini, ulasan produk e-commerce dikelompokkan menjadi positif atau negatif. Saya membandingkan model Scikit-learn dengan Gemini menggunakan dataset dan data test yang sama.

### Pendekatan

1. **Model klasik:** TF-IDF dan Logistic Regression dari Scikit-learn.
2. **Gemini:** zero-shot prompt melalui Gemini Interactions API dengan model `gemini-3.8-flash`.

Notebook menghitung Accuracy, weighted Precision/Recall/F1-Score, dan waktu proses.

### Hasil Eksperimen

Data dibagi dengan rasio 80:20 (`random_state=42`), lalu kedua model diuji pada 40 ulasan yang sama. TF-IDF + Logistic Regression mendapat Accuracy, Precision, Recall, dan F1-Score sebesar 1,00. Confusion matrix-nya menunjukkan 18 ulasan negatif dan 22 ulasan positif berhasil diprediksi dengan benar. Prosesnya memerlukan sekitar 0,10 detik.

Gemini juga mendapat nilai 1,00 untuk keempat metrik tersebut, dengan confusion matrix yang sama: 18 ulasan negatif dan 22 ulasan positif diprediksi dengan benar. Satu request untuk seluruh data test memerlukan sekitar 324,62 detik. Waktu ini dapat berbeda tergantung kondisi API dan koneksi internet.

### Struktur Project

```text
model-experiment-assignment/
├── data/
│   └── customer_reviews_sentiment.csv - customer_reviews_sentiment.csv
├── notebook/
│   └── starter_notebook.ipynb
├── README.md
└── requirements.txt
```

Dataset dipakai apa adanya. Notebook membaca kolom `review_text` dan `sentiment`.

### Menjalankan Eksperimen

1. Buat dan aktifkan virtual environment, lalu install dependensi:

   ```powershell
   python -m pip install -r requirements.txt
   ```

2. Atur API key Gemini sebagai environment variable di PowerShell (jangan menaruh key di notebook atau README):

   ```powershell
   $env:GEMINI_API_KEY = "API_KEY_ANDA"
   ```

3. Buka `notebook/starter_notebook.ipynb` di VS Code, pilih environment project sebagai kernel, lalu jalankan semua cell dari atas secara berurutan.

Gemini mengirim seluruh data test dalam satu request dan meminta satu label untuk setiap ulasan. Jika kuota habis, request gagal, atau format jawabannya tidak sesuai, notebook akan menampilkan error dan tidak menghitung metrik dari hasil yang belum lengkap.

### Analisis Trade-off

Pada 40 ulasan test, Logistic Regression dan Gemini sama-sama mendapat Accuracy, Precision, Recall, dan F1-Score sebesar 1,00. Tidak ada ulasan yang salah diklasifikasikan pada percobaan ini.

Perbedaan utamanya ada pada waktu. Logistic Regression memproses data dalam sekitar 0,10 detik dan berjalan di komputer sendiri. Model ini perlu dilatih, tetapi setelah itu ulasan tidak perlu dikirim ke layanan online. Kekurangannya, model belajar dari pola kata pada data latihan sehingga belum tentu memahami konteks dengan baik. Gemini tidak perlu dilatih dengan dataset ini dan hasilnya pada percobaan ini sama baiknya. Namun, satu request untuk seluruh data test memerlukan sekitar 325 detik dan tetap bergantung pada internet serta kuota API. Penggunaan API mungkin dikenai biaya sesuai pengaturan akun.

### Rekomendasi

Untuk tugas ini, saya merekomendasikan TF-IDF + Logistic Regression. Hasilnya sama dengan Gemini pada 40 data test, tetapi prosesnya jauh lebih cepat dan tidak membutuhkan internet atau kuota API. Hasil ini hanya berdasarkan 40 ulasan test, jadi belum tentu sama untuk kumpulan ulasan lain.

### Alur Eksperimen

**Prepare:** membaca dataset dan memahami label sentimennya.
**Experiment:** membagi data, melatih model klasik, dan meminta Gemini memprediksi data test yang sama.
**Evaluate:** membandingkan metrik, confusion matrix, dan waktu proses.
**Recommend:** memilih pendekatan berdasarkan hasil dan kebutuhan penggunaan.
