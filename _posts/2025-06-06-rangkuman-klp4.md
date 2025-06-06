---
title: Rangkuman Desain dan Analisis Algoritma
date: 2025-05-05 07:30:00 +0800
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Kelompok 4 - N-Queens Problem
---

## N-Queens Problem

### Pengantar
**Masalah N-Queens** adalah sebuah permasalahan klasik
dalam bidang ilmu komputer dan matematika
kombinatorik yang melibatkan penempatan N buah ratu
catur pada sebuah papan catur berukuran N × N,
sedemikian rupa sehingga tidak ada dua ratu yang
saling menyerang. Dalam aturan catur, seorang ratu
dapat bergerak secara horizontal (baris), vertikal
(kolom), dan diagonal. Oleh karena itu, solusi dari
masalah ini harus memastikan bahwa tidak ada dua
ratu yang berada pada baris, kolom, atau diagonal yang
sama.

---

**Tujuan**
1. Menemukan semua konfigurasi penempatan ratu yang memenuhi syarat tidak saling menyerang.
2. Mengembangkan dan menguji algoritma pencarian dan optimasi, seperti backtracking, DFS, heuristic search, atau algoritma genetika.
3. Melatih logika pemrograman dan pemecahan masalah, terutama dalam konteks constraint satisfaction problem (CSP).

---

**Aplikasi di Dunia Nyata**
1. Penjadwalan tugas (di mana konflik harus dihindari),
2. Penempatan modul dalam sirkuit elektronik,
2. Pengalokasian sumber daya yang saling eksklusif

---

**Implementasi Kode**

```cpp
/**
* Fungsi untuk menectak solusi yangditemukan.
* Menampilkan posisi ratu ('Q') dan titik kosong ('.') dalam bentuk papan.
*/

void printSolution() {
    cout << "Solusi #" << ++solutionCount << ":\n";
    for (int i = 0; i < N; i++) {
        for (int i = 0; i < N; j++) {
            cout << (board[i][j] ? 'Q' : '.') << ' ';
        }
        cout << '\n';
    }
    cout << '\n';
}

/**
* Fungsi untuk mengecek apakah posisi (row, col) aman untuk menempatkan ratu
* Mengecek apakah tidak ada ratu di baris yang sama, diagonal kiri atas dan diagonal kiri bawah
*/

bool isSafe(int row, int col) {
    // Periksa baris sebelah kiri
    for (int i = 0; i < col; i++)
        if (board[row][i])
            return false;

    // Periksa diagonal kiri atas
    for (int i = row, j = col; i >= 0 && j >= 0; i--, j--)
        if (board[i][j])
            return false;

    // Periksa diagonal kiri bawah
    for (int i = row, j = col; i < N && j >= 0; i++, j--)
        if (board[i][j])
            return false;

    return true;
}

/**
* Fungsi rekursif untuk menyelesaikan N-Queens dengan backtracking
* Mencoba menempatkan ratu di setiap baris dan kolom 'col' dan melanjutkan ke kolom berikutnya
*/

void solveNQueensutil(int col) {
    // Jika semua ratu sudah ditempatkan cetak solusi
    if (col >= N) {
        printSolution();
        return;
    }

    // Coba tempatkan ratu di setiap baris di dalam kolom saat ini
    for (int i = 0; i < N; i++) {
        if (isSafe(i, col)) {
            board[i][col] = 1;          // Tempatkan ratu
            solveNQueensUtil(col + 1);  // Rekursi untuk kolom berikutnya
            board[i][col] = 0;         // Backtrack (hapus ratu)
        }
    }
}

/**
* Fungsi utama untuk menyelesaikan N-Queens
* Inisialisasi papan dan memulai pencarian solusi
*/

void solveNQueens() {
    board = vector<vector<int>>(N, vector<int>(N, 0)); // Inisialisasi papan kosong
    solveNQueensutil(0);
    if (solutionCount == 0) {
        cout << "Solusi tidak tersedia\n";
    } else {
        cout << "Total solusi: " << solutionCount << endl;
    }
}

/**
* Fungsi utama program
* Meminta input N dari pengguna dan memulai penyelesaian N-Queens
*/

int main() {
    cout << "Masukkan Nilai N: ";
    cin >> N;
    solveNQueens();
    return 0;
}
```