https://leetcode.com/problems/smallest-palindromic-rearrangement-i/description/?envType=daily-question&envId=2026-07-28

# Lexicographically Smallest Palindrome

## Brute Force Approach: Sort First Half

### Loop Analysis
1. `sort(begin(s), begin(s) + mid)` → **O((n/2) log(n/2)) = O(n log n)**
2. `for (int i = 0; i < mid; i++)` → **O(n/2) = O(n)**

### Note
Original: `baaaab`

First half: `baa`

After sorting: `aab`

Mirror it:

`aab` + `baa` = `aabbaa`

If the input is not a palindrome (example: `aaaabbbb`), this approach will not work because the second half does not match the first half.

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

https://leetcode.com/problems/smallest-palindromic-rearrangement-ii/description/?envType=daily-question&envId=2026-07-29

## Better Approach

### Time Complexity: O(n × 26 × 26 × n)
### Space Complexity: O(n)

```cpp
class Solution {
public:
    long long nCr(int n, int r, int k) {
        r = min(r, n - r);
        long long sum = 1;
        for (int i = 1; i <= r; i++) {
            sum *= (n - i + 1);
            sum /= i;

            if (sum > k) {
                return k;
            }
        }
        return sum;
    }
    long long countWays(vector<int>& half, int total, int k) {
        long long ways = 1;

        for (int i = 0; i < 26; i++) {
            if (half[i]) {
                ways *= nCr(total, half[i], k);

                if (ways >= k)
                    return k;

                total -= half[i];
            }
        }

        return ways;
    }
    string smallestPalindrome(string s, int k) {
        vector<int> freq(26, 0);
        vector<int> half(26, 0);
        int n = s.size();
        string result = "";
        char mid = '1';
        for (char c : s) {
            freq[c - 'a']++;
        }

        for (int i = 0; i < 26; i++) {
            half[i] = freq[i] / 2;
            if (freq[i] % 2 == 1) {
                mid = i + 'a';
            }
        }

        for (int pos = 0; pos < n / 2; pos++) {
            for (int i = 0; i < 26; i++) {
                if (half[i]) {
                    half[i]--; // set char at pos now checking other char and
                               // their ways
                    int total = n / 2 - pos - 1;
                    long long ways = countWays(half, total, k);

                    if (ways >= k) {
                        result += i + 'a';
                        break;
                    }

                    k -= ways;
                    half[i]++;
                }
            }
        }

        if (result.size() != (n / 2)) {
            return "";
        }
        string ans = result;
        if (mid != '1') {
            ans += mid;
        }
        reverse(result.begin(), result.end());
        ans += result;
        return ans;
    }
};
```
