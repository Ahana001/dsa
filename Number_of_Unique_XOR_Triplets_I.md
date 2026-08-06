https://leetcode.com/problems/number-of-unique-xor-triplets-i/description/?envType=daily-question&envId=2026-07-23

# Brute Force

## Intuition
- Generate every possible triplet `(i, j, k)` where `i <= j <= k`.
- Compute the XOR of the three elements: `nums[i] ^ nums[j] ^ nums[k]`.
- Store each XOR value in a `set` to keep only unique results.
- The answer is the size of the set.

## Time Complexity
- **O(n³ log n)** – There are `O(n³)` triplets, and each insertion into a `set` takes `O(log n)`.

## Space Complexity
- **O(U)** – `U` is the number of unique XOR values stored in the set.

## Code

```cpp
class Solution {
public:
    int uniqueXorTriplets(vector<int>& nums) {
        int n = nums.size();
        set<int> st;

        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                for (int k = j; k < n; k++) {
                    st.insert(nums[i] ^ nums[j] ^ nums[k]);
                }
            }
        }

        return st.size();
    }
};
```
---

## Better Approach 

The array is a permutation of [1, n], so it contains every power of two up to the highest bit of n (1, 2, 4, 8, ...). These powers of two act as independent bit selectors. Any number between 0 and mask is just a combination of these bits, so we can create it by XORing the required powers of two. If we need exactly three numbers, we can use a ^ b ^ b = a to add a duplicate element and keep the same XOR value. Therefore every value from 0 to mask is achievable, giving mask + 1 unique XOR results

## Time Complexity
- **O(n)** – Traverse the array once.

## Space Complexity
- **O(1)** – Uses only one extra variable.

## Code

```cpp
int uniqueXorTriplets(vector<int>& nums) {
    int n = nums.size();

    if (n <= 2) return n;

    int mask = 0;
    for (int num : nums) {
        mask |= num;
    }

    return mask + 1;
}
```

## Code

```cpp
class Solution {
public:
    int uniqueXorTriplets(vector<int>& nums) {
        int n = nums.size(); // [1, 2, 3, 4, 5]
        // if (n < 3) {
        //     return n;
        // }
        // int bits = 0;
        // // bits = 0 → 1 << 0 = 1
        // // bits = 1 → 1 << 1 = 2
        // // bits = 2 → 1 << 2 = 4
        // // bits = 3 → 1 << 3 = 8 (stop)
        while ((1 << bits) <= n) {
            bits++;
        }
        // bits = 3
        return (1 << bits); // 1 << 3 -> 0001 -> 8
    }
};
```
---

## Optimal Approach 

## Time Complexity
- **O(1)** 

## Space Complexity
- **O(1)** – Uses only one extra variable.

## Code

```cpp
class Solution {
public:
    int uniqueXorTriplets(vector<int>& nums) {
        int n = nums.size(); // [1, 2, 3, 4, 5]
        if (n <= 2)
            return n;
        return 1 << bit_width((unsigned)n); // 1 shift because 0 is possible 
    }
};
```

---

https://leetcode.com/problems/number-of-unique-xor-triplets-ii/description/?envType=daily-question&envId=2026-07-24

## Time Complexity

- **Pair XOR Computation:** `O(n²)`
- **Triplet XOR Generation:** `O(2048 × n) = O(n)` (2048 is a constant)
- **Counting Unique XORs:** `O(2048) = O(1)`

**Overall Time Complexity:** **`O(n²)`**

## Space Complexity

- `pair_xor[2048]`
- `triplet_xor[2048]`

**Overall Space Complexity:** **`O(1)`** (constant extra space)

## Code

```cpp
class Solution {
public:
    int uniqueXorTriplets(vector<int>& nums) {
        const int max_xor = 2048;

        vector<bool> pair_xor(max_xor, false);
        vector<bool> triplet_xor(max_xor, false);

        int n = nums.size();

        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                pair_xor[nums[i] ^ nums[j]] = true;
            }
        }

        for (int x = 0; x < max_xor; x++) {
            if (!pair_xor[x]) continue;
            for (int v : nums) {
                triplet_xor[x ^ v] = true;
            }
        }

        int count = 0;
        for (int i = 0; i < max_xor; i++) {
            if (triplet_xor[i]) count++;
        }

        return count;
    }
};
```

## Summary

| Complexity | Value |
|------------|-------|
| **Time Complexity** | **O(n²)** |
| **Space Complexity** | **O(1)** |
