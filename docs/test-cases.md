# Restful Booker API Testing - Detailed Test Cases

## TC-001: Health Check

### TC-001.1: Verify API is accessible
- **Method:** GET `/ping`
- **Expected:** 201 Created
- **Validates:** API connectivity and availability

### TC-001.2: Verify response time is acceptable
- **Method:** GET `/ping`
- **Expected:** Response time below 5000ms
- **Validates:** Basic API performance

---

## TC-002: Authentication

### Positive Tests

#### TC-002.1: Generate auth token with valid credentials
- **Method:** POST `/auth`
- **Body:** `username`, `password`
- **Expected:** 200 OK, token returned
- **Validates:** Successful authentication flow

#### TC-002.2: Verify token exists in response
- **Method:** POST `/auth`
- **Expected:** Response contains `token`
- **Validates:** Token generation

#### TC-002.3: Save token to environment
- **Method:** POST `/auth`
- **Expected:** `token` environment variable is created
- **Validates:** Environment variable handling

#### TC-002.4: Verify token is a string
- **Method:** POST `/auth`
- **Expected:** Token value is string type
- **Validates:** Response datatype validation

### Negative Tests

#### TC-002.5: Invalid password returns auth failure
- **Method:** POST `/auth`
- **Body:** Invalid password
- **Expected:** 200 OK with `reason: Bad credentials`
- **Validates:** Invalid credential handling

#### TC-002.6: Missing credentials
- **Method:** POST `/auth`
- **Body:** Empty body
- **Expected:** 200 OK with auth failure response
- **Validates:** Required field validation

---

## TC-003: Booking Creation

### Positive Tests

#### TC-003.1: Create booking with valid data
- **Method:** POST `/booking`
- **Expected:** 200 OK, booking created
- **Validates:** Booking creation functionality

#### TC-003.2: Verify bookingId exists
- **Method:** POST `/booking`
- **Expected:** Response contains `bookingid`
- **Validates:** Booking identifier generation

#### TC-003.3: Verify firstname matches request
- **Method:** POST `/booking`
- **Expected:** Response firstname equals request firstname
- **Validates:** Request/response consistency

#### TC-003.4: Verify lastname matches request
- **Method:** POST `/booking`
- **Expected:** Response lastname equals request lastname
- **Validates:** Request/response consistency

#### TC-003.5: Verify totalprice is positive
- **Method:** POST `/booking`
- **Expected:** `totalprice > 0`
- **Validates:** Positive price validation

#### TC-003.6: Verify bookingdates object exists
- **Method:** POST `/booking`
- **Expected:** Response contains `bookingdates`
- **Validates:** Nested object validation

#### TC-003.7: Verify checkin and checkout exist
- **Method:** POST `/booking`
- **Expected:** Response contains `checkin` and `checkout`
- **Validates:** Date field validation

#### TC-003.8: Save bookingId to environment
- **Method:** POST `/booking`
- **Expected:** `bookingId` environment variable created
- **Validates:** Runtime variable handling

#### TC-003.9: Verify response schema
- **Method:** POST `/booking`
- **Expected:** Response contains required fields
- **Validates:** API response structure

#### TC-003.10: Verify response time
- **Method:** POST `/booking`
- **Expected:** Response time below 5000ms
- **Validates:** API performance

### Negative Tests

#### TC-003.11: Create booking without firstname
- **Method:** POST `/booking`
- **Expected:** API should reject request or create invalid booking
- **Validates:** Required field validation

#### TC-003.12: Create booking without lastname
- **Method:** POST `/booking`
- **Expected:** Validation failure or API bug detection
- **Validates:** Missing field handling

#### TC-003.13: Create booking with negative totalprice
- **Method:** POST `/booking`
- **Expected:** API should reject negative value
- **Validates:** Business logic validation

#### TC-003.14: Create booking with invalid checkin date
- **Method:** POST `/booking`
- **Expected:** API should reject invalid date
- **Validates:** Date validation

#### TC-003.15: Create booking with checkout earlier than checkin
- **Method:** POST `/booking`
- **Expected:** Validation failure
- **Validates:** Booking date logic

#### TC-003.16: Create booking with invalid data types
- **Method:** POST `/booking`
- **Expected:** Validation failure
- **Validates:** Datatype validation

#### TC-003.17: Create booking with empty body
- **Method:** POST `/booking`
- **Expected:** 400/500 response
- **Validates:** Empty payload handling

#### TC-003.18: Create booking with invalid JSON
- **Method:** POST `/booking`
- **Expected:** 400 Bad Request
- **Validates:** JSON parser validation

---

## TC-004: Get Booking

### Positive Tests

#### TC-004.1: Get booking by valid ID
- **Method:** GET `/booking/{bookingId}`
- **Expected:** 200 OK
- **Validates:** Booking retrieval

#### TC-004.2: Verify booking contains required fields
- **Method:** GET `/booking/{bookingId}`
- **Expected:** Required fields exist
- **Validates:** Response structure

#### TC-004.3: Verify returned booking matches created booking
- **Method:** GET `/booking/{bookingId}`
- **Expected:** Values match original booking
- **Validates:** Data persistence

#### TC-004.4: Verify bookingdates fields exist
- **Method:** GET `/booking/{bookingId}`
- **Expected:** `checkin` and `checkout` exist
- **Validates:** Nested response validation

### Negative Tests

#### TC-004.5: Get booking with invalid ID
- **Method:** GET `/booking/000000`
- **Expected:** 404 Not Found
- **Validates:** Invalid resource handling

#### TC-004.6: Get booking with non-numeric ID
- **Method:** GET `/booking/invalid`
- **Expected:** 404/405
- **Validates:** Invalid datatype handling

---

## TC-005: Search & Filters

### Positive Tests

#### TC-005.1: Search booking by firstname
- **Method:** GET `/booking?firstname={firstname}`
- **Expected:** Response array contains bookingId
- **Validates:** Search by firstname

#### TC-005.2: Search booking by lastname
- **Method:** GET `/booking?lastname={lastname}`
- **Expected:** Booking found
- **Validates:** Search by lastname

#### TC-005.3: Search booking by fullname
- **Method:** GET `/booking?firstname={firstname}&lastname={lastname}`
- **Expected:** Matching booking returned
- **Validates:** Combined filtering

#### TC-005.4: Search booking by dates
- **Method:** GET `/booking?checkin={date}&checkout={date}`
- **Expected:** Matching booking returned
- **Validates:** Date filtering

#### TC-005.5: Verify bookingId exists in search results
- **Method:** GET `/booking`
- **Expected:** Array includes created bookingId
- **Validates:** Response array validation

#### TC-005.6: Verify response is array
- **Method:** GET `/booking`
- **Expected:** Array response
- **Validates:** API response type

### Negative Tests

#### TC-005.7: Search non-existent booking
- **Method:** GET `/booking?firstname=InvalidUser`
- **Expected:** Empty array
- **Validates:** Empty search results handling

#### TC-005.8: Search with invalid date format
- **Method:** GET `/booking?checkin=0000-00-00`
- **Expected:** Empty response or validation failure
- **Validates:** Invalid filter handling

#### TC-005.9: Search with random parameters
- **Method:** GET `/booking?abc=123`
- **Expected:** Empty response or ignored params
- **Validates:** Unknown parameter handling

---

## TC-006: Update Booking (PUT)

### Positive Tests

#### TC-006.1: Update booking with valid auth
- **Method:** PUT `/booking/{bookingId}`
- **Expected:** 200 OK
- **Validates:** Full update functionality

#### TC-006.2: Verify updated firstname
- **Method:** PUT `/booking/{bookingId}`
- **Expected:** Updated firstname returned
- **Validates:** Field update persistence

#### TC-006.3: Verify updated lastname
- **Method:** PUT `/booking/{bookingId}`
- **Expected:** Updated lastname returned
- **Validates:** Field update persistence

#### TC-006.4: Verify updated totalprice
- **Method:** PUT `/booking/{bookingId}`
- **Expected:** Updated price returned
- **Validates:** Numeric field updates

#### TC-006.5: Verify updated dates
- **Method:** PUT `/booking/{bookingId}`
- **Expected:** Updated dates returned
- **Validates:** Date updates

#### TC-006.6: Verify response schema after update
- **Method:** PUT `/booking/{bookingId}`
- **Expected:** Response contains required fields
- **Validates:** Response consistency

### Negative Tests

#### TC-006.7: PUT without auth
- **Method:** PUT `/booking/{bookingId}`
- **Expected:** 403 Forbidden
- **Validates:** Authorization enforcement

#### TC-006.8: PUT with invalid bookingId
- **Method:** PUT `/booking/000000`
- **Expected:** 405 Method Not Allowed
- **Validates:** Invalid resource handling

#### TC-006.9: PUT with invalid token
- **Method:** PUT `/booking/{bookingId}`
- **Expected:** 403 Forbidden
- **Validates:** Invalid auth handling

#### TC-006.10: PUT with invalid request body
- **Method:** PUT `/booking/{bookingId}`
- **Expected:** Validation failure
- **Validates:** Payload validation

---

## TC-007: Partial Update (PATCH)

### Positive Tests

#### TC-007.1: Update firstname only
- **Method:** PATCH `/booking/{bookingId}`
- **Expected:** Updated firstname
- **Validates:** Partial update functionality

#### TC-007.2: Update lastname only
- **Method:** PATCH `/booking/{bookingId}`
- **Expected:** Updated lastname
- **Validates:** Selective updates

#### TC-007.3: Verify unchanged fields remain unchanged
- **Method:** PATCH `/booking/{bookingId}`
- **Expected:** Other fields preserved
- **Validates:** Partial update logic

#### TC-007.4: PATCH with valid auth
- **Method:** PATCH `/booking/{bookingId}`
- **Expected:** 200 OK
- **Validates:** Authorized partial updates

#### TC-007.5: Verify response schema
- **Method:** PATCH `/booking/{bookingId}`
- **Expected:** Valid response structure
- **Validates:** Response integrity

### Negative Tests

#### TC-007.6: PATCH without auth
- **Method:** PATCH `/booking/{bookingId}`
- **Expected:** 403 Forbidden
- **Validates:** Authorization enforcement

#### TC-007.7: PATCH invalid bookingId
- **Method:** PATCH `/booking/000000`
- **Expected:** 405 Method Not Allowed
- **Validates:** Invalid resource handling

#### TC-007.8: PATCH with invalid field datatype
- **Method:** PATCH `/booking/{bookingId}`
- **Expected:** Validation failure
- **Validates:** Datatype validation

#### TC-007.9: PATCH with empty body
- **Method:** PATCH `/booking/{bookingId}`
- **Expected:** No update or validation failure
- **Validates:** Empty payload handling

---

## TC-008: Delete Booking

### Positive Tests

#### TC-008.1: Delete booking with valid auth
- **Method:** DELETE `/booking/{bookingId}`
- **Expected:** 201 Created
- **Validates:** Booking deletion

#### TC-008.2: Verify deleted booking is unavailable
- **Method:** GET `/booking/{bookingId}`
- **Expected:** 404 Not Found
- **Validates:** Resource deletion persistence

#### TC-008.3: Verify cleanup flow
- **Method:** DELETE + GET
- **Expected:** Booking fully removed
- **Validates:** End-to-end cleanup

### Negative Tests

#### TC-008.4: DELETE without auth
- **Method:** DELETE `/booking/{bookingId}`
- **Expected:** 403 Forbidden
- **Validates:** Authorization enforcement

#### TC-008.5: DELETE invalid bookingId
- **Method:** DELETE `/booking/000000`
- **Expected:** 405 Method Not Allowed
- **Validates:** Invalid resource handling

#### TC-008.6: DELETE already deleted booking
- **Method:** DELETE `/booking/{bookingId}`
- **Expected:** 404/405
- **Validates:** Duplicate deletion handling

---

## TC-009: Cleanup

#### TC-009.1: Delete created booking
- **Method:** DELETE `/booking/{bookingId}`
- **Expected:** 201 Created
- **Validates:** Test data cleanup

#### TC-009.2: Verify booking is deleted
- **Method:** GET `/booking/{bookingId}`
- **Expected:** 404 Not Found
- **Validates:** Cleanup verification

#### TC-009.3: Clear runtime environment variables
- **Method:** GET `/ping`
- **Expected:** Variables removed from environment
- **Validates:** Environment cleanup

#### TC-009.4: Verify token variable is cleared
- **Method:** Cleanup script
- **Expected:** `token` variable undefined
- **Validates:** Sensitive data cleanup
