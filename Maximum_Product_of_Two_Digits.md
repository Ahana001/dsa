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
