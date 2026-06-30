
#### Authentication -
- server puchega kon ho - db m check krega if that banda exists

##### Cookies and Session -
- coz server each time puchega - kon ho
- cookies (saved in browser) k help s, session create ho skta h
- ek route p cookie set kara, multiple routes p vo cookie available ho jaega (coz browser p store ho jagga and with each nxt req, cookie jata h)

```js
//set cookies -
res.cookie("name","value");

//get cookies -
console.log(req.cookies);
```

#### Authorization -
- server tumhe limited operations karne dega, according to your role (eg. admin,etc)


#### Bcrypt -
- we store encrypted (hashed) pass in db. 
  
1. pass   --encrypt-->   hash
2. hash   --check-->     with og pass


#### JWT -
- 1st browser req -------> ek string server dega with res, to browser
- now browser ---------sends--------->  req   +   string
- jwt is used to create that string.
  
- string = algo + data + sign
- data   ---we put-->  generally email (coz unique)
- this string is saved as cookie in browser
- create string (aka token) --> jwt.sign()
- to extract details from string -->  jwt.verify()