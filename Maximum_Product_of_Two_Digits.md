https://leetcode.com/problems/maximum-product-of-two-digits/description/?envType=daily-question&envId=2026-07-25

## Better Approach

### Time Complexity
- **O(d log d)**
  - `d` = number of digits in the number.
  - Sorting the digits takes `O(d log d)` time.

### Space Complexity
- **O(d)**
  - Extra vector is used to store all digits.

### Code

```cpp
class Solution {
public:
    int maxProduct(int n) {
        vector<int> digits;
        while (n > 0) {
            digits.push_back(n % 10);
            n = n / 10;
        }
        sort(digits.begin(), digits.end());
        return digits[digits.size() - 1] * digits[digits.size() - 2];
    }
};
```

---

# Optimal Approach 

### Time Complexity
- **O(d)**
  - Traverse all digits once.

### Space Complexity
- **O(1)**
  - Uses only two variables to keep track of the largest and second largest digits.

### Code

```cpp
class Solution {
public:
    int maxProduct(int n) {
        int max = 0;
        int secondMax = 0;
        while (n > 0) {
            int num = n % 10;
            if (max <= num) {
                secondMax = max;
                max = num;
            } else if (secondMax < num) {
                secondMax = num;
            }
            n = n / 10;
        }
        return max * secondMax;
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
