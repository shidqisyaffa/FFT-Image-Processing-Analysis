# FFT Image Processing & Analysis

Proyek ini berisi implementasi berbagai teknik pemrosesan citra berbasis transformasi Fourier (FFT) menggunakan Python, OpenCV, dan NumPy.

## Fitur

Proyek ini mencakup 4 bagian utama:

1. **FFT, Spektrum, dan Filter Frekuensi Dasar**
2. **Homomorphic Filtering**
3. **Phase Correlation (Deteksi Pergeseran)**
4. **Analisis dan Deteksi Pola Frekuensi (Tekstur)**

## Persyaratan Sistem

### Library yang Dibutuhkan

```bash
pip install opencv-python numpy matplotlib requests pandas
```

### Versi Python
- Python 3.7 atau lebih tinggi

## Struktur Kode

### 1. FFT dan Filter Frekuensi Dasar

Bagian ini mendemonstrasikan:
- Komputasi FFT 2D dan spektrum magnitudo
- Low-pass filtering (meloloskan frekuensi rendah)
- High-pass filtering (meloloskan frekuensi tinggi)

**Fungsi Utama:**
- `compute_fft_and_magnitude(img)` - Menghitung FFT dan magnitudo spektrum
- `apply_filter(Fshift, mask)` - Menerapkan mask filter pada domain frekuensi

**Output:** Visualisasi citra asli, spektrum frekuensi, dan hasil filtering

### 2. Homomorphic Filtering

Teknik untuk meningkatkan citra dengan memperbaiki illuminasi dan meningkatkan detail.

**Parameter:**
- `D0`: Radius cut-off (default: 30)
- `gammaL`: Gain untuk komponen frekuensi rendah (default: 0.5)
- `gammaH`: Gain untuk komponen frekuensi tinggi (default: 2.0)
- `c`: Konstanta sharpness (default: 1.0)

**Fungsi Utama:**
- `homomorphic_filter(img_asli, D0, gammaL, gammaH, c)` - Implementasi filter homomorphic

**Output:** Citra dengan illuminasi yang lebih baik dan detail yang lebih tajam

### 3. Phase Correlation (Deteksi Pergeseran)

Mendeteksi pergeseran translasi antara dua frame menggunakan phase correlation.

**Fungsi Utama:**
- `preprocess_for_motion(img)` - Pre-processing dengan Canny edge detection
- `phase_corr_shift(f1, f2)` - Menghitung pergeseran (dy, dx) antara dua citra

**Fitur:**
- Deteksi arah pergerakan (horizontal dan vertikal)
- Windowing dengan Hanning window untuk hasil lebih akurat
- Automatic resize jika ukuran frame berbeda

**Output:** Nilai pergeseran dalam piksel dan arah pergerakan

### 4. Analisis dan Deteksi Pola Frekuensi

Menganalisis dan mendeteksi pola tekstur dominan dalam citra.

**Fungsi Utama:**
- `compute_fft_logmag(gray)` - Komputasi FFT dengan log magnitude
- `suppress_dc(logmag, center, radius)` - Supresi komponen DC
- `greedy_peaks(logmag, center, topk, min_dist)` - Deteksi puncak frekuensi dominan
- `show_metrics(peaks, H, W)` - Menghitung periode dan sudut spasial pola

**Output:** 
- Visualisasi spektrum dengan puncak yang terdeteksi
- Tabel metrik berisi periode (dalam piksel) dan sudut spasial (dalam derajat)

## Cara Penggunaan

### Konfigurasi URL Gambar

Sebelum menjalankan kode, ganti URL gambar sesuai kebutuhan:

```python
URL_gambar = "URL_GAMBAR_ANDA"      # Untuk bagian 1 & 2
URL_FRAME1 = "URL_FRAME_1"          # Untuk bagian 3
URL_FRAME2 = "URL_FRAME_2"          # Untuk bagian 3
URL_PATTERN = "URL_PATTERN_TEKSTUR" # Untuk bagian 4
```

### Menjalankan Kode

Jalankan setiap bagian secara terpisah atau seluruh kode sekaligus:

```bash
python nama_file.py
```

### Contoh Output

**Bagian 1 - FFT Dasar:**
- Citra asli dan spektrum frekuensi
- Hasil low-pass dan high-pass filtering

**Bagian 2 - Homomorphic:**
- Citra asli, spektrum log, dan hasil filtering

**Bagian 3 - Phase Correlation:**
- Dua frame input dan informasi pergeseran di console

**Bagian 4 - Deteksi Pola:**
- Citra input dan spektrum dengan puncak terdeteksi
- Tabel metrik pola (periode dan sudut)

## Fungsi Pembantu

### `read_image_from_url(url, is_grayscale=True)`

Mengunduh dan membaca gambar dari URL.

**Parameter:**
- `url` (str): URL gambar
- `is_grayscale` (bool): True untuk grayscale, False untuk RGB

**Return:** Array NumPy (OpenCV format) atau None jika gagal

## Catatan Penting

1. **Format URL**: Pastikan URL mengarah langsung ke file gambar (.jpg, .png, dll)
2. **Ukuran Gambar**: Untuk phase correlation, jika ukuran frame berbeda, frame kedua akan di-resize otomatis
3. **Koneksi Internet**: Diperlukan koneksi internet untuk mengunduh gambar dari URL
4. **Error Handling**: Semua fungsi dilengkapi dengan error handling untuk menangani kegagalan download atau decoding

## Penjelasan Teknis

### FFT (Fast Fourier Transform)
Mengubah citra dari domain spasial ke domain frekuensi, memungkinkan analisis dan filtering berbasis frekuensi.

### Homomorphic Filtering
Memisahkan komponen illuminasi (frekuensi rendah) dan reflectance (frekuensi tinggi) untuk meningkatkan kualitas citra.

### Phase Correlation
Memanfaatkan sifat pergeseran dalam domain Fourier untuk mendeteksi translasi dengan akurasi sub-piksel.

### Analisis Pola Tekstur
Mengidentifikasi periodicitas dan orientasi pola tekstur melalui analisis spektrum frekuensi.

## Troubleshooting

**Problem:** Gambar tidak dapat diunduh
- **Solusi:** Periksa koneksi internet dan validitas URL

**Problem:** Error ukuran gambar pada phase correlation
- **Solusi:** Kode sudah menangani ini dengan auto-resize

**Problem:** Hasil filter tidak sesuai harapan
- **Solusi:** Sesuaikan parameter filter (radius mask, D0, gammaL, gammaH)

## Lisensi

Kode ini dibuat untuk tujuan edukatif dan penelitian.

## Kontributor

Silakan berkontribusi dengan membuat pull request atau melaporkan issue.

---

**Catatan:** Pastikan untuk mematuhi hak cipta dan ketentuan penggunaan saat mengunduh gambar dari URL eksternal.