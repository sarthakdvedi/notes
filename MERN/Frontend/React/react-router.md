

### 1. `navigate("/dashboard")` vs `<Navigate to="/dashboard"/>`

- **`useNavigate()` (Imperative Way):** Ye ek **function** hai. Iska matlab hota hai: _"Jaise hi ye line execute ho, user ko turant us page par feko."_ Ye kisi event (jaise button click ya successful API response) ke andar use karne ke liye perfect hai.
    
- **`<Navigate/>` (Declarative Way):** Ye ek **React Component** hai. Iska matlab hota hai: _"Jab ye component screen par render (load) hoga, tab navigation trigger hoga."_