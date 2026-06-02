# Sort 0s, 1s, and 2s

## Brute Force Approach - Merge Sort / Quick Sort

**Time Complexity:** `O(n log n)`  
**Space Complexity:** `O(n)`

## Better Approach - Count 0s, 1s, and 2s

**Time Complexity:** `O(2n) ≈ O(n)`  
**Space Complexity:** `O(1)`

```cpp
int zero = 0;
int first = 0;
int second = 0;

for (int i = 0; i < nums.size(); i++) {
    if (nums[i] == 0) {
        zero++;
    } else if (nums[i] == 1) {
        first++;
    } else {
        second++;
    }
}

int index = 0;

while (zero != 0) {
    nums[index] = 0;
    index++;
    zero--;
}

while (first != 0) {
    nums[index] = 1;
    index++;
    first--;
}

while (second != 0) {
    nums[index] = 2;
    index++;
    second--;
}
```

---

## Optimal Solution - Dutch National Flag Algorithm

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(1)`

### Pointer Representation

- `0 → low - 1` ⇒ All elements are `0`
- `low → mid - 1` ⇒ All elements are `1`
- `mid → high` ⇒ Unsorted part
- `high + 1 → n - 1` ⇒ All elements are `2`

### Code

```cpp
class Solution {
public:
    void sortZeroOneTwo(vector<int>& nums) {
        int low = 0;
        int mid = 0;
        int high = nums.size() - 1;

        while (mid <= high) {
            int temp;

            if (nums[mid] == 0) {
                temp = nums[low];
                nums[low] = nums[mid];
                nums[mid] = temp;

                low++;
                mid++;
            }
            else if (nums[mid] == 1) {
                mid++;
            }
            else {
                temp = nums[high];
                nums[high] = nums[mid];
                nums[mid] = temp;

                high--;
            }
        }
    }
};
```

### Final Complexity

| Approach | Time Complexity | Space Complexity |
|-----------|----------------|------------------|
| Merge/Quick Sort | O(n log n) | O(n) |
| Counting Method | O(n) | O(1) |
| Dutch National Flag Algorithm | O(n) | O(1) |
