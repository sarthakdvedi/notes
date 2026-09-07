
to find max subarray -

it can be solved using sliding window ( but only if all +ve or -ve )
{ as mixed integers destroy decision making ability in sliding window approach (whether to move left or right) }
Without additional constraints (like a target sum or limited subarray length):

- **Max sum with only positives** = Sum of the entire array.
    
- **Min sum with only positives** = Smallest single element in the array.


### Basic kadane idea -> 
1. bestEnding (till last idx) + cur_value (at i th idx)
2. if cur_value is better alone, then move forward with it only


### Proceed this way -
- collect all possible best (like ---> noDel and oneDel)
- set initial condition for ans, and all bests
- see how to update each best at idx i

update bestEnding (with these two choices on each iteration)


```cpp
int maxSubArray(vector<int>& nums) {

	    int n = nums.size();
	    int ans = nums[0];
	    int maxEnding = nums[0];	
	
	    for(int i=1; i < n; i++){
		// maxEnding is a temporary best state only	
	        maxEnding = max(nums[i], maxEnding + nums[i]);
	        // so updaing ans in loop is imp
	        ans = max(ans, maxEnding);
	        
	    }
	    
	    return ans;
 }
```


```cpp
    int maxSubArray(vector<int>& nums) {
        int n=nums.size(), maxSum=INT_MIN, curSum=0;

        for(int i=0;i<n;i++){
            curSum = max(curSum + nums[i], nums[i]);
            maxSum = max(maxSum, curSum);
        }

        return maxSum;
    }
```


---


examples -
- max multiplication subarray (carry - min and max)
- max sum subarray with one possible deletion (carry - maxSum with oneDelete and noDelete)

in types me -> multiple values types carry karte hue chalo till every idx


- max subarray sum in circular array
-> return max(totalSum - minSum, maxSum);      idea - (pure m se min hatake ---- bachega max)