# Find GCD of Minimum and Maximum Numbers
---

# Method 1: Brute Force Approach

### Code
```cpp
class Solution {
public:
    int findGCD(vector<int>& nums) {
        int small = INT_MAX;
        int large = INT_MIN;

        for (int num : nums) {
            small = min(small, num);
            large = max(large, num);
        }

        for (int i = small; i >= 1; i--) {
            if (small % i == 0 && large % i == 0)
                return i;
        }

        return 1;
    }
};
```

### Time Complexity
- Finding minimum and maximum: **O(n)**
- Checking divisors: **O(minElement)**

**Overall:** **O(n + minElement)**

### Space Complexity
- **O(1)**

---

# Method 2: Euclidean Algorithm (Optimal)

### Idea
The Euclidean Algorithm is based on the property:

### Code
```cpp
class Solution {
public:
    int findGCD(vector<int>& nums) {
        int small = INT_MAX;
        int large = INT_MIN;

        for (int num : nums) {
            small = min(small, num);
            large = max(large, num);
        }

        while (small > 0 && large > 0) {
            if (large > small)
                large %= small;
            else
                small %= large;
        }

        return (small == 0) ? large : small;
    }
};
```

### Time Complexity
- Finding minimum and maximum: **O(n)**
- Euclidean Algorithm: **O(log(phi)(minElement))**

**Overall:** **O(n + log(minElement))**

### Space Complexity
- **O(1)**

---

# Comparison

| Method | Time Complexity | Space Complexity | Recommended |
|---------|----------------|------------------|-------------|
| Brute Force | **O(n + minElement)** | **O(1)** | ❌ No |
| Euclidean Algorithm | **O(n + log(minElement))** | **O(1)** | ✅ Yes |

