# Restful Booker API Testing - Postman Collection

A comprehensive Postman collection for testing the core functionality of the Restful Booker REST API. Designed for **Manual QA engineers** who want to practice API testing, validation of business logic, authorization flows, environment variables, and negative test scenarios using Postman.

---

# What's Included

## Test Folders & Scenarios

| Folder | Methods Tested | Positive Tests | Negative Tests |
|--------|---------------|----------------|----------------|
| **Health Check** | GET | 2 | - |
| **Auth** | POST | 4 | 2 |
| **Booking** | POST, GET | 10 | 8 |
| **Update Booking** | PUT | 6 | 4 |
| **Partial Update** | PATCH | 5 | 4 |
| **Delete Booking** | DELETE | 3 | 3 |
| **Search & Filters** | GET | 6 | 3 |
| **Cleanup** | DELETE, GET | 4 | - |
| **Total** | | **40** | **24** |

---

# Test Flow

The collection follows a logical API testing workflow:

```text
Health Check (/ping)
        |
        v
Create Auth Token (/auth)
        |
        v
Create Booking (/booking)
        |
        v
Get Booking by ID
        |
        v
Search Booking by Name & Date
        |
        v
Update Booking (PUT)
        |
        v
Partial Update Booking (PATCH)
        |
        v
Delete Booking
        |
        v
Verify Deleted Booking
        |
        v
Cleanup Environment Variables
```

---

# What Each Test Validates

- **Status codes** — correct HTTP response codes for success and error cases
- **Response body validation** — required fields, correct values, JSON structure
- **Business logic** — booking creation, updates, deletion, authorization
- **Negative scenarios** — invalid IDs, invalid dates, missing fields, invalid auth
- **Environment variables** — automatic saving of token and bookingId
- **Data validation** — positive price, valid dates, required fields
- **Authorization handling** — Basic Auth and token-based access
- **Response time** — critical endpoints respond within acceptable time

---

# Prerequisites

1. **Postman** — Download from https://www.postman.com/downloads/
2. **Restful Booker API** — Public demo API:
   - https://restful-booker.herokuapp.com/apidoc/index.html

---

# Quick Start

## 1. Clone the Repository

```bash
git clone <repository-url>
cd restful-booker-api-postman-tests
```

---

## 2. Import into Postman

1. Open Postman
2. Click **Import**
3. Import:
   - `collections/Restful-Booker_API_Tests.postman_collection.json`
   - `environments/Restful-Booker.postman_environment.example.json`

---

## 3. Configure Environment

Select the environment:

```text
Restful Booker API Testing Env
```

Only these variables are required initially:

| Variable | Value |
|---|---|
| host | https://restful-booker.herokuapp.com |
| username | admin |
| password | password123 |

> Important: Runtime variables such as `token` and `bookingId` are automatically generated and saved during test execution.

---

## 4. Run the Collection

### Option A — Run full collection (recommended)

1. Open Collection Runner
2. Select:
   - Collection: `Restful Booker API Testing`
   - Environment: `Restful Booker API Testing Env`
3. Run collection

---

### Option B — Run folders individually

Folders can be executed separately, but some requests depend on previously generated variables.

Example:
- `Update Booking` requires existing `bookingId`
- `Delete Booking` requires valid `token` and `bookingId`

---

### Option C — Run single requests

1. Open request
2. Click **Send**
3. View results in:
   - **Test Results**
   - **Console**
   - **Response Body**

---

# Project Structure

```text
restful-booker-api-postman-tests/
├── README.md                          # This file
├── collections/
│   └── Restful-Booker_API_Tests.postman_collection.json   # Main test collection
├── environments/
│   └── Restful-Booker.postman_environment.example.json    # Environment variables
├── docs/
│   ├── test-cases.md                  # Detailed test case documentation
└── .gitignore
```

---

# Environment Variables Reference

| Variable | Set By | Description |
|---|---|---|
| `host` | Pre-configured | Base API URL |
| `username` | Pre-configured | API username |
| `password` | Pre-configured | API password |
| `token` | Auto (tests) | Auth token generated via `/auth` |
| `bookingId` | Auto (tests) | ID of created booking |
| `firstname` | Auto/User | Test booking firstname |
| `lastname` | Auto/User | Test booking lastname |
| `UpdFirstname` | Auto/User | Updated firstname |
| `UpdLastname` | Auto/User | Updated lastname |

---

# Running Order & Dependencies

The collection is designed to run sequentially:

1. **Health Check**
2. **Auth**
3. **Create Booking**
4. **Get Booking**
5. **Search & Filters**
6. **Update Booking**
7. **Partial Update**
8. **Delete Booking**
9. **Verify Deleted Booking**
10. **Cleanup**

> Negative tests are independent and can be executed separately.

---

# Cleanup

The **Cleanup** folder:

- Deletes created test booking
- Verifies booking deletion
- Clears runtime environment variables

Automatically cleared variables:

```text
token
bookingId
firstname
lastname
UpdFirstname
UpdLastname
```

Base variables (`host`, `username`, `password`) remain unchanged.

---

# Negative Testing Coverage

Examples of covered negative scenarios:

- Missing required fields
- Invalid booking dates
- Negative totalprice
- Invalid booking ID
- Unauthorized PUT/PATCH/DELETE requests
- Invalid search filters
- Invalid auth credentials

---

# Security Notes

This repository does NOT include:

- real personal credentials
- runtime tokens
- local Postman environments

Only environment templates are committed.

Runtime variables are automatically generated during collection execution.

---

# Troubleshooting

| Issue | Solution |
|---|---|
| `403 Forbidden` | Missing authorization token or Basic Auth |
| `404 Not Found` | Invalid or deleted bookingId |
| `405 Method Not Allowed` | Invalid endpoint or unsupported method |
| Empty environment variables | Run Auth/Create Booking first |
| Empty search results | Booking may not match filter parameters |

---

# API Documentation

- https://restful-booker.herokuapp.com/apidoc/index.html

---

# Skills Demonstrated

- REST API Testing
- Postman Collections
- Environment Variables
- JavaScript Test Scripts
- Positive & Negative Testing
- Authorization Testing
- CRUD Operations
- JSON Validation
- API Cleanup Strategy
- Bug Detection & Validation
