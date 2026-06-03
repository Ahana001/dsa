## Brute Force and Optimal Approach

### Brute Force

```cpp
int n = matrix.size();
vector<vector<int>> temp(n, vector<int>(n));

for(int i = 0; i < n; i++){
    for(int j = 0; j < n; j++){
        temp[j][n - 1 - i] = matrix[i][j];
    }
}

for(int i = 0; i < n; i++){
    for(int j = 0; j < n; j++){
        matrix[i][j] = temp[i][j];
    }
}
```

#### Time Complexity: O(2n²) ~ O(n²)
#### Space Complexity: O(n²)

----

### Optimal Approach (In-place)


```cpp
int n = matrix.size();

// transpose
for(int i = 0; i < n; i++){
    for(int j = i; j < n; j++){
        swap(matrix[i][j], matrix[j][i]);
    }
}

// reverse each row
for(int i = 0; i < n; i++){
    reverse(matrix[i].begin(), matrix[i].end()); //  n/2 if use pointer approach to swap
}
```

#### Time Complexity: O(n/2) + O(n*n/2) ~ O(n²) 
#### Space Complexity: O(1)
