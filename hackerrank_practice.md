# HackerRank Problem Solving (Basic) - Latihan

## Info Tes

| Detail | Info |
|--------|------|
| Durasi | 1 jam 30 menit |
| Jumlah soal | 2 soal |
| Topik | Array, String, Logic |
| Level | Easy - Medium Easy |
| Link | https://www.hackerrank.com/skills-verification/problem_solving_basic |

---

## Soal 1: Minimum Moves to Target

### Soal

Diberikan array of integers `nums` dan integer `target`. Setiap elemen dalam array bisa diubah ke integer lain dalam satu langkah. Tentukan jumlah minimum langkah yang diperlukan agar semua elemen dalam array sama dengan `target`.

### Batasan

- 1 ≤ nums.length ≤ 10⁵
- 0 ≤ nums[i], target ≤ 10⁹

### Contoh

**Contoh 1:**
```
Input: nums = [1, 2, 3], target = 2
Output: 2
Penjelasan: Ubah nums[0] = 1 menjadi 2, dan nums[2] = 3 menjadi 2. Sekarang semua elemen adalah 2.
```

**Contoh 2:**
```
Input: nums = [5, 5, 5], target = 5
Output: 0
Penjelasan: Semua elemen sudah sama dengan target.
```

**Contoh 3:**
```
Input: nums = [1, 1, 1, 1, 10], target = 1
Output: 1
Penjelasan: Hanya ubah nums[4] = 10 menjadi 1.
```

### Solusi

**Pendekatan:** Hitung berapa banyak elemen yang TIDAK sama dengan target. Itu adalah jumlah minimum langkah.

**Time Complexity:** O(n)
**Space Complexity:** O(1)

```python
def min_moves(nums, target):
    moves = 0
    for num in nums:
        if num != target:
            moves += 1
    return moves

# Alternatif (lebih pendek):
def min_moves(nums, target):
    return sum(1 for num in nums if num != target)
```

### Test Cases

```python
assert min_moves([1, 2, 3], 2) == 2
assert min_moves([5, 5, 5], 5) == 0
assert min_moves([1, 1, 1, 1, 10], 1) == 1
assert min_moves([], 1) == 0
assert min_moves([7], 7) == 0
assert min_moves([0], 1) == 1
```

### Penting untuk Diperhatikan

- Kasus array kosong → return 0
- Kasus semua elemen sudah target → return 0
- Kasus hanya 1 elemen → cek apakah sama dengan target

---

## Soal 2: Count Pairs with Difference

### Soal

Diberikan array of integers `nums` dan integer `k`. Hitung jumlah pasangan (i, j) dimana i < j dan |nums[i] - nums[j]| = k.

### Batasan

- 1 ≤ nums.length ≤ 10⁵
- 0 ≤ k ≤ 10⁹

### Contoh

**Contoh 1:**
```
Input: nums = [1, 5, 3, 4, 2], k = 2
Output: 3
Penjelasan: Pasangan dengan beda 2: (1,3), (3,5), (2,4)
```

**Contoh 2:**
```
Input: nums = [1, 1, 1, 1], k = 0
Output: 6
Penjelasan: Pasangan dengan beda 0: (0,1), (0,2), (0,3), (1,2), (1,3), (2,3) = 6 pasangan
```

**Contoh 3:**
```
Input: nums = [1, 3, 5, 7, 9], k = 2
Output: 4
Penjelasan: Pasangan dengan beda 2: (1,3), (3,5), (5,7), (7,9)
```

### Solusi

**Pendekatan:** Gunakan dictionary untuk menghitung frekuensi. Untuk setiap angka, cek apakah `num + k` ada di dictionary.

**Time Complexity:** O(n)
**Space Complexity:** O(n)

```python
def count_pairs(nums, k):
    from collections import Counter
    freq = Counter(nums)
    count = 0
    
    if k == 0:
        # Hitung pasangan angka yang sama
        for num, cnt in freq.items():
            count += cnt * (cnt - 1) // 2
    else:
        for num in freq:
            if num + k in freq:
                count += freq[num] * freq[num + k]
    
    return count
```

### Test Cases

```python
assert count_pairs([1, 5, 3, 4, 2], 2) == 3
assert count_pairs([1, 1, 1, 1], 0) == 6
assert count_pairs([1, 3, 5, 7, 9], 2) == 4
assert count_pairs([1, 2, 3, 4, 5], 1) == 4
assert count_pairs([1], 1) == 0
```

### Penting untuk Diperhatikan

- Kasus k = 0 → hitung pasangan angka yang sama (bukan satu angka dengan dirinya sendiri)
- Kasus array 1 elemen → return 0
- Perhatikan bahwa (i, j) dan (j, i) dihitung sebagai pasangan yang SAMA (karena i < j)

---

## Tips Mengerjakan di HackerRank

### Sebelum Mulai

1. Baca soal dengan teliti — pahami input/output format
2. Catat batasan (constraints) — menentukan kompleksitas yang dibutuhkan
3. Tulis test cases manual dulu — termasuk edge cases

### Saat Mengerjakan

1. Mulai dari brute force — baru optimasi kalo perlu
2. Test dengan contoh di soal dulu — pasti bener
3. Cek edge cases — array kosong, 1 elemen, semua sama
4. Jangan overthinking — soal basic, solusi sederhana cukup

### Setelah Selesai

1. Submit awal — partial score lebih baik daripada timeout
2. Kalo stuck, skip ke soal lain — waktunya cukup (90 menit buat 2 soal)

---

## Latihan Tambahan (Free)

- HackerRank: https://www.hackerrank.com/domains/algorithms
- LeetCode Easy: https://leetcode.com/problemset/?difficulty=Easy
- Codeforces Div 2 A: https://codeforces.com/contests

---

## Cheat Sheet

### Pola Umum Soal Basic

| Pola | Solusi |
|------|--------|
| Cari angka yang hilang | XOR atau sum difference |
| Hitung frekuensi | Dictionary/hash map |
| Palindrom | Two pointer dari ujung |
| Two Sum | Dictionary (simpan sisa kebutuhan) |
| Valid parenthesis | Stack |
| Reverse string | Two pointer atau slicing |

### Kompleksitas yang Dibutuhkan

| Constraints | Kompleksitas |
|-------------|-------------|
| n ≤ 10 | O(n!) atau O(2^n) |
| n ≤ 100 | O(n³) |
| n ≤ 1000 | O(n²) |
| n ≤ 10⁵ | O(n log n) |
| n ≤ 10⁶ | O(n) |

---

Good luck! 🔥
