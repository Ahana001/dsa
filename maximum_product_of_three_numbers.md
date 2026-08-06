# Maximum Product of Two Elements in an Array

https://leetcode.com/problems/maximum-product-of-two-elements-in-an-array/description/?envType=daily-question&envId=2026-07-27

## Approach: Single Pass

### Time Complexity
- **O(n)**

### Space Complexity
- **O(1)**

```cpp
class Solution {
public:
int maxProduct(vector<int>& nums) {
int n = nums.size();
int ans = 0;
int curMax = nums[0];

    for (int i = 1; i < n; i++) {
        ans = max(ans, (curMax - 1) * (nums[i] - 1));
        curMax = max(curMax, nums[i]);
    }

    return ans;
}
};
```

---

https://leetcode.com/problems/maximum-product-of-three-numbers/description/?envType=daily-question&envId=2026-07-26

# Maximum Product of Three Numbers

## Better Approach 1: Sorting

### Time Complexity
- **O(n log n)**

### Space Complexity
- **O(1)**

```cpp
class Solution {
public:
int maximumProduct(vector<int>& nums) {
sort(nums.begin(),nums.end());
int n=nums.size();

    int result1=nums[n-1]*nums[n-2]*nums[n-3];
    int result2=nums[0]*nums[1]*nums[n-1];

    return max(result1,result2);

    }
};
```

---

## Approach 2: Single Pass (Without Sorting)

### Time Complexity
- **O(n)**

### Space Complexity
- **O(1)**

```cpp
class Solution {
public:
int maximumProduct(vector<int>& nums) {
int max1 = -1000;
int max2 = -1000;
int max3 = -1000;
int min1 = 0;
int min2 = 0;
int n = nums.size();
if (n < 2) {
return nums[0] * nums[1];
}

    for (int i = 0; i < n; i++) {
        int ele = nums[i];
        if (ele >= max1) {
            max3 = max2;
            max2 = max1;
            max1 = nums[i];
        } else if (ele >= max2) {
            max3 = max2;
            max2 = nums[i];
        } else if (ele >= max3) {
            max3 = nums[i];
        }

        if(min1 >= nums[i]){
            min2 = min1;
            min1 = nums[i];
        }else if(min2 >= nums[i]){
            min2 = nums[i];
        }
    }
    return max(max1 * max2 * max3, max1 * min1 * min2);
}
};
```
