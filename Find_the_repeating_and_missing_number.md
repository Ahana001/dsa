## Brute Force Approach

```cpp
// Size of the array
int n = nums.size();

int repeating = -1;
int missing = -1;

// Find the repeating and missing number
for (int i = 1; i <= n; i++) {

    // Count the occurrences
    int cnt = 0;

    for (int j = 0; j < n; j++) {
        if (nums[j] == i)
            cnt++;
    }

    // Check if i is repeating or missing
    if (cnt == 2)
        repeating = i;
    else if (cnt == 0)
        missing = i;

    // If both are found, break
    if (repeating != -1 && missing != -1)
        break;
}

return {repeating, missing};
```

### Time Complexity

```text
O(N²)
```

### Space Complexity

```text
O(1)
```

---

## Better Approach: Frequency Count (Hashing)

```cpp
int duplicate = 0;
int missing = 0;
int index = 0;

vector<int> count(nums.size() + 1, 0);

for (int i = 1; i < count.size(); i++) {
    count[nums[index]]++;
    index++;
}

for (int i = 1; i < count.size(); i++) {
    if (count[i] == 2) {
        duplicate = i;
    }

    if (count[i] == 0) {
        missing = i;
    }
}

cout << "The duplicate number is: " << duplicate;
cout << "The missing number is: " << missing;
```

### Time Complexity

```text
O(2N)
```

### Space Complexity

```text
O(N)
```

---

## Optimal Approach 1: Mathematical Equations

```cpp
int n = nums.size();

long long int sum = n * (n + 1) / 2;
long long int sum2 = n * (n + 1) * (2 * n + 1) / 6;

long long int actual_sum = 0;
long long int actual_sum2 = 0;

for (int i = 0; i < nums.size(); i++) {
    actual_sum += nums[i];
    actual_sum2 += nums[i] * nums[i];
}

int missing = 0;
int duplicate = 0;

long long int E1 = sum - actual_sum;              // x - y
long long int E2 = (sum2 - actual_sum2) / E1;    // x + y

missing = (E1 + E2) / 2;
duplicate = E2 - missing;

cout << "The missing number is: " << missing;
cout << "The duplicate number is: " << duplicate;
```

### Time Complexity

```text
O(N)
```

### Space Complexity

```text
O(1)
```

---

## Optimal Approach 2: XOR Method

```cpp
int xor1 = 0;

for (int i = 0; i < nums.size(); i++) {
    xor1 ^= nums[i];
    xor1 ^= i + 1;
}

// Find rightmost set bit
int bitNo = 0;

while (1) {
    if ((xor1 & (1 << bitNo)) != 0) {
        break;
    }
    bitNo++;
}

int ones = 0;
int zeros = 0;

for (int i = 0; i < nums.size(); i++) {
    if ((nums[i] & (1 << bitNo)) != 0) {
        ones ^= nums[i];
    } else {
        zeros ^= nums[i];
    }
}

int count = 0;

for (int i = 0; i < nums.size(); i++) {
    if (nums[i] == ones) {
        count++;
    }
}

if (count == 2) {
    cout << "The duplicate number is: " << ones;
    cout << "The missing number is: " << zeros;
} else {
    cout << "The missing number is: " << zeros;
    cout << "The duplicate number is: " << ones;
}
```

### Time Complexity

```text
O(2N) ~ O(N)
```

### Space Complexity

```text
O(1)
```
