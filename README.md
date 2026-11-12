---
title: "Komputasi Numerik"
author: "Ardiansyah Wahyu Hartono"
---
| Keterangan | Informasi |
| :--- | :--- |
| **Nama Mahasiswa** | Ardiansyah Wahyu Hartono |
| **NIM** | 202511420040 |
| **Nama Dosen** | Budi Santoso, S.T., M.T. |
| **NIDN** | 0715117402 |
| **NUPTK** | 3447752653130113 |

---

# 🧮 Penyelesaian Sistem Persamaan Linear (SPL) menggunakan Metode Eliminasi Gauss

> **Panduan & Dokumentasi Kode Python** untuk implementasi metode numerik Eliminasi Gauss dengan Python (Google Colab / Jupyter Notebook).

---

## 📌 Daftar Isi
- [Tentang Program](#-tentang-program)
- [Struktur Sel & Kode Program](#-struktur-sel--kode-program)
  - [Sel 1: Import Library](#sel-1-import-library)
  - [Sel 2: Definisi Matriks Augmented](#sel-2-definisi-matriks-augmented)
  - [Sel 3: Proses Substitusi Mundur & Eliminasi](#sel-3-proses-substitusi-mundur--eliminasi)
  - [Sel 4: Eksekusi Program & Hasil Akhir](#sel-4-eksekusi-program--hasil-akhir)
- [📊 Hasil Eksekusi Program](#-hasil-eksekusi-program)

---

## 🎯 Tentang Program
Program ini dirancang untuk menyelesaikan Sistem Persamaan Linear (SPL) secara komputasional menggunakan **Metode Eliminasi Gauss**. Prosesnya dibagi menjadi beberapa tahapan utama:
1. Pembentukan Matriks Augmented dari koefisien dan konstanta.
2. Proses **Eliminasi Maju** untuk mengubah matriks menjadi bentuk segitiga atas.
3. Proses **Substitusi Mundur** (*Back-Substitution*) untuk mendapatkan nilai dari masing-masing variabel ($x_1, x_2, x_3$).

---

## 📂 Struktur Sel & Kode Program

### 📝 Sel 1: Import Library
> **Fungsi:** Memasukkan (*import*) library `numpy` ke dalam lingkungan eksekusi. Library ini sangat penting dan wajib ada karena menyediakan fungsi-fungsi untuk mengolah matriks dan array dengan mudah dalam perhitungan Eliminasi Gauss.

---

### 📝 Sel 2: Definisi Matriks Augmented
> **Fungsi:** Mendefinisikan Sistem Persamaan Linear (SPL) ke dalam bentuk Matriks Augmented (penggabungan antara matriks koefisien variabel dan matriks konstanta hasil di sebelah kanan). Tipe data diatur sebagai `float` agar hasil pembagian pecahan atau desimal tidak dibulatkan menjadi angka nol secara otomatis oleh Python.

---

### 💻 Sel 3: Proses Substitusi Mundur & Eliminasi
> **Fungsi:** Inti dari algoritma Eliminasi Gauss dan Substitusi Mundur. Melakukan Operasi Baris Elementer (OBE) secara otomatis untuk mengubah bagian bawah diagonal matriks menjadi angka 0, lalu menghitung nilai variabel dari bawah ke atas secara berurutan.

```python
# SEL 3: Proses Substitusi Mundur
def substitusi_mundur(M, n):
    x = np.zeros(n)
    for i in range(n - 1, -1, -1):
        x[i] = (M[i, -1] - np.dot(M[i, i+1:n], x[i+1:n])) / M[i, i]
    return x

# SEL 4: Input Data dan Menjalankan Program

# 1. Definisi Matriks Koefisien (A) dan Vektor Konstanta (b)
A = np.array([
    [2.0,  1.0, -1.0],
    [-3.0, -1.0,  2.0],
    [-2.0,  1.0,  2.0]
], dtype=float)

b = np.array([8.0, -11.0, -3.0], dtype=float)

# 2. Jalankan Langkah-Langkah
M, n = eliminasi_gauss(A, b)
M_segitiga = eliminasi_maju(M, n)
solusi = substitusi_mundur(M_segitiga, n)

# 3. Tampilkan Hasil Akhir
print("=== Hasil Solusi Variabel ===")
for i in range(n):
    print(f"x{i+1} = {solusi[i]:.2f}")


=== Matriks Augmented Awal ===
[[  2.   1.  -1.   8.]
 [ -3.  -1.   2. -11.]
 [ -2.   1.   2.  -3.]]

-----------------------------------

=== Matriks Setelah Eliminasi Maju (Segitiga Atas) ===
[[ 2.   1.  -1.   8. ]
 [ 0.   0.5  0.5  1. ]
 [ 0.   0.  -1.   1. ]]

-----------------------------------

=== Hasil Solusi Variabel ===
x1 = 2.00
x2 = 3.00
x3 = -1.00
