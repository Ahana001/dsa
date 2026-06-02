# Maximum Subarray Sum Solutions

---

## 1. Brute Force Approach

**Time Complexity:** O(n²)  
**Space Complexity:** O(1)

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int minsum = INT_MIN;
        for(int i=0; i<nums.size(); i++){
            int sum = 0;
            for(int j=0; j<=i; j++){
                sum += nums[j];
            }
            if(sum > minsum){
                minsum = sum;
            }
        }

        return minsum;
    }
};
```

---

## 2. Kadane’s Algorithm (Better Approach)

**Time Complexity:** O(n)  
**Space Complexity:** O(1)

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int minsum2 = INT_MIN;
        int sum = 0;
        int start = 0;  // Print array
        int ansStart = 0;
        int ansEnd = 0;

        for(int i=0; i<nums.size(); i++){
            if(sum == 0) start = i; 

            sum += nums[i];

            // If sum is negative we already capture it then reset sum so no problem. 
            if(sum > minsum2){ 
                minsum2 = sum;
                // Copied into ansStart is Safer: if we update `start` while the previous subarray was the current max,
                // `start` could point to a different, irrelevant position. 
                // Example: {-2,1,-3,4,-1,2,1,-5,-5,-3,4,1,-2,1}
                ansStart = start; 
                ansEnd = i;
            }

            // If we do not reset the sum when it becomes negative, we may miss the correct maximum subarray,
            // especially for cases where the best subarray lies in the middle of the array.
            // For example: [-2,1,-3,4,-1,2,1,-5,-5,-3,4,1,-2,1] has the maximum subarray [4, -1, 2, 1].
            // Without resetting, we keep carrying forward negative sums, which reduces the chance of starting
            // a new subarray from a better position. Kadane’s Algorithm fixes this by resetting the sum to 0
            // whenever it becomes negative, allowing us to properly evaluate all possible subarrays..  
            if (sum < 0) {
                sum = 0; 
                start = i + 1; // If last element then this will be update. 
            }
        }

        return minsum2;
    }
};
```

---

## 3. Notes

- Brute Force checks every possible subarray.
- Kadane’s Algorithm optimizes by resetting negative sums.
- Your original comments are preserved exactly as written.
