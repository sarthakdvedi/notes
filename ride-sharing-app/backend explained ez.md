# A Simple Guide to the Backend for Frontend Developers
*(Explain Like I’m 5)*

Hey there! If you’ve only worked with regular single-server Node.js apps and terms like **Microservices** and **RabbitMQ** sound scary, don't worry. 

From your perspective as a frontend developer, **this backend works just like any normal backend you’ve ever used**.

---

## 1. The Big Picture: Think of a Pizza Restaurant 🍕

Imagine you walk into a pizza restaurant:

1. **The Gateway (`http://localhost:3000`) is the Cashier at the front door.**  
   You (the Frontend) **only talk to the Cashier**. You never need to walk into the back rooms or worry about the other port numbers.
   - If you ask about user accounts, the cashier sends your note to the **User Room (`port 3001`)**.
   - If you ask about drivers, the cashier sends it to the **Captain Room (`port 3002`)**.
   - If you ask about booking a cab, the cashier sends it to the **Ride Room (`port 3003`)**.

2. **What is RabbitMQ? It's just a Walkie-Talkie in the kitchen! 📻**  
   - You, the frontend engineer, **never touch RabbitMQ**. You don't need any library for it.
   - It is simply a walkie-talkie the backend rooms use to talk to each other.
   - *Example:* When the **Ride Room** creates a ride, it shouts into its walkie-talkie: *"Hey Captain Room! Tell online drivers there's a new passenger waiting!"*

---

## 2. All You Need to Run the Backend

To start all 4 services at once, open your terminal in the backend root directory and type:
```bash
npm run dev
```
That's it! All rooms are now open and listening behind the front door: **`http://localhost:3000`**.

---

## 3. The Whole Story: Step-by-Step Data Flow

Here is the exact story of how a ride happens from screen to screen:

```
[ Rider App ]                                                    [ Captain App ]
      │                                                                 │
  1. Register / Login                                               2. Register / Login
  (Save token)                                                      (Save token)
      │                                                                 │
      │                                                             3. Turn Online
      │                                                             (PATCH /captain/toggle-availability)
      │                                                                 │
  2. See online cabs on Map                                         4. Wait for rides
  (GET /captain/available-captains)                                 (GET /captain/new-ride)
      │                                                                 │
  3. Book Ride ───────────────────────[ RabbitMQ shouts ]───────────────▶
  (POST /ride/create-ride)             "New ride available!"            │
  (Rider gets 4-digit OTP)                                          5. Screen pops up:
      │                                                             "Accept Ride?"
      │                                                                 │
      │ ◀─────────────────────────────[ RabbitMQ shouts ]────────── 6. Captain clicks Accept
  4. Rider Polls                      "Captain Alex accepted!"      (PUT /ride/accept-ride)
  (GET /ride/:id)                                                       │
  Status becomes "accepted"!                                            │
      │                                                                 │
  5. Watch Captain Move on Map ◀──────[ Pushes GPS Every 3s ]────── 7. Driving to Pickup
  (GET /ride/:id/live-tracking)                                     (PATCH /ride/:id/location)
      │                                                                 │
      │ ══════════════════ Captain arrives at pickup ══════════════════ │
      │                                                                 │
  6. Rider tells OTP to Captain ─────────(Speaks in person)────────────▶ 8. Captain enters OTP
                                                                    (POST /ride/start-ride)
                                                                    Status: "started"
      │                                                                 │
      │ ══════════════════════ Driving to destination ═════════════════ │
      │                                                                 │
  7. Rider sees "Completed" ◀───────── Captain ends ride ────────── 9. Clicks Complete
                                                                    (POST /ride/complete-ride)
```

---

## 4. The Complete API Cheat-Sheet in Chronological Order

All requests go to: **`http://localhost:3000`**  
Always pass: `headers: { "Authorization": "Bearer <YOUR_TOKEN>" }`

---

### Phase 1: Authentication

#### 1. Rider Sign Up
- **URL:** `POST /user/register`
- **Body:** `{ "name": "John", "email": "john@gmail.com", "password": "123", "phone": "9999999999" }`
- **What to do:** Save `response.data.token` in `localStorage`.

#### 2. Captain Sign Up
- **URL:** `POST /captain/register`
- **Body:** `{ "name": "Alex", "email": "alex@gmail.com", "password": "123", "vehicle": { "plate": "DL-01-1234", "vehicleType": "car" } }`
- **What to do:** Save `response.data.token` in `localStorage`.

---

### Phase 2: Captain Goes Online

#### 3. Toggle Captain Online / Offline
- **URL:** `PATCH /captain/toggle-availability`
- **Header:** `Authorization: Bearer <CAPTAIN_TOKEN>`
- **Result:** Captain is now online and visible to users.

#### 4. Captain Screen: Waiting for Rides (Long Polling)
- **URL:** `GET /captain/new-ride`
- **Header:** `Authorization: Bearer <CAPTAIN_TOKEN>`
- **How it works:** This request will stay open and "hang" for up to 30 seconds until a rider creates a ride. When a ride is created, this request immediately completes and returns the ride data!
- **Frontend tip:** Once it returns a ride, show the *"Accept Ride"* popup. If it times out after 30 seconds with status `204 (No Content)`, simply call `GET /captain/new-ride` again in a loop while the captain is online!

---

### Phase 3: Rider Books a Ride

#### 5. Show Nearby Drivers on Leaflet Map
- **URL:** `GET /captain/available-captains`
- **Header:** None required
- **Result:** Returns an array of online drivers with coordinates:
  ```json
  [
    {
      "name": "Alex",
      "currentLocation": { "lat": 28.6139, "lng": 77.2090 }
    }
  ]
  ```
- **What to do:** Plot moving car markers on your Leaflet map:  
  `L.marker([captain.currentLocation.lat, captain.currentLocation.lng]).addTo(map)`

#### 6. Rider Clicks "Book Ride"
- **URL:** `POST /ride/create-ride`
- **Header:** `Authorization: Bearer <USER_TOKEN>`
- **Body:**
  ```json
  {
    "pickup": { "address": "Connaught Place", "lat": 28.6315, "lng": 77.2167 },
    "destination": { "address": "India Gate", "lat": 28.6129, "lng": 77.2295 },
    "fare": 150
  }
  ```
- **Result:** Returns the new ride object with a **`4-digit OTP`** (e.g. `"4821"`).  
  **Important:** Show this OTP prominently on the Rider’s screen! They need to tell it to the driver to start the trip.

---

### Phase 4: Captain Accepts & Meets Rider

#### 7. Captain Clicks "Accept"
- **URL:** `PUT /ride/accept-ride?rideId=<RIDE_ID>`
- **Header:** `Authorization: Bearer <CAPTAIN_TOKEN>`
- **Result:** Assigns this captain to the ride. If another captain already accepted it, you'll receive a `400 "Ride already accepted"` error.

#### 8. Rider Checks Ride Status (Polling)
- **URL:** `GET /ride/<RIDE_ID>` (or `GET /ride/user/active-ride`)
- **Header:** `Authorization: Bearer <USER_TOKEN>`
- **How it works:** While the rider is on the "Searching for driver..." screen, call this every 3 seconds. Once `response.data.status === "accepted"`, switch the screen to *"Driver is on the way!"*

---

### Phase 5: Real-Time Leaflet GPS Tracking

#### 9. Captain Sends Live GPS Coordinates
- **URL:** `PATCH /ride/<RIDE_ID>/location`
- **Header:** `Authorization: Bearer <CAPTAIN_TOKEN>`
- **Body:** `{ "lat": 28.6250, "lng": 77.2200, "heading": 90 }`
- **Frontend tip:** Use browser `navigator.geolocation.watchPosition((pos) => { ... })` to send coordinates every 3 to 5 seconds.

#### 10. Rider Updates Map with Captain's Position
- **URL:** `GET /ride/<RIDE_ID>/live-tracking`
- **Header:** `Authorization: Bearer <USER_TOKEN>`
- **How it works:** Rider polls this every 3 seconds to smoothly animate the car marker on Leaflet:
  ```javascript
  captainMarker.setLatLng([data.captainLocation.lat, data.captainLocation.lng]);
  ```

---

### Phase 6: Start & Complete the Ride

#### 11. Captain Starts the Trip (OTP Verification)
When the driver arrives, the passenger verbally shares their 4-digit OTP.
- **URL:** `POST /ride/start-ride`
- **Header:** `Authorization: Bearer <CAPTAIN_TOKEN>`
- **Body:** `{ "rideId": "<RIDE_ID>", "otp": "4821" }`
- **Result:** Status becomes `"started"`. (If the driver types the wrong code, returns `400 "Invalid OTP"`).

#### 12. Captain Ends the Trip
When arriving at the destination:
- **URL:** `POST /ride/complete-ride`
- **Header:** `Authorization: Bearer <CAPTAIN_TOKEN>`
- **Body:** `{ "rideId": "<RIDE_ID>" }`
- **Result:** Status becomes `"completed"`. Show the payment / summary screen!

---

### Phase 7: Browser Refresh Safety (Crucial for Frontend!)

If the user or captain accidentally refreshes the browser page:
- Call **`GET /ride/user/active-ride`** on user app load.
- Call **`GET /ride/captain/active-ride`** on captain app load.
- If it returns a ride, you can immediately restore the active ride screen and map markers without starting over!

---

## 5. Summary: What the Frontend Engineer Needs to Remember

1. **Only 1 Base URL:** Always use `http://localhost:3000`. You never need to call ports 3001, 3002, or 3003 directly.
2. **CORS is fully enabled:** You won't get any blocked browser requests.
3. **No WebSockets required:** Simple `setInterval` polling every 2–3 seconds handles all tracking and status changes smoothly.
4. **RabbitMQ is invisible to you:** The backend takes care of message passing behind the scenes. You just make standard HTTP `fetch()` or `axios()` calls!