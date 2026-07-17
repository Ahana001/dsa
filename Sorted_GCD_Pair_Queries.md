## Sorted GCD Pair Queries

```cpp
class Solution {
public:
    vector<int> gcdValues(vector<int>& nums, vector<long long>& queries) {
        // Find max element because GCD cannot be greater than the maximum
        // element in nums. max_element() does not return the maximum value. It
        // returns an iterator pointing to the maximum element.
        int maxNum = *max_element(nums.begin(), nums.end());

        // Count the frequency of each number since duplicate values contribute
        // multiple times to GCD pairs.
        vector<int> frequency(maxNum + 1, 0);
        for (int num: nums) {
            frequency[num]++;
        }

        // divCnt[i] = number of elements in nums that are divisible by i.
        vector<long long> divCount(maxNum + 1, 0);
        for (int i = 1; i <= maxNum; i++) {
            for (int j = i; j <= maxNum; j += i) {
                // Check all multiples of i (i, 2*i, 3*i, ...) and count how
                // many numbers are divisible by i.
                divCount[i] += frequency[j];
            }
        }

        // Example: nums = [2, 4, 8]
        // divCnt[2] = 3 because all three numbers are divisible by 2.
        // Total pairs divisible by 2 = C(3,2) = 3
        // Pairs: (2,4), (2,8), (4,8)
        // But these are NOT all pairs with GCD exactly 2.
        // gcd(2,4) = 2
        // gcd(2,8) = 2
        // gcd(4,8) = 4
        // So later we subtract the pairs already counted for larger GCDs
        // (multiples of 2) to get the exact count of pairs with GCD = 2.
        for (int i = maxNum; i >= 1; i--) {
            long long pairs = (divCount[i] * (divCount[i] - 1)) / 2;
            for (int j = i + i; j <= maxNum; j += i) {
                pairs -= divCount[j];
            }
            divCount[i] = pairs;
        }

        // Why prefix + binary search?
        // Suppose we have exact GCD counts:
        // gcd = 1 -> 5 pairs
        // gcd = 2 -> 3 pairs
        // gcd = 3 -> 2 pairs
        //
        // Without prefix:
        // For every query, we need to scan from gcd = 1 to M,
        // keep adding counts until we reach the query index.
        // This takes O(M) time per query. and if have q queries then O(q * M)
        // With prefix:
        // Convert exact counts into cumulative counts:
        //
        // prefix[1] = 5  -> 5 gcdPairs elements are <= 1
        // prefix[2] = 8  -> 8 gcdPairs elements are <= 2
        // prefix[3] = 10 -> 10 gcdPairs elements are <= 3
        //
        // Now prefix is sorted (non-decreasing), so we can binary search
        // the smallest gcd where prefix[gcd] > query index.
        // Query time reduces from O(q * M) to O(q log M).
        vector<long long> binarySearchPrefix(maxNum + 1, 0);
        for (int i = 1; i <= maxNum; i++) {
            binarySearchPrefix[i] = binarySearchPrefix[i - 1] + divCount[i];
        }

        vector<int> ans;
        for (long long q : queries) {
            int l = 1;
            int h = maxNum;
            while (l <= h) {
                int mid = l + (h -  l) / 2;
                if (binarySearchPrefix[mid] > q) {
                    h = mid - 1;
                } else {
                    l = mid + 1;
                }
            }
            ans.push_back(l);
        }
        return ans;
    }
};
```

# Approach

## 1. Find Maximum Element

```cpp
int maxNum = *max_element(nums.begin(), nums.end());
```

### Complexity

```
O(n)
```

---

# 2. Build Frequency Array

```cpp
vector<int> frequency(maxNum + 1, 0);

for (int num : nums) {
    frequency[num]++;
}
```

### Complexity

Time:

```
O(n)
```

Space:

```
O(M)
```

where `M` is the maximum value in `nums`.

---

# 3. Count Numbers Divisible by Each Value

```cpp
for (int i = 1; i <= M; i++) {
    for (int j = i; j <= M; j += i) {
        divCount[i] += frequency[j];
    }
}
```

### Complexity

Time:

```
O(M log M)
```

---

# 4. Find Exact GCD Count

Initially:

```cpp
(divCount[i] * (divCount[i]-1)) / 2
```

### Complexity

Same divisor pattern:

```
O(M log M)
```

---

# 5. Build Prefix Array

```cpp
for (int i = 1; i <= M; i++) {
    prefix[i] = prefix[i-1] + divCount[i];
}
```

### Complexity

```
O(M)
```

---

# 6. Binary Search Queries

Each query:

```
O(log M)
```

For `Q` queries:

```
O(Q log M)
```

---

# Time Complexity Analysis

Let:

```
n = size of nums

M = maximum element in nums

Q = number of queries
```

| Operation | Complexity |
|-----------|------------|
| Find maximum element | O(n) |
| Build frequency array | O(n) |
| Count divisible numbers | O(M log M) |
| Calculate exact GCD counts | O(M log M) |
| Build prefix array | O(M) |
| Binary search queries | O(Q log M) |

Total:

\[
O(n)+O(n)+O(M\log M)+O(M\log M)+O(M)+O(Q\log M)
\]

Ignoring smaller terms:

```
O(n + M log M + Q log M)
```

---

# Space Complexity

Extra arrays used:

```
frequency -> O(M)

divCount -> O(M)

prefix -> O(M)
```

Total:

```
O(M)
```

---

# Why Not Build and Sort gcdPairs?

Number of pairs:

\[
P=\frac{n(n-1)}{2}
\]

If we create all GCD pairs:

```
gcdPairs size = O(n^2)
```

Sorting:

```
O(P log P)
```

Approximately:

```
O(n^2 log n)
```

This is too slow for large input.

Therefore, we use:

```
Frequency Count
        |
        v
Count Multiples
        |
        v
Find Exact GCD Counts
        |
        v
Prefix Sum
        |
        v
Binary Search Queries
```

This reduces the complexity to:

```
O(n + M log M + Q log M)
```
