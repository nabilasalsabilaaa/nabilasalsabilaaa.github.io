---
title: Breadth-First Search
date: 2025-06-10
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Kelompok 7
---

## Breadth-First Search
Breadth-First Search (BFS) adalah metode untuk menjelajahi graph atau pohon dengan menelusuri simpul-simpul berdasarkan jaraknya dari titik awal. Secara sederhana, BFS akan mengeksplorasi semua simpul yang paling dekat terlebih dahulu, baru kemudian beralih ke simpul yang lebih jauh. Jadi pendekatannya menyebar ke seluruh arah secara merata dari pusat.

---

### Konsep Dasar
1. BFS menggunakan struktur queue (antrian).
2. Mulai dari simpul awal → kunjungi semua tetangga → lanjut ke tetangga dari tetangga.
3. Bersifat level-order traversal (per lapisan)

---

### Langkah-langkah Algoritma Breadth-First Search
1. Tentukan simpul awal (start node) 1.2. Masukkan simpul (node) ke dalam antrian (queue)
3. Ambil simpul dari queue terdepan, tandai bahwa simpul telah dikunjungi, dan cek apakah merupakan solusi/tujuan
4. Selama antrian tidak kosong atau simpul aktif bukan merupakan tujuan, lakukan:
    * Ulangi proses pencarian mulai langkah ke-2 sampai ke-3
    * Keluarkan simpul dari antrian (dequeue)
    * Untuk setiap tetangga dari simpul (jika ada):
      - Kunjungi semua tetangga yang belum dikunjungi lalu
      tandai sebagai dikunjungi
      - Tambahkan ke antrian (enqueue)

> Ulangi sampai simpul tujuan (goal node) ditemukan atau queue sudah kosong

---

### Cara Kerja Breadth-First Search

```plaintext
         [S]  'Start Node'
        /   \
       /     \
      /       \
     /         \
   [A]         [B]
  /   \       /   \
[C]   [D]   [E]   [F]
           /   \
         [H]   [G]  'Goal Node'
```

|  Queue   |  Visited  |  Simpul aktif  |
|:--------:|:---------:|:--------------:|
|S         |S          |S               |
|A, B      |SA         |A               |  
|B, C, D   |SAB        |B               |
|C, D, E, F|SABC       |C               |
|D, E, F   |SABCD      |D               |
|E, F      |SABCDE     |E               |
|F, H, G   |SABCDEF    |F               |
|H, G      |SABCDEFG   |G               |
|G         |SABCDEFGH  |H               |

---

### Implementasi Kode

```cpp
using namespace std;

// inisiallisasi graf dengan adjacency list
unordered_map<char, vector<char>> graf;

// menyimpan simpul yang sudah dikunjungi
unordered_map<char, bool> sudahDikunjungi;

// menyimpan jallur: simpul_sekarang -> simpul_sebelumnya
unordered_map<char start, char> parent;

void bfs(char start, char goal) {
    queue<char> q;
    q.push(start;
    sudahDikunjungi[start] = true;
    parent[start] = '-'; // titik awal tidak punya parent

    while(!q.empty()) {
        char sekarang = q.front();
        q.pop();
        cout << "Kunjungi node: " << sekarang << endl;

        // jika goal ditemukan, langsung hentikan
        if (sekarang == goal) break;

        for (char tetangga : graf[sekarang]) {
            if (!sudahDikunjungi[tetangga]) {
                q.push(tetangga);
                sudahDikunjungi[tetangga] = true;
                parent[tetangga] = sekarang;
            }
        }

        // cetak jalur terpendek dari goal ke start
        vector<char> jalur;
        char current = goal;
        while (current !- '-') {
            jalur.push_back(current);
            current = parent[current];
        }

        cout << "\n=== Hasil ===" << endl;
        cout << "Start Node: " << start << endl; 
        cout << "Goal Node: " << goal << endl; 
        cout << "Jalur terpendek: ";
        for (int i = jalur.size() - 1; i >= 0; i--) {
            cout << jalur[i];
            if (i != 0) cout << " ->";
        }
        cout << endl;
    }
}
```

---

### Aplikasi Nyata BFS

1. Digunakan untuk mencari jalan terpendek dari titik awal ke tujuan. Contohnya game PacMan.
2. Memetakan semua perangkat (PC, server, router) dalam jaringan
3. Platform seperti Facebook atau LinkedIn menggunakan BFS untuk menemukan teman atau koneksi dalam jarak tertentu (misal: "Orang yang mungkin Anda kenal").
4. BFS digunakan untuk menemukan rute terpendek dari titik A ke B dengan asumsi semua edge memiliki bobot yang sama (misal: jumlah jalan, bukan jarak).

---

### Kelebihan dan Kekurangan

* **Kelebihan**
Menjamin ditemukannya solusi yang paling baik (komplit dan optimal)

* **Kekurangan**
Membutuhkan memori dan waktu yang cukup banyak
