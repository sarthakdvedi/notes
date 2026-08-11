
## Only Difference

1. C struct doesn't have methods like cpp
2. structure --> default (public), class --> default (private)




## INIT

int arr[5] = {1};

// 1 gets at only 0th idx, and rest all init as 0 by default inside int main 


## STL

### Vectors
- size vs capacity ---> capacity doubles with each insertion (push_back) {except 1st time }
- push_back --> wants perfect obj,  (faster) emplace_back --> convert in required obj
- front, back -- O(1)
- erase(start_it, end_it), insert(it,val) -- O(n)
- clear -- clears space (capacity remains), empty

#### Vector Iterators -
- vec.begin(), vec.end()
- vec.rbegin(), vec.rend() --- just works rev. with it++
- vector<int>: : iterator it;
	
	for( it = vec.begin(); it != vec.end(); it++ ){
	cout << *(it) ;
	}
	
	simply --
	for(auto it = "){ " }


list - implemented as doubly LL (so front and back insertion and deletion)]
deque - implemented as double ended queue " " " "

priority queue - implemented as heap tree (just # include queue *works*)```
	priority_queue<int>q; //max - heap
	priority_queue<int, vector<int>, greater<int>>q; //min - heap
	
	q.push
	
	q.top(), q.pop() -- sorted o/p

map - 
map<int,int>mpp = {{1,2},{2,3}}; 
mpp.insert({3,4});
or
mpp.emplace(3,4);

inert, erase, count -- O(log n) (coz sorted -- as self balancing tree)
but O(1), O(n) - worst in  unordered_map

ordered map search -> log n
unordered_map search -> 1, but n at worst case

erase() erases all occurences of a key in multimap<int,int>m;




set --- very similar to map (coz sorted, unique values)   ---- also, multiset, unordered_set
uses tree ds
=>
inert, erase, count -- O(log n) (coz sorted -- as self balancing tree)

use in set ->
auto it = s.upper_bound(x);


### Algos -
1. sort(vec, vec+n);   or   sort( vec.begin(), vec.end() );
   sort(vec, vec+n, greater<int>() )  // desc. order
   
   
 custom comparator --
   vector<pair<int,int>> vec = {{1,2}, {2,3}} ;
   
   // to sort acc. to second val
   
   bool comp( pair<int,int> p1, pair<int,int> p2 ){
	   if(p1.second < p2.second) return true ; 
	   else return false;
   }
   
   // to sort acc. to second val and if same then first val
    
   bool comp( pair<int,int> p1, pair<int,int> p2 ){
	   if( p1.second < p2.second ) return true ; 
	   else if( p1.second > p2.second ) return false;
	   
	   if( p1.first < p2.first ) return true;
	   else return false;
   }
   
   
2. reverse ( vec.begin(), vec.end() );
3. next_permutation( vec.begin(), vec.end() );
4. swap, min, max
5. max/ min_element( vec.begin(), vec.end() );
6. binary_search( vec.begin(), vec.end(), target );
7. __builtin_popcount ( );      or      __builtin_popcountl ( );      or       __builtin_popcountll ( ); // dep on data type (int, long, long long) -- resp.
8.         auto it = upper_bound(vec.begin(), vec.end(), x);
            if(it == vec.end()) continue;


