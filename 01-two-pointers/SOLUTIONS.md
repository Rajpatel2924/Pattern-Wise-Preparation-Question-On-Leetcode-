# Solutions - Two Pointers

---

## 1) 15. 3Sum
### Problem
Given an array `nums`, return all unique triplets `[nums[i], nums[j], nums[k]]` such that `nums[i] + nums[j] + nums[k] = 0`.

### Intuition
Sort the array. Fix one number `a = nums[i]`, then use two pointers to find pairs that sum to `-a`. Moving pointers based on current sum allows O(n^2). Skip duplicates to keep results unique.

### Python
```python
from typing import List

class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res = []
        n = len(nums)
        for i in range(n):
            if i > 0 and nums[i] == nums[i-1]:
                continue
            if nums[i] > 0:
                break
            l, r = i+1, n-1
            while l < r:
                s = nums[i] + nums[l] + nums[r]
                if s == 0:
                    res.append([nums[i], nums[l], nums[r]])
                    l += 1
                    r -= 1
                    while l < r and nums[l] == nums[l-1]:
                        l += 1
                    while l < r and nums[r] == nums[r+1]:
                        r -= 1
                elif s < 0:
                    l += 1
                else:
                    r -= 1
        return res
```

### Java
```java
import java.util.*;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            if (nums[i] > 0) break;
            int l = i + 1, r = n - 1;
            while (l < r) {
                int s = nums[i] + nums[l] + nums[r];
                if (s == 0) {
                    res.add(Arrays.asList(nums[i], nums[l], nums[r]));
                    l++;
                    r--;
                    while (l < r && nums[l] == nums[l - 1]) l++;
                    while (l < r && nums[r] == nums[r + 1]) r--;
                } else if (s < 0) {
                    l++;
                } else {
                    r--;
                }
            }
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
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<vector<int>> res;
        int n = nums.size();
        for (int i = 0; i < n; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            if (nums[i] > 0) break;
            int l = i + 1, r = n - 1;
            while (l < r) {
                int s = nums[i] + nums[l] + nums[r];
                if (s == 0) {
                    res.push_back({nums[i], nums[l], nums[r]});
                    l++; r--;
                    while (l < r && nums[l] == nums[l - 1]) l++;
                    while (l < r && nums[r] == nums[r + 1]) r--;
                } else if (s < 0) {
                    l++;
                } else {
                    r--;
                }
            }
        }
        return res;
    }
};
```

---

## 2) 42. Trapping Rain Water
### Problem
Given `height[i]`, compute how much water can be trapped after raining.

### Intuition
Two pointers from both ends. Maintain `leftMax` and `rightMax`. The side with smaller max determines water level at that pointer: if `leftMax <= rightMax`, water at left is `leftMax - height[l]`, else use `rightMax`.

### Python
```python
from typing import List

class Solution:
    def trap(self, height: List[int]) -> int:
        l, r = 0, len(height) - 1
        left_max = right_max = 0
        ans = 0
        while l < r:
            if height[l] <= height[r]:
                left_max = max(left_max, height[l])
                ans += left_max - height[l]
                l += 1
            else:
                right_max = max(right_max, height[r])
                ans += right_max - height[r]
                r -= 1
        return ans
```

### Java
```java
class Solution {
    public int trap(int[] height) {
        int l = 0, r = height.length - 1;
        int leftMax = 0, rightMax = 0;
        int ans = 0;
        while (l < r) {
            if (height[l] <= height[r]) {
                leftMax = Math.max(leftMax, height[l]);
                ans += leftMax - height[l];
                l++;
            } else {
                rightMax = Math.max(rightMax, height[r]);
                ans += rightMax - height[r];
                r--;
            }
        }
        return ans;
    }
}
```

### C++
```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int trap(vector<int>& height) {
        int l = 0, r = (int)height.size() - 1;
        int leftMax = 0, rightMax = 0;
        int ans = 0;
        while (l < r) {
            if (height[l] <= height[r]) {
                leftMax = max(leftMax, height[l]);
                ans += leftMax - height[l];
                l++;
            } else {
                rightMax = max(rightMax, height[r]);
                ans += rightMax - height[r];
                r--;
            }
        }
        return ans;
    }
};
```

---

## 3) 76. Minimum Window Substring
### Problem
Given strings `s` and `t`, return the minimum window in `s` which contains all characters in `t` (including duplicates).

### Intuition
Sliding window with counts. Expand right pointer, update freq. When window covers all chars required, try to shrink from left while maintaining validity. Track best length.

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
        best = (float('inf'), None, None)
        for r, ch in enumerate(s):
            if need[ch] > 0:
                missing -= 1
            need[ch] -= 1

            while missing == 0:
                if r - l + 1 < best[0]:
                    best = (r - l + 1, l, r)
                left_ch = s[l]
                need[left_ch] += 1
                if need[left_ch] > 0:
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
        if (t.length() == 0 || s.length() == 0) return "";
        int[] need = new int[128];
        for (char c : t.toCharArray()) need[c]++;
        int missing = t.length();
        int l = 0;
        int bestLen = Integer.MAX_VALUE;
        int bestL = -1, bestR = -1;

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

## 4) 167. Two Sum II - Input Array Is Sorted
### Problem
Given sorted array `numbers`, return indices (1-based) of two numbers such that they add up to `target`.

### Intuition
Two pointers: one at start, one at end. If sum is too small, move left pointer right; if too large, move right pointer left.

### Python
```python
from typing import List

class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, r = 0, len(numbers) - 1
        while l < r:
            s = numbers[l] + numbers[r]
            if s == target:
                return [l + 1, r + 1]
            elif s < target:
                l += 1
            else:
                r -= 1
        return []
```

### Java
```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int l = 0, r = numbers.length - 1;
        while (l < r) {
            int s = numbers[l] + numbers[r];
            if (s == target) return new int[]{l + 1, r + 1};
            if (s < target) l++; else r--;
        }
        return new int[0];
    }
}
```

### C++
```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int l = 0, r = (int)numbers.size() - 1;
        while (l < r) {
            int s = numbers[l] + numbers[r];
            if (s == target) return {l + 1, r + 1};
            if (s < target) l++;
            else r--;
        }
        return {};
    }
};
```


