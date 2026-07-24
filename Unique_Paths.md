# Unique Paths (LeetCode 62)

## 1. Recursion (Brute Force)

### Code

```cpp
class Solution {
public:
    int recurrence(int m, int n, int row, int col) {
        if (row == m - 1 && col == n - 1)
            return 1;

        if (row >= m || col >= n)
            return 0;

        int down = recurrence(m, n, row + 1, col);
        int right = recurrence(m, n, row, col + 1);

        return down + right;
    }

    int uniquePaths(int m, int n) {
        return recurrence(m, n, 0, 0);
    }
};
```

### Time Complexity

- **Time:** `O(2^(m+n))`
- **Space:** `O(m+n)` (Recursion stack)

---

# 2. Memoization (Top-Down DP)

### Code

```cpp
class Solution {
public:
    int memoization(int m, int n, int row, int col, vector<vector<int>>& dp) {
        if (row == m - 1 && col == n - 1)
            return 1;

        if (row >= m || col >= n)
            return 0;

        if (dp[row][col] != -1)
            return dp[row][col];

        int down = memoization(m, n, row + 1, col, dp);
        int right = memoization(m, n, row, col + 1, dp);

        return dp[row][col] = down + right;
    }

    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, -1));
        return memoization(m, n, 0, 0, dp);
    }
};
```

### Time Complexity

- **Time:** `O(m × n)`
- **Space:** `O(m × n) + O(m+n)` (DP + recursion stack)

---

# 3. Tabulation (Bottom-Up DP)

### Code

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> dp(m, vector<int>(n, 0));

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {

                if (i == 0 && j == 0) {
                    dp[i][j] = 1;
                    continue;
                }

                int up = 0;
                int left = 0;

                if (i > 0)
                    up = dp[i - 1][j];

                if (j > 0)
                    left = dp[i][j - 1];

                dp[i][j] = up + left;
            }
        }

        return dp[m - 1][n - 1];
    }
};
```

### Time Complexity

- **Time:** `O(m × n)`
- **Space:** `O(m × n)`

---

# 4. Space Optimized DP

### Code

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> prev(n, 0);

        for (int i = m - 1; i >= 0; i--) {

            vector<int> curr(n, 0);

            for (int j = n - 1; j >= 0; j--) {

                if (i == m - 1 && j == n - 1) {
                    curr[j] = 1;
                    continue;
                }

                int up = 0;
                int left = 0;

                if (i < m - 1)
                    up = prev[j];

                if (j < n - 1)
                    left = curr[j + 1];

                curr[j] = up + left;
            }

            prev = curr;
        }

        return prev[0];
    }
};
```

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> prev(n, 0);

        for (int i = 0; i < m; i++) {

            vector<int> curr(n, 0);

            for (int j = 0; j < n; j++) {

                if (i == 0 && j == 0) {
                    curr[j] = 1;
                    continue;
                }

                int up = 0;
                int left = 0;

                if (i > 0)
                    up = prev[j];

                if (j > 0)
                    left = curr[j - 1];

                curr[j] = up + left;
            }

            prev = curr;
        }

        return prev[n - 1];
    }
};
```

### Time Complexity

- **Time:** `O(m × n)`
- **Space:** `O(n)`

---

# Complexity Summary

| Method | Time Complexity | Space Complexity |
|---------|-----------------|------------------|
| Recursion | `O(2^(m+n))` | `O(m+n)` |
| Memoization | `O(m × n)` | `O(m × n) + O(m+n)` |
| Tabulation | `O(m × n)` | `O(m × n)` |
| Space Optimized DP | `O(m × n)` | `O(n)` |
