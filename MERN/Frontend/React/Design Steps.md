1. empty, components and hollow routes define
2. form UI bana
3. form control kar -> useState and handleSubmit, handleChange(state updated rakhni h) define karke
4. context define kar (3 steps + route wrap + dummy try with login with hardcoded token)
5. protectedRoutes define kar + route wrap (agar authenticated nahi h to redirect to login)
6. main data jaha render hoga, dummy bana (eg. dashboard) + card component render karwa (with dummy data)
7. api layer design
8. consume api's (jaha data chahiye)
9. `token` -> localStorage m rahega, but `user` ko app open each first time fetch taki latest user aye !
10. useEffect ka use karke, first time dashboard load p, data le lenge and sare contacts ek bar m render ho jayenge.
11. then functionalities banyenge -> add, edit / update, delete implement
12. delete dhyan se -> coz dashboard pr hi h, to button click se -> backend se bhi delete karna h and UI se bhi remove.
    islie ->
    Agar aap ( delete ) API function ko `ContactCard` me import karke wahan call karoge, toh card delete toh ho jayega backend se, par `DashboardPage` ko pata nahi chalega ki kisi card ko hatana hai (kyunki contacts state Dashboard ke paas hai). Isliye hum function ko `DashboardPage` me banate hain aur `ContactCard` ko as a prop (`onDelete`) bhejte hain. Isko **"Lifting State Up"** kehte hain.
13. loading implement -> conditional rendering of loading and contactCard component, also implement -> "Add your first contact to get started." if no contacts (just to polish)
    why loading ->
    **loading state** add karo. Agar user ka internet slow hua aur usne register button par 3-4 baar click kar diya, to backend par multiple requests chali jaengi