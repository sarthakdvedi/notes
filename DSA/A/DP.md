
#### Types-
- Recursive (top down) --->  from top to base case
- Tabulation (bottom up) ----> from base to top

#### Recursion Setup -
1. express strings in terms of idxs
2. explore all paths / possibilities
3. return req (min of all)
4. BC (think of smallest valid input)

--------------------------


1. tabulation m loop karu 1->n tak (as 0 p base case hota h generally, so vo lene ki need ni h)

	1. input variable pata kro
	2. rec chalao input small karke
	3. BC -> for min/smallest value of each variable
	4. discover all stuff


--------------------------

### Memoise 2d -ve idx -

1. use -> simple vector of vector                  { shift idx (so that start from 0)  }
2. use ->   vector<map<int,int>>dp(n);
3. use ->   map<string,int>dp;        gen string ->   "a_b"

   
   #### Rule of thumb:

- **Know the range?** → Shift & use 2D vector. Fastest, cache-friendly.
- **Sparse states / range too large?** → `vector<map<int,int>>` (better than string map).
- **Unknown/complex multi-param states?** → `map<string,int>` (last resort, slowest).


-----------------------------




#### Time complexity -
- total states * work in each     (eg. ----> in 2d dp Q ----->  (n * 4 states ) * 3)



------------------

#### GOOD Revision Problems -

##### Grid -
1. [1594. Maximum Non Negative Product in a Matrix](https://leetcode.com/problems/maximum-non-negative-product-in-a-matrix/)
2. 

##### LIS -
Jaha p chain, linked, sequence m, ek pattern m cheeze chal ri ho ------->    waha LIS laga
eg - longest arithmetic subs, largest divisible subset, longest string chain
1. [1027. Longest Arithmetic Subsequence](https://leetcode.com/problems/longest-arithmetic-subsequence/)
2. [1626. Best Team With No Conflicts](https://leetcode.com/problems/best-team-with-no-conflicts/) (khud se kia, ---> max of all valid -- >add up)

--------------

#### Top Down vs Bottom up -
- in top down   ----->   we start and discrete answer is stored in each call  (which only adds up on hitting correct base case)
- in bottom up   ----->   we add up all from base case   (which sometimes leads to overflow)
- eg ---> see rec and tabulation solution for  (https://leetcode.com/problems/coin-change-ii/description/)
- in tabulation, we have handled overflow



----------------
#### Tips -
- linear recursion   ----->   NO dp (or no memoization)

- #### IF bottom up OVERFLOWS -
  ```cpp
// use long long for dp table       +    typecast while storing   ---->

                if(s[i-1]==t[j-1])
                dp[i][j] = (int)(dp[i-1][j-1] + dp[i-1][j]);

                else
                dp[i][j] = dp[i-1][j];
  ```




#### Recursion  ->  Tabulation
recursion ka   "return"      ----->       loop (tabulation) m   "continue"   hota h

---



### Digit DP -
- [3753. Total Waviness of Numbers in Range II](https://leetcode.com/problems/total-waviness-of-numbers-in-range-ii/) 