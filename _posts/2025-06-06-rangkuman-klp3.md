---
title: Rangkuman Desain dan Analisis Algoritma
date: 2025-05-05 07:30:00 +0800
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Kelompok 1 - Activity Selection Problem
---

## Huffman Coding

### Pengantar
Huffman Coding adalah algoritma yang digunakan untuk mengurangi ukuran data dengan cara mengganti simbol yang sering muncul dengan kode bit lebih pendek.

---

### Prinsip Kerja
- Berdasarkan frekuensi karakter dalam data.
- Karakter dengan frekuensi tinggi → kode pendek.
- Karakter dengan frekuensi rendah → kode panjang.
- Representasi data menggunakan pohon biner.

---

### Langkah Huffman Coding
1. Hitung frekuensi tiap karakter dalam data.
2. Buat simpul untuk setiap karakter.
3. Gabungkan dua simpul dengan frekuensi terkecil.
4. Ulangi hingga terbentuk satu pohon Huffman.
5. Tentukan kode biner untuk tiap karakter (0: kiri, 1: kanan).

---

### Contoh Kasus
Terdapat sebuah `String = "ABBCCCDDDD"`

- Frekuensi :
    - A : 1
    - B : 2
    - C : 3
    - D : 4
- Bangun pohon Huffman berdasarkan frekuensi
- Hasil kode mungkin : 

                [20]
               /    \
            [9]     [11]
           /   \     /   \
         [5]   [4] [5]   [6]
        / \    |   |     |
     E:2 A:3  D:4  C:4   B:6


### Implementasi Kode 
```cpp
Huffman(C)
    n = |C|
    Q = C
    for i = 1 to n - 1
        allocate new node z
        z.left = x = Extract-Min(Q)
        z.right = y = Extract-Min(Q)
        insert(Q, z)
    return Extract-Min(Q)
```
**Kompleksitas waktu = O(N log N)**
**(N = Jumlah karakter unik)**

---

### Kelebihan dan Kekurangan
**Kelebihan**
✅ Lossless: tidak ada data yang hilang.
✅ Efisien untuk data dengan distribusi karakter tidak merata.
✅ Digunakan luas di sistem 

**Kekuranan**
❌ Kurang optimal jika frekuensi karakter merata.
❌ Memerlukan tabel kode untuk dekompresi.

---


