# 484. Find Permutation

## 🧩 Problem Statement

A permutation `perm` of `n` integers (from 1 to n) can be described using a string `s` of length `n - 1`, where:

- `s[i] == 'I'` means `perm[i] < perm[i + 1]`
- `s[i] == 'D'` means `perm[i] > perm[i + 1]`

Given such a string `s`, return the **lexicographically smallest** permutation that satisfies the description.

---

## 🧪 Examples

### Example 1:

Input: s = "I"
Output: [1, 2]
Explanation: Only one valid permutation exists: [1, 2]

### Example 2:

Input: s = "DI"
Output: [2, 1, 3]
Explanation: "DI" corresponds to permutations like [2, 1, 3], [3, 1, 2], etc.
The smallest one lexicographically is [2, 1, 3].

---

## ✅ Constraints

- `1 <= s.length <= 10^5`
- `s[i]` is either `'I'` or `'D'`

---

## 💡 Approach

We initialize a sorted array from 1 to `n` (where `n = s.length + 1`). For each continuous sequence of `'D'`, we reverse the corresponding part of the array. Reversing the decreasing segments ensures the **lexicographically smallest** permutation.

### Why it works:

- By default, ascending order is the smallest.
- When we encounter a `'D'`, we reverse only that range to satisfy the decreasing condition while keeping the result minimal.

---

## 🧠 Complexity

- **Time Complexity:** O(n), where `n = s.length + 1`
- **Space Complexity:** O(n), for the output array

---

## 🧾 Java Code

```java
class Solution {
    public int[] findPermutation(String s) {
        int n = s.length(), arr[] = new int[n + 1];
        for (int i = 0; i <= n; i++) arr[i] = i + 1; // start with [1, 2, ..., n+1]

        for (int h = 0; h < n; h++) {
            if (s.charAt(h) == 'D') {
                int l = h;
                while (h < n && s.charAt(h) == 'D') h++;
                reverse(arr, l, h); // reverse D-segment
            }
        }
        return arr;
    }

    void reverse(int[] arr, int l, int h) {
        while (l < h) {
            arr[l] ^= arr[h];
            arr[h] ^= arr[l];
            arr[l] ^= arr[h];
            l++; h--;
        }
    }
}
```
