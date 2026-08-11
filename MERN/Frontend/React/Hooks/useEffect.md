
basically, api call component k render p karni ho,
to directly component function m na karke
component function k andar -> useEffect k andar hi karna h


### Problem -
- Mujhe dashboard p contact chahiye
- m `Dashboard` component k render hone par `getContacts-api` hit karke data launga
- data update se state change hogi -> matlab re-render. (`useState` change pr re render karta h)
- so dashboard firse re-render hoga.
- Thus LOOP.

### Solution -
- ONLY first time render of `dashboard` par fetch karle or rakhle


### Bahut important rule

React bolta hai -->

> "Body ke andar side-effect mat likho."

Component body me sirf ye cheezein honi chahiye:

```
useState()

useEffect()

JS calculations

return JSX
```

Ye nahi:

```
fetch()

axios()

getContacts()

setTimeout()

addEventListener()
```

Ye sab **side effects** hain.

Aur side effects ka ghar hai

```
useEffect()
```

---




## Dependency array -

### Case 1:
```
useEffect(() => {

}, []);
```

Matlab

> "Ye effect kisi bhi React state ya prop pe depend nahi karta."

Isliye

> Mount hone ke baad ek baar chalao.


### Case 2:
```
useEffect(() => {

});
```

Dependency hi nahi di.

React bolega

> Mujhe kuch pata nahi.

Safe side pe

> Har render ke baad effect chala deta hu.

Isi wajah se infinite loop ban jata hai.


### Case 3:
```
useEffect(() => {
  loadContact();
}, [id]);
```

ka matlab hai contact id change ho to naya contact load karo.