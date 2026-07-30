# Rotate Array

## Time Complexity

### Approach 1 (Extra Array)

- **Time Complexity:** `O(k) + O(n-k) + O(k) = O(n)`
- **Space Complexity:** `O(k)`

## Code

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        // SC - O(k)
        // TC - O(k) + O(n-k) + O(k) ~ O(n)
        vector<int> temp;
        int n = nums.size();
        k = k % n;

        for (int i = n - k; i < n; i++) {
            temp.push_back(nums[i]);
        }

        for (int i = n - k - 1; i >= 0; i--) {
            nums[i + k] = nums[i];
        }

        for (int i = 0; i < k; i++) {
            nums[i] = temp[i];
        }
    }
};
```

---

### Approach 2 (Reversal Algorithm)

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        k = k % n;
        reverse(nums.begin(), nums.end());
        reverse(nums.begin(), nums.begin() + k);
        reverse(nums.begin() + k, nums.end());
    }
};
```

- **Time Complexity:** `O(2n)`
- **Space Complexity:** `O(1)`

---

https://leetcode.com/problems/shift-2d-grid/description/?envType=daily-question&envId=2026-07-20

# Rotate Array - Approach 1 (Extra Array)

## Time Complexity

- **Time Complexity:** `O(k) + O(n-k) + O(k) = O(n)`
- **Space Complexity:** `O(k)`

## Code

```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        vector<int> temp;
        int n = nums.size();
        k = k % n;

        for (int i = n - k; i < n; i++) {
            temp.push_back(nums[i]);
        }

        for (int i = n - k - 1; i >= 0; i--) {
            nums[i + k] = nums[i];
        }

        for (int i = 0; i < k; i++) {
            nums[i] = temp[i];
        }
    }
};
```

---

# Rotate Array - Approach 2 (Reversal Algorithm)

## Time Complexity

- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

## Code

```cpp
class Solution {
public:
    vector<vector<int>> shiftGrid(vector<vector<int>>& grid, int k) {
        int m = grid.size();    // rows
        int n = grid[0].size(); // columns
        vector<vector<int>> ans(m, vector<int>(n));
        int total = m * n;
        k = k % total;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int oldIndex = i * n + j;

                int newIndex = (oldIndex + k) % total;

                int newRow = newIndex / n;
                int newCol = newIndex % n;

                ans[newRow][newCol] = grid[i][j];
            }
        }

        return ans;
    }
};
```

---

# Shift 2D Grid - Approach 2 (Reversal Algorithm)

## Time Complexity

- **Time Complexity:** `O(m × n)`
- **Space Complexity:** `O(1)`

## Code

```cpp
class Solution {
public:
    void shift(vector<vector<int>>& grid, int i, int j) {
        int r = grid.size(), c = grid[0].size();
        while (i < j) {
            swap(grid[i / c][i % c], grid[j / c][j % c]);
            i++;
            j--;
        }
    };

    vector<vector<int>> shiftGrid(vector<vector<int>>& grid, int k) {
        if (!k)
            return grid;
        int r = grid.size(), c = grid[0].size();
        int n = r * c;

        k = k % n;
        if (!k)
            return grid;

        shift(grid, 0, n - 1);
        shift(grid, 0, k - 1);
        shift(grid, k, n - 1);
        return grid;
    }
};
```
