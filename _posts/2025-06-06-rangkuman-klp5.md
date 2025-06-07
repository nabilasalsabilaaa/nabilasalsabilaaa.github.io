---
title: Rangkuman Desain dan Analisis Algoritma
date: 2025-06-06
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

---

### Variasi Masalah Subset Sum Problem
- Bounded Subset Sum Problem, setiap elemen dalam himpunan hanya dapat digunakan sekali untuk membentuk subset yang jumlahnya sama dengan target. 

```plaintext
Contohnya :
Set = {3, 34, 4, 12, 5, 2}, Target = 9
Subset {4, 5} menghasilkan total 9
Kita tidak boleh menggunakan 4 atau 5 lebih dari sekali
```

- Partition Problem, mencari subset dengan jumlah sama dengan setengah dari total seluruh elemen himpunan.

```plaintext
Contohnya :
Set = {1, 5, 11, 5}
Total = 22 → Target subset = 11
Kita bisa buat dua subset :
{11} dan {1, 5, 5} → keduanya berjumlah 11
```

- Exact k Elements Subset Sum, mencari subset yang jumlahnya sama dengan target dan terdiri dari tepat k elemen. 

```plaintext
Contohnya :
Set = {1, 2, 3, 4, 5}, Target = 9, k = 2
Subset {4, 5} terdiri dari 2 elemen dan jumlahnya 9. Namun subset seperti {2, 3, 4} juga jumlahnya 9, tapi terdiri dari 3 elemen, tidak valid. 
```

- Unbounded Subset Sum Problem, setiap elemen boleh digunakan berulang kali untuk mencapai target. Ini berarti jika kita memiliki angka 3 dalam himpunan, maka kita bisa memakainya dua, tiga, atau bahkan lebih kali selama tidak melebihi target.

```plaintext
Contohnya :
Set = {1, 3, 4}, Target = 6
Kemungkinannya :
o 1 + 1 + 1 + 3 = 6
o 3 + 3 = 6
o 2 × 1 + 4 = 6
```

- Multi-target Subset Sum Problem, mencari subset yang memenuhi lebih dari satu kriteria, misalnya jumlah total dan batas berat. 

```plaintext
Set barang:
o Barang A: harga = 40, berat = 1 kg
o Barang B: harga = 60, berat = 1.5 kg
o Barang C: harga = 30, berat = 0.5 kg
o Target: total harga ≤ 100 dan total berat ≤ 2 kg
Kombinasi Barang A + C → total harga 70, berat 1.5 kg → valid
Tapi A + B → harga 100, berat 2.5 kg → tidak valid karena melebihi berat. 
```

- Approximate Subset Sum, tidak ada subset yang jumlahnya tepat sama dengan target, jadi dicari subset terbaik yang mendekati target, biasanya tidak boleh melebihi.

```plaintext
Contohnya :
Set = {2, 5, 10, 14}, Target = 15
Tidak ada subset yang tepat 15. Tapi:
o {10, 2} = 12
o {5, 10} = 15 ✅ (tepat)
Kalau target = 16, dan tidak ada kombinasi pas, kita bisa ambil{14} atau {10, 5} = 15 → solusi terbaik
```

---

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

---

### Aplikasi Permaslahan Subset Sum di Dunia Nyata
1. Kriptografi
2. Alokasi sumber daya
3. Genetika dan Bioinformatika
4. Keuangan dan Investasi
5. Perancangan permainan dan teka-teki

---