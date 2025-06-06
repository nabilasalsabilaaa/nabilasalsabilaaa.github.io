---
title: Rangkuman Desain dan Analisis Algoritma
date: 2025-06-06 10:22:00 +0800
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Kelompok 2 - Fractional Knapsack
---

## Fractional Knapsack

### Pengantar
**Knapsack Problem** adalah masalah optimasi untuk memilih barang dari sekumpulan item agar nilai total maksimal tanpa melebihi kapasitas ransel.

**Dua variasi utama:**
1. **0/1 Knapsack** – Barang harus diambil seluruhnya atau tidak sama sekali.
2. **Fractional Knapsack** – Barang bisa diambil sebagian (fraksi) sesuai kebutuhan.

> 📝 **Catatan:**  
> 0/1 Knapsack lebih kompleks → butuh *Dynamic Programming*  
> Fractional Knapsack lebih sederhana → bisa pakai *Greedy Algorithm*

---

### Karakteristik Masalah
- Setiap barang memiliki nilai (*value*) dan berat (*weight*)
- Kapasitas tas terbatas
- Barang boleh dipotong/diambil sebagian
- Cocok diselesaikan dengan algoritma **greedy**

---

### Strategi Penyelesaian (Greedy)
1. Hitung rasio nilai per berat → `value / weight`
2. Urutkan item berdasarkan rasio tertinggi
3. Ambil sebanyak mungkin dari item dengan rasio tertinggi
4. Jika tersisa kapasitas, ambil sebagian dari item terakhir

---

### Studi Kasus

**Data Item:**

| Item | Nilai (Value) | Berat (Weight) |
|:----:|:-------------:|:--------------:|
|  A   |      50       |       10       |
|  B   |      60       |       20       |
|  C   |     140       |       40       |
|  D   |      60       |       30       |

**Kapasitas Tas (W) = 50**

---

### Langkah Penyelesaian

1. **Hitung rasio value/weight**:
   - A: 5.0  
   - B: 3.0  
   - C: 3.5  
   - D: 2.0

2. **Urutkan**: A (5.0), C (3.5), B (3.0), D (2.0)

3. **Isi tas**:
   - Ambil **A** (10kg, nilai 50) → sisa 40
   - Ambil **C** (40kg, nilai 140) → sisa 0
   - **B** dan **D** tidak diambil

---

### Solusi Optimal
**Total Nilai Maksimum = 50 + 140 = 190**

---

### Implementasi Kode 

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

struct Item {
    string name;
    double weight;
    double value;

    // Hitung rasio value/weight
    double ratio() const {
        return value / weight;
    }
};

// Fungsi comparator untuk mengurutkan berdasarkan rasio terbesar
bool compare(Item a, Item b) {
    return a.ratio() > b.ratio();
}

int main() {
    double capacity = 30.0; // kapasitas maksimal kurir
    vector<Item> items = {
        {"Laptop", 10, 300},
        {"Buku Paket", 20, 200},
        {"Baju", 30, 180}
    };

    // Urutkan berdasrkan rasio value/weight tertinggi
    short(items.begin(), items.end(), compare);

    double totalValue = 0.0;
    double totalWeight = 0.0;

    cout << "Barang yang dipilih:\n";
    for (const auto & item : items) {
        if (capacity == 0) break;

        if (item.weight <= capacity) {
            // Ambil seluruh barang
            totalValue += item.value;
            capacity -= item.weight;
            cout << "_ " <<item.name << " (berat: " << item.weight << " kg, nilai: " << item.value << ")\n";
        } else {
            // Ambil sebagian barang (fractional)
            double fraction = capacity / item.weight;
            totalValue += item.value * fraction;
            cout << "_ " << item.name << " (berat: " << capacity << " kg dari " << item.weight << " kg, nilai: " << item.value * fraction << ")\n"
            capacity = 0;
        }
    }

    cout << "\nTotal nilai yang dibawa: " << totalValue << endl;

    return 0;
}
```

---

### Kompleksitas Waktu
`O(n log n)` untuk mengurutkan item berdasarkan rasio value/weight.
`O(n)` untuk memasukkan item ke dalam tas.

---

### Aplikasi
1. Penjadwalan tugas dengan sumber daya terbatas
2. Investasi dana ke beberapa proyek 
3. Pengalokasian bandwidth di jaringan 
4. Optimisasi logistik

---