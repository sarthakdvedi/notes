
#### Collision type idea (like TOC Machine) -
1. Like Valid Parenthesis
2. [2751. Robot Collisions](https://leetcode.com/problems/robot-collisions/) 
3. [Remove All Adjacent Duplicates in String II - LeetCode](https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string-ii/description/) 
4. 

---------------------------------


#### Monotonic stack thinking -
1. kya chahiye finally (greatest/ largest)
   
2.  ** pop el p focus (nikal greatest/ smallest) ***********  (if greater el ----> pse/nse dekh,  
	else if smaller el  ---->  pge/ nge dekh)
	
3. stack k andar el. p focus (esa koi pattern nhi dekha filhal)





- Some applications of monotone (increase/decrease) stack in leetcode: 
    [Next Greater Element II](https://leetcode.com/problems/Next-Greater-Element-II/description/) (a very basic one)  
    [Largest Rectangle in Histogram](https://leetcode.com/problems/Largest-Rectangle-in-Histogram/description/)(almost the same as this problem)  
    [Maximal Rectangle](https://leetcode.com/problems/Maximal-Rectangle/description/)(please do this problem after you solve the above one)  
    [Trapping Rain Water](https://leetcode.com/problems/Trapping-Rain-Water/description/) (challenge)  
    [Remove Duplicate Letters](https://leetcode.com/problems/remove-duplicate-letters/description/)(challenge)  
    [Remove K Digits](https://leetcode.com/problems/remove-k-digits/description/)  
    [Create Maximum Number](https://leetcode.com/problems/create-maximum-number/description/)  
    [132 Pattern](https://leetcode.com/problems/132-pattern/description/)(challenge, instead of focusing on the elements in the stack, this problem focuses on the elements poped from the monotone stack)  
    [sliding window maximum](https://leetcode.com/problems/sliding-window-maximum/description/)(challenge, monotone **queue**)  
    [Max Chunks To Make Sorted II](https://leetcode.com/problems/Max-Chunks-To-Make-Sorted-II/description/)


## Monotonic (top to bottom) Stack (nge/pge +  nse/pse)

1. [Online Stock Span - LeetCode](https://leetcode.com/problems/online-stock-span/description/) (pop p dhyan)
2. [Largest Rectangle in Histogram - LeetCode](https://leetcode.com/problems/largest-rectangle-in-histogram/description/) (optimest approach bad m pdunga)
3. [Sum of Subarray Minimums - LeetCode](https://leetcode.com/problems/sum-of-subarray-minimums/description/) (think -> each el. kitne subarrays me min h)
4. [Sum of Subarray Ranges - LeetCode](https://leetcode.com/problems/sum-of-subarray-ranges/description/)
5. [Number of Visible People in a Queue - LeetCode](https://leetcode.com/problems/number-of-visible-people-in-a-queue/description/) (observe karo pattern)
6. [Remove K Digits](https://leetcode.com/problems/remove-k-digits/) (starting k greatest chahiye/ soch -> greatest kab pop honge (store krlenge tab))
   
```cpp
		vector<int>nge(nums.size(),-1);
        
        for(int i = n-1; i >= 0; i--){
            
            while(!s.empty() && s.top() <= nums[i]) s.pop();
            
            if(!s.empty()) nge[i] = s.top();
            
            s.push(nums[i]);
        }
```

2. [Trapping Rain Water - LeetCode](https://leetcode.com/problems/trapping-rain-water/)
   prefix max and suffix max concept **








saved -
[Sum of Total Strength of Wizards - LeetCode](https://leetcode.com/problems/sum-of-total-strength-of-wizards/description/)
[Find Building Where Alice and Bob Can Meet - LeetCode](https://leetcode.com/problems/find-building-where-alice-and-bob-can-meet/description/)



#### Recursion x stack -
i thought of something. anything solved with recursion can be solved iteratively with stack. is it correct

**Yes, you are 100% correct!** That is a brilliant realization to hit upon as a fresher.

In computer science, this is a fundamental law: **Any problem that can be solved using recursion can also be solved iteratively using an explicit stack.** In fact, it goes both ways—they are completely interchangeable in terms of what problems they can solve. Here is exactly why your thought is spot-on, explained simply.