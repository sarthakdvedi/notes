
Q: so basically, if someone uses multer, he will handle req.body and req.file at backend (And both are normal js objects) ? did i get it right ?



In Express, how a request is parsed and attached to the `req` object depends on the **content type** sent by the client and the **middleware** you use to process it.

  

Here are the primary ways to send data to an Express backend, along with what middleware handles them and what properties they populate on the `req` object:

  

---

### 1. URL Query Parameters (GET Requests)

- **How it's sent:** Data is appended directly to the URL (`/search?category=shoes&page=2`).
    
      
    
- **Middleware required:** **None** (built into Express).
    
      
    
- **Where it lands on `req`:** `req.query`
    
      
    
- **Type:** A JavaScript object.
    
      
    

JavaScript

```
// URL: /api/products?sort=asc&limit=10
app.get('/api/products', (req, res) => {
  console.log(req.query); 
  // Output: { sort: 'asc', limit: '10' }
});
```

---

### 2. Route Parameters (URL Pathing)

- **How it's sent:** Dynamic segments embedded inside the URL path (`/users/42`).
    
      
    
- **Middleware required:** **None** (defined directly in your route path using `:`).
    
      
    
- **Where it lands on `req`:** `req.params`
    
      
    
- **Type:** A JavaScript object.
    
      
    

JavaScript

```
// Route: /users/:id/posts/:postId
app.get('/users/:id/posts/:postId', (req, res) => {
  console.log(req.params); 
  // Output: { id: '42', postId: '108' }
});
```

---

### 3. Standard URL-Encoded Form Data (`application/x-www-form-urlencoded`)

- **How it's sent:** Default behavior of standard HTML `<form>` submissions without file uploads.
    
      
    
- **Middleware required:** `express.urlencoded({ extended: true })`
    
      
    
- **Where it lands on `req`:** `req.body`
    
      
    
- **Type:** A JavaScript object.
    
      
    

JavaScript

```
app.use(express.urlencoded({ extended: true }));

app.post('/login', (req, res) => {
  console.log(req.body); 
  // Output: { email: 'user@example.com', password: 'secretpassword' }
});
```

---

### 4. HTTP Headers (Metadata & Auth)

- **How it's sent:** Custom headers or standard auth tokens sent with the HTTP request (e.g., `Authorization: Bearer <token>`).
    
      
    
- **Middleware required:** **None** (built into Express).
    
      
    
- **Where it lands on `req`:** `req.headers` or `req.get('header-name')`
    
      
    
- **Type:** A JavaScript object containing all header key-value pairs.
    
      
    

JavaScript

```
app.get('/protected', (req, res) => {
  console.log(req.headers.authorization); 
  // Output: "Bearer eyJhbGciOi..."
});
```

---

### 5. Cookies

- **How it's sent:** Small key-value pairs stored in the browser and automatically sent with HTTP requests via the `Cookie` header.
    
      
    
- **Middleware required:** `cookie-parser`
    
      
    
- **Where it lands on `req`:** `req.cookies` (or `req.signedCookies` if using signed cookies).
    
      
    
- **Type:** A JavaScript object.
    
      
    

JavaScript

```
const cookieParser = require('cookie-parser');
app.use(cookieParser());

app.get('/dashboard', (req, res) => {
  console.log(req.cookies); 
  // Output: { sessionId: 'abc123xyz', theme: 'dark' }
});
```

---

### 6. Raw Text / Plain Text (`text/plain`)

- **How it's sent:** Sending raw string data (e.g., CSV content, log entries, XML strings) directly in the request body.
    
      
    
- **Middleware required:** `express.text()`
    
      
    
- **Where it lands on `req`:** `req.body`
    
      
    
- **Type:** A JavaScript **string** (not an object).
    
      
    

JavaScript

```
app.use(express.text());

app.post('/logs', (req, res) => {
  console.log(req.body); 
  // Output: "2026-08-31 12:00:00 [INFO] System initialized." (String)
});
```

---

### 7. Raw Binary Streams / Octet-Stream (`application/octet-stream`)

- **How it's sent:** Raw binary files or byte arrays sent directly without `multipart/form-data` wrapper (often used in direct file stream uploads).
    
      
    
- **Middleware required:** `express.raw()`
    
      
    
- **Where it lands on `req`:** `req.body`
    
      
    
- **Type:** A Node.js **`Buffer` object**.
    
      
    

JavaScript

```
app.use(express.raw({ type: 'application/octet-stream', limit: '10mb' }));

app.post('/upload-raw', (req, res) => {
  console.log(req.body); 
  // Output: <Buffer 89 50 4e 47 0d 0a 1a 0a ...> (Node Buffer)
});
```

---

### 8. WebSockets / WebTransport (Persistent Connections)

- **How it works:** Unlike HTTP requests that open and close, a WebSocket establishes a persistent, two-way connection (usually using libraries like `socket.io` or `ws` alongside Express).
    
      
    
- **Where it lands:** Handled via event listeners rather than `req` object.
    

JavaScript

```
io.on('connection', (socket) => {
  socket.on('chat-message', (data) => {
    console.log(data); // Can be a JS object, string, or Buffer
  });
});
```

---

### Cheat Sheet Summary

| **Sent Format / Method** | **Express Middleware Needed** | **Populates**                       | **JS Data Type**            |
| ------------------------ | ----------------------------- | ----------------------------------- | --------------------------- |
| **JSON**                 | `express.json()`              | `req.body`                          | `Object`                    |
| **URL Query (`?a=1`)**   | None                          | `req.query`                         | `Object`                    |
| **URL Params (`/:id`)**  | None                          | `req.params`                        | `Object`                    |
| **HTML Form Data**       | `express.urlencoded()`        | `req.body`                          | `Object`                    |
| **Multipart (Files)**    | `multer`                      | `req.body` & `req.file`/`req.files` | `Object` & `Object`/`Array` |
| **Headers**              | None                          | `req.headers`                       | `Object`                    |
| **Cookies**              | `cookie-parser`               | `req.cookies`                       | `Object`                    |
| **Plain Text**           | `express.text()`              | `req.body`                          | `String`                    |
| **Raw Binary**           | `express.raw()`               | `req.body`                          | `Buffer`                    |
