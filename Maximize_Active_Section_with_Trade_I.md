https://leetcode.com/problems/maximize-active-section-with-trade-i/description/?envType=daily-question&envId=2026-07-21

# Storing Zero Blocks In Vector

## Time Complexity

* **Time Complexity:** O(n) + O(n) + O(k) = O(n)
* **Space Complexity:** O(n)

## Code

```cpp
class Solution {
public:
    int maxActiveSectionsAfterTrade(string s) {
        // O(n) + O(n) + O(pair)
        int count = 0;
        for (char c : s) {
            if (c == '1') {
                count++;
            }
        }
        vector<int> zeroBlocks;
        int i = 0;
        while (i < s.size()) {
            if (s[i] == '0') {
                int cnt = 0;
                while (i < s.size() && s[i] == '0') {
                    cnt++;
                    i++;
                }
                zeroBlocks.push_back(cnt);
            } else {
                i++;
            }
        }

        int maxBlock = 0;
        for (int i = 1; i < zeroBlocks.size(); i++) {
            maxBlock = max(maxBlock, zeroBlocks[i] + zeroBlocks[i - 1]);
        }
        return count + maxBlock;
    }
};
```
---

# Tracking Consecutive Zero Blocks On The Fly

## Time Complexity

* **Time Complexity:** O(n) + O(n) = O(n)
* **Space Complexity:** O(1)

## Code

```cpp
class Solution {
public:
    int maxActiveSectionsAfterTrade(string s) {
        // O(n) + O(n) + O(pair)
        int count = 0;
        for (char c : s) {
            if (c == '1') {
                count++;
            }
        }
        vector<int> zeroBlocks;
        int i = 0;
        int prev = 0;
        int cur = 0;
        int best = 0;
        while (i < s.size()) {
            if (s[i] == '0') {
                int cnt = 0;
                while (i < s.size() && s[i] == '0') {
                    cnt++;
                    i++;
                }
                prev = cur;
                cur = cnt;
                if (prev)
                    best = max(best, prev + cur);
            } else {
                i++;
            }
        }
        return count + best;
    }
};
```
