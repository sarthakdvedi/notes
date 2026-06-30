
- express stores middlewares using array (aka **stack** because of how control flows through layers.)
- it does a linear search  --like--> next() or next(err) (to find errorHandler)


- an errorHandler middleware is defined as a middleware with 4 parameter (err,req,res,next)


------------------------
### 2. The Logic of "The Sequence" -

- ErrorHandler middleware---> after routes (so on next(err)  --->   express finds errorHandler middleware, if any route throws an error)

- Similarly, app.use(express.json()); is kept before routes as data comes with req and express has to translate that raw text into a JavaScript object **before** the request reaches your route.

The order is determined by whether the middleware is **preparing** the request or **cleaning up** after it.

#### The "Pre-Processors" (Must be Before)

These prepare the environment so the route can do its job:

- `express.json()`: Translates the body.
    
- `cors()`: Checks if the sender is allowed.
    
- `morgan()`: Logs the incoming request.
    

#### The "Routes" (The Middle)

This is where the actual business logic happens (e.g., saving a user to a database).

#### The "Post-Processors" (Must be After)

These handle things that the route _produced_ (like errors):

- `errorHandler`: Only runs if a route failed.


**The Golden Rule:** Place a middleware **before** the routes that **depend** on its work, and **after** the routes that **trigger** its work.

------------------------


