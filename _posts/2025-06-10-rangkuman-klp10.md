---
title: Dijkstra's Algorithm
date: 2025-06-10
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Kelompok 10
---
## Dijkstra's Algorithm
Dijkstra's Algorithm adalah sebuah metode yang digunakan untuk mencari jalur terpendek antara dua titik dalam sebuah graf.

---

### Cara Kerja
1. Buat tabel dan kolom sebagai tempat nilai atau jarak dari simpul, sedangkan baris sebagai posisi simpul.
2. Pilih simpul awal dan simpul tujuan, dengan syarat simpul tersebut harus terhubung secara langsung. 
3. Hitung jarak beberapa simpul tujuan yang telah dipiilih.
4. Setelah semua simpul diuji, lalu pilih jarak  yang terpendek.
5. Simpul yang dipilih akan menjadi acuan untuk tahap selanjutnya, ulangi seperti sebelumnya sampai semua simpul telah diuji

---

### Contoh Permasalahan

**Carilah nilai dan lintasan terpendek dari simpul A ke F**

<div style="display: flex; align-items: flex-start; gap: 20px;">
  <img src="/assets/img/10satu.png" alt="Graf 1" style="width: 500px; border-radius: 0px;"> 
  <img src="/assets/img/10dua.png" alt="Graf 2" style="width: 500px; border-radius: 0px;"> 
</div>

`Lintasan Terpendek adalah ABEF/ABDF = 4`

---

### Implementasi Kode

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>
#include <stack>

using namespace std;

// Fungsi untuk membuat daftar adjacency
vector<vector<pair<int, int>>> constructAdj(vector<vector<int>> &edges, int V) {
    vector<vector<pair<int, int>>> adj(V);
    for (const auto &edge : edges) {
        int u = edge[0];
        int v = edge[1];
        int wt = edge[2];
        adj[u].push_back({v, wt});
        adj[v].push_back({u, wt});
    }
    return adj;
}

// Fungsi Dijkstra untuk mencari jarak terpendek dari sumber ke semua simpul lainnya
vector<int> dijkstra(int V, vector<vector<int>> &edges, int src, vector<int> &prev) {
    vector<vector<pair<int, int>>> adj = constructAdj(edges, V);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    vector<int> dist(V, INT_MAX);
    pq.push({0, src});
    dist[src] = 0;
    
    // Array prev untuk melacak jalur
    prev[src] = -1;

    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();

        for (auto x : adj[u]) {
            int v = x.first;
            int weight = x.second;

            if (dist[v] > dist[u] + weight) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
                prev[v] = u; // Menyimpan simpul sebelumnya
            }
        }
    }
    return dist;
}

// Fungsi untuk mencetak jalur dari src ke dest
void printPath(vector<int> &prev, int dest) {
    stack<int> path;
    for (int v = dest; v != -1; v = prev[v]) {
        path.push(v);
    }

    cout << "Jalur: ";
    while (!path.empty()) {
        cout << (char)(path.top() + 'A') << " ";
        path.pop();
    }
    cout << endl;
}

int main() {
    int V, E, src, dest;
    
    // Input jumlah simpul dan sisi
    cout << "Masukkan jumlah simpul (V): ";
    cin >> V;
    
    cout << "Masukkan jumlah sisi (edges): ";
    cin >> E;
    
    vector<vector<int>> edges(E);
    
    // Input data sisi
    cout << "Masukkan sisi dan bobot (format: u v weight):\n";
    for (int i = 0; i < E; i++) {
        char u_char, v_char;
        int wt;
        cout << "Sisi " << i+1 << ": ";
        cin >> u_char >> v_char >> wt;

        // Mengonversi huruf ke angka
        int u = u_char - 'A'; // Mengonversi 'A' -> 0, 'B' -> 1, dll
        int v = v_char - 'A'; // Mengonversi 'A' -> 0, 'B' -> 1, dll

        edges[i] = {u, v, wt};
    }
    
    // Input simpul sumber dan tujuan
    char src_char, dest_char;
    cout << "Masukkan simpul sumber (src): ";
    cin >> src_char;
    src = src_char - 'A'; // Mengonversi huruf ke angka
    
    cout << "Masukkan simpul tujuan (dest): ";
    cin >> dest_char;
    dest = dest_char - 'A'; // Mengonversi huruf ke angka

    vector<int> prev(V, -1);  // Array untuk melacak jalur

    // Mencari jarak terpendek
    vector<int> result = dijkstra(V, edges, src, prev);

    // Mencetak jarak terpendek
    cout << "Jarak terpendek dari simpul " << src_char << " ke " << dest_char << ": " << result[dest] << endl;

    // Mencetak jalur yang dilalui
    printPath(prev, dest);

    return 0;
}
```

---

### Contoh Penggunaan

1.  Navigasi Jalan. Misalnya kita ingin mencari rute terpendek dari rumah ke sekolah. Dijkstra's Algorithm akan membantu kita menentukan jalan mana yang lebih pendek dengan mempertimbangkan semua jalan yang ada dan menghitung jarak yang terpendek dari rumah ke sekolah.

2. Pengiriman Barang. Sebuah perusahaan ekspedisi ingin mengirim paket dari gudang ke beberapa pelanggan. Dijkstra’s Algorithm akan membantu menentukan rute pengiriman yang paling efisien agar paket bisa sampai lebih cepat dan tidak boros bensin atau tenaga

---

### Kelebihan dan Kekurangan

* **Kelebihan**
1. Menjamin jalur terpendek
2. Efisien untuk banyak aplikasi
3. Dapat menyelesaikan banyak tujuan sekaligus

* **Kekurangan**
1. Tidak bekerja dengan bobot negatif
2. Kurang efisien untuk graf besar yang jarang terhitung
3. Perhitungan bisa terlalu luas

---
