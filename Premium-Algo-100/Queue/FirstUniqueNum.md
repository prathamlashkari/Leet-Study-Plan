## [1429. First Unique Number](https://leetcode.com/problems/first-unique-number/)

**Difficulty:** Medium  
**Tags:** Array, Hash Table, Design, Queue, Data Stream  
**Companies:** Amazon, Meta, Uber, TomTom

---

### 📝 Description

You have a queue of integers, and you need to retrieve the first unique integer in the queue.

Implement the `FirstUnique` class:

- `FirstUnique(int[] nums)` Initializes the object with the numbers in the queue.
- `int showFirstUnique()` Returns the value of the first unique integer of the queue, and returns -1 if there is no such integer.
- `void add(int value)` Inserts `value` to the queue.

---

### 📘 Examples

#### Example 1

**Input:**
["FirstUnique","showFirstUnique","add","showFirstUnique","add","showFirstUnique","add","showFirstUnique"]
[[[2,3,5]],[],[5],[],[2],[],[3],[]]

**Output:**
[null,2,null,2,null,3,null,-1]

**Explanation:**

````cpp
FirstUnique firstUnique = new FirstUnique([2,3,5]);
firstUnique.showFirstUnique(); // return 2
firstUnique.add(5);            // the queue is now [2,3,5,5]
firstUnique.showFirstUnique(); // return 2
firstUnique.add(2);            // the queue is now [2,3,5,5,2]
firstUnique.showFirstUnique(); // return 3
firstUnique.add(3);            // the queue is now [2,3,5,5,2,3]
firstUnique.showFirstUnique(); // return -1
Example 2
Input:

css
Copy code
["FirstUnique","showFirstUnique","add","add","add","add","add","showFirstUnique"]
[[[7,7,7,7,7,7]],[],[7],[3],[3],[7],[17],[]]
Output:

[null,-1,null,null,null,null,null,17]

---

## Constraints

- `1 <= nums.length <= 10^5`
- `1 <= nums[i] <= 10^8`
- `1 <= value <= 10^8`
- At most 50,000 calls will be made to `showFirstUnique` and `add`.

---

## Solution (C++)

```cpp
class FirstUnique {
public:
    queue<int> qu;                     // To keep the order of elements maintained
    unordered_map<int, int> freq;      // To keep the frequency of each element

    FirstUnique(vector<int>& nums) {
        freq.clear();
        while (!qu.empty()) qu.pop();
        for (auto num : nums) {
            qu.push(num);
            freq[num]++;
        }
    }

    int showFirstUnique() {
        while (!qu.empty() && freq[qu.front()] > 1) {
            qu.pop();
        }
        if (qu.empty()) return -1;
        return qu.front();
    }

    void add(int value) {
        qu.push(value);
        freq[value]++;
    }
};
````
