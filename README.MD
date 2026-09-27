## AI Model Experiment & Evaluation

## Deskripsi

Eksperimen ini digunakan untuk mengklasifikasikan ulasan pelanggan menjadi dua label, yaitu `positif` dan `negatif`. Dataset berisi teks ulasan pelanggan, nama produk, dan label sentimen.

File dataset yang digunakan adalah:

data/customer_reviews_sentiment.csv - customer_reviews_sentiment.csv

Kolom utama yang digunakan:

- `review_text`: isi ulasan pelanggan
- `sentiment`: label `positif` atau `negatif`

### Pendekatan yang Digunakan

Ada dua pendekatan yang disiapkan di notebook:

1. Model klasik:  Decision Tree dari scikit-learn.
2. LLM API: Gemini API untuk memprediksi sentimen berdasarkan isi ulasan.



### Hasil Model Klasik

Model TF-IDF + Decision Tree menghasilkan evaluasi berikut pada data testing:

- Accuracy: 0.8250
- Precision: 0.8740
- Recall: 0.8250
- F1-Score: 0.8227

Confusion matrix menunjukkan bahwa 9 data negatif diprediksi sebagai positif dan 5 data positif diprediksi sebagai negatif.

Evaluasi Gemini belum selesai karena kuota request API terbatas. Oleh karena itu, hasil Gemini belum dibandingkan dengan angka model klasik.

### Trade-off dan Limitasi

TF-IDF + Decision Tree cukup cepat dan dapat dijalankan secara lokal tanpa koneksi API. Metode ini juga tidak membutuhkan biaya penggunaan API. Kekurangannya, model lebih bergantung pada kata-kata yang muncul pada data training dan belum tentu memahami konteks, sarkasme, typo, atau kata baru.

Gemini API lebih fleksibel dalam memahami teks, tetapi memiliki kuota request. Jika jumlah ulasan yang diproses banyak, penggunaannya juga dapat menimbulkan biaya yang lebih besar. Selain itu, prosesnya bergantung pada koneksi internet dan ketersediaan layanan API.

### Rekomendasi

Untuk dataset ini,Decision Tree cocok digunakan sebagai model awal karena sederhana, cepat, dan tidak membutuhkan API. Gemini dapat digunakan sebagai model pembanding setelah kuota API tersedia dan seluruh data testing berhasil diproses.

### Alur Eksperimen

Prepare dilakukan dengan menyiapkan dataset ulasan pelanggan dan memahami label sentimen.

Experiment dilakukan dengan melatih  Decision Tree dan menyiapkan inference Gemini API.

Evaluate dilakukan dengan mengukur Accuracy, Precision, Recall, dan F1-Score.

Recommend dilakukan dengan membandingkan kelebihan, keterbatasan, biaya, dan menentukan pendekatan yang sesuai.

### Cara Menjalankan Notebook

1. Buka folder project di VS Code.
2. Buka `notebook/starter_notebook.ipynb`.
3. Pilih Python interpreter atau kernel yang digunakan project.
4. Jalankan sel dari atas secara berurutan sampai bagian evaluasi model klasik.
5. Untuk menjalankan Gemini, masukkan API key melalui environment variable:

