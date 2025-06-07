## [760. Find Anagram Mappings](https://leetcode.com/problems/find-anagram-mappings/)

**Difficulty:** Easy  
**Tags:** Array, Hash Table  
**Companies:** Google

---

### 📝 Description

You are given two integer arrays `nums1` and `nums2` where `nums2` is an anagram of `nums1`. Both arrays may contain duplicates.

Return an index mapping array mapping from `nums1` to `nums2` where `mapping[i] = j` means the `i`th element in `nums1` appears in `nums2` at index `j`. If there are multiple answers, return any of them.

An array `a` is an anagram of an array `b` means `b` is made by randomizing the order of the elements in `a`.

---

### 📘 Examples

**Example 1:**  
Input: `nums1 = [12,28,46,32,50]`, `nums2 = [50,12,32,46,28]`  
Output: `[1,4,3,2,0]`  
Explanation:

- `mapping[0] = 1` because `nums1[0] = 12` appears at `nums2[1]`
- `mapping[1] = 4` because `nums1[1] = 28` appears at `nums2[4]`
- and so on...

**Example 2:**  
Input: `nums1 = [84,46]`, `nums2 = [84,46]`  
Output: `[0,1]`

---

### ✅ Constraints

- `1 <= nums1.length <= 100`
- `nums2.length == nums1.length`
- `0 <= nums1[i], nums2[i] <= 10^5`
- `nums2` is an anagram of `nums1`.

---

### 💻 Solution (C++)

```cpp
class Solution {
public:
    vector<int> anagramMappings(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size();
        unordered_map<int, int> mp;
        for (int i = 0; i < n; i++) {
            mp[nums2[i]] = i;
        }
        vector<int> ans(n);
        for (int i = 0; i < n; i++) {
            ans[i] = mp[nums1[i]];
        }
        return ans;
    }
};
```
