## Brute Force Approach

```cpp
int n = intervals.size();
vector<vector<int>> result;

sort(intervals.begin(), intervals.end());

for(int i=0; i<n; i++){
        int start = intervals[i][0];
        int end = intervals[i][1];

        if(!result.empty() && end <= result.back()[1]){ // check all element if it is already considered in below loop then skip it
            continue;
        }

        for(int j=0; j<n; j++){ // pick one interval go till all intervals and make one interval and push it
            if(intervals[j][0] <= end){
                end = max(end, intervals[j][1]);
                j++;
            }else{
                break;
            }
        }
        result.push_back({start, end});
        
    }

```

### Time Complexity

```text
O(n log n) + O(n²) ~ O(n²) -> If all interval in one range then inner for loop go till end and outter loop again check and return from condition
```

### Space Complexity

```text
O(n)
```
----


## Optimal Approach


```cpp
int n = intervals.size();
vector<vector<int>> result;
sort(intervals.begin(), intervals.end());

for(int i=0; i<n; i++){
    int start = intervals[i][0];
    int end = intervals[i][1];

    int j = i + 1;
    while(j < n && intervals[j][0] <= end){
        end = max(end, intervals[j][1]);
        j++;
    }

    result.push_back({start, end});
    i = j - 1;
}
```

### Time Complexity

```text
O(n log n) + O(n)
```

### Space Complexity

```text
O(n)
```
