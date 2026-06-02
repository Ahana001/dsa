# Stock Buy and Sell Problem

---

## 1. Brute Force Approach

**Time Complexity:** O(n²)  
**Space Complexity:** O(1)

```cpp
class Solution{
public:
    int stockBuySell(vector<int> arr, int n){

        int profit = 0;

        for(int i = 0; i < arr.size(); i++){ // decide Buy
            for(int j = i + 1; j < arr.size(); j++){ // decide sell must be in future and not same day
                if(arr[j] - arr[i] > profit){
                    profit = arr[j] - arr[i];
                }
            }
        }

        return profit;
    }
};
```

---

## 2. Better Approach (Kadane-like Greedy)

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

```cpp
class Solution{
public:
    int stockBuySell(vector<int> arr, int n){
        // If sell on x day must buy on min day in past for max profit
        int min = 0;
        int profit = 0;

        for(int i = 1; i < n; i++){
            profit = max(profit, arr[i] - arr[min]);

            if(arr[i] < arr[min])
                min = i;
        }

        return profit;
    }
};
```
