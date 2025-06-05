---
title: Rangkuman Desain dan Analisis Algoritma
date: 2025-05-05 07:30:00 +0800
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Rangkuman materi Kelompok 1
---

## Activity Selection Problem

**Activity Selection Problem** merupakan masalah optimasi klasik dalam ilmu komputer. Kita diberikan sejumlah aktivitas yang masing-masing didefinisikan dengan waktu mulai (s) dan waktu selesai (f). Dua aktivitas dikatakan kompatibel jika mereka tidak tumpang tindih secara waktu,artinya salah satu aktivitas selesai sebelum aktivitas lainnya dimulai. Tantangannya adalah menentukan subset terbesar dari aktivitas yang semuanya kompatibel satu sama lain.

**Algoritma Greedy** adalah strategi pemecahan masalah optimasi yang bekerja dengan membuat pilihan yang tampak paling baik pada setiap langkah, dengan harapan rangkaian pilihan ini akan mengarah pada solusi yang optimal secara keseluruhan.

**Algoritma Activity Selection Problem** menggunakan pendekatan greedy dengan memilih aktivitas berdasarkan waktu selesai (finish time). Ide kuncinya adalah dengan memilih aktivitas yang selesai paling awal, kita memaksimalkan waktu tersisa untuk aktivitas lainnya.

**Step :**
1. Urutkan semua aktivitas berdasarkan waktu selesai (finish time)
2. Pilih aktivitas pertama (aktivitas dengan waktu selesai paling awal)
3. Untuk aktivitas berikutnya, pilih jika waktu mulainya lebih besar atau sama dengan waktu selesai aktivitas yang dipilih sebelumnya


**Implementasi Kode :**
```c++

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

```Output
Aktivitas yang terpilih: A1 A4 A5

```
