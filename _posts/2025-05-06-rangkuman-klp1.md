---
title: Rangkuman Desain dan Analisis Algoritma
date: 2025-05-05 07:30:00 +0800
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Rangkuman Materi Kelompok 1
---

## Activity Selection Problem

**Activity Selection Problem** merupakan masalah optimasi klasik dalam ilmu komputer. Kita diberikan sejumlah aktivitas yang masing-masing didefinisikan dengan waktu mulai (s) dan waktu selesai (f). Dua aktivitas dikatakan kompatibel jika mereka tidak tumpang tindih secara waktu,artinya salah satu aktivitas selesai sebelum aktivitas lainnya dimulai. Tantangannya adalah menentukan subset terbesar dari aktivitas yang semuanya kompatibel satu sama lain.

**Algoritma Greedy** adalah strategi pemecahan masalah optimasi yang bekerja dengan membuat pilihan yang tampak paling baik pada setiap langkah, dengan harapan rangkaian pilihan ini akan mengarah pada solusi yang optimal secara keseluruhan.

**Algoritma Activity Selection Problem** menggunakan pendekatan greedy dengan memilih aktivitas berdasarkan waktu selesai (finish time). Ide kuncinya adalah dengan memilih aktivitas yang selesai paling awal, kita memaksimalkan waktu tersisa untuk aktivitas lainnya.

**Step :**
1. Urutkan semua aktivitas berdasarkan waktu selesai (finish time)
2. Pilih aktivitas pertama (aktivitas dengan waktu selesai paling awal)
3. Untuk aktivitas berikutnya, pilih jika waktu mulainya lebih besar atau sama dengan waktu selesai aktivitas yang dipilih sebelumnya

**Problem Solution**
-----------------------------------------
|  Aktivitas  |  Mulai (s)  |  Selesai  |
-----------------------------------------
|      A1     |      1      |     4     |
|      A2     |      3      |     5     |
|      A3     |      0      |     6     |
|      A4     |      5      |     7     |
|      A5     |      8      |     9     |
|      A6     |      5      |     9     |
+-------------+-------------+-----------+

**Langkah Solusi**
1. **Urutkan** berdasarkan waktu selsai: ```[A1, A2, A3, A4, A5, A6]```
2. **Pilih A1** (selesai paling awal)
3. **Iterasi:**
    - A2, A3: *Tumpang tindih* (❌)
    - A4: *Kompatibel* (✔️) -> ```{A1, A4}```
    - A5: *Kompatibel* (✔️) -> ```{A1, A4, A5}```
    - A6: *Tumpang tindih* (❌)
    
**Solusi optimal:** ```{A1, A4, A5}``` (3 aktivitas)

**Implementasi Kode :**
```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

struct Activity {
    int start, finish;
    int index;
}

bool activityCompare(Activity s1, Activity s2) {
    return (s1.finish < s2.finish);
}

void printMaxActivities (vector<Activity>& arr, int n) {
    sort(arr.begin(), arr.end(), activityCompare) :
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

```Aktivitas yang terpilih: A1 A4 A5```

**Analisis Kompleksitas**
1. Kompleksitas Waktu:
    - Pengurutan aktivitas berdasarkan waktu selesai: O(n log n)
    - Pemilihan aktivitas: O(n)
    - Total kompleksitas waktu: O(n log n)

2. Kompleksitas Ruang:
    - Menyimpan aktivitas: O(n)
    - Tidak memerlukan ruang tambahan yang signifikan selain untuk menyimpan input dan output

**Aplikasi Dunia Nyata**
1. Jadwal ruang kelas
2. Jadwal meeting
3. Jadwal proses CPU
4. Rute kendaraan
5. Alokasi bandwidth