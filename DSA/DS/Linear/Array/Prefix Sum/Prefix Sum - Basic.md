
- prefix[i] = prefix[i-1] + arr[i-1];
where, prefix[i] -> sum of all elements till i-1th idx or ith idx (acc. to need)

- suffix[i] = suffix[i+1] + arr[i+1];
#### IMPORTANT EQ - 
- pref[i] + arr[i] + suff[i] = totalSum; 


soch ->
- green se ek mathematical eq bana
- same eq ---> total ki bana k dekh      and     red ki bana
- something must be common (jispe map chalega)



-------------------

Q - [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) 
Edge TT (be careful and mindful about it) -
nums = {1} , k = 0

#### NOTE -
- update map at super last.
- first get ans updated.

------------------------------


Q - [Subarray Sums Divisible by K - LeetCode](https://leetcode.com/problems/subarray-sums-divisible-by-k/description/) 

#### THINK -
- red part + green part = sum (total)
- green = sum(total)  - red
- pehle dekh (breakdown kr) ---> sum (total) kya h,  and  green kya h
- fir red kya hona chahiye  ---> y define kar
- and uske according hi map work karega

trick -
- **hashmap me jisko dhundna h ----------- usko key banado
- -ve remainder aye to  ---->  + k     karo usme       (trick)
- mean --->   -x % y = - (x % y) + y
- coz  ----> -x % y    ka    accurate ans nahi deta cpp
- cpp deta h ---->  -x % y = -(x % y)          (so ---> + k     karo usme)

------------------------------------


Q - [Contiguous Array - LeetCode](https://leetcode.com/problems/contiguous-array/) 

soch ->
- green se eq ek mathematical eq bana
- same eq ---> total ki bana k dekh      and     red ki bana
- something must be common (jispe map chalega)

##### SUPER IMP ----->
- coz max len chiye ----> means longest green part  ---> means shortest red part
- so first red part store kr only




nice prefix sum Q.
think ---> in state of x, a, b (what is sum diff of zeroes and ones)
#### IMP NOTE -
It is a classic "trap" in LeetCode-style problems. At first glance, a "contiguous subarray" with a specific property (equal number of 0s and 1s) screams **Sliding Window**, but that technique fails here for a very specific reason.

##### Why Sliding Window Doesn't Work

The Sliding Window technique relies on **monotonicity**. For a window to expand or shrink logically, there must be a clear rule:

- "If I add this element, the sum/count only goes **up**."
    
- "If I remove this element, the sum/count only goes **down**."
    

In Problem 525, you are looking for an equal count of 0s and 1s. Let's say you treat 0 as -1 and 1 as +1. You want a subarray that sums to $0$.

### The Exception: What if it was only 0s?

If the problem was "Find subarrays with more than five 0s" (and there were no 1s to subtract from the count), then **Sliding Window would work perfectly**. Adding an element would only ever increase the count of 0s, and removing one would only ever decrease it.

The moment you introduce 1s as a "negative" force, you lose that linear predictability.


**The Rule of Thumb:** > * If adding an element **always** increases the total (or keeps it same): **Sliding Window** is possible.

- If adding an element can **decrease** the total (like the -1s in the "more 0s" problem): **Prefix Sum + HashMap/BIT** is mandatory.


---------------------


Q - [Longest Span in two Binary Arrays | Practice | GeeksforGeeks](https://www.geeksforgeeks.org/problems/longest-span-with-same-sum-in-two-binary-arrays5142/1)
y mene completely khud s kara hai
two diff eq banegi like prefix [x=a+b] (coz 2 arrays hai)  ----->  dono ko merge karke 1 single eq m laaa




