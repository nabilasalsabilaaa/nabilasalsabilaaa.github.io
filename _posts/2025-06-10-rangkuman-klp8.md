---
title: Depth-First Search
date: 2025-06-10
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Kelompok 8
---

## Depth-First Search
Depth-first search (dfs) adalah algoritma pencarian atau penelusuran pada struktur data graf atau pohon yang bekerja dengan menjelajahi satu cabang sedalam mungkin sebelum mundur (backtrack) dan melanjutkan ke cabang berikutnya.

---

## Prinsip Utama

1. Masukkan simpul (node) akar ke dalam stack
2. Ambil node dari stack teratas, lalu cek apakah node tersebut merupakan solusi?
    * jika node merupakan solusi, pencarian selesai dan hasil dikembalikan
    * jika node bukan solusi, masukkan seluruh node anak ke dalam stack
3. Jika stack kosong, dan setiap node sudah dicek. pencarian berakhir
4. Jika stack tidak kosong, ulangi pencarian mulai langkah ke-2

---

### Contoh Kasus
Jika penelusuran dilakukan menggunakan Depth-First Search (DFS) dari simpul awal 1, dengan akhir 10 tuliskan kemungkinan urutan kunjungan simpul!

<div style="display: flex; align-items: flex-start; gap: 20px;">
    <img src="/assets/img/dfs.png" alt="Maze Example" style="width: 500px; border-radius: 0px;"> 
        <p >
            Kemungkinan DFS (urutan eksplorasi berbeda): 1, 2, 4, 6, 9, 10
        </p>
</div>

---

### Implementasi Kode
```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

void DFS(int start, vector<vector<int>>& graph, vector<bool>& visited) {
    stack<int> s;
    s.push(start);
    
    while (!s.empty()) {
        int node = s.top();
        s.pop();
        
        if (!visited[node]) {
            cout << node << " ";
            visited[node] = true;
        }

        for (int neighbor : graph[node]) {
            if (!visited[neighbor]) {
                s.push(neighbor);
            }
        }
    }
}

int main() {
    int n = 6;
    vector<vector<int>> graph(n);
    
    graph[0].push_back(1);
    graph[0].push_back(2);
    graph[1].push_back(0);
    graph[1].push_back(3);
    graph[1].push_back(4);
    graph[2].push_back(0);
    graph[2].push_back(5);
    graph[3].push_back(1);
    graph[4].push_back(1);
    graph[5].push_back(2);
    vector<bool> visited(n, false);
    
    cout << "DFS traversal starting from node 2: ";
    DFS(1, graph, visited);
    cout << endl;

    return 0;
}
```

---

### Kelebihan dan Kekurangan

* **Kelebihan**
1. Penggunaan Memori Lebih Efisien
2. Mudah Diimplementasikan
3. Cocok untuk Menemukan Solusi Kedalaman Maksimal
4. Digunakan Dalam Banyak Algoritma Penting

* **Kekurangan**
1. Tidak Menjamin Solusi Terbaik
2. Bisa Masuk ke Infinite Loop (pada graf siklik)
3. Kurang Efisien di Graf Luas Tapi Dangkal
4. Tidak Cocok untuk Semua Masalah
