


### OVERFLOW maths-
INT_MAX = 2 * 10^10
Long Long range -> 9 * 10^18

----

### Sieve of prime -  **O(n . log log n)**
```cpp
    vector<bool>temp(n+1,true);
    temp[0] = false;
    temp[1] = false;

    for(int i=2; i*i<=n; i++){

        if(temp[i]){
	        for(int j=i*i; j<=n; j+=i){
	            temp[j] = false;
	        }
	    }
    }
```




------------------

### Modular movement -
#### 1. `int diff = abs(target - val);` (along linear region)

This calculates the **straight-line (linear) distance** between your current remainder (`val`) and where you want to go (`target`). This is the cost of walking directly from one to the other without wrapping around the edges.

#### 2. `k - diff` (around rounded region)

This calculates the **wrapped (circular) distance**. If you went the opposite direction around the clock, this is how many steps it would take.




### Summary Checklist for Future Problems

Whenever a problem asks you to minimize operations and features:

1. Changing values by $\pm 1$.
    
2. Evaluating those values using a **modulo  condition.
    

...your brain should immediately think: **"This is a circular track of size $k$."** The shortest distance between two points on a track can go either clockwise or counter-clockwise!


------------------------


## Ceil / floor -

- Ceil (a / b)   =   (a + b - 1) / b
- or ->    ceil( (double)a / (double)b  )            (typecast to double, then divide)
- for floor  ->  typecast to (int)


------------------
### Digits -
- sum of all digits in a number  =   n - 9 * ((n / 10) + (n / 100) + (n / 1000) + (n / 10000))
- number of digits in n  ==>  (int)log10(abs(n)) + 1;          (it uses log base 10)

-------------

## Modular Arithmetic -

- pi = acos(-1.0);   (most accurate pi)
- 
* -x % y = - (x % y) + y     ------->>  CPP = -(x%y) deta h,   so  (+ y ) khud s kar


###### FLT -
-  (a / b) % prime_no      -----> use math technique (fermat little theorem) else wrong answer
- (a/b) % M = (a mod M  *  ( b^(M-2) mod M ))  mod  M
- basically ->  (a  *  b^(M-2) )   %  M
- b-> prime     &     b not divisible by M
- eg - [2906. Construct Product Matrix](https://leetcode.com/problems/construct-product-matrix/)  we did pref and suf -->coz  (a *   b) % MOD is fine.  

-----

## Combination -

The sum of combinations of \(n\) elements chosen an odd / even number at a time is ==exactly== **\(2^{n-1}\)**. [[1](https://math.stackexchange.com/questions/1602518/summation-of-even-combinations)]

- **Sum of Even Combinations:**  
    \({n \choose 0}+{n \choose 2}+{n \choose 4}+\dots =2^{n-1}\)
- **Sum of Odd Combinations:**  
    \({n \choose 1}+{n \choose 3}+{n \choose 5}+\dots =2^{n-1}\)

----

## Triangle Prop-
If given -> 3 sides,     to find ->  all angles
use Law of cosine:   cos x = ( a^2 + b^2 - c^2 ) / 2*a*b 
find x by cos inverse function  ---> acos (  ^"  )               * (180 / pi)   {for radians -> degrees}

if given -> 1 side, 2 angle,       to find -> other sides
use Law of sines

-----

#### Nice / stupid Questions -
1. [168. Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title/) 



------------------

## Circular array -
A **circular array** means the end of the array connects to the beginning of the array. Formally, the next element of `nums[i]` is `nums[(i + 1) % n]` and the previous element of `nums[i]` is `nums[(i - 1 + n) % n]`.



-------------------------

### Revision-
- [3102. Minimize Manhattan Distances](https://leetcode.com/problems/minimize-manhattan-distances/) 

---

## Basic formula -
```cpp

// 1. sum of n digits 
   int sum = n(n+1) / 2
   
// 2. sum from x to x+y
	int sum = (n / 2) * (start + end);
```