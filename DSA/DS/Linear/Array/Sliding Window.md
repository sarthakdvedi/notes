---

---

#### IMP NOTE -
sliding window is only application if  --------> jab ek hi parameter h monotonically inc or dec.

#### Think in these STEPS   (approach) -
1. if Q is of fixed or dynamic window.  (SUPER IMP ...)
2. if dynamic --->  follows which structure (min window or max window)
3. 


- variable window ->

```cpp
int longestKSubstr(string &s, int k) {
        int n = s.size();
        int i = 0;
        int j = 0;
        int length = -1;
        int charCount = 0;
        
        int freq[26] = {0};
        
        while(j < n){
             // 1.) take the new idx into window
            if(freq[s[j]-'a'] == 0) charCount++;
            freq[s[j]-'a']++;
             
             // 3.) before, correct the window (acc. to condition)
            // use 'if' instead of 'while' for optimal
            while(charCount > k){
                
                freq[s[i]-'a']--;
                if(freq[s[i]-'a'] == 0) charCount--;
                
                i++;
            }
             // 2.) update the answer variable
            if(charCount == k) length = max(length, j-i+1);
            // if subarray is required -> store startIdx and windowSize
            j++;
        }
        
        return length;
    }

```


### Two Structure (super imp***) -
1. Max window (sum <= k)
   
   include j wala
   while(galat h) // trim
   sahi h -> //update  len = max(len, j-i+1);

2. Min window (sum >= k)
   
   include j wala
   while(sahi h) // trim + update  len = max(len, j-i+1);
   galat h -> // include j++






### Revision important questions -

1. [Longest Repeating Character Replacement - LeetCode](https://leetcode.com/problems/longest-repeating-character-replacement/description/) (simply kar)
2. [Binary Subarrays With Sum - LeetCode](https://leetcode.com/problems/binary-subarrays-with-sum/description/) (ingenius)
3. https://leetcode.com/problems/minimum-subarray-length-with-distinct-sum-at-least-k/ ( q reframe (ese padh) -> ek subarray m distinct element ka sum, not distinct el. ki subarray !!! )
4. minimum window substring (super imp)


#### Nice Fixed window problem -
1. [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/)  --similar-- [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/) 
2. 