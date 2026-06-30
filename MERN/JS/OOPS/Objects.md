In JavaScript, OOP is primarily a layer of syntactic sugar over its native prototype-based architecture.

---
### Create Object -

#### 1. Object Literal
#### 2. Factory function -
	returns a custom(based on inputs) object

#### 3. Constructor function -
	1. convention - capital 1st letter
	2. uses 'new' keyword
		1. creates empty object { }
		2. points 'this' keyword to the created object
		3. initialises values
		4. implicitly returns the object
	3. if 'new' not used -> 'this' points to 'global' object (`window` in browsers)


### Delete a key-val pair -
```js
delete obj.key
// or
delete obj['key']
```


---


### Object constructor -
- every obj have a constructor property that reps the function ( constructor ) used to build that object.
- each object created using object literal syntax uses a default constructor -> `Object()`
- ```js
  let x = {}; // this is easy to use
  // it is same as ->
  let x = new Object(); // js creates object  
  ```

#### Wrapper Object Constructors -
- besides object, there are default constructors for multiple things like ->
- ```js
  let s = "";
  // or
  let s = new String("");
  let val = new Number();
  let flag = new Boolean();
  throw new Error('internal error');
  
  // Pro tip: They work as type converter
  let s = new String(123); // number to string
  ```

#### Functions are Objects -
- they use `Function()` built in constructor to create a function.
- ```js
  // a custom object constructor function
  function circle1 (radius){
	  this.radius = radius;
  }
  const mycircle1 = new circle(5);
  
  // fn created using Function() which does the exact same job as above
  const circle2 = Function('radius',`
  this.radius = radius;
  `);
  const mycircle2 = new circle(6);
  
  
  // now as we know functions are objects,
  // let's disect how js interprets `new circle(6);`
  
  // each function have properties -> call, apply
  
  // `new circle(6);` is same as ->
  circle.call({}, 6);
  
  // and `circle(6)` is same as ->
  circle.call(window, 6);
  ```

----




### Enumerating on Obj -
```js
// 1. for in loop
for(let key in myobj){
// ek ek karke key ati rhegi
}

// 2.
const keys = Object.keys(myobj); // return array of keys
const keys = Object.entries(myobj); // return array of arrays of keys-values
```

#### `in` operator -
```js
// it can be used by array or object
if('mykey' in myobj)
if('mykey' in keys)
```

---





### Copy -
```js
let obj2 = {... obj1}; // nested objects -> copied by ref, direct val -> by val

let obj2 = JSON.parse(JSON.stringify(obj1));
// now this makes a deep copy
//means everything is copied by value, (even the nested objects)
```

### Optional Chaining -
```js
obj?.address?.city;
// if vo field h -> value dedega
// else undefined dedega, (error ni dega**)
```

---
