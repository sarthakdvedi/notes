
#### What -
1. npm package
2. backend framwork
3. manages everything from receiving the request and giving the response

#### Flow -
req ->   each middleware | one route | error handler  -> res

-------------------------------------------
#### Middlewares -

- app.use()         ----means---->     for each req
##### Parsers -
- app.use(express.json());              (json data ata h use fix karta h)
- app.use(express.urlencoded({ extended : true }));       (jab form submit hoke ata h)
- when sending data to backend -> they make it readable

##### Custom Middlewares -
must use  --- >    next()      {unlike, inbuilt middlewares like parsers, as they internally do next()}

------------------------------------
#### Session -
- if no session   ->   logout after each req
- if session   ->   stays login till session (any no. of req within session)

-------------------------------

#### Use async controllers -
- **Errors in async code:** If an error happens inside an `async` function (like the database connection dropping), it becomes a **"Rejected Promise."** Express (version 4 and below) is "blind" to rejected promises. It won't realize an error happened; it will just let the request hang forever. By making the controller `async` and wrapping it in `asyncHandler`, you ensure that those database failures are caught and sent to your `next(err)` pipeline.
- for smooth async functioning and performing tasks (taking new requests) till an async work is pending (like db communication or I/O)