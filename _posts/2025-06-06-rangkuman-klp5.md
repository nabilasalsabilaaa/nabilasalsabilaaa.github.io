---
title: Rangkuman Desain dan Analisis Algoritma
date: 2025-05-05 07:30:00 +0800
categories: [Desain dan Analisis Algoritma]
tags: [DAA, rangkuman]
description: Kelompok 5 - Subset Sum Problem
---

## Subset Sum Problem

### Pengantar
**Subset Sum Problem** adalah masalah klasik dalam ilmu komputer. Diberikan sebuah himpunan bilangan bulat dan sebuah nilai target, tugasnya adalah menentukan apakah ada subset dari himpunan tersebut yang jumlah elemennya sama dengan nilai target.

```cpp 
Input: arr = [1, 2, 3], target_sum = 3
Output: true
```

**Penjelasan** : Terdapat subset {1, 2} yang jumlahnya 3.

```plaintext
set = 1  2  2
subset = {1}, {1, 2}, {1, 2, 3}
         {2}, {2, 3}, {1, 3}
         {3}
```

```plaintext
subset sums = {1, [3], 6, 2, 5, 4, 3}
                   |
                  true
```

**Variasi Masalah Subset Sum Problem** 
1. Bounded Subset Sum Problem, 
### Implementasi Kode

```cpp
#include <iostream>
#include <vector>
using namespace std;

void carisubset(int arr[], int n, int index, int target, vector<int>& subset) {
    if (target == 0) {
        cout << "Subset ditemukan: ";
        for (int num : subset) cout << num << " ";
        cout <<endl;
        return;
    }
    if (index == n || target < 0) return;

    subset.push_back(arr[index]);
    cariSubset(arr, n, index + 1, target - arr[index], subset);

    subset.pop_back();
    cariSubset(arr, n, index + 1, target, subset);
}

int main() {
    int n, target;
    cout << "Masukkan jumlah elemen: ";
    cin >> n;

    int arr(100);
    cout << "Masukkan elemen: ";
    for (int i = 0; i < n; i++) cin >> arr[i];

    cout << "Masukkan target: ";
    cin >> target;

    vector<int> subset;
    cout << "Subset yang jumlahnya " << target << ":\n";
    cariSubset(arr, n, 0, target, subset);

    return 0;
}

```
