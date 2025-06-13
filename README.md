# Smart Pantry Chef - Capstone Project CC25-CF348


## Latar Belakang

Masalah umum yang sering dialami oleh mahasiswa kos maupun individu lainnya adalah banyaknya bahan makanan yang tersimpan namun tidak dimanfaatkan secara optimal. Hal ini seringkali terjadi karena kebingungan dalam menentukan menu masakan dari bahan yang tersedia. Terinspirasi dari kondisi ini, tim kami mengembangkan "Smart Pantry Chef", sebuah aplikasi web berbasis AI yang bertujuan untuk merekomendasikan resep makanan berdasarkan bahan-bahan yang dimiliki pengguna.

Sistem ini dirancang untuk memanfaatkan teknologi *computer vision* guna mendeteksi bahan dari gambar, serta sistem rekomendasi untuk memberikan saran resep yang relevan dan informatif.

## Tujuan Proyek

Tujuan utama dari proyek "Smart Pantry Chef" adalah:
* Menyediakan solusi praktis untuk masalah pengelolaan bahan makanan yang sering berujung pada pemborosan.
* Mengatasi kebingungan pengguna dalam menentukan menu masakan dari bahan-bahan yang mereka miliki.
* Mengoptimalkan pemanfaatan bahan makanan di dapur melalui rekomendasi resep yang cerdas dan informatif.

## Arsitektur & Teknologi

Proyek ini dibagi menjadi dua jalur utama: Machine Learning dan Pengembangan Web (FEBE).

| Komponen            | Teknologi yang Digunakan                                        |
| ------------------- | --------------------------------------------------------------- |
| **Machine Learning** | `Python`, `TensorFlow`, `Keras`, `Scikit-learn`, `Pandas`         |
| **Frontend** | `React.js`, `Vite`, `Tailwind CSS`                      |
| **Backend** | `Node.js`, `Express.js` (untuk RESTful API)               |

## Hasil Proyek

* **Model Machine Learning:** Berhasil membangun dan melatih model klasifikasi gambar dengan **akurasi sekitar 82%**  untuk mengenali **194 kategori bahan makanan** setelah melalui proses konsolidasi data yang ekstensif.
* **Aplikasi Web:** Berhasil mengembangkan antarmuka pengguna (frontend) yang responsif untuk proses login dan unggah gambar.
* **Status Integrasi:** Proyek menghadapi kendala pada integrasi model ML dengan backend karena masalah teknis (ketidakcocokan versi Node.js dengan tensorflow.js) dan keterbatasan sumber daya tim FEBE. [cite_start]Oleh karena itu, sistem rekomendasi end-to-end belum dapat dijalankan.

## Cara Mereplikasi Proyek

Berikut adalah langkah-langkah detail untuk mereplikasi pekerjaan yang telah kami lakukan.

### Bagian 1: Mereplikasi Model Machine Learning

Seluruh proses ini didokumentasikan dalam notebook Google Colab yang kami sediakan dan dapat dijalankan secara langsung.

**Prasyarat:**
* Akun Google dengan akses ke Google Colab.
* Akun Kaggle untuk mengunduh dataset (membutuhkan file `kaggle.json`).

**Langkah-langkah:**

1.  **Buka Notebook Colab:**
    * Buka notebook proyek kami di Google Colab: [Notebook ML Model](https://colab.research.google.com/drive/1DcOjcB2nV-XUg2acg5hbs/ML2AZp4rY?usp=shari)

2.  **Setup Environment:**
    * Jalankan sel pertama untuk menginstal library Kaggle.
    * Unggah file `kaggle.json` Anda saat diminta. Kode akan secara otomatis menempatkannya di direktori yang benar.

3.  **Unduh dan Ekstrak Dataset:**
    * Jalankan sel kode yang berisi perintah `!kaggle datasets download ...` dan `!unzip ...`. Skrip ini akan mengunduh 8 dataset yang kami gunakan, antara lain:
        * `recipe-ingredients-image-dataset`
        * `vegetable-image-dataset`
        * `food-and-beverage-labels`
        * `fruits`
        * `meat-freshness-image-dataset`
        * `indonesian-spices-dataset`
        * `indo-spices-new`
        * `food-image-classification-dataset`

4.  **Pra-pemrosesan Data Gambar:**
    * Skrip akan menggabungkan semua gambar dari 8 dataset ke dalam satu direktori utama (`dataset_bahan_gabungan`).
    * Selanjutnya, dilakukan proses **konsolidasi label**, di mana **330 label granular awal** (contoh: `apple_10`, `apple_braeburn_1`) dipetakan menjadi **194 kelas akhir** yang lebih bermakna (contoh: `apple`, `banana`). Proses ini didefinisikan dalam kamus `label_consolidation_map`.
    * Setelah konsolidasi, `LabelEncoder` dibuat dan disimpan sebagai `consolidated_label_encoder.pkl`.

5.  **Pembagian Data dan Pembuatan Generator:**
    * Dataset dibagi menjadi set training (70%), validasi (15%), dan testing (15%) secara *stratified*.
    * `ImageDataGenerator` dari Keras digunakan untuk membuat generator data, menerapkan augmentasi pada data training, dan normalisasi pada semua data.

6.  **Pelatihan Model:**
    * Model dibangun menggunakan arsitektur **MobileNetV2** sebagai *base model* (Transfer Learning). Lapisan klasifikasi kustom ditambahkan di atasnya.
    * Model dilatih menggunakan data generator yang telah dibuat. Model terbaik berdasarkan `val_loss` akan disimpan sebagai `best_model.h5`.

### Bagian 2: Menjalankan Aplikasi Web (FEBE)

**Prasyarat:**
* Node.js dan npm (atau yarn) terinstal.
* Git terinstal.

**Langkah-langkah:**

1.  **Clone Repository:**
    ```bash
    git clone [https://github.com/tahira0405/Capstone-Project-CC25-CF348.git](https://github.com/tahira0405/Capstone-Project-CC25-CF348.git)
    cd Capstone-Project-CC25-CF348
    ```

2.  **Menjalankan Frontend:**
    *(Asumsi direktori frontend ada di dalam repo)*
    ```bash
    # Masuk ke folder frontend (sesuaikan namanya jika berbeda)
    cd frontend 
    # Install dependencies
    npm install
    # Jalankan development server
    npm run dev
    ```

3.  **Menjalankan Backend:**
    *(Asumsi direktori backend ada di dalam repo)*
    ```bash
    # Masuk ke folder backend (sesuaikan namanya jika berbeda)
    cd backend
    # Install dependencies
    npm install
    # Jalankan server
    npm start
    ```
    [cite_start]**Catatan Penting:** Seperti yang disebutkan dalam *Project Brief*, terdapat kendala teknis pada integrasi model ML di backend. Skrip backend yang ada di repository mungkin belum mencakup fungsionalitas penuh untuk memanggil model ML.

## Tim Kami

| Peran | ID            | Nama                      | Institusi                     | Status   |
| ----- | ------------- | ------------------------- | ----------------------------- | -------- |
| ML    | MC002D5X1710  | Tahira Aliyya             | Institut Teknologi Bandung    | [Aktif]  |
| ML    | MC002D5X1313  | Salwa Sabira              | Institut Teknologi Bandung    | [Aktif]  |
| ML    | MC002D5Y0775  | Ghaisan Zaki Pratama      | Institut Teknologi Bandung    | [Aktif]  |
| FEBE  | FC787D5Y0281  | Arya Choirul Fikri        | Universitas Safin Pati        | [Aktif]  |
| FEBE  | FC009D5Y1052  | M. Daffa Atha Syahputra   | Universitas Gunadarma         | [Tidak Aktif]  |
| FEBE  | FC595D5Y0022  | Andri Adi Putra           | Universitas Sangga Buana YPKP | [Tidak Aktif]  |

---