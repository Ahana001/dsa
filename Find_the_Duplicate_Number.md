## Brute Force Approach

```cpp
vector<int> nums = {1,3,4,2,4};
int n = nums.size();

sort(nums.begin(), nums.end());

for(int i=0; i<n - 1; i++){
    if(nums[i] == nums[i+1]){
        cout << "The duplicate number is: " << nums[i];
        break;
    }
}
```
### Time Complexity

`O(nlogn) + O(n)`

### Space Complexity

`O(1)`

----

## Better Force Approach

```cpp
vector<int> nums = {1,3,4,2,2};
int n = nums.size();

vector<int> count(n, 0);

for(int i=0; i<n; i++){
    count[nums[i]]++;
}

for(int i=0; i<=n; i++){
    if(count[i] == 2){
        cout << "The duplicate number is: " << count[i];
        break;
    }
}
```

### Time Complexity

`O(2n)`

### Space Complexity

`O(n)`

---

## Optimal 

```cpp
for(int i=0; i<n; i++){
    if(count[i] == 1){
        cout << "The duplicate number is: " << count[i];
        break;
    }
}
```

### Time Complexity

`O(n)`

### Space Complexity

`O(n)`

## Invalid Approach


### Note

This method is not used because duplicate value can be more than one.

```cpp
vector<int> nums = {1,3,4,2,4};
int n = nums.size();

long long int sum = 0;
long long int expectedSum = 0;

for(int i=0; i<n ; i++){
    sum += nums[i];
    expectedSum += i;
}
```

### Time Complexity

`O(2n)`

### Space Complexity

`O(1)`

---

## Optimal Approach: Floyd's Cycle Detection Algorithm (Tortoise and Hare)

```cpp
vector<int> nums = {1, 3, 4, 2, 3};

int slow = nums[0];
int fast = nums[0];

slow = nums[slow];
fast = nums[nums[fast]];

while(slow != fast){
    slow = nums[slow];       // 3, 2
    fast = nums[nums[fast]]; // 2, 2
}

slow = nums[0];

while(slow != fast){
    slow = nums[slow];
    fast = nums[fast];
}
```
### Time Complexity

`O(n)`

### Space Complexity

`O(1)`
