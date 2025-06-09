## [1231. Divide Chocolate](https://leetcode.com/problems/divide-chocolate/)

**Difficulty:** Medium  
**Tags:** Binary Search, Greedy  
**Companies:** N/A

---

### 📝 Description

You have one chocolate bar that consists of some chunks. Each chunk has its own sweetness given by the array `sweetness`.

You want to share the chocolate with your `k` friends so you start cutting the chocolate bar into `k + 1` pieces using `k` cuts, each piece consists of some consecutive chunks.

Being generous, you will eat the piece with the minimum total sweetness and give the other pieces to your friends.

Find the maximum total sweetness of the piece you can get by cutting the chocolate bar optimally.

---

### 📘 Examples

**Input:**  
`sweetness = [1,2,3,4,5,6,7,8,9], k = 5`  
**Output:**  
`6`  
**Explanation:** You can divide the chocolate into [1,2,3], [4,5], [6], [7], [8], [9]

---

**Input:**  
`sweetness = [5,6,7,8,9,1,2,3,4], k = 8`  
**Output:**  
`1`  
**Explanation:** There is only one way to cut the bar into 9 pieces.

---

**Input:**  
`sweetness = [1,2,2,1,2,2,1,2,2], k = 2`  
**Output:**  
`5`  
**Explanation:** You can divide the chocolate into [1,2,2], [1,2,2], [1,2,2]

---

### ✅ Constraints

- 0 <= k < sweetness.length <= 10⁴
- 1 <= sweetness[i] <= 10⁵

---

### 💡 Solution (C++)

```cpp
class Solution {
public:
    int maximizeSweetness(vector<int>& A, int K) {
        int left = 1, right = 1e9 / (K + 1);
        while (left < right) {
            int mid = (left + right + 1) / 2;
            int cur = 0, cuts = 0;
            for (int a : A) {
                if ((cur += a) >= mid) {
                    cur = 0;
                    if (++cuts > K) break;
                }
            }
            if (cuts > K)
                left = mid;
            else
                right = mid - 1;
        }
        return left;
    }
};
```
