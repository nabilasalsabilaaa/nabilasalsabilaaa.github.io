---

title: Rangkuman Desain dan Analisis Algoritma
date: 2025-06-07
categories: \[Desain dan Analisis Algoritma]
tags: \[DAA, rangkuman]
description: Kelompok 6 - Rat in a Maze
---------------------------------------

## Rat in a Maze

### Definisi

**Rat in a Maze** merupakan salah satu permasalahan algoritma klasik, di mana seekor tikus (rat) harus mencari jalan keluar dari sebuah labirin (maze) dalam bentuk matriks NxN. Tikus memulai dari titik awal di pojok kiri atas (0, 0) dan harus mencapai titik akhir di pojok kanan bawah (N-1, N-1). Tikus hanya boleh melangkah pada sel dengan nilai 1, dan tidak boleh mengunjungi sel lebih dari satu kali dalam satu jalur.

Masalah ini dapat diselesaikan menggunakan algoritma **Backtracking**, yaitu mencoba semua kemungkinan jalur yang tersedia, dan jika tidak berhasil maka kembali (mundur) ke langkah sebelumnya untuk mencoba jalur lain.

---

### Prinsip Kerja

1. Tikus memulai dari posisi (0, 0)
2. Tikus mencoba bergerak ke satu arah dari posisi saat ini: kanan (R), bawah (D), kiri (L), atau atas (U)
3. Jika langkah valid (tidak keluar dari batas dan bukan dinding), lanjutkan ke sel tersebut
4. Tandai sel yang sudah dikunjungi
5. Jika tidak ada jalur ke tujuan dari posisi tersebut, kembali ke posisi sebelumnya (backtrack)
6. Ulangi hingga mencapai tujuan atau semua jalur dicoba

> **📝 Catatan**
>
> * Nilai `1` dalam matriks artinya bisa dilewati (jalan)
> * Nilai `0` artinya tidak bisa dilewati (tembok)
> * Arah pergerakan: R (kanan), D (bawah), L (kiri), U (atas)

---

### Contoh Maze

```
1 0 0 0
1 1 0 1
1 1 0 0
0 1 1 1
```

Start: (0,0) → End: (3,3)

---

### Visualisasi Simulasi

<figure>
  <img src="/assets/img/riam-1.png" alt="Simulasi Rat in a Maze">
  <figcaption>Simulasi langkah demi langkah tikus mencari jalan keluar.</figcaption>
</figure>

---

### Kode Implementasi (Java)

```java
import java.util.*;

class Solution {
    private static void solve(int i, int j, int[][] a, int n, ArrayList<String> ans, String move, int[][] vis) {
        if (i == n - 1 && j == n - 1) {
            ans.add(move);
            return;
        }

        // Down
        if (i + 1 < n && vis[i + 1][j] == 0 && a[i + 1][j] == 1) {
            vis[i][j] = 1;
            solve(i + 1, j, a, n, ans, move + 'D', vis);
            vis[i][j] = 0;
        }

        // Left
        if (j - 1 >= 0 && vis[i][j - 1] == 0 && a[i][j - 1] == 1) {
            vis[i][j] = 1;
            solve(i, j - 1, a, n, ans, move + 'L', vis);
            vis[i][j] = 0;
        }

        // Right
        if (j + 1 < n && vis[i][j + 1] == 0 && a[i][j + 1] == 1) {
            vis[i][j] = 1;
            solve(i, j + 1, a, n, ans, move + 'R', vis);
            vis[i][j] = 0;
        }

        // Up
        if (i - 1 >= 0 && vis[i - 1][j] == 0 && a[i - 1][j] == 1) {
            vis[i][j] = 1;
            solve(i - 1, j, a, n, ans, move + 'U', vis);
            vis[i][j] = 0;
        }
    }
}
```

---

### Kelebihan dan Kekurangan

**Kelebihan:**

* Sederhana dan mudah dipahami
* Menemukan semua jalur yang memungkinkan
* Cocok untuk studi kasus sederhana
* Tidak memerlukan struktur data kompleks

**Kekurangan:**

* Tidak efisien untuk ukuran labirin besar
* Dapat menyebabkan stack overflow jika rekursi terlalu dalam
* Tidak optimal (tidak mencari jalur terpendek)
* Berisiko mencoba jalur berulang jika tidak ditandai dengan benar

---

### Aplikasi di Kehidupan Nyata

* Sistem navigasi robot
* Rute dalam game dan simulasi virtual
* Pencarian jalur GPS dan routing
* Masalah optimisasi dalam AI

---

### Simulasi Online (Opsional)

> 🔗 Coba simulasi: [https://visualgo.net/en/backtracking](https://visualgo.net/en/backtracking)

Jika ingin membuat simulasi interaktif sendiri, bisa menggunakan JavaScript dan HTML Grid dengan tombol “Next Step” untuk memvisualisasikan tiap gerakan tikus.

---

**Kelompok 6 - DAA 2025**

> Rangkuman ini disusun oleh Kelompok 6 sebagai dokumentasi pembelajaran mata kuliah Desain dan Analisis Algoritma.
