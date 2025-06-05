---
title: Rangkuman DAA Tugas 1
date: 2025-05-05 07:30:00 +0800
categories: [Desain Analisis Algoritma, Tugas 1]
tags: [daa, rangkuman]
description: Rangkuman materi tugas 1 DAA
---

## Brute Force

**Brute Force** adalah pendekatan langsung untuk menyelesaikan masalah.

### Contoh Kode:
```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

```

