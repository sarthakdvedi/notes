
## Destructure -

### Array Des. -
```js

  const numbers = [1, 2, 3, 4];
  const [first, ...others] = numbers;

```

### Obj Des. -

- ```js
	const user = { name: "Alice", age: 25, city: "Paris" };
	const { name, ...rest } = user;
  // ^ rest operator (...) se start wala
  
console.log(name);
-> 'Alice'
console.log(rest);
-> {age: 25, city: 'Paris'}
  ```


---


