## Brute Force Approach

```cpp
int m = nums1.size();
int n = nums2.size();
vector<vector<int>> result(m + n);
int i=0;
int j=0;

while( i < m || j < n){
    if(i<m && nums1[i] < nums2[j]){
        result[k] = nums1[i];
        i++;
        k++;
    }else{
        if(j< n){
            result[k] = nums2[j];
            j++;
            k++;
        }
    }
}

for(int i=0; i<result.size(); i++){
    nums1[i] = result[i];
}

```

**Time Complexity:** `O(2(m + n))` ~ `O(m + n)`
**Space Complexity:** `O(m + n)`

---

## Better Approach

```cpp
int m = nums1.size();
int n = nums2.size();

int i=0;
while( i < m ){
    if( i < m && nums1[i] > nums2[0]){
        swap(nums1[i], nums2[0]);

        int k = 0;
        while(k < n - 1 && nums2[k] > nums2[k+1]){
            swap(nums2[k], nums2[k+1]);
            k++;
        }
    }
    i++;
}

for(int j=0; j<n; j++){
    nums1[m+j] = nums2[j];
}
```

**Time Complexity:** `O(m * n)`
**Space Complexity:** `O(1)`

---

## Optimal Approach (Sorting After Swapping)

```cpp
int m = nums1.size();
int n = nums2.size();
int j=0;
int i =  m - 1;

while( i >=0  && j < n){
    if(nums1[i] > nums2[j]){
        swap(nums1[i], nums2[j]);
        j++;
        i--;
    }else{
        break;
    }
}

sort(nums1.begin(), nums1.end());
sort(nums2.begin(), nums2.end());

for(int i=0; i<nums2.size(); i++){
   nums1[m + i] = nums2[i];
}

```

**Time Complexity:** `O(m log m + n log n + O(min( m,n )`  
**Space Complexity:** `O(1)`

---

## Optimal Approach (Gap Method / Shell Sort Idea)

```cpp
vector<int> nums1 = {-5, -2, 4, 5};
vector<int> nums2 = {-3, 1, 8};

int m = nums1.size();
int n = nums2.size();

int gap = (m + n) / 2 + (m + n) % 2;

while (gap > 0) {
    int i = 0;
    int j = i + gap;

    while (j < m + n) {

        if (i < m && j >= m) {
            if (nums1[i] > nums2[j - m]) {
                swap(nums1[i], nums2[j - m]);
            }
        }
        else if (i >= m) {
            if (nums2[i - m] > nums2[j - m]) {
                swap(nums2[i - m], nums2[j - m]);
            }
        }
        else {
            if (nums1[i] > nums1[j]) {
                swap(nums1[i], nums1[j]);
            }
        }

        i++;
        j++;
    }

    if (gap == 1) {
        break;
    }

    gap = gap / 2 + gap % 2;
}
```

**Time Complexity:** `O((m + n) log(m + n))`  
**Space Complexity:** `O(1)`
