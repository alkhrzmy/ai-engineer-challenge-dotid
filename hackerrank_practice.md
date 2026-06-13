# HackerRank Problem Solving (Basic) - Latihan Soal

---

## Soal 1: Minimum Difference

**Soal:** Diberikan array angka, cari pasangan dua angka yang memiliki selisih paling kecil.

**Input:**
```
[1, 5, 3, 19, 18, 25]
```

**Output:**
```
1  (antara 18 dan 19)
```

**Solusi:**
```python
def minimumDifference(arr):
    arr.sort()
    min_diff = float('inf')
    for i in range(1, len(arr)):
        diff = arr[i] - arr[i-1]
        if diff < min_diff:
            min_diff = diff
    return min_diff

arr = list(map(int, input().split()))
print(minimumDifference(arr))
```

**Penjelasan:**
1. Sort array → angka berurutan
2. Iterasi, hitung selisih tiap pasangan bertetangga
3. Simpan selisih terkecil

**Kompleksitas:** O(n log n) karena sorting

---

## Soal 2: Two Sum

**Soal:** Diberikan array dan target, cari dua angka yang jumlahnya sama dengan target. Return index keduanya.

**Input:**
```
[2, 7, 11, 15]
target = 9
```

**Output:**
```
0 1  (karena 2 + 7 = 9)
```

**Solusi:**
```python
def twoSum(nums, target):
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []

nums = list(map(int, input().split()))
target = int(input())
print(*twoSum(nums, target))
```

**Penjelasan:**
1. Iterasi array, simpan angka yang sudah dilihat di dictionary
2. Cari complement (target - num) di dictionary
3. Kalo ketemu, return index keduanya

**Kompleksitas:** O(n) — satu pass

---

## Soal 3: Reverse Words in String

**Soal:** Balik urutan kata dalam string tanpa membalik karakter.

**Input:**
```
"the sky is blue"
```

**Output:**
```
"blue is sky the"
```

**Solusi:**
```python
def reverseWords(s):
    words = s.split()
    return ' '.join(reversed(words))

s = input().strip()
print(reverseWords(s))
```

**Penjelasan:**
1. Split string jadi list kata
2. Reverse list
3. Join kembali dengan spasi

**Kompleksitas:** O(n)

---

## Soal 4: Valid Palindrome

**Soal:** Cek apakah string palindrome (dibaca sama dari depan dan belakang). Abaikan spasi, tanda baca, dan huruf besar/kecil.

**Input:**
```
"A man, a plan, a canal: Panama"
```

**Output:**
```
True
```

**Solusi:**
```python
def isPalindrome(s):
    cleaned = ''.join(c.lower() for c in s if c.isalnum())
    return cleaned == cleaned[::-1]

s = input().strip()
print(isPalindrome(s))
```

**Penjelasan:**
1. Hapus semua karakter non-alphanumeric
2. Ubah ke lowercase
3. Bandingkan dengan versi terbaliknya

**Kompleksitas:** O(n)

---

## Soal 5: Maximum Subarray Sum

**Soal:** Cari jumlah maksimum dari subarray kontigu.

**Input:**
```
[-2, 1, -3, 4, -1, 2, 1, -5, 4]
```

**Output:**
```
6  (subarray [4, -1, 2, 1])
```

**Solusi:**
```python
def maxSubarraySum(arr):
    max_sum = arr[0]
    current_sum = arr[0]
    for i in range(1, len(arr)):
        current_sum = max(arr[i], current_sum + arr[i])
        max_sum = max(max_sum, current_sum)
    return max_sum

arr = list(map(int, input().split()))
print(maxSubarraySum(arr))
```

**Penjelasan (Kadane's Algorithm):**
1. Iterasi array, simpan jumlah sementara
2. Di tiap langkah, pilih: mulai baru atau lanjut yang lama
3. Update jumlah maksimum

**Kompleksitas:** O(n)

---

## Soal 6: Count Occurrences

**Soal:** Hitung berapa kali angka tertentu muncul dalam array.

**Input:**
```
[1, 2, 3, 2, 2, 4, 5]
target = 2
```

**Output:**
```
3
```

**Solusi:**
```python
def countOccurrences(arr, target):
    count = 0
    for num in arr:
        if num == target:
            count += 1
    return count

arr = list(map(int, input().split()))
target = int(input())
print(countOccurrences(arr, target))
```

**Penjelasan:**
1. Iterasi array
2. Kalo angka == target, tambah counter
3. Return counter

**Kompleksitas:** O(n)

---

## Soal 7: Remove Duplicates

**Soal:** Hapus duplikat dari array, pertahankan urutan pertama kali muncul.

**Input:**
```
[1, 2, 2, 3, 4, 4, 5]
```

**Output:**
```
[1, 2, 3, 4, 5]
```

**Solusi:**
```python
def removeDuplicates(arr):
    seen = set()
    result = []
    for num in arr:
        if num not in seen:
            seen.add(num)
            result.append(num)
    return result

arr = list(map(int, input().split()))
print(removeDuplicates(arr))
```

**Penjelasan:**
1. Pakai set untuk tracking angka yang sudah dilihat
2. Kalo belum ada di set, tambah ke result

**Kompleksitas:** O(n)

---

## Soal 8: Find Missing Number

**Soal:** Diberikan array berisi angka 1 sampai N dengan satu angka hilang. Cari angka yang hilang.

**Input:**
```
[1, 2, 4, 5, 6]
```

**Output:**
```
3
```

**Solusi:**
```python
def findMissingNumber(arr, n):
    expected_sum = n * (n + 1) // 2
    actual_sum = sum(arr)
    return expected_sum - actual_sum

arr = list(map(int, input().split()))
n = int(input())
print(findMissingNumber(arr, n))
```

**Penjelasan:**
1. Hitung jumlah yang seharusnya (rumus deret aritmatika)
2. Hitung jumlah aktual
3. Selisihnya = angka yang hilang

**Kompleksitas:** O(n)

---

## Soal 9: Is Anagram

**Soal:** Cek apakah dua string adalah anagram (huruf yang sama, urutan beda).

**Input:**
```
listen
silent
```

**Output:**
```
True
```

**Solusi:**
```python
def isAnagram(s1, s2):
    s1 = s1.lower()
    s2 = s2.lower()
    if len(s1) != len(s2):
        return False
    return sorted(s1) == sorted(s2)

s1 = input().strip()
s2 = input().strip()
print(isAnagram(s1, s2))
```

**Penjelasan:**
1. Ubah ke lowercase
2. Kalo panjang beda, langsung False
3. Sort kedua string, bandingkan

**Kompleksitas:** O(n log n)

---

## Soal 10: Fibonacci

**Soal:** Return angka ke-N dari deret Fibonacci.

**Input:**
```
6
```

**Output:**
```
8  (0, 1, 1, 2, 3, 5, 8)
```

**Solusi:**
```python
def fibonacci(n):
    if n <= 1:
        return n
    a, b = 0, 1
    for _ in range(2, n + 1):
        a, b = b, a + b
    return b

n = int(input())
print(fibonacci(n))
```

**Penjelasan:**
1. Base case: F(0)=0, F(1)=1
2. Iterasi dari 2 sampai n
3. Update: a jadi b, b jadi a+b

**Kompleksitas:** O(n)

---

## Soal 11: Sum of Two Arrays

**Soal:** Dua array berisi digit angka. Hitung jumlahnya dan return sebagai array digit.

**Input:**
```
[1, 2, 3]
[4, 5, 6]
```

**Output:**
```
[5, 7, 9]
```

**Solusi:**
```python
def sumArrays(a, b):
    result = []
    carry = 0
    i, j = len(a) - 1, len(b) - 1
    while i >= 0 or j >= 0 or carry:
        val = carry
        if i >= 0:
            val += a[i]
            i -= 1
        if j >= 0:
            val += b[j]
            j -= 1
        result.append(val % 10)
        carry = val // 10
    return result[::-1]

a = list(map(int, input().split()))
b = list(map(int, input().split()))
print(sumArrays(a, b))
```

**Penjelasan:**
1. Iterasi dari belakang (digit paling kecil)
2. Jumlahkan digit + carry
3. Simpan sisa bagi 10, carry = bagi 10

**Kompleksitas:** O(max(m, n))

---

## Soal 12: Longest Common Prefix

**Soal:** Cari prefix terpanjang yang sama dari beberapa string.

**Input:**
```
flower, flow, flight
```

**Output:**
```
"fl"
```

**Solusi:**
```python
def longestCommonPrefix(strs):
    if not strs:
        return ""
    prefix = strs[0]
    for s in strs[1:]:
        while not s.startswith(prefix):
            prefix = prefix[:-1]
            if not prefix:
                return ""
    return prefix

strs = input().split(',')
print(longestCommonPrefix(strs))
```

**Penjelasan:**
1. Ambil string pertama sebagai prefix awal
2. Bandingkan dengan string lain
3. Potong prefix kalo gak match

**Kompleksitas:** O(S) — total karakter semua string

---

## Soal 13: Move Zeroes

**Soal:** Pindahkan semua angka 0 ke akhir array tanpa mengubah urutan angka non-nol.

**Input:**
```
[0, 1, 0, 3, 12]
```

**Output:**
```
[1, 3, 12, 0, 0]
```

**Solusi:**
```python
def moveZeroes(arr):
    insert_pos = 0
    for num in arr:
        if num != 0:
            arr[insert_pos] = num
            insert_pos += 1
    while insert_pos < len(arr):
        arr[insert_pos] = 0
        insert_pos += 1
    return arr

arr = list(map(int, input().split()))
print(moveZeroes(arr))
```

**Penjelasan:**
1. Iterasi array, simpan angka non-nol di depan
2. Isi sisa dengan 0

**Kompleksitas:** O(n)

---

## Soal 14: Find Duplicate

**Soal:** Cari angka yang muncul lebih dari sekali dalam array.

**Input:**
```
[1, 3, 4, 2, 2]
```

**Output:**
```
2
```

**Solusi:**
```python
def findDuplicate(arr):
    seen = set()
    for num in arr:
        if num in seen:
            return num
        seen.add(num)
    return -1

arr = list(map(int, input().split()))
print(findDuplicate(arr))
```

**Penjelasan:**
1. Iterasi array, simpan angka di set
2. Kalo sudah ada di set, itu duplikat

**Kompleksitas:** O(n)

---

## Soal 15: Binary Search

**Soal:** Cari posisi angka dalam array yang sudah terurut. Return -1 jika tidak ditemukan.

**Input:**
```
[2, 5, 8, 12, 16, 23, 38, 56, 72, 91]
target = 23
```

**Output:**
```
5
```

**Solusi:**
```python
def binarySearch(arr, target):
    left, right = 0, len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1

arr = list(map(int, input().split()))
target = int(input())
print(binarySearch(arr, target))
```

**Penjelasan:**
1. Ambil tengah array
2. Kalo target == tengah, selesai
3. Kalo target > tengah, cari di kanan
4. Kalo target < tengah, cari di kiri

**Kompleksitas:** O(log n)

---

**Total: 15 soal dengan solusi dan penjelasan**
