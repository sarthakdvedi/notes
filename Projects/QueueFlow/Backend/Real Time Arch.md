
You have hit on two extremely important design concepts:  **event-driven real-time updates**.


### Part 2: "This ticket table must be updated very frequently in real-time."

You are 100% correct. Since positions change, numbers get called, and people snooze, the database needs to reflect these updates instantly.

However, we have to be careful about **how** we do this so we don't crash our database. We use a combination of two things: **Triggers** and **WebSockets**.

#### How it works without WebSockets (The Bad Way - "Polling")

Imagine Alice's phone asking the server every 2 seconds: _"Am I next yet? Am I next yet? Am I next yet?"_ If you have 1,000 customers waiting, your database is getting hit with **500 queries every single second**. This is called "polling," and it will slow down your database very quickly.

#### How it works with WebSockets (The Good Way - "Event-Driven")

Instead of Alice constantly asking the database, we use **Socket.io** to establish a open, live two-way line of communication between Alice's phone and our server (like a phone call that stays active).

Here is the life of a real-time update:

1. **The Trigger**: The Admin clicks the **"Call Next Customer"** button on their screen.
2. **The Database Write**: The server updates Alice’s ticket status from `WAITING` to `SERVING` in the database. (This is a single, quick database update).
3. **The Broadcast**: Immediately after updating the database, the server sends a broadcast through Socket.io:
    
    > _"Hey Alice's phone, your ticket is now being served!"_
    
4. **The Screen Update**: Alice’s browser receives this message and updates her screen instantly, showing a notification and changing the status to "Please proceed to Counter 1".

### Summary

- **Yes**, the customer's identity lives inside the `Ticket` table.
- The database is only updated when a **real event** happens (someone joins, gets called, snoozes, or leaves).
- **Socket.io** handles the heavy lifting of telling the customer's phone about these updates instantly, saving the database from being flooded with constant queries.