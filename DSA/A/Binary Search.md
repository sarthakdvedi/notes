

### Pattern -
- minimise the maximum
- max the min


-------------------


- Upper Bound -     smallest / 1st el > x                           nums= { 2,2,3 }, target = 2
- Lower Bound -     smallest / 1st el >= x                         LB = idx( 0 ),        UB = idx( 2 )

- Ceil -      smallest / 1st el >= x
- Floor -    largest / last el <= x

- *NOTE* -
1. Ceil == Lower Bound
2. ceil == floor ( if exact target is present )



---

### Tips: When to use which?

#### Use **Iterative** when:

1. **Finding "Boundaries":** If you are looking for Floor, Ceiling, First Occurrence, or Last Occurrence. The `ans = mid` pattern is much cleaner iteratively.
    
2. **Memory is a Concern:** In competitive programming or embedded systems, iterative is safer because it avoids the overhead of the function call stack.
    
3. **Simple Ranges:** When the search space is a simple linear array.
    

#### Use **Recursive** when:

1. **The Structure is Recursive:** If you are searching in a **Binary Search Tree (BST)** or a **Quadtree**. Since the data structure itself is recursive, the code feels more natural.
    
2. **Divide and Conquer:** If you aren't just searching, but also performing operations on the way back up the stack (like updating heights in an AVL tree).
    
3. **Interviews (Sometimes):** Some interviewers like to see recursion to test your understanding of the stack, but they will almost always accept (and often prefer) the iterative version for a standard array binary search.


for ub, lb, floor, ceil -> use iterative (as it is clear and simple --> saves best candidate so far)

----------------


### POINTERS -
- rotated sorted is always half sorted.



------------------------

### BS on Answers -

When half part satisfies condition and is a valid answer 
and other half does not satisfies the condition.

BS special case: [LC Study Guide: Binary Search on Answer](https://leetcode.com/discuss/study-guide/3444552/binary-search-on-answer-template-generic-template)  
Must do to master the binary search on answer:

- [https://leetcode.com/problems/minimum-time-to-repair-cars/](https://leetcode.com/problems/minimum-time-to-repair-cars/) <-- this one is gold!!!
- [https://leetcode.com/problems/minimum-speed-to-arrive-on-time/](https://leetcode.com/problems/minimum-speed-to-arrive-on-time/)
- [https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)
- [https://leetcode.com/problems/koko-eating-bananas/](https://leetcode.com/problems/koko-eating-bananas/)
- [https://leetcode.com/problems/maximum-candies-allocated-to-k-children/](https://leetcode.com/problems/maximum-candies-allocated-to-k-children/)
- [https://leetcode.com/problems/magnetic-force-between-two-balls/](https://leetcode.com/problems/magnetic-force-between-two-balls/)
- [https://leetcode.com/problems/sell-diminishing-valued-colored-balls/](https://leetcode.com/problems/sell-diminishing-valued-colored-balls/)
- [https://leetcode.com/problems/minimum-limit-of-balls-in-a-bag/](https://leetcode.com/problems/minimum-limit-of-balls-in-a-bag/)
- [https://leetcode.com/problems/divide-chocolate/](https://leetcode.com/problems/divide-chocolate/) <-- this one is gold!!! (hard)






-----------------

### Good problem (revise krlo bhaiya) -
- [3932. Count K-th Roots in a Range](https://leetcode.com/problems/count-k-th-roots-in-a-range/) 
- [1539. Kth Missing Positive Number](https://leetcode.com/problems/kth-missing-positive-number/) (bhai kya q h ye,   ---->  SUPER HOT Q)