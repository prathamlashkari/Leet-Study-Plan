# 772. Basic Calculator III

## 🧩 Problem Statement

Implement a basic calculator to evaluate a simple expression string.

The expression string may contain:

- Non-negative integers
- Operators: `+`, `-`, `*`, `/`
- Parentheses: `(` and `)`
- Spaces

All intermediate results are guaranteed to be in the range `[-2^31, 2^31 - 1]`.  
**Integer division truncates toward zero.**  
**You must NOT use `eval()` or any other built-in evaluation functions.**

---

## 🧪 Examples

### Example 1:

Input: s = "1+1"
Output: 2

### Example 2:

Input: s = "6-4/2"
Output: 4

### Example 3:

Input: s = "2*(5+5*2)/3+(6/2+8)"
Output: 21

---

## ✅ Constraints

- `1 <= s.length <= 10^4`
- `s` consists of digits, '+', '-', '\*', '/', '(', ')', and spaces.
- `s` is a valid mathematical expression.

---

## 💡 Approach

We use **recursion** and a **stack-based simulation** to process the string expression. The idea is:

- Parse and evaluate from left to right.
- When encountering `(`, recursively evaluate until the corresponding `)`.
- For each number and operator, process them and maintain a stack for interim values.
  - `+` → push number
  - `-` → push negative number
  - `*` and `/` → apply to top of stack and current number

### Key Points:

- Maintain index `i` globally to track parsing across recursive calls.
- Use a helper to parse numbers from characters.
- Accumulate result at the end by summing the stack.

---

## 🧠 Complexity

- **Time Complexity:** O(n), where n = length of the string `s`
- **Space Complexity:** O(n), due to recursion and the stack

---

## 🧾 C++ Code

```cpp
class Solution {
public:
    int calculate(string s) {
        int i = 0;
        return parseExpr(s, i);
    }

    int parseExpr(string& s, int& i) {
        vector<int> nums;
        char op = '+';

        for (; i < s.length() && op != ')'; i++) {
            if (s[i] == ' ') continue;
            int n = (s[i] == '(') ? parseExpr(s, ++i) : parseNum(s, i);

            switch (op) {
                case '+': nums.push_back(n); break;
                case '-': nums.push_back(-n); break;
                case '*': nums.back() *= n; break;
                case '/': nums.back() /= n; break;
            }

            op = s[i];
        }

        int res = 0;
        for (int n : nums) res += n;
        return res;
    }

    int parseNum(string& s, int& i) {
        int n = 0;
        while (i < s.length() && isdigit(s[i]))
            n = n * 10 + (s[i++] - '0');
        return n;
    }
};
```
