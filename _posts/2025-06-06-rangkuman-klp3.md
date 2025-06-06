---
title: Rangkuman Desain dan Analisis Algoritma
date: 2025-06-06 14:50:00 +0800
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Kelompok 1 - Huffman Coding
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
Terdapat sebuah `String = "BCCABBDDAECCBBAEDDCC"`

- Frekuensi :

|  Huruf  | Frekuensi |
|:-------:|:---------:|
|    A    |     3     |
|    B    |     5     |
|    C    |     6     | 
|    D    |     4     |
|    E    |     2     |

- Langkah pertama: Urutkan jumlah kemunculan huruf dari yang terkecil ke yang terbesar

  [E-2]  [A-3] [D-4]  [B-5] [C-6]

---

- Langkah kedua: Kemudian ambil dua node yang paling kecil dan gabungkan keduanya. `E + A = 5`

```plaintext
       [5]
      /   \
  [E-2]  [A-3] [D-4]  [B-5] [C-6]
```

---

- Langkah ketiga: Kemudian, `ambil dua nilai terkecil dan gabungkan`. Di sini, `5` dan `4` adalah yang terkecil, jadi kita gabungkan menjadi `5 + D[4] = 9`
                
```plaintext
          [9]            
         /   \            
        /     \            
       [5]     \          
      /   \     \      
  [E-2]  [A-3] [D-4]  [B-5] [C-6]
```

---

- Langkah keempat: Kemudian, `ambil dua nilai terkecil dan gabungkan`. Di sini, `4` dan `6` adalah yang terkecil, jadi kita gabungkan menjadi `B[5] + C[6] = 11`

```plaintext
          [9]            
         /   \            
        /     \            
       [5]     \          [11]
      /   \     \         /  \
  [E-2]  [A-3] [D-4]  [B-5] [C-6]
```

---

- Langkah kelima: Gabungkan `9` dan `11` = `20`

```plaintext
                [20]
               /    \
              /      \
             /        \
            /          \
           /            \
          [9]            \
         /   \            \
        /     \            \
       [5]     \          [11]
      /   \     \         /  \
  [E-2]  [A-3] [D-4]  [B-5] [C-6]
```

---

- Langkah keenam: Tandai sisi kiri dengan 0 dan sisi kanan dengan 1, kemudian lakukan transversal dari node akar ke setiap huruf. Misalkan kita ingin menuju A dari node akar `20`, maka jaeaknya akan menjadi `001`, untuk B menjadi `10` dan seterusnya.

```plaintext
                [20]
               /    \
              /      \
             /        \
            /          \
       `0` /            \ `1`
          [9]            \
         /   \            \
     `0`/     \            \
       [5]     \          [11]
   `0`/`1`\  `1`\      `0`/  \ `1`
  [E-2]  [A-3] [D-4]  [B-5] [C-6]
```

---

Untuk `A`, kita membutuhkan `3 bit`, untuk `B 2 bit`, `C 2 bit`, `D 2 bit` dan ke `E 3 bit`

Untuk A jumlah = 3 jadi total nya 3 x 3 = 9 bit. Begitu seterusnya

|  Huruf  |   Kode   | Frekuensi | Total bit |
|:-------:|:--------:|:---------:|:---------:|
|    A    |   001    |     3     |     9     |
|    B    |    10    |     5     |    10     |
|    C    |    11    |     6     |    12     |
|    D    |    01    |     4     |     8     |
|    E    |   000    |     2     |     6     |

**Tanpa Kompresi (Fixed-length encoding)**
Jumlah karakter unik = 5 (A, B, C, D, E)
→ Maka setiap karakter butuh 3 bit (2³ = 8 kemungkinan, cukup untuk 5 karakter)

Jumlah karakter total = 20
→ Total bit tanpa kompresi = 20 × 3 = `60 bit`

**Dengan Huffman Coding** = Total `45 bit`

---

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
- ✅ Lossless: tidak ada data yang hilang.
- ✅ Efisien untuk data dengan distribusi karakter tidak merata.
- ✅ Digunakan luas di sistem 

**Kekuranan**
- ❌ Kurang optimal jika frekuensi karakter merata.
- ❌ Memerlukan tabel kode untuk dekompresi.

---


