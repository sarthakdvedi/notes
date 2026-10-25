
Viewed package.json:1-18
Ran command: `npm install cors`
Created app.js
Created captain.model.js
Created captain.controller.js
Created captain.routes.js
Created ride.model.js
Created ride.controller.js
Created ride.routes.js
Created test_backend.js
Ran command: `node app.js`
Ran command: `node server.js`
Ran command: `node server.js`
Ran command: `node server.js`
Ran command: `node C:\Users\DELL\.gemini\antigravity-ide\brain\d0441401-ce77-4c44-9d45-c96267561219\scratch\test_backend.js`
Used tool: manage_task
Used tool: manage_task
Used tool: manage_task
Used tool: manage_task

### Backend Updated for Leaflet.js Real-Time Map Tracking

I have updated your backend models, controllers, and routes to support **Leaflet.js map tracking**. 

---

### What Changed on the Backend

#### 1. CORS Enabled on API Gateway ([gateway/app.js](file:///c:/Users/DELL/Documents/Projects/ride-sharing-app/gateway/app.js))
- Installed `cors` and configured the gateway so any web frontend (e.g. `localhost:5173`, `localhost:3000`) can make HTTP requests without being blocked by browser CORS policies.

#### 2. Captain Live GPS Location ([captain.model.js](file:///c:/Users/DELL/Documents/Projects/ride-sharing-app/captain/models/captain.model.js))
- Added `currentLocation: { lat, lng, heading, updatedAt }` to the Captain model.
- Added **`PATCH /captain/location`**: Captain app sends periodic GPS updates (`lat`, `lng`, `heading`).
- Added **`GET /captain/available-captains`**: Returns all online captains with their `[lat, lng]` coordinates so the frontend can plot moving taxi icons on the map before booking.

#### 3. Ride Coordinates & Live Tracking ([ride.model.js](file:///c:/Users/DELL/Documents/Projects/ride-sharing-app/ride/models/ride.model.js))
- `pickup` and `destination` now store both the text address and `[lat, lng]` coordinates (supports backwards-compatible strings as well).
- Added `captainLocation: { lat, lng, heading, updatedAt }` directly to the active ride document.
- Added **`PATCH /ride/:id/location`**: Captain app pushes live in-ride coordinates during pickup and transit.
- Added **`GET /ride/:id/live-tracking`**: Rider polls this lightweight endpoint every 2–3 seconds to update the captain marker on Leaflet in real-time.

---

### API Reference for Frontend Integration

#### A. Show Available Cabs on Map (Before Ride is Booked)
- **Endpoint:** `GET http://localhost:3000/captain/available-captains`
- **Frontend Leaflet Usage:**
```javascript
fetch('http://localhost:3000/captain/available-captains')
  .then(res => res.json())
  .then(captains => {
    captains.forEach(c => {
      if (c.currentLocation.lat) {
        L.marker([c.currentLocation.lat, c.currentLocation.lng], { icon: carIcon })
          .addTo(map)
          .bindPopup(`Captain: ${c.name}`);
      }
    });
  });
```

---

#### B. Captain Pushes Live GPS Updates
When the captain is driving (using browser `navigator.geolocation.watchPosition`):
- **Endpoint:** `PATCH http://localhost:3000/ride/<RIDE_ID>/location`
- **Header:** `Authorization: Bearer <CAPTAIN_TOKEN>`
- **Body:**
```json
{
  "lat": 28.6250,
  "lng": 77.2200,
  "heading": 90
}
```

---

#### C. Rider Polls Live Ride Map Tracking
The rider app polls this every 2–3 seconds to update the map:
- **Endpoint:** `GET http://localhost:3000/ride/<RIDE_ID>/live-tracking`
- **Header:** `Authorization: Bearer <USER_TOKEN>`
- **Response:**
```json
{
  "rideId": "6addf23cf2f5ad20a2093786",
  "status": "accepted",
  "pickup": {
    "address": "Connaught Place",
    "lat": 28.6315,
    "lng": 77.2167
  },
  "destination": {
    "address": "India Gate",
    "lat": 28.6129,
    "lng": 77.2295
  },
  "captainLocation": {
    "lat": 28.6250,
    "lng": 77.2200,
    "heading": 90,
    "updatedAt": "2026-10-25T12:12:44.474Z"
  },
  "captainId": "6addf23b9c6f7733708b5e15",
  "fare": 120
}
```

---

### Frontend Engineer Cheat-Sheet (Leaflet.js Implementation Example)

Share this snippet with your frontend engineer:

```javascript
// 1. Initialize Map
const map = L.map('map').setView([28.6139, 77.2090], 13);
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);

let captainMarker = null;

// 2. Poll live tracking endpoint every 3 seconds
setInterval(async () => {
  const res = await fetch(`http://localhost:3000/ride/${rideId}/live-tracking`, {
    headers: { 'Authorization': `Bearer ${userToken}` }
  });
  const data = await res.json();

  // Plot pickup & destination once
  if (!window.markersAdded) {
    L.marker([data.pickup.lat, data.pickup.lng]).addTo(map).bindPopup("Pickup");
    L.marker([data.destination.lat, data.destination.lng]).addTo(map).bindPopup("Destination");
    window.markersAdded = true;
  }

  // Smoothly move captain icon on map
  if (data.captainLocation && data.captainLocation.lat) {
    const coords = [data.captainLocation.lat, data.captainLocation.lng];
    if (!captainMarker) {
      captainMarker = L.marker(coords).addTo(map).bindPopup("Captain");
    } else {
      captainMarker.setLatLng(coords);
    }
  }
}, 3000);
```