
### 1. Callbacks -
#### Arrow fn use in callback -

```js
// here, deliver is a callback for createOrder

// 1. pass function reference (As fn.s are pass by ref)
createOrder(deliver);

// or

//2. "Wrapper" Function
createOrder(() => {
// multiple statements like -> console.log("order created");
    deliver(orderId);
});
```
use 2nd when -
1. Jab arguments pass karne ho in callback fn.
2. Jab multiple statements likhne ho
3. Jab callback ke arguments ko modify karna ho
---

### 2. Promises -
