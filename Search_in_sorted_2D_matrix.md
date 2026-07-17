# Search a 2D Matrix

## Problem Statement

Given an `m x n` matrix with the following properties:

- Each row is sorted in ascending order.
- The first integer of each row is greater than the last integer of the previous row.

Return `true` if the target value exists in the matrix, otherwise return `false`.

---

## Brute Force Approach

```cpp
int m = matrix.size();
int n = matrix[0].size();

// for (int i = 0; i < m; i++) {
//     for (int j = 0; j < n; j++) {
//         if (matrix[i][j] == target) {
//             return true;
//         }
//     }
// }
```

## Time Complexity: O(m * n)
## Space Complexity: O(1)

--- 

## Brute-V2 Approach
// for (int i = 0; i < m; i++) {
//     if (matrix[i][0] > target)
//         continue;
//     if (matrix[i][n - 1] > target)
//         continue;
//     for (int j = 0; j < n; j++) {
//         if (matrix[i][j] == target) {
//             return true;
//         }
//     }
// }

## Time Complexity: O(m * n)
## Space Complexity: O(1)

---

```cpp
## Better Approach
// for (int i = 0; i < m; i++) {
//     if (matrix[i][0] <= target && target <= matrix[i][n - 1]) {
//         // Binary Search
//         int l = 0;
//         int h = n - 1;
//         while (l <= h) {
//             int mid = (l + h) / 2;
//             if (matrix[i][mid] == target)
//                 return true;
//             if (matrix[i][mid] < target) {
//                 l = mid + 1;
//             } else {
//                 h = mid - 1;
//             }
//         }
//     }
// }
```

## Time Complexity: O(m + log n)
## Space Complexity: O(1)

---

## Optimal Approach

```cpp
int l = 0;
int h = n * m - 1;

while (l <= h) {
    int mid = (l + h) / 2;
    int row = mid / n;
    int col = mid % n;

    if (matrix[row][col] == target) {
        return true;
    }

    if (matrix[row][col] < target) {
        l = mid + 1;
    } else {
        h = mid - 1;
    }
}
```

## Time Complexity: O(log(m * n))
## Space Complexity: O(1)


