

### Where to import -
API function (`deleteContact`) ko hamesha us component me import karna chahiye jo **prop de raha hai (yani Parent Component / `DashboardPage`)**.

---

### Re-render -

1. **Atal Niyam** - jis component ki state change hogi, vo rerender hoga
2. Jab Parent (Dashboard) firse run hoga, to uske JSX ke andar likha hua `<ContactCard .../>` child component bhi firse execute hoga. Is baar Dashboard usko **naya prop** bhejega
3. 💡 **Short me Yaad Rakho:** React me jab bhi koi **Parent re-render hota hai, to uske saare Child components by default re-render (firse run) hote hi hain**, chahe unka prop badla ho ya na badla ho! (Jab tak hum unhe `React.memo` se optimize na karein).