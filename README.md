# 📑 **Pipeline Pemrosesan & Ekstraksi Tanda Tangan (Signature Processing Pipeline)**

Notebook ini dirancang untuk memproses berkas tanda tangan digital secara massal (*batch processing*) menggunakan pustaka **OpenCV (Python)**. Terdapat dua pendekatan alur kerja utama yang dapat Anda gunakan sesuai kebutuhan proyek Anda.

---

## 🚀 **Alur Kerja Utama (Workflow Overview)**

### **1. Image Processing V1 (Standard Grayscale & Binarization)**
Alur kerja ini memproses tanda tangan menjadi format binarisasi hitam-putih murni berukuran tetap atau asli:
* **Data Loading**: Mengekstrak berkas arsip `TandaTangan - Package.zip` secara otomatis.
* **Grayscale Conversion**: Mengubah gambar masukan berwarna ke skala abu-abu untuk fokus pada struktur goresan.
* **Otsu Binarization**: Memisahkan goresan tinta hitam secara bersih dari kertas/bayangan menggunakan ambang batas otomatis Otsu (`cv2.THRESH_BINARY`).
* **Dual Mode Size Options**:
  * Versi Standar: Menyimpan dengan resolusi seragam $224 \times 224$ piksel.
  * Versi Ukuran Asli (*Original Size*): Menyimpan gambar binarisasi tanpa mengubah dimensi awal berkas.

### **2. Image Processing V2 (Latar Belakang Transparan / Transparent PNG)**
Alur kerja ini berfokus pada penghapusan latar belakang kertas untuk menghasilkan stiker tanda tangan transparan:
* **Luminance Thresholding**: Menghitung tingkat kecerahan piksel untuk mengisolasi goresan tinta.
* **Alpha Channel Creation**: Mengatur bagian kertas menjadi transparan (Alpha = 0) dan mempertahankan warna alami goresan pena asli.
* **Auto-Trim Margin**: Memotong ruang kosong putih di sekitar tanda tangan secara otomatis agar hasil akhir presisi dengan tambahan batas aman (*padding*).
* **Format Ekspor**: Disimpan sebagai `.png` dengan dukungan transparansi penuh.

---

## 🛠️ **Struktur Direktori**
* `/content/input_signatures/` : Folder tempat mengunggah file `.zip` tanda tangan Anda.
* `/content/extracted_signatures/` : Hasil ekstraksi otomatis dari paket zip.
* `/content/PROCESSED_OUTPUT/` : Folder penyimpanan hasil akhir pemrosesan tanda tangan.

---

## 📥 **Cara Menggunakan**
1. Unggah berkas `.zip` tanda tangan Anda ke direktori `/content/input_signatures/` dengan nama `TandaTangan - Package.zip`.
2. Jalankan sel **RAW FILE UPLOAD** untuk mengekstrak berkas.
3. Pilih dan jalankan salah satu pipeline pemrosesan yang diinginkan (**V1** untuk kebutuhan biner hitam-putih, atau **V2** untuk transparan PNG).
4. Gunakan blok **Result Preview** untuk mengonfirmasi hasil visualisasi.
5. Jalankan blok **BATCH DOWNLOAD** untuk mengunduh semua hasil dalam satu berkas `.zip` langsung ke komputer Anda.
