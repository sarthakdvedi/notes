# Ride Sharing App — Backend API Documentation

  

**Base Gateway URL:** `http://localhost:3000`  

**Authentication:** Pass `Authorization: Bearer <TOKEN>` in the request header (or automatic cookies).  

**CORS:** Enabled for all origins.

  

---

  

## 1. Quick Start for Frontend Devs

  

To start the entire backend with all 4 services running simultaneously:

```bash

npm install

npm run dev

```

This boots:

- Gateway: `http://localhost:3000`

- User Service: `http://localhost:3001`

- Captain Service: `http://localhost:3002`

- Ride Service: `http://localhost:3003`

  

All your frontend calls should target the Gateway: **`http://localhost:3000`**.

  

---

  

## 2. Authentication Flow

  

### A. User (Rider) Auth

- **`POST /user/register`**

  - **Body:** `{ "name": "John", "email": "john@test.com", "password": "pass", "phone": "1234567890" }`

  - **Returns:** `{ "token": "...", "user": { "_id": "...", "name": "...", "email": "..." } }`

- **`POST /user/login`**

  - **Body:** `{ "email": "john@test.com", "password": "pass" }`

  - **Returns:** `{ "token": "...", "user": { ... } }`

- **`GET /user/profile`** (Auth: User)

  - **Returns:** User profile object

- **`GET /user/logout`** (Auth: User)

  - Invalidates token

  

### B. Captain (Driver) Auth

- **`POST /captain/register`**

  - **Body:** `{ "name": "Alex", "email": "alex@test.com", "password": "pass", "phone": "...", "vehicle": { "plate": "ABC-1234", "vehicleType": "car" } }`

  - **Returns:** `{ "token": "...", "captain": { ... } }`

- **`POST /captain/login`**

  - **Body:** `{ "email": "alex@test.com", "password": "pass" }`

  - **Returns:** `{ "token": "...", "captain": { ... } }`

- **`GET /captain/profile`** (Auth: Captain)

  - **Returns:** Captain profile object

- **`PATCH /captain/toggle-availability`** (Auth: Captain)

  - Flips `isAvailable` between `true` and `false`

- **`GET /captain/logout`** (Auth: Captain)

  - Invalidates token

  

---

  

## 3. Real-Time Leaflet Map Endpoints

  

### A. Show Available Cabs on Map (Before Ride Booking)

- **`GET /captain/available-captains`** (Public)

  - Returns all online captains and their current coordinates.

  - **Response:**

    ```json

    [

      {

        "_id": "...",

        "name": "Captain Alex",

        "vehicle": { "plate": "DL-01-AB-1234", "vehicleType": "car" },

        "currentLocation": { "lat": 28.6139, "lng": 77.2090, "heading": 90 }

      }

    ]

    ```

  

### B. Captain Pushes Live GPS Location

- **`PATCH /captain/location`** (Auth: Captain)

  - Call periodically while online or driving:

  - **Body:** `{ "lat": 28.6139, "lng": 77.2090, "heading": 90 }`

  

---

  

## 4. Ride Booking & State Machine

  

### A. Rider Creates Ride

- **`POST /ride/create-ride`** (Auth: User)

  - **Body:**

    ```json

    {

      "pickup": { "address": "Connaught Place", "lat": 28.6315, "lng": 77.2167 },

      "destination": { "address": "India Gate", "lat": 28.6129, "lng": 77.2295 },

      "fare": 150

    }

    ```

  - **Response:**

    ```json

    {

      "_id": "6addf23cf2f5ad20a2093786",

      "user": "...",

      "status": "requested",

      "otp": "4821",

      "fare": 150,

      "pickup": { "address": "Connaught Place", "lat": 28.6315, "lng": 77.2167 },

      "destination": { "address": "India Gate", "lat": 28.6129, "lng": 77.2295 }

    }

    ```

  

### B. Captain Waiting for New Rides (Long Polling)

- **`GET /captain/new-ride`** (Auth: Captain)

  - Holds request until a new ride is booked, then returns the ride object.

  

### C. Captain Accepts Ride

- **`PUT /ride/accept-ride?rideId=<RIDE_ID>`** (Auth: Captain)

  - Atomically assigns the ride to the captain.

  - **Returns:** `{ "_id": "...", "status": "accepted", "captain": "..." }`

  - *(If already accepted by someone else, returns 400)*

  

### D. Check Active Ongoing Ride (On Page Refresh)

If user or captain refreshes their browser page:

- **`GET /ride/user/active-ride`** (Auth: User)

  - Returns the user's current ongoing ride (status: `requested`, `accepted`, or `started`).

- **`GET /ride/captain/active-ride`** (Auth: Captain)

  - Returns the captain's current ongoing ride (status: `accepted` or `started`).

  

### E. Rider Polls Live Map Tracking (Every 2–3s)

- **`GET /ride/:id/live-tracking`** (Auth: User or Captain)

  - **Response:**

    ```json

    {

      "rideId": "...",

      "status": "accepted",

      "pickup": { "address": "...", "lat": 28.6315, "lng": 77.2167 },

      "destination": { "address": "...", "lat": 28.6129, "lng": 77.2295 },

      "captainLocation": { "lat": 28.6250, "lng": 77.2200, "heading": 120 },

      "captainId": "...",

      "fare": 150

    }

    ```

  

### F. Captain Pushes Transit GPS Location

- **`PATCH /ride/:id/location`** (Auth: Captain)

  - **Body:** `{ "lat": 28.6250, "lng": 77.2200, "heading": 120 }`

  

### G. Captain Starts Ride (With OTP)

- **`POST /ride/start-ride`** (Auth: Captain)

  - **Body:** `{ "rideId": "...", "otp": "4821" }`

  - **Response:** `{ "message": "Ride started successfully", "ride": { "status": "started" } }`

  

### H. Captain Completes Ride

- **`POST /ride/complete-ride`** (Auth: Captain)

  - **Body:** `{ "rideId": "..." }`

  - **Response:** `{ "message": "Ride completed successfully", "ride": { "status": "completed" } }`

  

### I. Cancel Ride

- **`POST /ride/cancel-ride`** (Auth: User)

  - **Body:** `{ "rideId": "..." }`