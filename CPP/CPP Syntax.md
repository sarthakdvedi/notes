



```cpp
using ll = long long; // prefer this one (modern)
typedef long long ll;         // both does the same
```








* hashmap me jisko dhundna h ----------- usko key banado
* typedef pair<int, pair<int,int>> ppi;          ----> use ppi shortly


```cpp
// direct use in map ->
for (auto &[s, freq] : mpp) {
    freq++; // increments the value in the map
}
```

- don't erase while for of - iterating over map
  (only erase  -if-> iterating with raw iterators)

- memset(dp,-1,n+1);
- ```cpp

// coz
int ans = find(grid,m,n,0,0) % 1e9+7;
//is treated as -
 (find(grid,m,n,0,0) % 1e9) + 7
 
 //so ->
 long long MOD = 1000000007;  
long long ans = find(grid,m,n,0,0) % MOD;


-----------------------------------*********************
1e9 --> double
1000000009 --> int

  ```

- `1e9` is a **double literal**, so `1e9+7` is also double.  
But `%` only works with integers → error.


- modulo should be applied on the same type to avoid overflow or implicit conversions.

- int mini = min({a,b,c,d});  // multi min

- compare pair techniques -
```cpp
auto [first,second] = it;   // deconstruct pair
if(it == make_pair(a,b)); // compare pair directly
```


- subset == subsequence,    <-----is different than----->    subarray  ==  substring


- SORT - custom comparator
- ```cpp
          sort(words.begin(),words.end(), // pass lambda exression (simply)

        [](const string& a, const string& b){
            return a.size() < b.size();
        });
  ```



- vectors ans map are directly comparable ---like--->  (vec1 == vec2)




- ### How to make it $O(1)$

If you only need to read the data or modify the original vector in place, use a **reference**:

```cpp
// O(1) - No copying happens, 'vec' is just an alias for the vector inside the map
auto& vec = mpp[revNum].second; 
```




- if pair is key ---->  map works   &   unordered_map doesn't
- !mpp.contains(key)        ==            !mpp.count(key)       (both gives same result)



#### element presence in vector -
```cpp
        auto v = mpp[{me,dir}];
        if(ranges :: contains(v, num)) return true;
```



#### Resize -
```cpp
vector<bool> isPrime;
isPrime.resize(maxEl+1, false);
```


---


### Tuple -
```cpp
using ppi = tuple<int, int, int>; 
ppi node = {5, 2, 4};
// Access elements by 0-based index
int effort = get<0>(node);
int row = get<1>(node);
int col = get<2>(node); 

// Modify elements directly
get<0>(node) = 10;
auto [effort, r, c] = pq.top();
```