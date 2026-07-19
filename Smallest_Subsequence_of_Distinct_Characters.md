# Smallest Subsequence of Distinct Characters

```cpp
class Solution {
public:
    string smallestSubsequence(string s) {
        vector<int> last(26);
        // O(n)
        for (int i = 0; i < s.size(); i++) {
            last[s[i] - 'a'] = i;
        }

        vector<bool> check(26, false);
        string st;

        // O(n)
        // pop can happen for each character at most one so (iteration O(n)) + (push O(n)) + (pop O(n)) ~ O(n)
        for (int i = 0; i < s.size(); i++) {
            char ch = s[i];

            // If already included then skip
            // string - abca then when a come again then skip
            if (check[ch - 'a'])
                continue;

            // have character in future - last[s[i] - 'a'] > i
            // remove till stack have greater element
            while (!st.empty() && st.back() > ch && last[st.back() - 'a'] > i) {
                check[st.back() - 'a'] = false;
                st.pop_back();
            }
            st.push_back(ch);
            check[ch - 'a'] = true;
        }
        return st;
    }
};
```

---

# Time Complexity

Let **n = s.size()**.

### 1. Finding the last occurrence
```cpp
for (int i = 0; i < s.size(); i++) {
    last[s[i] - 'a'] = i;
}
```

- Traverses the string once.
- **Time:** `O(n)`

---

### 2. Building the answer

```cpp
for (int i = 0; i < s.size(); i++) {
    ...
    while (...) {
        st.pop_back();
    }
    st.push_back(ch);
}
```

Although there is a nested `while` loop, the overall complexity is still **O(n)**.

#### Why?

- Each character occurrence is **pushed into the stack at most once**.
- Each pushed occurrence is **popped at most once**.
- Therefore:
  - Total `push_back()` operations ≤ **n**
  - Total `pop_back()` operations ≤ **n**

So the total work is:

- Loop iterations → `O(n)`
- All pushes → `O(n)`
- All pops → `O(n)`

```
O(n) + O(n) + O(n) = O(3n) = O(n)
```

This is an **amortized analysis**.

---

# Space Complexity

- `last` → 26 integers → `O(1)`
- `check` → 26 booleans → `O(1)`
- `st` → At most one occurrence of each lowercase letter (maximum 26 characters) → `O(1)`

Overall:

- **Space Complexity:** `O(1)` (fixed lowercase English alphabet)

> If the character set were not fixed, the stack could grow up to `O(n)`.

---

# Final Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`
