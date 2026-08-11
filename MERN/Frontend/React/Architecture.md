

### Why user not in localStorage -

Haan, **kar sakta hai**. Technically ye chalega:

```
Login success
→ token localStorage me save
→ /users/current call
→ user localStorage me save
→ app reopen
→ user localStorage se read
```

But professional reason se **user ko localStorage me store karna ideal nahi hai**.

### Problem kya hai?

`localStorage` ka data **stale** ho sakta hai.

Example:

```
Aaj user email/name change karta hai
ya backend me account delete/disable hota hai
ya token expire ho jata hai
ya role change hota hai
```

Tumhare localStorage me purana user pada rahega. Frontend sochega user valid hai, but backend nahi.

### Better rule

```
localStorage me token store kar sakte ho
user ko memory/AuthContext me rakho
app start par /users/current se fresh user lao
```

Simple line yaad rakh:
**Token proves identity. `/current` confirms identity.**

---

refer: https://share.gemini.google/VBSehdAP9ms3 

### Render and useEffect Flow - ( for Context API)

2. Pehle parent render hoga, fir uska andar ke child render hoge ( render matlab jsx and component methods se h ) `Render: top to bottom`
3. fir  UI show hogi
4. Ui show ke sath hi, 
5. ek bar render ho gya, to useEffect run hoga child se parent ka. `useEffect: bottom to top`

#### Step-by-Step Timeline:

1. **App Load Hui (Render Phase):** `AuthProvider` aur `LoginPage` dono render hue (memory me unka code chala).
    
2. **Screen par UI Dikhayi Di (Mount Phase):** User ko browser me text boxes (email, password) aur "Submit" button dikhna shuru ho gaya.
    
3. **`useEffect` Fire Hua:** UI chipakte hi, React ne line se saare `useEffect` chala diye (pehle child ka, fir parent ka). Yani **`AuthProvider` ka `useEffect` isiliye chal gaya kyunki page screen par load ho chuka hai.**
    
4. **User Action (Submit Phase):** Ab user aaram se apna email type karega, password type karega (isme kam se kam 2-5 seconds lagenge), aur phir "Submit" button par click karega.


### **IMPORTANT -**
- render (top to bottom) -> UI mount -> useEffect fire (bottom to top) -> ab user k actions register honge ( like submit form )      `{ like dfs recursive call }`