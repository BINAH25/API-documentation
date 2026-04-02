# API Endpoints Documentation

## Table of Contents

1. [Writer Statistics Endpoint](#writer-statistics-endpoint)
2. [Detailed Tickets Endpoint](#detailed-tickets-endpoint)
3. [Game Types Endpoint](#game-types-endpoint)
4. [Today's Sales Endpoint](#todays-sales-endpoint)
5. [Today's Top Ups Endpoint](#todays-top-ups-endpoint)

---

## Writer Statistics Endpoint

### Overview

Returns comprehensive writer statistics including total sales, stake counts, and topup information. Perfect for creating leaderboards and performance dashboards.

### Request

**Method:** `GET`

**Route:** `/api/v1/writers/statistics/`

**Base URL:**
`https://onassismystrocore-production.up.railway.app/api/v1/writers/statistics/`

**Authentication:** Required (Bearer Token)

**Headers:**

```
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Response Format

**Status Code:** `200 OK`

```json
{
  "data": {
    "totalwriterFloat": "GHS 128,198.03",
    "totalwriters": "1547",
    "writers": [
      {
        "sales": "GHS 558.00",
        "total_stakes": "520",
        "topup": "GHS 324.00",
        "writer": {
          "id": "21",
          "name": "Gloria Aballa",
          "profileImage": null,
          "online": true,
          "lastSeen": "2026-04-02 11:24:15",
          "contact": {
            "email": null,
            "phone": "0549698956"
          }
        }
      }
    ]
  }
}
```

---

## Detailed Tickets Endpoint

### Overview

Returns comprehensive ticket and stake information with all related data (game type, play type, writer details). Ideal for detailed transaction reporting and analysis.

### Request

**Method:** `GET`

**Route:** `/api/v1/sales/tickets/detailed_list/`

**Base URL:**
`https://onassismystrocore-production.up.railway.app/api/v1/sales/tickets/detailed_list/`

**Authentication:** Required (Bearer Token)

**Headers:**

```
Authorization: Bearer <access_token>
Content-Type: application/json
```

---

## Game Types Endpoint

### Overview

Returns a list of all available game types with their configuration details.

### Request

**Method:** `GET`

**Route:** `/api/v1/games/types/`

**Base URL:**
`https://onassismystrocore-production.up.railway.app/api/v1/games/types/`

**Authentication:** Required (Bearer Token)

**Headers:**

```
Authorization: Bearer <access_token>
Content-Type: application/json
```

---

## Today's Sales Endpoint

### Endpoint: Get Today's Total Sales

**Route:** `GET /api/v1/sales/tickets/today_sales/`

**Full URL:**
`https://onassismystrocore-production.up.railway.app/api/v1/sales/tickets/today_sales/`

**Description:** Returns the total sales amount and ticket count for the current day.

**Authentication:** Required (Bearer Token)

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/sales/tickets/today_sales/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

---

## Today's Top Ups Endpoint

### Endpoint: Get Today's Total Top Ups

**Route:** `GET /api/v1/writers/today-topup/`

**Full URL:**
`https://onassismystrocore-production.up.railway.app/api/v1/writers/today-topup/`

**Description:** Returns the total top up amount and count of top up transactions for the current day.

**Authentication:** Required (Bearer Token)

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/writers/today-topup/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

---

## Authentication

All endpoints require JWT token authentication:

### Get Token

```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
```

Body:

```json
{
  "email": "user@example.com",
  "password": "password"
}
```

### Use Token

```
Authorization: Bearer <access_token>
```

### Refresh Token

```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/token/refresh/
```

---

## Common Response Errors

### 401 Unauthorized

```json
{
  "detail": "Authentication credentials were not provided."
}
```

### 403 Forbidden

```json
{
  "detail": "You do not have permission to perform this action."
}
```

### 404 Not Found

```json
{
  "detail": "Not found."
}
```

---

## Status Codes

| Code | Meaning               |
| ---- | --------------------- |
| 200  | OK                    |
| 201  | Created               |
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 403  | Forbidden             |
| 404  | Not Found             |
| 500  | Internal Server Error |

---

## Base URL

```
https://onassismystrocore-production.up.railway.app/api/v1/
```

---

## Last Updated

April 2, 2026

## API Version

v1
