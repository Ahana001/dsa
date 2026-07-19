# Majority Element

## Approach 1: Brute Force

### Code

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {

        // Brute Force - O(n^2)
        for (int i = 0; i < nums.size(); i++) {
            int count = 1;

            for (int j = i + 1; j < nums.size(); j++) {
                if (nums[j] == nums[i]) {
                    count++;
                }
            }

            if (count > (nums.size() / 2))
                return nums[i];
        }

        return -1;
    }
};
```

### Time Complexity O(n^2)
### Space Complexity O(1)

---

## Approach 2: Hash Map (Better Approach)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {

        unordered_map<int, int> freq;

        // Store frequency of each element
        for (int i = 0; i < nums.size(); i++) {
            freq[nums[i]]++;
        }

        // Find majority element
        for (auto it : freq) {
            if (it.second > (nums.size() / 2))
                return it.first;
        }

        return -1;
    }
};
```

### Time Complexity O(n)
### Space Complexity O(n)

---

## Approach 3: Boyer-Moore Voting Algorithm (Optimal Approach)

```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {

        int count = 1;
        int element = nums[0];

        for (int i = 1; i < nums.size(); i++) {

            if (count == 0)
                element = nums[i];

            if (element == nums[i]) {
                count++;
            } 
            else {
                count--;
            }
        }

        return element;
    }
};
```

### Time Complexity O(n)
### Space Complexity O(1)

---

## Complexity Comparison

| Approach                                    | Time Complexity | Space Complexity | Works Without Guarantee |
| ------------------------------------------- | --------------- | ---------------- | ----------------------- |
| Brute Force                                 | O(n²)           | O(1)             | ✅ Yes                   |
| Hash Map                                    | O(n)            | O(n)             | ✅ Yes                   |
| Boyer-Moore Voting Algorithm + Verification | O(n)            | O(1)             | ✅ Yes                   |
| Boyer-Moore Voting Algorithm Only           | O(n)            | O(1)             | ❌ No                    |


