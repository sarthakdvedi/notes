
to find max subarray -

#### Basic kadane idea -> 
1. bestEnding (till last idx) + cur_value (at i th idx)
2. if cur_value is better alone, then move forward with it only


### Proceed this way -
- collect all possible best (like ---> noDel and oneDel)
- set initial condition for ans, and all bests
- see how to update each best at idx i

update bestEnding (with these two choices on each iteration)


snippet ->

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



examples -
- max multiplication subarray (carry - min and max)
- max sum subarray with one possible deletion (carry - maxSum with oneDelete and noDelete)

in types me -> multiple values types carry karte hue chalo till every idx


- max subarray sum in circular array
-> return max(totalSum - minSum, maxSum);      idea - (pure m se min hatake ---- bachega max)