https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array/?envType=daily-question&envId=2026-07-27

## Brute Force

### Time Complexity: O(n²)
### Space Complexity: O(1)

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int product = 0;
        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                product = max((nums[i] - 1) * (nums[j] - 1), product);
            }
        }
        return product;
    }
};
```

## Better Approach — Find Two Maximums

### Time Complexity: O(n)
### Space Complexity: O(1)

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int product = 0;
        int currentMax = nums[0];
        for (int i = 1; i < nums.size(); i++) {
            product = max((currentMax - 1) * (nums[i] - 1), product);
            currentMax = max(currentMax, nums[i]);
        }
        return product;
    }
};
```

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int max1 = 0;
        int max2 = 0;

        for (int num : nums) {
            if (num > max1) {
                max2 = max1;
                max1 = num;
            } else if (num > max2) {
                max2 = num;
            }
        }

        return (max1 - 1) * (max2 - 1);
    }
};
```
