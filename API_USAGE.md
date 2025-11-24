# API Usage Summary

## Currently Used APIs

### 1. **Nominatim API** (OpenStreetMap)
- **File:** `server.js`
- **Line:** ~208-270
- **Function:** `findPlaces()`
- **Purpose:** Search for tourist attractions and points of interest by location/city name
- **Endpoint:** `https://nominatim.openstreetmap.org/search.php`
- **Method:** GET
- **Usage:** Multiple queries with different phrases to find attractions
```
GET https://nominatim.openstreetmap.org/search.php?q=tourist+attraction+in+San+Francisco&format=jsonv2&limit=5
```

### 2. **Overpass API** (OpenStreetMap)
- **File:** `server.js`
- **Lines:** ~167-202, ~240-265
- **Function:** `findPlacesAroundCoords()`
- **Purpose:** Query points of interest around specific coordinates or within a city
- **Endpoint:** `https://overpass-api.de/api/interpreter`
- **Method:** POST
- **Usage:** OverpassQL queries to find tourism sites, museums, galleries, etc.
```
POST https://overpass-api.de/api/interpreter
Data: [out:json][timeout:25]; (node["tourism"](around:1200,37.7749,-122.4194); ...);
```

### 3. **Yelp API** (NEW)
- **File:** `server.js`
- **Lines:** ~90-125
- **Function:** `searchYelp()`
- **Purpose:** Search for restaurants, cafes, and dining recommendations
- **Endpoint:** `https://api.yelp.com/v3/businesses/search`
- **Method:** GET
- **Authentication:** Bearer token in Authorization header
- **Rate Limit:** 5,000 calls/day (free tier)
- **Setup:** Sign up at https://www.yelp.com/developers
- **Usage Example:**
```javascript
const results = await searchYelp('Italian restaurants', 'San Francisco', 5);
```
- **Environment Variable:** `YELP_API_KEY`
- **Features:** Returns business name, rating, review count, phone, address, URL, image

### 4. **Eventbrite API** (NEW)
- **File:** `server.js`
- **Lines:** ~127-185
- **Function:** `searchEventbrite()`
- **Purpose:** Search for events, concerts, exhibitions, and conferences in a city
- **Endpoint:** `https://www.eventbriteapi.com/v3/events/search`
- **Method:** GET
- **Authentication:** Bearer token in Authorization header
- **Rate Limit:** 1,000 requests/hour (free tier)
- **Setup:** Sign up at https://www.eventbrite.com/platform/api
- **Usage Example:**
```javascript
const events = await searchEventbrite('concerts', 'San Francisco', 5);
```
- **Environment Variable:** `EVENTBRITE_API_KEY`
- **Features:** Returns event name, start/end time, location, description, URL

### 5. **Internal API - /api/message**
- **File:** `index.html`, `preview.html`
- **Line:** ~309 (in sendMessage function)
- **Purpose:** Main chatbot endpoint - sends user messages and receives bot responses
- **Endpoint:** `http://localhost:3000/api/message`
- **Method:** POST
- **Payload:**
```json
{
  "sessionId": "session-xxx",
  "message": "Find attractions near San Francisco",
  "consentLocation": false,
  "coords": {"lat": "37.7749", "lon": "-122.4194"}
}
```

### 6. **Internal API - /api/health**
- **File:** `server.js`
- **Line:** ~420
- **Purpose:** Health check endpoint for server status
- **Endpoint:** `http://localhost:3000/api/health`
- **Method:** GET

---

## File Breakdown - Where APIs Are Used

### **server.js** (Main API Implementation)
| Line | API | Function | Purpose |
|------|-----|----------|---------|
| 7 | node-fetch | Import | HTTP requests library |
| 112-152 | Generic | fetchWithRetry() | Helper for all API calls with retry logic |
| 90-125 | Yelp | searchYelp() | Restaurant/dining search (NEW) |
| 127-185 | Eventbrite | searchEventbrite() | Event/concert search (NEW) |
| 167-202 | Overpass | findPlacesAroundCoords() | POI lookup by coordinates |
| 207-270 | Nominatim | findPlaces() | Location search for attractions |
| 240-265 | Overpass | Fallback query | Secondary lookup for city-based queries |
| 339-413 | Internal | /api/message endpoint | Main chatbot API (updated with Yelp/Eventbrite logic) |
| 415-417 | Internal | /api/health endpoint | Health check API |

### **index.html** (Frontend API Calls)
| Line | API | Purpose |
|------|-----|---------|
| 309 | Internal /api/message | Send chat messages to server |
| 309 | Browser Geolocation API | Get user's location coordinates |

### **preview.html** (Frontend API Calls)
| Line | API | Purpose |
|------|-----|---------|
| 309 | Internal /api/message | Send chat messages to server |
| 309 | Browser Geolocation API | Get user's location coordinates |

---

## External Libraries Used

- **express** - Web framework for Node.js
- **cors** - Enable CORS for cross-origin requests
- **body-parser** - Parse JSON request bodies
- **node-fetch** - Make HTTP requests to external APIs
- **fuse.js** - Fuzzy search for QnA matching

---

## Missing/Not Yet Implemented APIs

According to `missing-features-and-gaps.txt`:

1. ✅ **Yelp API** - Restaurant & business search (NOW ADDED!)
2. ✅ **Eventbrite API** - Event & concert search (NOW ADDED!)
3. ❌ **OpenAI API** - Advanced NLP and conversation
4. ❌ **Azure LUIS** - Language Understanding
5. ❌ **Azure QnA Maker** - Knowledge base management
6. ❌ **Google Translate API** - Translation (UI ready, not implemented)
7. ❌ **Database APIs** - MongoDB, PostgreSQL, Firebase
8. ❌ **Twilio** - SMS notifications
9. ❌ **SendGrid** - Email notifications
10. ❌ **Weather API** - OpenWeather, WeatherAPI
11. ❌ **Payment APIs** - Stripe, PayPal
12. ❌ **Booking APIs** - Restaurant, hotel reservations

---

## API Rate Limits & Handling

- **Nominatim:** Respects rate limits (1 request/second recommended)
- **Overpass:** Rate limit: 4 concurrent requests
- **Retry Logic:** fetchWithRetry() implements exponential backoff (600ms, 1200ms, 1800ms)
- **Timeout:** 4 seconds per request

---

## Environment Variables Needed (Future)

```
# Free Tier APIs (Now Integrated)
YELP_API_KEY=your_yelp_api_key
EVENTBRITE_API_KEY=your_eventbrite_api_key

# Email & SMS (Added)
EMAIL_HOST=sandbox.smtp.mailtrap.io
EMAIL_PORT=2525
EMAIL_USER=your_mailtrap_user
EMAIL_PASS=your_mailtrap_password
EMAIL_FROM=concierge@hotelcityque.com
HF_API_KEY=your_hugging_face_token

# Future APIs
OPENAI_API_KEY=your_key
GOOGLE_TRANSLATE_API_KEY=your_key
OPENWEATHER_API_KEY=your_key
MONGODB_URI=your_connection_string
TWILIO_ACCOUNT_SID=your_sid
TWILIO_AUTH_TOKEN=your_token
```

---

## Next Steps

To add more APIs:

1. Install required npm packages
2. Add environment variables to `.env` file
3. Create new functions in `server.js`
4. Add new endpoints to `/api/*`
5. Update `index.html` to call new endpoints
6. Test and handle errors

**Recommended Next APIs:** Google Translate (UI ready!), Weather API, Payment processing

---

## Setup Instructions for New APIs

### **Yelp API Setup**
1. Go to https://www.yelp.com/developers
2. Sign up for a free account
3. Create a new app to get API key
4. Add to `.env` file:
   ```
   YELP_API_KEY=your_api_key_here
   ```
5. Restart server: `npm start`
6. Try asking: "Find Italian restaurants near San Francisco"

### **Eventbrite API Setup**
1. Go to https://www.eventbrite.com/platform/api
2. Sign up for a free account
3. Create API token in account settings
4. Add to `.env` file:
   ```
   EVENTBRITE_API_KEY=your_api_key_here
   ```
5. Restart server: `npm start`
6. Try asking: "What events are happening in San Francisco?"

---

## Recently Added (v2.1)

✅ **Yelp API Integration** - Search for restaurants, cafes, and businesses with ratings and reviews
✅ **Eventbrite API Integration** - Search for events, concerts, exhibitions, and conferences  
✅ **Enhanced Intent Detection** - Dining intent now triggers Yelp searches automatically
✅ **Enhanced Local Attractions** - Event searches integrated into attractions finder
