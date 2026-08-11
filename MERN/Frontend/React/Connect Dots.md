
### `Disabled` attribute -

#### in HTML -
```html
<button type="button" disabled>Click Me!</button>
```
#### in JS -
```js
document.getElementById("myBtn").disabled = true; // isme disabled ko bool value dete h
```

#### in React -
```js
          <button
          onClick={() => handleDelete(contact._id)}
          className="btn btn-sm btn-error"
          disabled={isDeleting} // js ki tarah hi
```

---



### HTML5 ka Rule: Button ek "Container" hai

HTML5 ke niyam ke mutabik, `<button>` tag sirf text ke liye nahi bana hai. Yeh ek **Container Tag** hai (jaise `<div>` ya `<span>` hote hain).

Iska matlab tum button ke andar text ke sath-sath:

- Icons (`<img>`, SVG, ya `<Trash2/>`)
    
- Text styling ke liye `<span>`
    
- Yahan tak ki loading ke liye dusre HTML elements bhi daal sakte ho.
    

Browser isko bade aaram se render karta hai kyunki uske liye ye sab button ke **Children** (bachhe) hain.