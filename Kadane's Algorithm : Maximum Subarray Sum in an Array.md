```
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
    // Brute Froce Approach - Time Complexity: O(n^2) Space Complexity: O(1)
    // int minsum = INT_MIN;
    // for(int i=0; i<nums.size(); i++){
    //     int sum = 0;
    //     for(int j=0; j<=i; j++){
    //         sum += nums[j];
    //     }
    //     if(sum > minsum){
    //         minsum = sum;
    //     }
    // }

    // Better Appoach - Time Complexity: O(n)
    int minsum2 = INT_MIN;
    int sum = 0;
    int start = 0;  // Print array
    int ansStart = 0;
    int ansEnd = 0;
    for(int i=0; i<nums.size(); i++){
        if(sum === 0) start = i;  // safe 
        sum += nums[i];
        if(sum > minsum2){ // If sum is negative we already capture it then reset sum so no problem. 
            minsum2 = sum;
            ansStart = start; // safer because if we update start and previous array was our answer then start is miscellaneous - {-2,1,-3,4,-1,2,1,-5,-5,-3,4,1,-2,1};
            ansEnd = i;
        }

        // If we not reset then if we have large subarray in middle of array like [-2,1,-3,4,-1,2,1,-5,4] which has max sum subarray is [4, -1, 2, 1] in above code if we not reset we are not checking for middle sub array we just start from first or last element and go till first/last element but kadan's algo is to reset if it become negative so we can check middle max subarray as well.  

        if (sum < 0) {
            sum = 0; 
            start = i + 1; // If last element then this will be update. 
        }
    }
    return minsum2;
    }
};
```
