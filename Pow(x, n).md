# Pow(x, n)

## Brute Force Approach
- **Time Complexity:** `O(n)`
- **Space Complexity:** `O(1)`

```cpp
// Brute Force Approach
double res = 1.0;
long long power = n;
if (power < 0) {
    x = 1 / x;
    power = -power;
}

for (int i = 1; i <= power; i++) {
    res = res * x;
}
return res;
```

---

## Better Approach (Recursive Binary Exponentiation)
- **Time Complexity:** `O(log n)`
- **Space Complexity:** `O(log n)` *(recursive call stack)*

```cpp
// Time Complexity: O(log n)
// Space Complexity: O(log n)   // Recursive call stack
double power(double x, long long n) {
    if (n == 0)
        return 1.0;
    if (n == 1)
        return x;
    if (n % 2 == 0)
        return power(x * x, n / 2);

    return x * power(x, n - 1);
}

// Better Approach
long long nn = n;
if (n < 0) {
    return (1.0 / power(x, -1 * nn));
}
return power(x, nn);
```

---

## Optimal Approach (Iterative Binary Exponentiation)
- **Time Complexity:** `O(log n)`
- **Space Complexity:** `O(1)`

```cpp
// Optimal Solution
// Example:
// x = 2, n = 6
// result = 1
//
// n = 6 (even)
// x = 2 * 2 = 4
// n = 3
//
// n = 3 (odd)
// result = 1 * 4 = 4
// n = 2
//
// n = 2 (even)
// x = 4 * 4 = 16
// n = 1
//
// n = 1 (odd)
// result = 4 * 16 = 64
// n = 0
//
// Answer = 64 = 2^6
long long nn = n;
double result = 1.0;
if (nn < 0)
    nn = -1 * nn;
while (nn > 0) {
    if (nn % 2 == 0) {
        x = x * x;
        nn = nn / 2;
    } else {
        result = result * x;
        nn = nn - 1;
    }
}
if (n < 0)
    result = (double)(1.0) / (double)(result);
return result;
```
