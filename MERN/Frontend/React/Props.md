

### in React -
- parent component se sare props ka object banke jata h
- and child component me `props` nam se access kar sakte h us object ko `function ContactCard(props)` <-- kuch esa dikhta h
- par hum generally, destructure kar lete h child component function p



---

### Special Props -

`key` **HTML attribute bhi nahi hai aur normal React prop bhi nahi hai.**

Ye React ka **special reserved prop** hai.

React me sirf do props aise hain jo special treatment paate hain:

1. `key` → Lists ki identity ke liye.
2. `ref` → DOM ya component reference ke liye.

Ye dono **React khud consume karta hai**, isliye ye tumhare component ke `props` me normally available nahi hote.

Isi liye jab bhi tum list render karo, dimaag me ye line yaad rakhna:

> **`key` is for React. Everything else is for my component.**


- kuch bhi karo, `key` prop component m nahi milega brooo. vo only react k lie h