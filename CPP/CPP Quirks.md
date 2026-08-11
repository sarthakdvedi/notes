
### CPP Quirks -

```cpp
    while(int a = printf("hi")){
        cout << a;
        break;
     }
     

vector<int> f = {1,0};
vector<int> c = {1,0};
cout << (f==c);




int i = 6;  // loop k andar initialise -> chalra h, lol
if(i = 7) cout << i;
```


---



```cpp
// this works due to right to left associativity of `=` operator
 
int x, y, z;
x = y = z = 50; // wht the heeeeeeell
cout << x << y<< z; // output: 50 50 50
```