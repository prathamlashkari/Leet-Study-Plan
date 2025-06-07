# 616. Add Bold Tag in String

## 🧩 Problem Statement

You are given a string `s` and an array of strings `words`.

Your task is to wrap all substrings in `s` that match any word in `words` with a pair of bold tags `<b>` and `</b>`.

- If two matching substrings **overlap** or are **consecutive**, merge them and use **a single** `<b>...</b>` wrapper.
- The final result should be a string with the **minimal number of tags**, preserving the character order.

---

## 🧪 Examples

### Example 1:

**Input:**  
`s = "abcxyz123"`  
`words = ["abc", "123"]`

**Output:**  
`"<b>abc</b>xyz<b>123</b>"`

---

### Example 2:

**Input:**  
`s = "aaabbb"`  
`words = ["aa", "b"]`

**Output:**  
`"<b>aaabbb</b>"`

**Explanation:**

- "aa" appears twice as part of "aaabbb"
- "b" appears three times.
- All overlaps and consecutive bold sections are merged into one: `<b>aaabbb</b>`

---

## ✅ Constraints

- `1 <= s.length <= 1000`
- `0 <= words.length <= 100`
- `1 <= words[i].length <= 1000`
- `s` and `words[i]` consist of English letters and digits
- All values in `words` are unique

---

## 💡 Approach Summary

1. **Find All Match Intervals**:  
   Loop through each word and find every index it appears in `s`. Store each match as an interval `[start, end)`.

2. **Merge Overlapping Intervals**:  
   Sort and merge the intervals to avoid multiple tags over overlapping or consecutive matches.

3. **Build Result**:  
   Walk through the string, insert `<b>` and `</b>` around the merged intervals, and append non-matching characters directly.

---

## 📝 Code (Java)

```java
import java.util.*;

class Solution {
   public String addBoldTag(String s, String[] dict) {
        List<Interval> intervals = new ArrayList<>();

        // Find all matching intervals for words in dict
        for (String str : dict) {
        	int index = -1;
        	index = s.indexOf(str, index);
        	while (index != -1) {
        		intervals.add(new Interval(index, index + str.length()));
        		index += 1;
        		index = s.indexOf(str, index);
        	}
        }

        // Merge overlapping or consecutive intervals
        intervals = merge(intervals);

        int prev = 0;
        StringBuilder sb = new StringBuilder();

        // Build result with bold tags around merged intervals
        for (Interval interval : intervals) {
        	sb.append(s.substring(prev, interval.start));
        	sb.append("<b>");
        	sb.append(s.substring(interval.start, interval.end));
        	sb.append("</b>");
        	prev = interval.end;
        }

        if (prev < s.length()) {
        	sb.append(s.substring(prev));
        }

        return sb.toString();
    }

	// Helper class to represent intervals
	class Interval {
		int start, end;
		public Interval(int s, int e) {
			start = s;
			end = e;
		}
		public String toString() {
			return "[" + start + ", " + end + "]";
		}
	}

	// Merge overlapping intervals
	public List<Interval> merge(List<Interval> intervals) {
        if (intervals == null || intervals.size() <= 1) {
            return intervals;
        }
        Collections.sort(intervals, new Comparator<Interval>() {
            public int compare(Interval a, Interval b) {
                return a.start - b.start;
            }
        });

        int start = intervals.get(0).start;
        int end = intervals.get(0).end;
        List<Interval> res = new ArrayList<>();

        for (Interval i : intervals) {
            if (i.start <= end) {
                end = Math.max(end, i.end);
            } else {
                res.add(new Interval(start, end));
                start = i.start;
                end = i.end;
            }
        }

        res.add(new Interval(start, end));
        return res;
    }
}
```
