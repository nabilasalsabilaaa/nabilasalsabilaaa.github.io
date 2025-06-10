---
title: Kahn's Algorithm
date: 2025-06-10
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Kelompok 9
---

## Kahn's Algorithm
Kahn’s Algorithm adalah algoritma penyusunan topologi (topological sorting) yang digunakan untuk menentukan urutan dalam sebuah Directed Acyclic Graph (DAG) berdasarkan ketergantungan antar simpul. 

**Digunakan untuk:**
1. Menjadwal tugas berdasarkan dependensi
2. Mendeteksi siklus dalam grafik terarah
3. Memproses dependensi dalam urutan yang benar

---

### Cara Kerja
1. Gunakan struktur in-degree (jumlah sisi masuk) untuk tiap simpul
2. Tambahkan semua simpul dengan in-degree = 0 ke antrean (queue)
3. Proses antrean satu per satu
4. Jika semua simpul telah diproses, maka graf tidak memiliki siklus

---

### Contoh Kasus
Misalnya kita punya dependensi antar mata kuliah:

|                |
|:--------------:|
|A -> C          |
|B -> C          |
|C -> D          |


* `A dan B adalah prasyarat untuk C`
* `C adalah prasyarat untuk D`

Urutan topologis yang valid: `A B C D` atau `B A C D`

---

### Implementasi Kode
```cpp
#include <iostream>
#include <unordered_map>
#include <vector>
#include <set>
#include <algorithm>
using namespace std;

unordered_map<char, vector<char>> graph;
unordered_map<char, int> in_degree;
set<char> vertices;

void allTopologicalSorts(vector<char> &res, vector<bool> &visited) {
    bool flag = false;
    for (char v : vertices) {
        if (!visited[v] && in_degree[v] == 0) {
            // pilih simpul
            visited[v] = true;
            res.push_back(v);

            // kurangi in-degree tetangga
            for (char neighbor : graph[v]) {
                in_degree[neighbor]--;
            }

            // rekursi
            allTopologicalSorts(res, visited);

            // backtrack
            visited[v] = false;
            res.pop_back();
            for (char neighbor : graph[v]) {
                in_degree[neighbor]++;
            }
            flag = true;
        }
    }
}

    int main() {
        int E;
        cout << "Masukkan jumlah edge (sisi): ";
        cin >> E;

        cout << "Masukkan sisi dalam format 'A B' tanpa panah:" << endl;
        for (int i = 0; i < E; ++i) {
            char u,v;
            cin >> u >> v;
            graph[u].push_back(v);
            in_degree[v]++;
            vertices.insert(u);
            vertices.insert(v);
        }

        for (char v : vertices) {
            if (in_degree.find(v) == in_degree.end()) {
                in_degree[v] = 0;
            }
        }

        vector<char> res;
        unordered_map<char, bool> visited_map;
        for (char v : vertices) {
            visited_map[v] = false;
        }

        vector<bool> visited(256, false); // asumsi char
        allTopologicalSorts(res, visited);

        return 0;
    }
```

---

### Kelebihan dan Kekurangan

* **Kelebihan**
Dari segi kompleksitas waktu sangan efisien, dapat mendeteksi siklus dalam graf berarah dan Cocok untuk masalah dependency seperti mata kuliah, build system, atau project tasks.

* **Kekurangan**
Dari segi graf siklus, ia tidak bisa digunakan pada graf yang mengandung siklus, bisa menghasilkan lebih dari satu urutan topologis yang valid dan memerlukan struktur data tambahan (in-degree dan graph).

