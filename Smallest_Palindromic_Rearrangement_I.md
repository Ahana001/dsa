https://leetcode.com/problems/smallest-palindromic-rearrangement-i/description/?envType=daily-question&envId=2026-07-28

# Lexicographically Smallest Palindrome

## Brute Force Approach: Sort First Half

### Loop Analysis
1. `sort(begin(s), begin(s) + mid)` → **O((n/2) log(n/2)) = O(n log n)**
2. `for (int i = 0; i < mid; i++)` → **O(n/2) = O(n)**

### Time Complexity
- **O(n log n)**

### Space Complexity
- **O(1)**

```cpp
class Solution {
public:
string smallestPalindrome(string s) {
int n = s.length();
int mid = n / 2;

    sort(begin(s), begin(s) + mid);

    for (int i = 0; i < mid; i++) {
        s[n - 1 - i] = s[i];
    }

    return s;
}
};
```

---

## Better Approach: Frequency Counting

### Loop Analysis
1. `for (char c : s)` → **O(n)**
2. `for (int i = 0; i < 26; i++)` → **O(26) = O(1)**
3. `while (freq[i] >= 2)` → **O(n/2)** (total across all iterations)

### Time Complexity
- **O(n)**

### Space Complexity
- **O(1)**

```cpp
class Solution {
public:
string smallestPalindrome(string s) {
vector<int> freq(26, 0);

    for (char c : s)
        freq[c - 'a']++;

    int n = s.size();
    string ans(n, ' ');

    int left = 0, right = n - 1;

    for (int i = 0; i < 26; i++) {
        while (freq[i] >= 2) {
            ans[left++] = char('a' + i);
            ans[right--] = char('a' + i);
            freq[i] -= 2;
        }

        if (freq[i] == 1) {
            ans[s.size() / 2] = char('a' + i);
        }
    }

    return ans;
}
};
```
