
#### What -

- CBT
- max/ min element O( 1 )

-------------------------------------

#### Heap v/s Sorted array -

Heap -> insertion/ deletion  ----> log n

----------------------------

#### Implementation -

- Priority queue implements heap internally
- use .top  (not .front,    like in queue)

```cpp

priority_queue<int>q; //max - heap

priority_queue<int, vector<int>, greater<int>>q; //min - heap
```

--------------------------

#### Q Pattern (keyword) -      O(n log k)

- k / largest    ------>   min heap
- k / smallest  ------>   max heap
- n log n        ---to--->      n log k

##### Top k largest is ->
- Largest group of 'k-size' me ----> min value
##### Top k smallest is ->
- Smallest group of 'k-size' me ----> max value

#### Intuition -
largest k --->  bade elements ko aane do(in k-grp) (minimum ko hatate raho)  -> so use min-heap
smallest k  -->  ulta "


```cpp
    int findKthLargest(vector<int>& nums, int k) {
        int n = nums.size();
        priority_queue<int,vector<int>,greater<int>> pq;
        
        for(int i=0; i < n; i++){  // note -> pushing first k el fully is important

            if(pq.size() < k || pq.top() < nums[i])
                pq.push(nums[i]);

            if(pq.size() > k) pq.pop();
        }

        return pq.top();
    }
```


-----------------------

#### Custom Comparator -

```cpp
// Common declaration
priority_queue<pair<int,int>, vector<pair<int,int>>, cmp> pq;

// Min heap on first, Min on second
struct cmp {

       bool operator()(pair<int,int>& a, pair<int,int>& b) {

           if(a.first == b.first)

               return a.second > b.second;   

           return a.first > b.first;        
       }
   };

// Min heap on first, Max on second
struct cmp {

       bool operator()(pair<int,int>& a, pair<int,int>& b) {

           if(a.first == b.first)

               return a.second < b.second;   

           return a.first > b.first;        
       }
};

// Max heap on first, Min on second
struct cmp {

       bool operator()(pair<int,int>& a, pair<int,int>& b) {

           if(a.first == b.first)

               return a.second > b.second;   

           return a.first < b.first;        
       }
   };

// Max heap on first, Max on second
struct cmp {

       bool operator()(pair<int,int>& a, pair<int,int>& b) {

           if(a.first == b.first)

               return a.second < b.second;   

           return a.first < b.first;       
       }
};
```

-------------------

#### Trick -
```cpp
typedef pair<int,vector<int>> piv;   // simply use piv

priority_queue<piv, vector<piv>, greater<piv>> pq;
```




#### Heap and set equivalence (can use set as heap sometimes)

```cpp

//can do -
st.insert(sum);

if(st.size() > 3)
    st.erase(st.begin());


// optimised -
if(st.size() < 3)
    st.insert(sum);

else if(*st.begin() < sum){
    st.erase(st.begin());
    st.insert(sum);
}
```


------------------
#### Nice Q -
1. implementation based [3885. Design Event Manager](https://leetcode.com/problems/design-event-manager/) (lazy del idea, storing -ve to sort rev)