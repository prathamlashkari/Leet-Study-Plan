# 439. Ternary Expression Parser

## 🧩 Problem Statement

You are given a string `expression` representing arbitrarily nested **ternary expressions**. Evaluate the expression and return the result.

The expression contains:

- `'T'` and `'F'` to represent boolean true and false.
- `?` and `:` for ternary conditionals.
- One-digit numbers (`0` to `9`) as result values.

Ternary expressions group **right-to-left** (just like in C/C++/Java). The result will always be a single character: a digit, `'T'`, or `'F'`.

---

## 🧪 Examples

### Example 1:

Input: expression = "T?2:3"
Output: "2"
Explanation: 'T' is true, so the result is 2.

### Example 2:

Input: expression = "F?1:T?4:5"
Output: "4"
Explanation:
F is false, so we evaluate the false branch → (T ? 4 : 5) → 4

### Example 3:

Input: expression = "T?T?F:5:3"
Output: "F"
Explanation:
T is true → evaluate (T ? F : 5) → F

---

## ✅ Constraints

- `5 <= expression.length <= 10^4`
- `expression` only contains characters `'0'`–`'9'`, `'T'`, `'F'`, `'?'`, and `':'`
- It is guaranteed to be a valid ternary expression
- Each result is a one-digit number or `'T'`/`'F'`

---

## 💡 Approach

We simulate the evaluation of the ternary expression using a **stack** because:

- Ternary expressions associate **right-to-left**
- Processing from the end ensures we evaluate inner expressions first
- Each ternary expression is of the form:  
  `condition ? true_value : false_value`

### Steps:

1. Traverse the expression from **right to left**
2. Push characters onto a stack
3. When we see a `'?'`, pop the next two results and evaluate based on the condition
4. Push the chosen value back to the stack
5. Continue until the entire expression is processed

---

## 🧠 Complexity

- **Time Complexity:** O(n), where n is the length of the expression
- **Space Complexity:** O(n), for the stack

---

## 🧾 Java Code

```java
class Solution {
  public String parseTernary(String expression) {
    if (expression == null || expression.length() == 0) return "";

    Deque<Character> stack = new LinkedList<>();

    for (int i = expression.length() - 1; i >= 0; i--) {
        char c = expression.charAt(i);

        // If we find a ternary condition
        if (!stack.isEmpty() && stack.peek() == '?') {
            stack.pop(); // remove '?'
            char trueExpr = stack.pop(); // get true result
            stack.pop(); // remove ':'
            char falseExpr = stack.pop(); // get false result

            // Choose which result to push back based on condition
            stack.push(c == 'T' ? trueExpr : falseExpr);
        } else {
            stack.push(c);
        }
    }

    // Final evaluated result
    return String.valueOf(stack.peek());
  }
}
```
