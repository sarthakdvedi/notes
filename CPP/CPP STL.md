
### Comparator -
```cpp
1. desired Ouput soch.
2. fir usme consecutive first nd second element uthale as a and b.
3. ab unme kya relation h, exactly vo as true return karde
   
   // this is for descending -->
        sort(nums.begin(),nums.end(),[](auto& a,auto& b){

            return a > b;

        });
        
```

---



## map v/s unordered_map -

| Feature            | `map`                               | `unordered_map`          |
| ------------------ | ----------------------------------- | ------------------------ |
| **Data Structure** | Binary Search Tree (Red-Black Tree) | Hash Table               |
| **Sorting**        | Keys are automatically sorted       | Keys are not sorted      |
| **Lookup Time**    | \(O(\log n)\) guaranteed            | O(1) average (very fast) |
| **Memory Usage**   | Lower per element                   | Higher per element       |

---



## set v/s multiset -

### Same -

| **Data Structure**  | Binary Search Tree (Red-Black Tree)     |
| ------------------- | --------------------------------------- |
| **Ordering**        | Elements are automatically sorted       |
| **Time Complexity** | \(O(\log n)\) insertion/deletion/lookup |

### Diff -

| Feature        | `set`                              | `multiset`                          |
| -------------- | ---------------------------------- | ----------------------------------- |
| **Duplicates** | Not allowed (unique elements only) | Allowed (stores duplicate elements) |


---

