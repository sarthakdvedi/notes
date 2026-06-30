
You have hit on two extremely important design concepts: **ephemeral users** (temporary users)

### Part 1: Are we storing the customer in the `Ticket` table?

**Yes, absolutely.**

Here is why we do this: In a queue system, you want **zero friction** for the customer. If a customer has to download an app, create an account, verify their email, and set a password just to wait for a table at a restaurant, they will get frustrated and leave.

So, we treat them as **anonymous/temporary guests**.

- They scan the QR code.
- They type their name (e.g., _"Alice"_).
- We create a record in the `Ticket` table that holds their name (_"Alice"_) and their ticket number (_"A-102"_).
- We do **not** create a permanent profile in a "Customer" table. Once Alice is served, her ticket status changes to `COMPLETED`, and her journey is finished.