## [1236. Web Crawler](https://leetcode.com/problems/web-crawler/)

**Difficulty:** Medium  
**Tags:** Graph, BFS, DFS  
**Companies:** —

---

### 📝 Problem Description

Given a starting URL `startUrl` and an interface `HtmlParser` that can fetch all URLs linked from a given URL, implement a web crawler that crawls **only** URLs under the same hostname as `startUrl`.

**Key points:**

- Start crawling from `startUrl`.
- Use `HtmlParser.getUrls(url)` to get all URLs on the page of `url`.
- Avoid crawling the same URL twice.
- Crawl **only** URLs with the same hostname as `startUrl`.
- URLs with trailing slashes `/` are considered different URLs.
- All URLs use `http` protocol without ports.

---

---

### ✅ Constraints

- `1 <= urls.length <= 1000`
- URLs length up to 300 characters.
- Hostname may include letters, digits, hyphens, and dots but not start or end with a hyphen.
- No duplicates in URL list.
- `startUrl` is guaranteed to be in the URLs.

---

### 💡 Approach

1. Extract the hostname from `startUrl` by finding substring up to the first `/` after `"http://"` (index 7).
2. Use BFS or DFS to crawl starting from `startUrl`.
3. For each URL obtained from `HtmlParser.getUrls(currentUrl)`:
   - Check if the URL has the same hostname as `startUrl`.
   - Check if it has been visited before.
4. If both pass, add to the queue/list and visited set.
5. Continue until no new URLs can be crawled.
6. Return all visited URLs.

---

### 💻 Code (C++)

```cpp
/*
 * The HtmlParser interface is given, with:
 * vector<string> getUrls(string url);
 */

class Solution {
public:
    vector<string> crawl(string startUrl, HtmlParser htmlParser) {
        // Extract hostname (up to the first '/' after http://)
        string hostname = startUrl.substr(0, startUrl.find('/', 7));

        vector<string> queue {startUrl};
        unordered_set<string> seen {startUrl};

        for (int i = 0; i < (int)queue.size(); i++) {
            string url = queue[i];
            for (const string& child : htmlParser.getUrls(url)) {
                // Only add URLs under the same hostname and not visited yet
                if (child.find(hostname) != 0 || seen.count(child)) continue;
                queue.push_back(child);
                seen.insert(child);
            }
        }
        return queue;
    }
};
```
