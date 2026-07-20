# Majority Element II (Elements Appearing More Than ⌊n/3⌋ Times)

## Method 1: Brute Force

```cpp
for (int i = 0; i < nums.size(); i++) {
    int count = 1;
    if (ans.size() == 0 || ans[0] != nums[i]) {
        for (int j = i + 1; j < nums.size(); j++) {
            if (nums[i] == nums[j]) {
                count++;
            }
        }
        if (count > (int)(nums.size() / 3))
            ans.push_back(nums[i]);
    }
    if (ans.size() == 2)
        break;
}
```

**Time Complexity:** `O(n²)`  
**Space Complexity:** `O(1)`

---

## Method 2: Brute Force V2 (Sorting)

```cpp
sort(nums.begin(), nums.end()); // O(nlogn)

int count = 1;
int element = nums[0];

// O(n)
for (int i = 1; i < nums.size(); i++) {
    if (element != nums[i]) {
        if (count > (int)(nums.size() / 3)) {
            ans.push_back(element);
        }
        count = 1;
        element = nums[i];
    } else {
        count++;
    }
}

if (count > (int)(nums.size() / 3)) {
    ans.push_back(element);
}
```

**Time Complexity:** `O(n log n)`  
**Space Complexity:** `O(1)` *(ignoring sorting implementation space)*

---

## Method 3: Better Approach (Hash Map)

```cpp
unordered_map<int, int> map;

for (int i = 0; i < nums.size(); i++) {
    map[nums[i]]++;
}

for (auto it : map) {
    if (it.second > (int)(nums.size() / 3)) {
        ans.push_back(it.first);
    }
}
```

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(n)`

---

## Method 4: Better Approach V2 (Single Pass Hash Map)

```cpp
unordered_map<int, int> map;

for (int i = 0; i < nums.size(); i++) {
    map[nums[i]]++;

    if (map[nums[i]] > (int)(nums.size() / 3) &&
        (ans.size() == 0 || ans[0] != nums[i])) {
        ans.push_back(nums[i]);
    }

    if (ans.size() == 2) {
        break;
    }
}
```

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(n)`

---

## Method 5: Optimal Approach (Boyer-Moore Voting Algorithm)

```cpp
int count1 = 0;
int count2 = 0;
int element1 = INT_MIN;
int element2 = INT_MIN;

for (int i = 0; i < nums.size(); i++) {
    if (count1 == 0 && element2 != nums[i]) {
        element1 = nums[i];
        count1 = 1;
    } else if (count2 == 0 && element1 != nums[i]) {
        element2 = nums[i];
        count2 = 1;
    } else if (element1 == nums[i]) {
        count1++;
    } else if (element2 == nums[i]) {
        count2++;
    } else {
        count1--;
        count2--;
    }
}

count1 = 0;
count2 = 0;

for (int i = 0; i < nums.size(); i++) {
    if (element1 == nums[i]) {
        count1++;
    } else if (element2 == nums[i]) {
        count2++;
    }
}

if (count1 > (int)(nums.size() / 3)) {
    ans.push_back(element1);
}

if (count2 > (int)(nums.size() / 3)) {
    ans.push_back(element2);
}
```

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(1)`
