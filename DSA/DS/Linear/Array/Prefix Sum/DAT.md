
- [3356. Zero Array Transformation II](https://leetcode.com/problems/zero-array-transformation-ii/) (kamal ka q ----> super learning  ---> super duper try kar)
- [2381. Shifting Letters II](https://leetcode.com/problems/shifting-letters-ii/) 


### Difference array technique -> (4g kheti technologia)
```cpp
        for(auto& v : shifts){

            int i = v[0], j=v[1];

            int x = v[2]==1 ? 1 : -1;

  

            dat[i] += x;

            if(j+1 < n) dat[j+1] -= x;

        }

  

        for(int i=1; i<n; i++){

            dat[i] += dat[i-1];

        }
```