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
