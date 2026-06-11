# Solutions - Sliding Window

---

## 1) 3. Longest Substring Without Repeating Characters
### Problem
Given a string `s`, find the length of the longest substring without repeating characters.

### Intuition
Use a sliding window `[l..r]` with a set/map of characters. Expand `r`. If you see a duplicate, shrink `l` until the duplicate is removed.

### Python
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        last = {}
        res = 0
        l = 0
        for r, ch in enumerate(s):
            if ch in last and last[ch] >= l:
                l = last[ch] + 1
            last[ch] = r
            res = max(res, r - l + 1)
        return res
```

### Java
```java
import java.util.*;

class Solution {
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> last = new HashMap<>();
        int res = 0;
        int l = 0;
        for (int r = 0; r < s.length(); r++) {
            char ch = s.charAt(r);
            if (last.containsKey(ch) && last.get(ch) >= l) {
                l = last.get(ch) + 1;
            }
            last.put(ch, r);
            res = Math.max(res, r - l + 1);
        }
        return res;
    }
}
```

### C++
```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char,int> last;
        int res = 0;
        int l = 0;
        for (int r = 0; r < (int)s.size(); r++) {
            char ch = s[r];
            if (last.count(ch) && last[ch] >= l) {
                l = last[ch] + 1;
            }
            last[ch] = r;
            res = max(res, r - l + 1);
        }
        return res;
    }
};
```

---

## 2) 76. Minimum Window Substring
### Problem
Given strings `s` and `t`, return the minimum window in `s` that contains all characters of `t` (with multiplicity).

### Intuition
Maintain counts of required chars. Expand `r` and update counts. When the window becomes valid, shrink from `l` to minimize length.

### Python
```python
from collections import Counter

class Solution:
    def minWindow(self, s: str, t: str) -> str:
        if not t or not s:
            return ""
        need = Counter(t)
        missing = len(t)
        l = 0
        best = (10**18, None, None)

        for r, ch in enumerate(s):
            if need[ch] > 0:
                missing -= 1
            need[ch] -= 1

            while missing == 0:
                if r - l + 1 < best[0]:
                    best = (r - l + 1, l, r)
                left = s[l]
                need[left] += 1
                if need[left] > 0:
                    missing += 1
                l += 1

        if best[1] is None:
            return ""
        return s[best[1]:best[2] + 1]
```

### Java
```java
import java.util.*;

class Solution {
    public String minWindow(String s, String t) {
        if (t.isEmpty() || s.isEmpty()) return "";
        int[] need = new int[128];
        for (char c : t.toCharArray()) need[c]++;
        int missing = t.length();
        int l = 0;
        int bestLen = Integer.MAX_VALUE, bestL = -1, bestR = -1;

        for (int r = 0; r < s.length(); r++) {
            char cr = s.charAt(r);
            if (need[cr] > 0) missing--;
            need[cr]--;

            while (missing == 0) {
                if (r - l + 1 < bestLen) {
                    bestLen = r - l + 1;
                    bestL = l;
                    bestR = r;
                }
                char cl = s.charAt(l);
                need[cl]++;
                if (need[cl] > 0) missing++;
                l++;
            }
        }
        return bestL == -1 ? "" : s.substring(bestL, bestR + 1);
    }
}
```

### C++
```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    string minWindow(string s, string t) {
        if (t.empty() || s.empty()) return "";
        vector<int> need(128, 0);
        for (char c : t) need[c]++;
        int missing = (int)t.size();
        int l = 0;
        int bestLen = INT_MAX, bestL = -1, bestR = -1;

        for (int r = 0; r < (int)s.size(); r++) {
            char cr = s[r];
            if (need[cr] > 0) missing--;
            need[cr]--;

            while (missing == 0) {
                if (r - l + 1 < bestLen) {
                    bestLen = r - l + 1;
                    bestL = l;
                    bestR = r;
                }
                char cl = s[l];
                need[cl]++;
                if (need[cl] > 0) missing++;
                l++;
            }
        }
        if (bestL == -1) return "";
        return s.substr(bestL, bestLen);
    }
};
```

---

## 3) 209. Minimum Size Subarray Sum
### Problem
Given an array of positive integers `nums` and an integer `target`, return the minimal length of a contiguous subarray whose sum is at least `target`. If no such subarray exists, return 0.

### Intuition
Since all numbers are positive, the window sum increases when you expand `r`, and decreases when you move `l`. Shrink while sum >= target to find minimal length.

### Python
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: list[int]) -> int:
        l = 0
        s = 0
        res = float('inf')
        for r, x in enumerate(nums):
            s += x
            while s >= target:
                res = min(res, r - l + 1)
                s -= nums[l]
                l += 1
        return 0 if res == float('inf') else res
```

### Java
```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int l = 0;
        int sum = 0;
        int res = Integer.MAX_VALUE;
        for (int r = 0; r < nums.length; r++) {
            sum += nums[r];
            while (sum >= target) {
                res = Math.min(res, r - l + 1);
                sum -= nums[l++];
            }
        }
        return res == Integer.MAX_VALUE ? 0 : res;
    }
}
```

### C++
```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int l = 0;
        long long sum = 0;
        int res = INT_MAX;
        for (int r = 0; r < (int)nums.size(); r++) {
            sum += nums[r];
            while (sum >= target) {
                res = min(res, r - l + 1);
                sum -= nums[l++];
            }
        }
        return res == INT_MAX ? 0 : res;
    }
};
```

---

## 4) 424. Longest Repeating Character Replacement
### Problem
You are given a string `s` and an integer `k`. Replace at most `k` characters to get the longest substring containing the same character.

### Intuition
Maintain window counts and track the max frequency `maxCount` inside window. If `(window length - maxCount) <= k`, window is valid; otherwise shrink.

### Python
```python
from collections import defaultdict

class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        cnt = defaultdict(int)
        maxCount = 0
        res = 0
        l = 0

        for r, ch in enumerate(s):
            cnt[ch] += 1
            maxCount = max(maxCount, cnt[ch])

            while (r - l + 1) - maxCount > k:
                cnt[s[l]] -= 1
                l += 1

            res = max(res, r - l + 1)
        return res
```

### Java
```java
import java.util.*;

class Solution {
    public int characterReplacement(String s, int k) {
        int[] cnt = new int[26];
        int maxCount = 0;
        int res = 0;
        int l = 0;

        for (int r = 0; r < s.length(); r++) {
            int idx = s.charAt(r) - 'A';
            cnt[idx]++;
            maxCount = Math.max(maxCount, cnt[idx]);

            while ((r - l + 1) - maxCount > k) {
                cnt[s.charAt(l) - 'A']--;
                l++;
            }
            res = Math.max(res, r - l + 1);
        }
        return res;
    }
}
```

### C++
```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int characterReplacement(string s, int k) {
        vector<int> cnt(26, 0);
        int maxCount = 0;
        int res = 0;
        int l = 0;

        for (int r = 0; r < (int)s.size(); r++) {
            int idx = s[r] - 'A';
            cnt[idx]++;
            maxCount = max(maxCount, cnt[idx]);

            while ((r - l + 1) - maxCount > k) {
                cnt[s[l] - 'A']--;
                l++;
            }
            res = max(res, r - l + 1);
        }
        return res;
    }
};
```


