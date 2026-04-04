# API Endpoints Documentation

## Table of Contents
1. [Writer Statistics Endpoint](#writer-statistics-endpoint)
2. [Detailed Tickets Endpoint](#detailed-tickets-endpoint)
3. [Game Types Endpoint](#game-types-endpoint)
4. [Today's Sales Endpoint](#todays-sales-endpoint)
5. [Today's Top Ups Endpoint](#todays-top-ups-endpoint)
6. [Writer Activity Endpoint](#writer-activity-endpoint)
7. [Top-Up Statistics Endpoint](#top-up-statistics-endpoint)
8. [Winning Statistics Endpoint](#winning-statistics-endpoint)
9. [Best & Worst Performance Endpoint](#best--worst-performance-endpoint)
10. [YTD Retention Rate Endpoint](#ytd-retention-rate-endpoint)
11. [Top 10 Writers Endpoint](#top-10-writers-endpoint)

---

## Writer Statistics Endpoint

### Overview
Returns comprehensive writer statistics including total sales, stake counts, and topup information. Perfect for creating leaderboards and performance dashboards.

### Request

**Method:** `GET`

**Route:** `/api/v1/writers/statistics/`

**Base URL:** `https://onassismystrocore-production.up.railway.app/api/v1/writers/statistics/`

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
      },
      {
        "sales": "GHS 445.50",
        "total_stakes": "380",
        "topup": "GHS 200.00",
        "writer": {
          "id": "15",
          "name": "John Smith",
          "profileImage": null,
          "online": false,
          "lastSeen": "2026-04-02 10:15:30",
          "contact": {
            "email": "john@example.com",
            "phone": "+233501234567"
          }
        }
      }
    ]
  }
}
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `data.totalwriterFloat` | string | Total sales across all writers (formatted with currency) |
| `data.totalwriters` | string | Count of writers in the system |
| `data.writers` | array | Array of individual writer statistics (sorted by sales descending) |
| `writers[].sales` | string | Writer's total sales (formatted with GHS currency) |
| `writers[].total_stakes` | string | Count of stakes/lines created by writer |
| `writers[].topup` | string | Total topup amount received (formatted with GHS currency) |
| `writers[].writer.id` | string | Writer's unique ID (human-readable) |
| `writers[].writer.name` | string | Writer's full name |
| `writers[].writer.profileImage` | null/string | URL to writer's profile photo (null if not set) |
| `writers[].writer.online` | boolean | Current online status |
| `writers[].writer.lastSeen` | string | Last activity timestamp (YYYY-MM-DD HH:MM:SS) |
| `writers[].writer.contact.email` | string/null | Writer's email address |
| `writers[].writer.contact.phone` | string | Writer's phone number in E.164 format |

### Postman Example

1. **Login:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
Body:
{
  "email": "operator@example.com",
  "password": "password"
}
```

2. **Get Writer Statistics:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/writers/statistics/
Headers:
  Authorization: Bearer <access_token>
```

### cURL Example

```bash
# Get access token
TOKEN=$(curl -X POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/ \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"pass"}' \
  | jq -r '.access')

# Get writer statistics
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/writers/statistics/ \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json"
```

---

## Detailed Tickets Endpoint

### Overview
Returns comprehensive ticket and stake information with all related data (game type, play type, writer details). Ideal for detailed transaction reporting and analysis.

### Request

**Method:** `GET`

**Route:** `/api/v1/sales/tickets/detailed_list/`

**Base URL:** `https://onassismystrocore-production.up.railway.app/api/v1/sales/tickets/detailed_list/`

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
  "data": [
    {
      "ticket_no": "108003562026040210493962241",
      "stakes": [
        {
          "stake_id": "550e8400-e29b-41d4-a716-446655440000",
          "created_at": "2026-04-02 10:52:27",
          "game": {
            "id": "1",
            "name": "Morning VAG",
            "code": "MORNING_VAG"
          },
          "event_id": 1,
          "event": "Morning VAG - April 02, 2026",
          "play_group": "Direct",
          "play": "Direct 2 (2 Sure)",
          "numbers": "5,10,15,20",
          "stake_amount": "0.50",
          "original_numbers": "5,10,15,20",
          "player_phone": "+233501234567",
          "stake_status": "ACTIVE",
          "writer": {
            "id": "1",
            "name": "John Doe",
            "phone": "+233501234567"
          }
        },
        {
          "stake_id": "550e8400-e29b-41d4-a716-446655440001",
          "created_at": "2026-04-02 10:52:27",
          "game": {
            "id": "2",
            "name": "Noon Rush",
            "code": "NOONRUSH"
          },
          "event_id": 2,
          "event": "Noon Rush - April 02, 2026",
          "play_group": "Perm",
          "play": "Perm 2",
          "numbers": "1,2,3,4,5",
          "stake_amount": "1.00",
          "original_numbers": "1,2,3,4,5",
          "player_phone": "+233501234567",
          "stake_status": "ACTIVE",
          "writer": {
            "id": "1",
            "name": "John Doe",
            "phone": "+233501234567"
          }
        }
      ]
    }
  ]
}
```

### Response Field Descriptions

#### Ticket Level
| Field | Type | Description |
|-------|------|-------------|
| `data[].ticket_no` | string | Unique system-generated ticket number |
| `data[].stakes` | array | Array of all stakes on this ticket |

#### Stake Level
| Field | Type | Description |
|-------|------|-------------|
| `stakes[].stake_id` | UUID | Unique identifier for the stake |
| `stakes[].created_at` | string | When stake was created (YYYY-MM-DD HH:MM:SS) |
| `stakes[].game.id` | string | Game type UUID |
| `stakes[].game.name` | string | Game type name (e.g., "Morning VAG", "Noon Rush") |
| `stakes[].game.code` | string | Game type code (e.g., "MORNING_VAG") |
| `stakes[].event_id` | integer | Draw event ID |
| `stakes[].event` | string | Draw event name and date |
| `stakes[].play_group` | string | Play group: "Direct", "Perm", "Banker to All", "Banker Against" |
| `stakes[].play` | string | Play type name (e.g., "Direct 2 (2 Sure)") |
| `stakes[].numbers` | string | Comma-separated selected numbers |
| `stakes[].stake_amount` | string | Per-line/unit stake amount (GHS) |
| `stakes[].original_numbers` | string | Original numbers in display format |
| `stakes[].player_phone` | string | Player phone (E.164 format) |
| `stakes[].stake_status` | string | Status: ACTIVE, WON, LOST, CLAIMED, CANCELLED, EXPIRED |
| `stakes[].writer.id` | string | Writer's human-readable ID |
| `stakes[].writer.name` | string | Writer's full name |
| `stakes[].writer.phone` | string | Writer's contact phone |

### Query Parameters

```
GET /api/v1/sales/tickets/detailed_list/?status=active
GET /api/v1/sales/tickets/detailed_list/?ticket_no=108003562026040210493962241
GET /api/v1/sales/tickets/detailed_list/?player_phone=%2B233501234567
```

### Postman Example

1. **Login:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
Body:
{
  "email": "user@example.com",
  "password": "password"
}
```

2. **Get Detailed Tickets:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/sales/tickets/detailed_list/
Headers:
  Authorization: Bearer <access_token>
```

### cURL Examples

**Get all tickets with details:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/sales/tickets/detailed_list/" \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json"
```

**Filter by ticket number:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/sales/tickets/detailed_list/?ticket_no=108003562026040210493962241" \
  -H "Authorization: Bearer TOKEN"
```

**Filter by status:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/sales/tickets/detailed_list/?status=won" \
  -H "Authorization: Bearer TOKEN"
```


---

## Game Types Endpoint

### Overview
Returns a list of all available game types with their configuration details. Essential for understanding the games available in the system

### Request

**Method:** `GET`

**Route:** `/api/v1/games/types/`

**Base URL:** `https://onassismystrocore-production.up.railway.app/api/v1/games/types/`

**Authentication:** Required (Bearer Token)

**Headers:**
```
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Response Format

**Status Code:** `200 OK`

```json
[
  {
    "id": "1",
    "name": "Morning VAG",
    "code": "MORNING_VAG",
    "description": "Morning Variation Game",
    "number_pool": "1-90",
    "numbers_drawn": "5",
    "allow_sunday_stake": true,
    "sales_open_time": "06:00:00",
    "sales_close_time": "09:45:00",
    "is_active": true,
    "created_at": "2026-04-02 08:00:00"
  },
  {
    "id": "2",
    "name": "Noon Rush",
    "code": "NOONRUSH",
    "description": "Midday Variation Game",
    "number_pool": "1-90",
    "numbers_drawn": "5",
    "allow_sunday_stake": true,
    "sales_open_time": "11:00:00",
    "sales_close_time": "12:45:00",
    "is_active": true,
    "created_at": "2026-04-02 08:00:00"
  },
  {
    "id": "3",
    "name": "Original Game",
    "code": "ORIGINAL",
    "description": "Evening Variation Game",
    "number_pool": "1-90",
    "numbers_drawn": "5",
    "allow_sunday_stake": true,
    "sales_open_time": "17:00:00",
    "sales_close_time": "19:45:00",
    "is_active": true,
    "created_at": "2026-04-02 08:00:00"
  }
]
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `[].id` | string | Unique identifier for the game type |
| `[].name` | string | Display name of the game (e.g., "Morning VAG", "Noon Rush") |
| `[].code` | string | System code for the game (e.g., "MORNING_VAG", "NOONRUSH") |
| `[].description` | string | Human-readable description of the game |
| `[].number_pool` | string | Range of numbers available for selection (e.g., "1-90") |
| `[].numbers_drawn` | string | Number of winning numbers drawn |
| `[].allow_sunday_stake` | boolean | Whether stakes are allowed on Sundays |
| `[].sales_open_time` | string | Time when sales window opens (HH:MM:SS) |
| `[].sales_close_time` | string | Time when sales window closes (HH:MM:SS) |
| `[].is_active` | boolean | Whether the game is currently active |
| `[].created_at` | string | When the game was created (YYYY-MM-DD HH:MM:SS) |

### Query Parameters

```
GET /api/v1/games/types/?is_active=true
GET /api/v1/games/types/?code=MORNING_VAG
```

| Parameter | Type | Description |
|-----------|------|-------------|
| `is_active` | boolean | Filter by active status (true/false) |
| `code` | string | Filter by game code |

### Postman Example

1. **Login:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
Body:
{
  "email": "writer@example.com",
  "password": "password"
}
```

2. **Get Game Types:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/games/types/
Headers:
  Authorization: Bearer <access_token>
```

### cURL Examples

**Get all game types:**
```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/games/types/ \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json"
```

**Filter by active status:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/games/types/?is_active=true" \
  -H "Authorization: Bearer TOKEN"
```

**Filter by game code:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/games/types/?code=MORNING_VAG" \
  -H "Authorization: Bearer TOKEN"
```


---

## Today's Sales Endpoint

### Endpoint: Get Today's Total Sales

**Route:** `GET /api/v1/sales/tickets/today_sales/`

**Description:** Returns the total sales amount and ticket count for the current day.

**Authentication:** Required (Bearer Token)

**Permissions:** `IsOperatorOrAbove` (operators and admins only)

### Response Format

**Status Code:** `200 OK`

```json
{
  "date": "2026-04-02",
  "total_sales": 20322.10,
  "ticket_count": 200,
  "currency": "GHS"
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `date` | string (ISO 8601) | The date for which sales are reported (always today's date) |
| `total_sales` | float | Sum of all ticket amounts sold today in GHS |
| `ticket_count` | integer | Number of tickets sold today |
| `currency` | string | Currency code (always "GHS") |

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/sales/tickets/today_sales/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

---

## Common Response Errors

### 401 Unauthorized
```json
{
  "detail": "Authentication credentials were not provided."
}
```
**Solution**: Ensure Authorization header includes valid Bearer token

### 403 Forbidden
```json
{
  "detail": "You do not have permission to perform this action."
}
```
**Solution**: User role doesn't have permission for this endpoint

### 404 Not Found
```json
{
  "detail": "Not found."
}
```
**Solution**: Resource doesn't exist or endpoint path is incorrect

---

## Authentication

All endpoints require JWT token authentication:

1. **Get Token:**
```
POST /api/v1/auth/login/
Body: {"email": "user@example.com", "password": "password"}
Response: {"access": "token...", "refresh": "token..."}
```

2. **Use Token:**
```
Header: Authorization: Bearer <access_token>
```

3. **Refresh Token (when expired):**
```
POST /api/v1/auth/token/refresh/
Body: {"refresh": "<refresh_token>"}
Response: {"access": "new_token..."}
```

---

## Status Codes

| Code | Meaning |
|------|---------|
| 200 | OK - Request successful |
| 201 | Created - Resource created |
| 400 | Bad Request - Invalid parameters |
| 401 | Unauthorized - Missing/invalid token |
| 403 | Forbidden - Insufficient permissions |
| 404 | Not Found - Resource doesn't exist |
| 500 | Internal Server Error - Server error |

---

## Last Updated
April 2, 2026

## API Version
v1

## Base URL
`https://onassismystrocore-production.up.railway.app/api/v1/`

```json
{
  "date": "2026-03-31",
  "total_sales": 0,
  "ticket_count": 0,
  "currency": "GHS"
}
```

### Example Response (With Sales)

```json
{
  "date": "2026-03-31",
  "total_sales": 2456.75,
  "ticket_count": 42,
  "currency": "GHS"
}
```


---

## Today's Top Ups Endpoint

### Endpoint: Get Today's Total Top Ups

**Route:** `GET /api/v1/writers/today-topup/`

**Description:** Returns the total top up amount and count of top up transactions for the current day.

**Authentication:** Required (Bearer Token)

**Permissions:** `IsWriterOrAbove` (writers and above can access)

### Response Format

**Status Code:** `200 OK`

```json
{
  "date": "2026-04-02",
  "total_topup": "GHS 12,345.60",
  "total_topup_amount": 12345.60,
  "topup_count": 15,
  "currency": "GHS"
}
```

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `date` | string (ISO 8601) | The date for which top ups are reported (always today's date) |
| `total_topup` | string | Sum of all top up amounts for today formatted with currency (GHS) and comma separators |
| `total_topup_amount` | float | Total top up amount as a numeric value for calculations |
| `topup_count` | integer | Number of top up transactions recorded today |
| `currency` | string | Currency code (always "GHS") |

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/writers/today-topup/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

### Postman Example

1. **Login:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
Body:
{
  "email": "operator@example.com",
  "password": "password"
}
```

2. **Get Today's Top Ups:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/writers/today-topup/
Headers:
  Authorization: Bearer <access_token>
```

### Response Examples

**When No Top Ups Exist:**
```json
{
  "date": "2026-04-02",
  "total_topup": "GHS 0.00",
  "total_topup_amount": 0.0,
  "topup_count": 0,
  "currency": "GHS"
}
```

**With Multiple Top Ups:**
```json
{
  "date": "2026-04-02",
  "total_topup": "GHS 50,000.00",
  "total_topup_amount": 50000.0,
  "topup_count": 25,
  "currency": "GHS"
}
```

## Writer Activity Endpoint

### Endpoint: Get Writer Activity Statistics

**Route:** `GET /api/v1/writers/active-writer-daily-stats/`

**Description:** Returns historical writer activity data including total writers and active writers (those who made sales) for each day in the specified period. Useful for tracking network growth and engagement trends.

**Authentication:** Required (Bearer Token)

**Permissions:** `IsOperatorOrAbove` (operators and admins only)

### Query Parameters

| Parameter | Type | Default | Range | Description |
|-----------|------|---------|-------|-------------|
| `days` | integer | 30 | 1-365 | Number of days to include in the report (last N days) |

### Response Format

**Status Code:** `200 OK`

```json
{
  "totals": {
    "total_writers": 1549,
    "active_writers": 1357
  },
  "period": {
    "start_date": "2026-03-05",
    "end_date": "2026-04-03",
    "days": 30
  },
  "days": [
    {
      "day": "2026-03-05",
      "total_writers": 1511,
      "active_writers": 697
    },
    {
      "day": "2026-03-06",
      "total_writers": 1512,
      "active_writers": 63
    },
    {
      "day": "2026-03-07",
      "total_writers": 1513,
      "active_writers": 722
    }
  ]
}
```

### Response Field Descriptions

#### Top-Level Fields
| Field | Type | Description |
|-------|------|-------------|
| `totals` | object | Aggregate statistics for the entire period |
| `period` | object | Information about the requested period |
| `days` | array | Daily breakdown of writer activity |

#### Totals Object
| Field | Type | Description |
|-------|------|-------------|
| `total_writers` | integer | Total count of all writers in the system |
| `active_writers` | integer | Count of unique writers with at least one ticket sold during the period |

#### Period Object
| Field | Type | Description |
|-------|------|-------------|
| `start_date` | string | Start date of the report (ISO 8601) |
| `end_date` | string | End date of the report (ISO 8601, usually today) |
| `days` | integer | Number of days in the report |

#### Day Object (in array)
| Field | Type | Description |
|-------|------|-------------|
| `day` | string | Date of the record (ISO 8601) |
| `total_writers` | integer | Total writers in the system on this date |
| `active_writers` | integer | Unique writers with at least one ticket sold on this date |

### Example Requests

**Last 30 days (default):**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/writers/active-writer-daily-stats/" \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

**Last 7 days:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/writers/active-writer-daily-stats/?days=7" \
  -H "Authorization: Bearer <your-jwt-token>"
```

**Last 90 days:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/writers/active-writer-daily-stats/?days=90" \
  -H "Authorization: Bearer <your-jwt-token>"
```

**Last year (365 days):**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/writers/active-writer-daily-stats/?days=365" \
  -H "Authorization: Bearer <your-jwt-token>"
```

### Postman Example

1. **Login:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
Body:
{
  "email": "operator@example.com",
  "password": "password"
}
```

2. **Get Writer Activity:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/writers/active-writer-daily-stats/
Headers:
  Authorization: Bearer <access_token>
```

---

## Top-Up Statistics Endpoint

### Endpoint: Get Historical Top-Up Statistics

**Route:** `GET /api/v1/financials/dashboard/topup-statistics/`

**Description:** Returns aggregated top-up amounts for various time periods (YTD, Last Week, Last Month, Last 3 Months). Useful for financial reporting and trend analysis.

**Authentication:** Required (Bearer Token)

**Permissions:** `IsOperatorOrAbove` (operators and admins only)

### Response Format

**Status Code:** `200 OK`

```json
{
    "ytd": {
        "label": "YTD",
        "total": "GHS 250.00",
        "total_amount": 250.0
    },
    "last_week": {
        "label": "Last Week",
        "total": "GHS 0.00",
        "total_amount": 0.0
    },
    "last_month": {
        "label": "Last Month",
        "total": "GHS 0.00",
        "total_amount": 0.0
    },
    "last_3_months": {
        "label": "Last 3 Months",
        "total": "GHS 250.00",
        "total_amount": 250.0
    }
}
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `{period}.label` | string | Human-readable period name |
| `{period}.total` | string | Total amount formatted with currency |
| `{period}.total_amount` | float | Numeric total for calculations |

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/financials/dashboard/topup-statistics/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

### Postman Example

1. **Login:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
Body:
{
  "email": "operator@example.com",
  "password": "password"
}
```

2. **Get Top-Up Statistics:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/financials/dashboard/topup-statistics/
Headers:
  Authorization: Bearer <access_token>
```

---

## Winning Statistics Endpoint

### Endpoint: Get Historical Winning Statistics

**Route:** `GET /api/v1/financials/dashboard/winning-statistics/`

**Description:** Returns aggregated winning amounts for various time periods (YTD, Last Week, Last Month, Last 3 Months). Useful for payout analysis and financial reporting.

**Authentication:** Required (Bearer Token)

**Permissions:** `IsOperatorOrAbove` (operators and admins only)

### Response Format

**Status Code:** `200 OK`

```json
{
    "ytd": {
      "label": "YTD",
      "total": "GHS 20,244,198.80",
      "total_amount": 20244198.80
    },
    "last_week": {
      "label": "Last Week",
      "total": "GHS 2,197,324.80",
      "total_amount": 2197324.80
    },
    "last_month": {
      "label": "Last Month",
      "total": "GHS 7,762,432.80",
      "total_amount": 7762432.80
    },
    "last_3_months": {
      "label": "Last 3 Months",
      "total": "GHS 20,041,399.60",
      "total_amount": 20041399.60
    }
}
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `{period}.label` | string | Human-readable period name |
| `{period}.total` | string | Total winning amount formatted with currency |
| `{period}.total_amount` | float | Numeric total for calculations |

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/financials/dashboard/winning-statistics/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

### Postman Example

1. **Login:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
Body:
{
  "email": "operator@example.com",
  "password": "password"
}
```

2. **Get Winning Statistics:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/financials/dashboard/winning-statistics/
Headers:
  Authorization: Bearer <access_token>
```

---

## Best & Worst Performance Endpoint

### Endpoint: Get Best & Worst Performing Months

**Route:** `GET /api/v1/financials/dashboard/best-worst-performance/`

**Description:** Returns the best performing month and worst performing month for the current year based on net profit (winnings - top-ups). Useful for identifying high-performing and underperforming periods.

**Authentication:** Required (Bearer Token)

**Permissions:** `IsOperatorOrAbove` (operators and admins only)

### Response Format

**Status Code:** `200 OK`

```json
{
    "best_month": {
      "month": "Mar '26",
      "performance": "+ GHS 1,102,384.74",
      "net_profit": 1102384.74,
      "topups": 0.0,
      "wins": 1102384.74
    },
    "worst_month": {
      "month": "Jan '26",
      "performance": "- GHS 673,816.38",
      "net_profit": -673816.38,
      "topups": 673816.38,
      "wins": 0.0
    }
}
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `data.best_month` | object or null | Month with highest net profit; null if no data |
| `data.worst_month` | object or null | Month with lowest net profit; null if no data |
| `best_month.month` | string | Month and year abbreviation (e.g., "Mar '26") |
| `best_month.performance` | string | Formatted net profit with +/- sign and currency |
| `best_month.net_profit` | float | Net profit amount (wins - topups) |
| `best_month.topups` | float | Total top-ups for the month |
| `best_month.wins` | float | Total winnings for the month |

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/financials/dashboard/best-worst-performance/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

### Postman Example

1. **Login:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
Body:
{
  "email": "operator@example.com",
  "password": "password"
}
```

2. **Get Best & Worst Performance:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/financials/dashboard/best-worst-performance/
Headers:
  Authorization: Bearer <access_token>
```
---

## YTD Retention Rate Endpoint

### Endpoint: Get YTD Retention Rate

**Route:** `GET /api/v1/financials/dashboard/retention-rate/`

**Description:** Returns YTD retention rate metrics including gross sales, net income (payouts), retention amount, and retention rate percentage.

**Authentication:** Required (Bearer Token)

**Permissions:** `IsOperatorOrAbove` (operators and admins only)

### Response Format

**Status Code:** `200 OK`

```json
{
  "gross_sales": 21790804.42,
  "net_income": 20244198.80,
  "retention_amount": 1546605.62,
  "retention_rate": "7.09%"
}
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `gross_sales` | float | Total winnings for YTD (all wins regardless of status) |
| `net_income` | float | Winnings claimed by players (payouts) |
| `retention_amount` | float | Amount retained = gross_sales - net_income |
| `retention_rate` | string | Retention percentage formatted as "X.XX%" |

### Calculation Method

```
Gross Sales = Sum of all wins (CLAIMED + PENDING + EXPIRED + VOIDED)
Net Income = Sum of CLAIMED wins only (money paid to players)
Retention Amount = Gross Sales - Net Income
Retention Rate = (Retention Amount / Gross Sales) × 100, formatted as "X.XX%"

```

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/financials/dashboard/retention-rate/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

### Postman Example

1. **Login:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
Body:
{
  "email": "operator@example.com",
  "password": "password"
}
```

2. **Get Retention Rate:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/financials/dashboard/retention-rate/
Headers:
  Authorization: Bearer <access_token>
```

---


## Top 10 Writers Endpoint

### Endpoint: Get Top 10 Writers Year-to-Date

**Route:** `GET /api/v1/writers/top-10-writers/`

**Description:** Returns the top 10 writers for the current year ranked by net profit (winnings - top-ups). Useful for identifying top performers, creating leaderboards, and analyzing writer productivity.

**Authentication:** Required (Bearer Token)

**Permissions:** `IsOperatorOrAbove` (operators and admins only)

### Response Format

**Status Code:** `200 OK`

```json
[
    {
      "rank": 1,
      "writer_id": 42,
      "writer_name": "Kwesi Mensah",
      "photo_url": "https://onassismystrocore-production.up.railway.app/media/writers/photos/kwesi_photo.jpg",
      "total_wins": {
        "formatted": "GHS 25,000,000.00",
        "amount": 25000000.0
      },
      "total_topups": {
        "formatted": "GHS 3,000,000.00",
        "amount": 3000000.0
      },
      "net_profit": {
        "formatted": "+ GHS 22,000,000.00",
        "amount": 22000000.0
      },
      "ticket_count": 1250
    },
    {
      "rank": 2,
      "writer_id": 23,
      "writer_name": "Prosper Owusu",
      "photo_url": "https://onassismystrocore-production.up.railway.app/media/writers/photos/prosper_photo.jpg",
      "total_wins": {
        "formatted": "GHS 18,500,000.00",
        "amount": 18500000.0
      },
      "total_topups": {
        "formatted": "GHS 2,500,000.00",
        "amount": 2500000.0
      },
      "net_profit": {
        "formatted": "+ GHS 16,000,000.00",
        "amount": 16000000.0
      },
      "ticket_count": 950
    }
]
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `rank` | integer | Position in leaderboard (1-10) |
| `writer_id` | integer | Unique writer identifier |
| `writer_name` | string | Writer's full name |
| `photo_url` | string or null | Full URL to writer's profile picture (null if not available) |
| `total_wins` | object | Total winnings for YTD |
| `total_wins.formatted` | string | Formatted amount (e.g., "GHS 25,000,000.00") |
| `total_wins.amount` | float | Numeric value for calculations |
| `total_topups` | object | Total top-ups invested YTD |
| `total_topups.formatted` | string | Formatted amount with GHS and commas |
| `total_topups.amount` | float | Numeric value for calculations |
| `net_profit` | object | Net profit (wins - topups) |
| `net_profit.formatted` | string | Formatted with sign indicator |
| `net_profit.amount` | float | Numeric value (positive or negative) |
| `ticket_count` | integer | Number of tickets sold YTD |
### Calculation Method

```
Net Profit = Total Wins - Total Top-Ups
Ranking = Sorted by Net Profit descending

Writers Included:
- Must have at least one win OR one top-up in YTD
- Ranked by net profit (highest to lowest)
- Top 10 only returned

Time Period: January 1 to present (current year only)
```

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/writers/top-10-writers/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

### Postman Example

1. **Login:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/auth/login/
Body:
{
  "email": "operator@example.com",
  "password": "password"
}
```

2. **Get Top 10 Writers:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/writers/top-10-writers/
Headers:
  Authorization: Bearer <access_token>
```
---

## Last Updated
April 3, 2026

## API Version
v1
