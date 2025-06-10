---
title: Activity Selection Problem
date: 2025-05-05
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Kelompok 1 
---

## Activity Selection Problem

### Pengantar
**Activity Selection Problem** merupakan masalah optimasi klasik dalam ilmu komputer. Kita diberikan sejumlah aktivitas yang masing-masing didefinisikan dengan waktu mulai (`start`) dan waktu selesai (`finish`). Dua aktivitas dikatakan **kompatibel** jika tidak tumpang tindih, artinya salah satu aktivitas selesai sebelum aktivitas lainnya dimulai. Tujuannya adalah memilih sebanyak mungkin aktivitas yang **tidak saling tumpang tindih**.

---

### Strategi Penyelesaiaan

**Algoritma Greedy** cocok digunakan untuk menyelesaikan masalah ini. Strateginya:
- Pilih aktivitas yang selesai paling awal terlebih dahulu.
- Aktivitas selanjutnya dipilih jika waktu mulainya tidak tumpang tindih dengan aktivitas terakhir yang dipilih.

**Step :**
1. Urutkan semua aktivitas berdasarkan waktu selesai (finish time)
2. Pilih aktivitas pertama (aktivitas dengan waktu selesai paling awal)
3. Untuk aktivitas berikutnya, pilih jika waktu mulainya lebih besar atau sama dengan waktu selesai aktivitas yang dipilih sebelumnya

---

### Contoh Soal

|  Aktivitas  |  Mulai (s)  | Selesai(f) |
|:-----------:|:-----------:|:----------:|
|      A1     |      1      |     4      |
|      A2     |      3      |     5      |
|      A3     |      0      |     6      |
|      A4     |      5      |     7      | 
|      A5     |      8      |     9      |
|      A6     |      5      |     9      |

---

### Langkah Solusi

- [x] Urutkan berdasarkan waktu selesai → `A1, A2, A3, A4, A5, A6`
- [x] Pilih **A1**
- [ ] A2: ❌ tumpang tindih (mulai 3, A1 selesai 4)
- [ ] A3: ❌ tumpang tindih (mulai 0)
- [x] A4: ✔️ kompatibel (mulai 5 ≥ 4)
- [x] A5: ✔️ kompatibel (mulai 8 ≥ 7)
- [ ] A6: ❌ tumpang tindih (mulai 5 < 7)
    
**Solusi optimal:** `{A1, A4, A5}` (3 aktivitas)

---

### Implementasi Kode 
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct Activity {
    int start, finish;
    int index;
};

bool activityCompare(Activity s1, Activity s2) {
    return (s1.finish < s2.finish);
}

void printMaxActivities (vector<Activity>& arr, int n) {
    sort(arr.begin(), arr.end(), activityCompare);
    cout << "Aktivitas yang terpilih: ";

    int i = 0;
    cout << "A" << arr[i].index << " ";

    for (int j = 1; j < n; j++) {
        if (arr[j].start >= arr[i].finish) {
            cout << "A" << arr[j].index << " ";
            i =j;
        }
    }
    cout << endl;
}

int main() {
    vector<Activity> arr = {
        {1, 4, 1}, //A1
        {3, 5, 2}, //A2
        {0, 6, 3}, //A3
        {5, 7, 4}, //A4
        {8, 9, 5}, //A5
        {5, 9, 6} //A6
    };

    int n = arr.size();
    printMaxActivities(arr, n);

    return 0;
}
```
**Output Kode :**

`Aktivitas yang terpilih: A1 A4 A5`

---

### Analisis Kompleksitas
**1. Kompleksitas Waktu:**
    - Pengurutan aktivitas berdasarkan waktu selesai: `O(n log n)`
    - Pemilihan aktivitas: `O(n)`
    - Total kompleksitas waktu: `O(n log n)`

**2. Kompleksitas Ruang:**
    - Menyimpan aktivitas: `O(n)`
    - Tidak memerlukan ruang tambahan yang signifikan selain untuk menyimpan input dan output

---

### Aplikasi Dunia Nyata
1. Jadwal ruang kelas
2. Jadwal meeting
3. Jadwal proses CPU
4. Rute kendaraan
5. Alokasi bandwidth jaringan

---