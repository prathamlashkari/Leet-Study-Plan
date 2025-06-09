## [1533. Find the Index of the Large Integer](https://leetcode.com/problems/find-the-index-of-the-large-integer/)

**Difficulty:** Medium  
**Tags:** Array, Binary Search, Interactive  
**Companies:** Amazon

---

### 📝 Description

You are given an integer array `arr` where all the integers are equal except for one integer which is larger than the rest. You do not have direct access to the array, but you can use an API `ArrayReader` which provides:

- `compareSub(l, r, x, y)`: Compares the sum of subarray `arr[l..r]` with the sum of subarray `arr[x..y]`.  
  Returns:

  - `1` if sum of first subarray > sum of second subarray
  - `0` if sums are equal
  - `-1` if sum of first subarray < sum of second subarray

- `length()`: Returns the size of the array.

You can call `compareSub` at most 20 times.

**Goal:** Return the index of the element in `arr` which is the largest.

---

### 📘 Examples

**Input:**  
`arr = [7,7,7,7,10,7,7,7]`  
**Output:**  
`4`  
**Explanation:** The largest element is 10 at index 4.

---

### ✅ Constraints

- 2 <= arr.length <= 5 \* 10⁵
- 1 <= arr[i] <= 100
- All elements of arr are equal except one element which is larger.

---

### 💡 Solution (Java / C#)

```java
class Solution {
    public int getIndex(ArrayReader rd) {
        int l = 0, r = rd.length() - 1;
        while (l < r) {
            int h = (r - l + 1) / 2;
            if (rd.compareSub(l, l + h - 1, l + h, l + h * 2 - 1) != 1)
                l = l + h;
            else
                r = l + h - 1;
        }
        return l;
    }
}
```
