
## At backend -

- we use ApiError.js     --->   taaki error consistent manner m structure ho each time
- and errorHandler middleware, jo ki last m placed rahega   ---->   taki agar controller ke beech m kahi bhi error occur ho, to ApiError.js se error ka correct consistent format bane and ye middleware error ko as a response sahi se client ko bhej dega.

### 🛠️ Beech me response kaise jayega?

1. **Normal Flow:** Agar koi error nahi aaya, toh controller ke andar likha hua `res.status(200).json(...)` chalega aur client ko response mil jayega. Request wahi khatam!
    
2. **Error Flow:** Jaise hi `throw new ApiError` hoga, niche ka normal response wala code bypass (skip) ho jayega. Express seedhe daudte hue `errorHandler` middleware ke paas jayega, aur wahan likha hua `res.status().json()` client ko error response send kar dega.
    

Dono ko sath use karne se fayda yeh hai ki aapko har controller me `res.status(400).json({ error: ... })` baar-baar repeat nahi karna padega. Controller ekdam saaf-suthra dikhega!