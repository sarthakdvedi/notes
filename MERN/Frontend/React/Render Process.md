
React ke internally 3 stages hoti hain:

## 1. **Trigger** → `setState()`
yahi se re-render start hota h


---
## 2. **Render Phase** →
Component function execute hota hai, new React tree banti hai, reconciliation/diffing hoti hai.

### JSX -
1. JSX is just a description (Ye DOM nahi hai, na hi html)
2. it's compiler (Babel) translates your JSX into JavaScript function calls (usually `React.createElement()`)
3. When those functions run, React reads them and builds a plain JavaScript object. This object is the **React Element**!
4. or y js object hi component function se return hota h
5. fir react us object ko pdke browser se bolke actual DOM bana deta h <-`(reconciliation yhi beech m hota h)`


### Reconciliation -
- Reconciliation is the smart algorithm that helps smartly update real DOM.
- define - "Purane aur naye React tree ko compare karke decide karna ki DOM me kya change karna hai."


1. **React Element Tree** ( *virtual DOM* ) - js object ka tree banega.
2. **Diffing** - Compare Old tree vs New tree and know the difference

---

## 2. **Commit Phase** →
- Sirf required DOM changes apply hote hain.
- **Actual-DOM Update** - only required changes karo to the actual real DOM.



---


### Actual Flow -

Component Function
↓
React Element Tree
↓
Reconciliation
      │
      ├── Diffing
      └── Decide changes
↓
Commit Phase
↓
DOM Update
↓
Browser Paint