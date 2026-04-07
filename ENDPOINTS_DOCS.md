# API Endpoints Documentation

## Table of Contents
### Sales Page
1. [Writer Statistics Endpoint](#writer-statistics-endpoint)
2. [Detailed Tickets Endpoint](#detailed-tickets-endpoint)
3. [Game Types Endpoint](#game-types-endpoint)
4. [Today's Sales Endpoint](#todays-sales-endpoint)
5. [Today's Top Ups Endpoint](#todays-top-ups-endpoint)

### Analytics
6. [Writer Activity Endpoint](#writer-activity-endpoint)
7. [Top-Up Statistics Endpoint](#top-up-statistics-endpoint)
8. [Winning Statistics Endpoint](#winning-statistics-endpoint)
9. [Best & Worst Performance Endpoint](#best--worst-performance-endpoint)
10. [YTD Retention Rate Endpoint](#ytd-retention-rate-endpoint)
11. [Top 10 Writers Endpoint](#top-10-writers-endpoint)

### LMCs
12. [Available LMC Owners Endpoint](#available-lmc-owners-endpoint)
13. [Register LMC Endpoint](#register-lmc-endpoint)
14. [LMC Detail Cards Endpoint](#lmc-detail-cards-endpoint)
15. [LMC Writers Overview Endpoint](#lmc-writers-overview-endpoint)
16. [LMC Transactions Endpoint](#lmc-transactions-endpoint)

### Draws & Winnings
17. [Draws & Winnings Endpoint](#draws--winnings-endpoint)
18. [Draws & Winnings Table Endpoint](#draws--winnings-table-endpoint)
19. [Draw Event Tickets Endpoint](#draw-event-tickets-endpoint)

### Admin Users
20. [List Admin Users Endpoint](#list-admin-users-endpoint)
21. [Create Admin User Endpoint](#create-admin-user-endpoint)
22. [Edit Admin User Endpoint](#edit-admin-user-endpoint)
23. [Activity Logs Endpoint](#activity-logs-endpoint)

### Writer Dashboard (Admin)
24. [All Writers List Endpoint](#all-writers-list-endpoint)
25. [Writer Profile Endpoint](#writer-profile-endpoint)
26. [Writer Sales Endpoint](#writer-sales-endpoint)
27. [Writer Winnings Endpoint](#writer-winnings-endpoint)
28. [Writer Top-Ups Endpoint](#writer-top-ups-endpoint)
29. [Writer Cashouts Endpoint](#writer-cashouts-endpoint)

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

## Available LMC Owners Endpoint

### Overview
Returns a list of users with the `lmc_owner` role who are **not yet assigned** to an LMC. Useful for populating the owner dropdown when registering a new LMC.

### Request

**Method:** `GET`

**Route:** `/api/v1/auth/users/available-lmc-owners/`

**Base URL:** `https://onassismystrocore-production.up.railway.app/api/v1/auth/users/available-lmc-owners/`

**Authentication:** Required (Bearer Token)

**Permissions:** Operator or above

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
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "email": "owner@example.com",
    "first_name": "Kwame",
    "last_name": "Mensah",
    "full_name": "Kwame Mensah",
    "phone": "+233501234567",
    "role": "lmc_owner",
    "is_active": true,
    "photo": null
  }
]
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | User's unique identifier |
| `email` | string | User's email address |
| `first_name` | string | User's first name |
| `last_name` | string | User's last name |
| `full_name` | string | Computed full name |
| `phone` | string | User's phone number |
| `role` | string | Always `lmc_owner` |
| `is_active` | boolean | Account active status |
| `photo` | string/null | URL to profile photo or null |

### Notes
- Only returns users with `role=lmc_owner` who do **not** already have an LMC assigned
- Results are ordered alphabetically by first name, then last name
- Returns an empty list `[]` if all LMC owners are already assigned

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/auth/users/available-lmc-owners/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

---

## Register LMC Endpoint

### Overview
Creates a new LMC (Lotto Marketing Company) assigned to an existing `lmc_owner` user. Automatically generates a sequential LMC code (e.g. `LMC-0001`) and creates an airtime wallet for the new LMC.

### Request

**Method:** `POST`

**Route:** `/api/v1/lmc/`

**Base URL:** `https://onassismystrocore-production.up.railway.app/api/v1/lmc/`

**Authentication:** Required (Bearer Token)

**Permissions:** Operator or above

**Headers:**
```
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Request Body

```json
{
  "owner": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "address": "123 Main Street, Accra",
  "is_active": true
}
```

### Request Field Descriptions

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `owner` | UUID | Yes | UUID of an `lmc_owner` user (use Available LMC Owners endpoint to get valid IDs) |
| `address` | string | No | Physical address of the LMC |
| `is_active` | boolean | No | Whether the LMC is active (defaults to `true`) |

### Response Format

**Status Code:** `201 Created`

```json
{
  "id": "f9e8d7c6-b5a4-3210-fedc-ba9876543210",
  "code": "LMC-0025",
  "name": "Kwame Mensah",
  "phone": "+233501234567",
  "address": "123 Main Street, Accra",
  "owner": {
    "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
    "full_name": "Kwame Mensah",
    "phone": "+233501234567",
    "photo": null
  },
  "is_active": true,
  "created_at": "2026-04-05T12:00:00Z",
  "updated_at": "2026-04-05T12:00:00Z"
}
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | LMC's unique identifier |
| `code` | string | Auto-generated sequential code (e.g. `LMC-0025`) |
| `name` | string | Owner's full name |
| `phone` | string | Owner's phone number |
| `address` | string | LMC physical address |
| `owner` | object | Owner user summary |
| `is_active` | boolean | Whether the LMC is active |
| `created_at` | datetime | Creation timestamp |
| `updated_at` | datetime | Last update timestamp |

### Error Responses

| Status | Condition |
|--------|-----------|
| `400 Bad Request` | Missing or invalid `owner` UUID |
| `400 Bad Request` | Owner already assigned to another LMC (unique constraint) |
| `401 Unauthorized` | Missing or invalid token |
| `403 Forbidden` | User role is below Operator |

### Workflow: Register a New LMC

1. **Get available owners:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/auth/users/available-lmc-owners/
```

2. **Pick an owner UUID from the response, then register:**
```
POST https://onassismystrocore-production.up.railway.app/api/v1/lmc/
Body:
{
  "owner": "<owner-uuid-from-step-1>",
  "address": "123 Main Street, Accra"
}
```

---

## LMC Detail Cards Endpoint

### Overview
Returns all LMCs with an operational snapshot (live writer counts + POS data) and financial aggregates for the current month. Designed for the LMC list/dashboard view where each LMC is shown as a card.

### Request

**Method:** `GET`

**Route:** `/api/v1/lmc/detail-cards/`

**Base URL:** `https://onassismystrocore-production.up.railway.app/api/v1/lmc/detail-cards/`

**Authentication:** Required (Bearer Token)

**Permissions:** Operator or above sees all LMCs; LMC owner sees only their own

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
    "id": "1a0dadec-9498-4a66-a51f-8345ae433c32",
    "code": "LMC-0004",
    "name": "Sallyrich Blessed Enterprise",
    "phone": "+233501234567",
    "address": "P.O. Box 123, Accra",
    "photo_url": null,
    "is_active": true,
    "operational": {
      "snapshot_date": "2026-03-01",
      "active": 10,
      "passive": 0,
      "inactive": 0,
      "recover": 0,
      "no_use": 0,
      "writers_total": 10,
      "pos_issued": 20,
      "pos_trading": 15,
      "pos_recovery": 5
    },
    "financial": {
      "wallet_balance": "1500.00",
      "monthly_topups": "5000.00",
      "monthly_sales": "12000.00",
      "monthly_commissions": "350.00"
    }
  }
]
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | LMC unique identifier |
| `code` | string | LMC code (e.g. `LMC-0004`) |
| `name` | string | Owner's full name |
| `phone` | string | Owner's phone number |
| `address` | string | LMC physical address |
| `photo_url` | string/null | Owner's profile photo URL or null |
| `is_active` | boolean | Whether the LMC is active |
| **`operational`** | object | Live writer counts + POS from latest snapshot |
| `operational.snapshot_date` | string/null | Date of latest snapshot (null if none exists) |
| `operational.active` | integer | **Live** count of writers with status `active` |
| `operational.passive` | integer | **Live** count of writers with status `passive` |
| `operational.inactive` | integer | **Live** count of writers with status `inactive` |
| `operational.recover` | integer | **Live** count of writers with status `recover` |
| `operational.no_use` | integer | **Live** count of writers with status `no_use` |
| `operational.writers_total` | integer | **Live** total writer count |
| `operational.pos_issued` | integer | POS devices issued (from snapshot) |
| `operational.pos_trading` | integer | POS devices trading (from snapshot) |
| `operational.pos_recovery` | integer | POS devices in recovery (from snapshot) |
| **`financial`** | object | Current month financial aggregates |
| `financial.wallet_balance` | decimal | Current airtime wallet balance |
| `financial.monthly_topups` | decimal | Total top-ups given to writers this month |
| `financial.monthly_sales` | decimal | Total ticket sales this month |
| `financial.monthly_commissions` | decimal | Total commissions earned this month |

### Data Source Notes

| Field Category | Source |
|----------------|--------|
| Writer status counts (active, passive, etc.) | **Live** — queried from `Writer` table in real-time |
| POS counts (issued, trading, recovery) | **Snapshot** — from latest `LMCDailySnapshot` |
| Financial aggregates | **Live** — aggregated from current month transactions |

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/lmc/detail-cards/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

---

## LMC Writers Overview Endpoint

### Overview
Returns detailed information for a single LMC: LMC info header, YTD summary cards with contribution ratios, and a paginated/filterable writers table. Designed for the LMC detail view.

### Request

**Method:** `GET`

**Route:** `/api/v1/lmc/{id}/writers-overview/`

**Base URL:** `https://onassismystrocore-production.up.railway.app/api/v1/lmc/{id}/writers-overview/`

**Authentication:** Required (Bearer Token)

**Permissions:** Operator or above; LMC owner for their own LMC

**Headers:**
```
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `status` | string | Filter writers by status: `active`, `passive`, `inactive`, `recover`, `no_use` |
| `search` | string | Search writers by name |
| `page` | integer | Page number (default: 1) |
| `page_size` | integer | Results per page (default: 10, max: 1000) |

### Response Format

**Status Code:** `200 OK`

```json
{
  "lmc_info": {
    "name": "Sallyrich Blessed Enterprise",
    "address": "P.O. Box 123, Accra",
    "phone": "+233501234567",
    "pos_issued": 20,
    "pos_trading": 15,
    "wallet_balance": "1500.00"
  },
  "summary": {
    "ytd_sales": "45000.00",
    "ytd_topups": "12000.00",
    "ytd_winnings": "8500.00",
    "writers_count": 10,
    "ytd_sales_ratio": 15,
    "ytd_topups_ratio": 12,
    "ytd_winnings_ratio": 8,
    "writers_ratio": 5
  },
  "writers": {
    "count": 10,
    "next": "https://onassismystrocore-production.up.railway.app/api/v1/lmc/{id}/writers-overview/?page=2",
    "previous": null,
    "results": [
      {
        "id": "b2c3d4e5-f6a7-8901-bcde-f23456789012",
        "name": "Gloria Aballa",
        "contact": "+233549698956",
        "sign_up_date": "2025-06-15T09:30:00Z",
        "dop": 295,
        "dot": 42,
        "ytd_sales": "5580.00",
        "ytd_topups": "3240.00",
        "status": "active"
      }
    ]
  }
}
```

### Response Field Descriptions

#### `lmc_info` — LMC header information

| Field | Type | Source | Description |
|-------|------|--------|-------------|
| `name` | string | Live | Owner's full name |
| `address` | string | Live | LMC physical address |
| `phone` | string | Live | Owner's phone number |
| `pos_issued` | integer | Snapshot | POS devices issued (0 if no snapshot) |
| `pos_trading` | integer | Snapshot | POS devices trading (0 if no snapshot) |
| `wallet_balance` | decimal | Live | Current airtime wallet balance |

#### `summary` — YTD summary cards

| Field | Type | Description |
|-------|------|-------------|
| `ytd_sales` | decimal | Year-to-date total ticket sales for this LMC |
| `ytd_topups` | decimal | Year-to-date total top-ups for this LMC |
| `ytd_winnings` | decimal | Year-to-date total winnings for this LMC |
| `writers_count` | integer | Live count of writers belonging to this LMC |
| `ytd_sales_ratio` | integer | This LMC's sales as a % of all LMCs (0–100) |
| `ytd_topups_ratio` | integer | This LMC's top-ups as a % of all LMCs (0–100) |
| `ytd_winnings_ratio` | integer | This LMC's winnings as a % of all LMCs (0–100) |
| `writers_ratio` | integer | This LMC's writer count as a % of all writers (0–100) |

#### `writers` — Paginated writer table

| Field | Type | Description |
|-------|------|-------------|
| `count` | integer | Total number of writers (before pagination) |
| `next` | string/null | URL for the next page |
| `previous` | string/null | URL for the previous page |
| `results` | array | Array of writer row objects |

#### Writer row fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | UUID | Writer's unique identifier |
| `name` | string | Writer's full name |
| `contact` | string | Writer's phone number |
| `sign_up_date` | datetime | When the writer was created |
| `dop` | integer | Days on platform (days since sign-up) |
| `dot` | integer | Days of trading (distinct days with sales YTD) |
| `ytd_sales` | decimal | Writer's year-to-date ticket sales |
| `ytd_topups` | decimal | Writer's year-to-date top-ups received |
| `status` | string | Writer's current status (`active`, `passive`, `inactive`, `recover`, `no_use`) |

### Example Requests

**Basic request:**
```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/lmc/1a0dadec-9498-4a66-a51f-8345ae433c32/writers-overview/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json"
```

**With filters:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/lmc/1a0dadec-9498-4a66-a51f-8345ae433c32/writers-overview/?status=active&search=Gloria&page=1" \
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

2. **Get Writers Overview:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/lmc/1a0dadec-9498-4a66-a51f-8345ae433c32/writers-overview/
Headers:
  Authorization: Bearer <access_token>
```

---

## LMC Transactions Endpoint

### Overview
Returns a unified, paginated transaction ledger for a single LMC. Merges commissions (earned from writer top-ups), top-ups (LMC → writer transfers), and deposits (money into LMC wallet) into one chronological list with a running balance column. Supports tab-style filtering by transaction type, date range, and source search.

### Request

**Method:** `GET`

**Route:** `/api/v1/lmc/{id}/transactions/`

**Base URL:** `https://onassismystrocore-production.up.railway.app/api/v1/lmc/{id}/transactions/`

**Authentication:** Required (Bearer Token)

**Permissions:** Operator or above; LMC owner for their own LMC

**Headers:**
```
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Query Parameters

| Parameter | Type | Description |
|-----------|------|-------------|
| `type` | string | Filter by transaction type: `commission`, `topup`, `transfer` (maps to UI tabs: Commissions, Top-ups, Transfers). Omit for "View All". |
| `search` | string | Search by source name or phone number |
| `date_from` | string | Start date filter (YYYY-MM-DD) |
| `date_to` | string | End date filter (YYYY-MM-DD) |
| `page` | integer | Page number (default: 1) |
| `page_size` | integer | Results per page (default: 30, max: 1000) |

### UI Tab Mapping

| UI Tab | Query |
|--------|-------|
| **View All** | No `type` parameter |
| **Commissions** | `?type=commission` |
| **Top-ups** | `?type=topup` |
| **Transfers** | `?type=transfer` |

### Response Format

**Status Code:** `200 OK`

```json
{
  "count": 579,
  "next": "https://onassismystrocore-production.up.railway.app/api/v1/lmc/{id}/transactions/?page=2",
  "previous": null,
  "results": [
    {
      "date": "Sun, 05 April 2026",
      "time": "03:56 PM",
      "type": "commission",
      "source_name": "Bemah Rose",
      "source_phone": "0598195262",
      "reference": null,
      "amount": "2.10",
      "balance": "4344.71"
    },
    {
      "date": "Sun, 05 April 2026",
      "time": "03:54 PM",
      "type": "commission",
      "source_name": "Mark Owusu Ansah",
      "source_phone": "0240375694",
      "reference": null,
      "amount": "0.88",
      "balance": "4342.61"
    },
    {
      "date": "Sun, 05 April 2026",
      "time": "03:26 PM",
      "type": "topup",
      "source_name": "Simon Ackachie",
      "source_phone": "0591385282",
      "reference": "LMCXFR-A1B2C3D4E5F6",
      "amount": "50.00",
      "balance": "4339.55"
    },
    {
      "date": "Sat, 04 April 2026",
      "time": "10:30 AM",
      "type": "transfer",
      "source_name": null,
      "source_phone": "0551234567",
      "reference": "LMCDEP-XYZ789ABC123",
      "amount": "500.00",
      "balance": "4200.00"
    }
  ]
}
```

### Response Field Descriptions

| Field | Type | Description |
|-------|------|-------------|
| `date` | string | Formatted date (e.g. "Sun, 05 April 2026") |
| `time` | string | Formatted time (e.g. "03:56 PM") |
| `type` | string | Transaction type: `commission`, `topup`, or `transfer` |
| `source_name` | string/null | Writer's full name (null for deposits) |
| `source_phone` | string/null | Writer's phone or mobile money number |
| `reference` | string/null | Payment reference (null for commissions) |
| `amount` | decimal | Transaction amount in GHS |
| `balance` | decimal | Running wallet balance after this transaction |

### Transaction Types

| Type | Direction | Description |
|------|-----------|-------------|
| `commission` | **IN** (+) | Commission earned from a writer's top-up (3.5% of top-up amount) |
| `topup` | **OUT** (-) | Airtime transferred from LMC wallet to a writer |
| `transfer` | **IN** (+) | Deposit into LMC wallet (via mobile money) |

### Running Balance

The `balance` field is a running balance computed from the current wallet balance, walking backwards through the transaction history. The newest transaction shows the current wallet balance, and each older transaction shows what the balance was at that point in time.

### Notes
- Only **successful** transfers are included (pending/failed transfers are excluded)
- Transactions are sorted newest-first by `created_at`
- The balance column matches the LMC's airtime wallet balance

### Example Requests

**View All (no filter):**
```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/lmc/1a0dadec-9498-4a66-a51f-8345ae433c32/transactions/ \
  -H "Authorization: Bearer <your-jwt-token>"
```

**Commissions tab only:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/lmc/1a0dadec-9498-4a66-a51f-8345ae433c32/transactions/?type=commission" \
  -H "Authorization: Bearer <your-jwt-token>"
```

**Search by writer name:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/lmc/1a0dadec-9498-4a66-a51f-8345ae433c32/transactions/?search=Bemah" \
  -H "Authorization: Bearer <your-jwt-token>"
```

**Date range filter:**
```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/lmc/1a0dadec-9498-4a66-a51f-8345ae433c32/transactions/?date_from=2026-04-01&date_to=2026-04-05" \
  -H "Authorization: Bearer <your-jwt-token>"
```

---

## Draws & Winnings Endpoint

### Endpoint: Get YTD Draws & Winnings

**Route:** `GET /api/v1/financials/dashboard/draws-and-winnings/`

**Description:** Returns year-to-date Draws & Winnings dashboard data in three card groups: YTD Sales, YTD Winnings (with claimed/unclaimed breakdown), and YTD Gross Gaming Revenue (with retention rate). Most data reads from the pre-computed `YTDSummary` model (updated nightly by Celery). The unique player count is a live distinct query on `Ticket.player_phone`.

**Authentication:** Required (Bearer Token)

**Permissions:** `IsOperatorOrAbove` (operators and admins only)

### Response Format

**Status Code:** `200 OK`

```json
{
  "ytd_sales": {
    "total_sales": "GHS 34,806,983.08",
    "total_sales_amount": 34806983.08,
    "unique_players": 56189,
    "total_coupons": 741002,
    "total_stakes": 20562983
  },
  "ytd_winnings": {
    "total_winnings": "GHS 20,687,915.60",
    "total_winnings_amount": 20687915.60,
    "claimed": "GHS 20,553,513.20",
    "claimed_amount": 20553513.20,
    "unclaimed": "GHS 134,402.40",
    "unclaimed_amount": 134402.40
  },
  "ytd_ggr": {
    "gross_gaming_revenue": "GHS 14,119,067.48",
    "gross_gaming_revenue_amount": 14119067.48,
    "retention_rate": "4.49%",
    "retention_rate_value": 4.49,
    "retention_value": "GHS 1,564,033.54",
    "retention_value_amount": 1564033.54
  }
}
```

### Response Field Descriptions

#### YTD Sales Card

| Field | Type | Description |
|-------|------|-------------|
| `total_sales` | string | Formatted YTD total ticket sales (e.g. "GHS 34,806,983.08") |
| `total_sales_amount` | float | Raw numeric value of total sales |
| `unique_players` | integer | Count of distinct `player_phone` values on valid tickets this year (live query) |
| `total_coupons` | integer | Total ticket count YTD (referred to as "coupons" in the UI) |
| `total_stakes` | integer | Total individual stake/line count across all tickets YTD |

#### YTD Winnings Card

| Field | Type | Description |
|-------|------|-------------|
| `total_winnings` | string | Formatted total win amount YTD |
| `total_winnings_amount` | float | Raw numeric value of total winnings |
| `claimed` | string | Formatted amount of winnings already claimed by players |
| `claimed_amount` | float | Raw numeric value of claimed winnings |
| `unclaimed` | string | Formatted amount of winnings not yet claimed (pending + expired) |
| `unclaimed_amount` | float | Raw numeric value of unclaimed winnings |

#### YTD Gross Gaming Revenue Card

| Field | Type | Description |
|-------|------|-------------|
| `gross_gaming_revenue` | string | Formatted GGR = total_sales − total_winnings |
| `gross_gaming_revenue_amount` | float | Raw numeric value of GGR |
| `retention_rate` | string | YTD retention rate formatted as "X.XX%" |
| `retention_rate_value` | float | Raw numeric retention rate percentage |
| `retention_value` | string | Formatted monetary value of retention = total_sales × retention_rate / 100 |
| `retention_value_amount` | float | Raw numeric retention monetary value |

### UI Card Mapping

| UI Card | Response Section | Key Fields |
|---------|-----------------|------------|
| **YTD Sales** (left) | `ytd_sales` | `total_sales`, `unique_players`, `total_coupons`, `total_stakes` |
| **YTD Winnings** (center) | `ytd_winnings` | `total_winnings`, `claimed`, `unclaimed` |
| **YTD Gross Gaming Revenue** (right) | `ytd_ggr` | `gross_gaming_revenue`, `retention_rate`, `retention_value` |

### Data Sources

| Field | Source | Notes |
|-------|--------|-------|
| Total sales, tickets, stakes, wins, GGR, retention rate | `YTDSummary` | Pre-computed nightly by Celery |
| Unique players | Live `Ticket` query | `COUNT(DISTINCT player_phone)` for current year, excluding blank phones and cancelled tickets |

### Calculation Methods

```
GGR = total_sales − total_winnings
Retention Value = total_sales × retention_rate ÷ 100
Unclaimed = total_winnings − claimed
```

### Example Request

```bash
curl -X GET https://onassismystrocore-production.up.railway.app/api/v1/financials/dashboard/draws-and-winnings/ \
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

2. **Get Draws & Winnings:**
```
GET https://onassismystrocore-production.up.railway.app/api/v1/financials/dashboard/draws-and-winnings/
Headers:
  Authorization: Bearer <access_token>
```

---

## Draws & Winnings Table Endpoint

Returns a paginated list of drawn events with result data for the Draws & Winnings drill-down table.

### URL
`GET /api/v1/games/events/draws-and-winnings/`

### Authentication
JWT Bearer token required.

### Permissions
- **Writer or above** (`IsWriterOrAbove`)

### Query Parameters

| Parameter        | Type   | Required | Description                              |
| ---------------- | ------ | -------- | ---------------------------------------- |
| `game_type`      | UUID   | No       | Filter by game type ID                   |
| `status`         | string | No       | Filter by event status                   |
| `draw_date`      | date   | No       | Filter by exact draw date (YYYY-MM-DD)   |
| `draw_date__gte` | date   | No       | Draw date greater than or equal           |
| `draw_date__lte` | date   | No       | Draw date less than or equal              |
| `page`           | int    | No       | Page number (default: 1)                 |
| `page_size`      | int    | No       | Results per page (default: 20)           |

### Response — `200 OK`

```json
{
  "count": 42,
  "next": "http://…?page=2",
  "previous": null,
  "results": [
    {
      "event_id": "a1b2c3d4-…",
      "event_no": 1234,
      "draw_date": "Sat, 05 Apr 2026",
      "event_name": "5/90 Original",
      "draw_time": "18:54:37",
      "pre_draw": "GHS 5,000.00",
      "pre_draw_amount": 5000.0,
      "draw_numbers": [5, 14, 29, 56, 51],
      "machine_numbers": [22, 33, 44, 55, 66],
      "post_draw_1": "GHS 1,200.00",
      "post_draw_1_amount": 1200.0,
      "post_draw_2": "GHS 800.00",
      "post_draw_2_amount": 800.0,
      "payout_ratio": "46.00%",
      "payout_ratio_value": 46.0,
      "total_winnings": "GHS 2,300.00",
      "total_winnings_amount": 2300.0
    }
  ]
}
```

### Row Fields

| Field                  | Type   | Description                                            |
| ---------------------- | ------ | ------------------------------------------------------ |
| `event_id`             | UUID   | DrawEvent primary key                                  |
| `event_no`             | int    | Sequential event number                                |
| `draw_date`            | string | Formatted date (e.g. "Sat, 05 Apr 2026")              |
| `event_name`           | string | Event/game name                                        |
| `draw_time`            | string | Draw time in HH:MM:SS format                           |
| `pre_draw`             | string | Pre-draw sales formatted as GHS                        |
| `pre_draw_amount`      | float  | Raw pre-draw sales value                               |
| `draw_numbers`         | array  | Drawn numbers (e.g. [5, 14, 29, 56, 51])              |
| `machine_numbers`      | array  | Machine-generated numbers                              |
| `post_draw_1`          | string | Post-draw I sales formatted as GHS                     |
| `post_draw_1_amount`   | float  | Raw post-draw I value                                  |
| `post_draw_2`          | string | Post-draw II sales formatted as GHS                    |
| `post_draw_2_amount`   | float  | Raw post-draw II value                                 |
| `payout_ratio`         | string | Payout ratio formatted as percentage                   |
| `payout_ratio_value`   | float  | Raw payout ratio value                                 |
| `total_winnings`       | string | Total winnings formatted as GHS                        |
| `total_winnings_amount`| float  | Raw total winnings value                               |

### Notes
- Only events with status `DRAWN` and an attached `DrawResult` are returned.
- Results are ordered newest-first by `draw_date` then `draw_time`.
- Clicking a row's "Pre-Draw" value opens the [Draw Event Tickets](#draw-event-tickets-endpoint) modal.

### Example Request

```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/games/events/draws-and-winnings/
  -H "Authorization: Bearer <your-jwt-token>"
```

---

## Draw Event Tickets Endpoint

Returns the paginated ticket list for a specific draw event (the "Pre Draw Tickets" modal). Each ticket includes its nested stakes with full detail (game, play type, numbers, writer info).

### URL
`GET /api/v1/games/events/{id}/tickets/`

### Authentication
JWT Bearer token required.

### Permissions
- **Writer or above** (`IsWriterOrAbove`)

### Path Parameters

| Parameter | Type | Required | Description       |
| --------- | ---- | -------- | ----------------- |
| `id`      | UUID | Yes      | DrawEvent UUID    |

### Query Parameters

| Parameter   | Type   | Required | Description                                              |
| ----------- | ------ | -------- | -------------------------------------------------------- |
| `search`    | string | No       | Filter by ticket number, writer name, or player phone    |
| `page`      | int    | No       | Page number (default: 1)                                 |
| `page_size` | int    | No       | Results per page (default: 20)                           |

### Response — `200 OK`

```json
{
  "event": {
    "event_no": 1234,
    "event_name": "5/90 Original",
    "draw_numbers": [5, 14, 29, 56, 51],
    "total_wins": "GHS 2,300.00",
    "total_wins_amount": 2300.0,
    "payout_ratio": "46.00%",
    "payout_ratio_value": 46.0,
    "draw_date": "Sat, 05 Apr 2026",
    "draw_time": "18:54:37"
  },
  "tickets": {
    "count": 25,
    "next": "http://…?page=2",
    "previous": null,
    "results": [
      {
        "ticket_id": "b2c3d4e5-…",
        "ticket_no": "123456789012345678901234567",
        "stake_count": 3,
        "stake_value": "GHS 15.00",
        "stake_value_amount": 15.0,
        "datetime": "Sat, 05 Apr 2026",
        "staked_by": "Kwame Asante",
        "phone_number": "+233501234567",
        "status": "active",
        "stakes": [
          {
            "stake_id": "c3d4e5f6-…",
            "created_at": "2026-04-05 14:30:00",
            "game": {
              "id": "11111111-1111-4111-b111-111111111111",
              "name": "5/90 Original",
              "code": "590_OG"
            },
            "event_id": "a1b2c3d4-…",
            "event": "5/90 Original - April 05, 2026",
            "play_group": "Direct",
            "play": "Direct 2 (2 Sure)",
            "numbers": "5,14",
            "stake_amount": "10.00",
            "original_numbers": "5,14",
            "player_phone": "+233501234567",
            "stake_status": "ACTIVE",
            "writer": {
              "id": "1",
              "name": "Kwame Asante",
              "phone": "+233241110001"
            }
          },
          {
            "stake_id": "d4e5f6g7-…",
            "created_at": "2026-04-05 14:30:00",
            "game": {
              "id": "11111111-1111-4111-b111-111111111111",
              "name": "5/90 Original",
              "code": "590_OG"
            },
            "event_id": "a1b2c3d4-…",
            "event": "5/90 Original - April 05, 2026",
            "play_group": "Perm",
            "play": "Perm 2",
            "numbers": "10,25,47",
            "stake_amount": "5.00",
            "original_numbers": "10,25,47",
            "player_phone": "+233501234567",
            "stake_status": "ACTIVE",
            "writer": {
              "id": "1",
              "name": "Kwame Asante",
              "phone": "+233241110001"
            }
          }
        ]
      }
    ]
  }
}
```

### Event Header Fields

| Field                | Type   | Description                               |
| -------------------- | ------ | ----------------------------------------- |
| `event_no`           | int    | Sequential event number                   |
| `event_name`         | string | Event/game name                           |
| `draw_numbers`       | array  | Drawn numbers                             |
| `total_wins`         | string | Total winnings formatted as GHS           |
| `total_wins_amount`  | float  | Raw total winnings value                  |
| `payout_ratio`       | string | Payout ratio formatted as percentage      |
| `payout_ratio_value` | float  | Raw payout ratio value                    |
| `draw_date`          | string | Formatted draw date                       |
| `draw_time`          | string | Draw time in HH:MM:SS format              |

### Ticket Row Fields

| Field               | Type   | Description                              |
| ------------------- | ------ | ---------------------------------------- |
| `ticket_id`         | UUID   | Ticket primary key                       |
| `ticket_no`         | string | Unique ticket number                     |
| `stake_count`       | int    | Number of stakes on the ticket           |
| `stake_value`       | string | Total stake value formatted as GHS       |
| `stake_value_amount`| float  | Raw total stake value                    |
| `datetime`          | string | Formatted sold-at date                   |
| `staked_by`         | string | Writer's full name                       |
| `phone_number`      | string | Player phone number                      |
| `status`            | string | Ticket status (active/won/lost/claimed)  |
| `stakes`            | array  | Nested list of stakes (see below)        |

### Nested Stake Fields

| Field              | Type       | Description                                                  |
| ------------------ | ---------- | ------------------------------------------------------------ |
| `stake_id`         | UUID       | Stake primary key                                            |
| `created_at`       | string     | Stake creation timestamp (`YYYY-MM-DD HH:MM:SS`)            |
| `game`             | object     | Game type `{id, name, code}`                                 |
| `event_id`         | UUID       | Draw event ID                                                |
| `event`            | string     | Event display name                                           |
| `play_group`       | string     | Play group ("Direct", "Perm", "Banker to All", "Banker Against") |
| `play`             | string     | Play type name (e.g. "Direct 2 (2 Sure)")                    |
| `numbers`          | string     | Staked numbers as comma-separated string                     |
| `stake_amount`     | string     | Stake amount as decimal string                               |
| `original_numbers` | string     | Original numbers (for BA: pipe-separated sets)               |
| `player_phone`     | string     | Player phone number                                          |
| `stake_status`     | string     | Ticket status in uppercase (e.g. "ACTIVE", "LOST", "WON")   |
| `writer`           | object     | Writer info `{id, name, phone}` or `null`                    |

### Notes
- Cancelled tickets are excluded.
- The `search` parameter matches against ticket number, writer first/last name, and player phone.
- Stakes are nested directly in each ticket row — no separate endpoint needed.
- Stakes are ordered by `sequence_no` (ascending).

### Example Request

```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/games/events/<event-uuid>/tickets/" \
  -H "Authorization: Bearer <your-jwt-token>"
```

---

## List Admin Users Endpoint

Returns a paginated list of all admin users. Supports search by name or phone number.

### URL
`GET /api/v1/auth/users/admins/`

### Authentication
JWT Bearer token required.

### Permissions
- **Admin only** (`IsAdmin`)

### Query Parameters

| Parameter   | Type   | Required | Description                              |
| ----------- | ------ | -------- | ---------------------------------------- |
| `search`    | string | No       | Search by first name, last name, or phone number |
| `page`      | int    | No       | Page number (default: 1)                 |
| `page_size` | int    | No       | Results per page (default: 30)           |

### Response — `200 OK`

```json
{
  "count": 4,
  "next": null,
  "previous": null,
  "results": [
    {
      "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
      "email": "testuser@example.com",
      "first_name": "Test",
      "last_name": "User",
      "full_name": "Test User",
      "phone": "+233593814832",
      "role": "admin",
      "is_active": true,
      "photo": null,
      "date_joined": "2025-09-06T10:00:00Z"
    }
  ]
}
```

### Row Fields

| Field         | Type     | Description                        |
| ------------- | -------- | ---------------------------------- |
| `id`          | UUID     | User primary key                   |
| `email`       | string   | User's email address               |
| `first_name`  | string   | First name                         |
| `last_name`   | string   | Last name                          |
| `full_name`   | string   | Computed full name                 |
| `phone`       | string   | Phone number                       |
| `role`        | string   | Always `admin`                     |
| `is_active`   | boolean  | Account active status              |
| `photo`       | string/null | Profile photo URL or null       |
| `date_joined` | datetime | Account creation timestamp         |

### Example Request

```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/auth/users/admins/?search=Benjamin" \
  -H "Authorization: Bearer <your-jwt-token>"
```

---

## Create Admin User Endpoint

Creates a new user with the `admin` role.

### URL
`POST /api/v1/auth/users/admins/`

### Authentication
JWT Bearer token required.

### Permissions
- **Admin only** (`IsAdmin`)

### Request Body

```json
{
  "email": "newadmin@example.com",
  "first_name": "New",
  "last_name": "Admin",
  "phone": "+233551112222",
  "password": "securepass123"
}
```

### Request Fields

| Field        | Type   | Required | Description              |
| ------------ | ------ | -------- | ------------------------ |
| `email`      | string | Yes      | Unique email address     |
| `first_name` | string | Yes      | First name               |
| `last_name`  | string | Yes      | Last name                |
| `phone`      | string | Yes      | Unique phone number      |
| `password`   | string | Yes      | Password (min 8 chars)   |
| `photo`      | file   | No       | Profile photo            |

### Response — `201 Created`

```json
{
  "id": "f9e8d7c6-b5a4-3210-fedc-ba9876543210",
  "email": "newadmin@example.com",
  "first_name": "New",
  "last_name": "Admin",
  "full_name": "New Admin",
  "phone": "+233551112222",
  "role": "admin",
  "is_active": true,
  "photo": null,
  "date_joined": "2026-04-06T12:00:00Z"
}
```

### Notes
- The `role` is automatically set to `admin` — it cannot be overridden via the request body.
- The user is created with `is_active=true` by default.

### Example Request

```bash
curl -X POST https://onassismystrocore-production.up.railway.app/api/v1/auth/users/admins/ \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json" \
  -d '{"email":"newadmin@example.com","first_name":"New","last_name":"Admin","phone":"+233551112222","password":"securepass123"}'
```

---

## Edit Admin User Endpoint

Updates an existing admin user. Only admin-role users can be edited via this endpoint.

### URL
`PATCH /api/v1/auth/users/{id}/admin-edit/`

### Authentication
JWT Bearer token required.

### Permissions
- **Admin only** (`IsAdmin`)

### Path Parameters

| Parameter | Type | Required | Description       |
| --------- | ---- | -------- | ----------------- |
| `id`      | UUID | Yes      | User UUID         |

### Request Body (partial update)

```json
{
  "first_name": "Updated",
  "phone": "+233559998888"
}
```

### Editable Fields

| Field        | Type    | Description              |
| ------------ | ------- | ------------------------ |
| `email`      | string  | Email address            |
| `first_name` | string  | First name               |
| `last_name`  | string  | Last name                |
| `phone`      | string  | Phone number             |
| `is_active`  | boolean | Activate/deactivate user |
| `photo`      | file    | Profile photo            |

### Response — `200 OK`

```json
{
  "id": "a1b2c3d4-e5f6-7890-abcd-ef1234567890",
  "email": "admin@example.com",
  "first_name": "Updated",
  "last_name": "Admin",
  "full_name": "Updated Admin",
  "phone": "+233559998888",
  "role": "admin",
  "is_active": true,
  "photo": null,
  "date_joined": "2025-09-06T10:00:00Z"
}
```

### Error Responses

| Status | Condition |
|--------|-----------|
| `400 Bad Request` | Target user is not an admin |
| `401 Unauthorized` | Missing or invalid token |
| `403 Forbidden` | Requesting user is not an admin |
| `404 Not Found` | User UUID does not exist |

### Example Request

```bash
curl -X PATCH "https://onassismystrocore-production.up.railway.app/api/v1/auth/users/<user-uuid>/admin-edit/" \
  -H "Authorization: Bearer <your-jwt-token>" \
  -H "Content-Type: application/json" \
  -d '{"first_name":"Updated","is_active":false}'
```

---

## Activity Logs Endpoint

Returns a paginated list of recent admin dashboard activity (logins, admin user creation, admin user edits).

### URL
`GET /api/v1/auth/users/activity-logs/`

### Authentication
JWT Bearer token required.

### Permissions
- **Admin only** (`IsAdmin`)

### Query Parameters

| Parameter   | Type | Required | Description                    |
| ----------- | ---- | -------- | ------------------------------ |
| `page`      | int  | No       | Page number (default: 1)       |
| `page_size` | int  | No       | Results per page (default: 30) |

### Response — `200 OK`

```json
{
  "count": 12,
  "next": null,
  "previous": null,
  "results": [
    {
      "id": 1,
      "actor_name": "Kwabena Mensah",
      "action": "login",
      "description": "Login (by Kwabena Mensah)",
      "created_at": "2026-04-06T16:00:00Z"
    },
    {
      "id": 2,
      "actor_name": "Kwabena Mensah",
      "action": "create_admin",
      "description": "Created admin user John Doe",
      "created_at": "2026-04-06T15:30:00Z"
    }
  ]
}
```

### Row Fields

| Field        | Type     | Description                                             |
| ------------ | -------- | ------------------------------------------------------- |
| `id`         | int      | Auto-incremented primary key                            |
| `actor_name` | string   | Full name of the user who performed the action          |
| `action`     | string   | Action type: `login`, `create_admin`, or `edit_admin`   |
| `description`| string   | Human-readable description of the action                |
| `created_at` | datetime | When the action occurred                                |

### Actions Logged

| Action          | Trigger                                          |
| --------------- | ------------------------------------------------ |
| `login`         | Successful login by an admin or operator user    |
| `create_admin`  | New admin user created via POST /admins/          |
| `edit_admin`    | Admin user edited via PATCH /admin-edit/          |

### Example Request

```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/auth/users/activity-logs/" \
  -H "Authorization: Bearer <your-jwt-token>"
```

---

## 24. All Writers List Endpoint

### Purpose
Returns a paginated list of all writers for the admin dashboard. Each row includes
YTD sales, YTD top-ups, days on platform, days of ticket activity, last transaction
date, and writer status.

### URL
`GET /api/v1/writers/all/`

### Authentication
Requires JWT. Minimum role: **LMC Owner** (lmc_owner, operator, admin).

### Query Parameters

| Parameter | Type   | Required | Description                                      |
| --------- | ------ | -------- | ------------------------------------------------ |
| `search`  | string | No       | Filter by first name, last name, or phone number |
| `status`  | string | No       | Filter by writer status (active, passive, etc.)  |
| `page`    | int    | No       | Page number (default 1)                          |

### Response Fields (each row)

| Field                  | Type     | Description                              |
| ---------------------- | -------- | ---------------------------------------- |
| `id`                   | UUID     | Writer primary key                       |
| `writer_id_display`    | string   | Zero-padded writer ID (e.g. "000042")    |
| `name`                 | string   | Writer full name                         |
| `contact`              | string   | Writer phone number                      |
| `sign_up_date`         | datetime | Writer creation date                     |
| `days_on_platform`     | int      | Days since sign-up                       |
| `days_of_tickets`      | int      | Distinct days with ticket sales          |
| `ytd_sales`            | decimal  | Year-to-date ticket sales total          |
| `ytd_topups`           | decimal  | Year-to-date top-up total                |
| `last_transaction_date`| datetime | Date of most recent ticket sale          |
| `status`               | string   | Writer status                            |

### Example Request

```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/writers/all/" \
  -H "Authorization: Bearer <your-jwt-token>"
```

---

```json
{
    "count": 35,
    "next": "http://localhost:8000/api/v1/writers/all/?page=2",
    "previous": null,
    "results": [
        {
            "id": "980d76e2-5c65-4760-aaea-c943272eef3c",
            "writer_id_display": "000001",
            "name": "Test Writer",
            "contact": "+233241110001",
            "sign_up_date": "2026-03-01T17:57:18.714000Z",
            "days_on_platform": 37,
            "days_of_tickets": 6,
            "ytd_sales": "1809.70",
            "ytd_topups": "0.00",
            "last_transaction_date": "2026-04-01T08:52:17.189024Z",
            "status": "active"
        },
        {
            "id": "c9c0d0b8-cae2-4517-89f7-67357e5a1ae0",
            "writer_id_display": "000002",
            "name": "Name",
            "contact": "+233202225630",
            "sign_up_date": "2026-03-01T17:57:18.717000Z",
            "days_on_platform": 37,
            "days_of_tickets": 16,
            "ytd_sales": "4736.70",
            "ytd_topups": "13839.00",
            "last_transaction_date": "2026-04-04T12:10:43.333984Z",
            "status": "active"
        },
    ]
}
```

## 25. Writer Profile Endpoint

### Purpose
Returns the full profile for a single writer, including summary cards (YTD sales,
top-ups, winnings), wallet balances, device info, tier ranking, and personal details.

### URL
`GET /api/v1/writers/{id}/profile/`

### Authentication
Requires JWT. Minimum role: **LMC Owner** (lmc_owner, operator, admin).

### Response Fields

| Field                 | Type     | Description                                  |
| --------------------- | -------- | -------------------------------------------- |
| `id`                  | UUID     | Writer primary key                           |
| `writer_id_display`   | string   | Zero-padded writer ID                        |
| `name`                | string   | Writer full name                             |
| `gender`              | string   | Gender (N/A if not set)                      |
| `date_of_birth`       | date     | Date of birth                                |
| `mobile`              | string   | Phone number                                 |
| `email`               | string   | Email address                                |
| `status`              | string   | Writer status                                |
| `serial_number`       | string   | Bound POS device serial number               |
| `terminal_number`     | string   | Terminal ID (truncated device UUID)           |
| `device_state`        | string   | Bound device status (trading/issued/recovery) |
| `days_on_platform`    | int      | Days since sign-up                           |
| `days_of_tickets`     | int      | Distinct days with ticket sales              |
| `lt_avg_sale`         | decimal  | Lifetime average ticket sale amount          |
| `sign_up_date`        | datetime | Writer creation date                         |
| `sales_wallet_balance`| string   | Airtime wallet balance                       |
| `sales_wallet_id`     | string   | Airtime wallet ID (truncated)                |
| `claims_wallet_balance`| string  | Claims wallet balance                        |
| `claims_wallet_id`    | string   | Claims wallet ID (truncated)                 |
| `ytd_sales`           | decimal  | Year-to-date ticket sales                    |
| `this_month_sales`    | decimal  | Current month ticket sales                   |
| `ytd_topups`          | decimal  | Year-to-date top-ups                         |
| `this_month_topups`   | decimal  | Current month top-ups                        |
| `ytd_winnings`        | decimal  | Year-to-date winnings                        |
| `this_month_winnings` | decimal  | Current month winnings                       |
| `ranking_tier`        | string   | Tier based on YTD top-ups (Tier I–IV)        |
| `avg_topup`           | decimal  | Average top-up amount                        |

### Tier Thresholds

| Tier     | YTD Top-Ups Threshold |
| -------- | --------------------- |
| Tier I   | ≥ GHS 50,000          |
| Tier II  | ≥ GHS 20,000          |
| Tier III | ≥ GHS 5,000           |
| Tier IV  | < GHS 5,000           |

### Example Request

```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/writers/{id}/profile/" \
  -H "Authorization: Bearer <your-jwt-token>"
```

```json
{
    "id": "d30a931e-2af3-4e6e-b72b-a1b7b0a31d7c",
    "writer_id_display": "000004",
    "name": "Kwame First",
    "gender": "N/A",
    "date_of_birth": "1990-01-01",
    "mobile": "+233204449258",
    "email": "+233204449258@writer.onassislotto.com",
    "status": "active",
    "serial_number": "POS-0004-4844",
    "terminal_number": "1c887e",
    "device_state": "trading",
    "days_on_platform": 37,
    "days_of_tickets": 26,
    "lt_avg_sale": "30.49",
    "sign_up_date": "2026-03-01T17:57:18.720000Z",
    "sales_wallet_balance": "0.00",
    "sales_wallet_id": "64826167-f12",
    "claims_wallet_balance": "0.00",
    "claims_wallet_id": "948c423d-91d",
    "ytd_sales": "19389.60",
    "this_month_sales": "2052.00",
    "ytd_topups": "671828.00",
    "this_month_topups": "671828.00",
    "ytd_winnings": "73320.00",
    "this_month_winnings": "73320.00",
    "ranking_tier": "Tier I",
    "avg_topup": "1056.33"
}
   ```

---

## 26. Writer Sales Endpoint

### Purpose
Returns a paginated list of ticket sales for a specific writer. This powers the
"Sales" tab on the writer detail page.

### URL
`GET /api/v1/writers/{id}/writer-sales/`

### Authentication
Requires JWT. Minimum role: **LMC Owner** (lmc_owner, operator, admin).

### Response Fields (each row)

| Field          | Type    | Description                            |
| -------------- | ------- | -------------------------------------- |
| `ticket_no`    | string  | Ticket number                          |
| `date`         | string  | Sale date (e.g. "Mon, 06 April 2026") |
| `time`         | string  | Sale time (e.g. "02:31:52 PM")        |
| `event_number` | int     | Draw event number                      |
| `game`         | string  | Game type name                         |
| `play`         | string  | Primary play type name (first stake)   |
| `amount_paid`  | decimal | Total ticket amount                    |
| `stakes`       | int     | Number of stakes on the ticket         |

### Example Request

```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/writers/{id}/writer-sales/" \
  -H "Authorization: Bearer <your-jwt-token>"
```

```json
{
    "id": "d30a931e-2af3-4e6e-b72b-a1b7b0a31d7c",
    "writer_id_display": "000004",
    "name": "Kwame First",
    "gender": "N/A",
    "date_of_birth": "1990-01-01",
    "mobile": "+233204449258",
    "email": "+233204449258@writer.onassislotto.com",
    "status": "active",
    "serial_number": "POS-0004-4844",
    "terminal_number": "1c887e",
    "device_state": "trading",
    "days_on_platform": 37,
    "days_of_tickets": 26,
    "lt_avg_sale": "30.49",
    "sign_up_date": "2026-03-01T17:57:18.720000Z",
    "sales_wallet_balance": "0.00",
    "sales_wallet_id": "64826167-f12",
    "claims_wallet_balance": "0.00",
    "claims_wallet_id": "948c423d-91d",
    "ytd_sales": "19389.60",
    "this_month_sales": "2052.00",
    "ytd_topups": "671828.00",
    "this_month_topups": "671828.00",
    "ytd_winnings": "73320.00",
    "this_month_winnings": "73320.00",
    "ranking_tier": "Tier I",
    "avg_topup": "1056.33"
}
   ```

---

## 27. Writer Winnings Endpoint

### Purpose
Returns a paginated list of winnings for a specific writer. This powers the
"Winnings" tab on the writer detail page.

### URL
`GET /api/v1/writers/{id}/writer-winnings/`

### Authentication
Requires JWT. Minimum role: **LMC Owner** (lmc_owner, operator, admin).

### Response Fields (each row)

| Field           | Type    | Description                              |
| --------------- | ------- | ---------------------------------------- |
| `ticket_id` | string  | Truncated ticket UUID                    |
| `ticket_number` | string  | Ticket number                            |
| `event_number`  | int     | Draw event number                        |
| `game`          | string  | Game type name                           |
| `play`          | string  | Primary play type name (first stake)     |
| `datetime`      | string  | Win computed datetime (dd/mm/yyyy HH:MM) |
| `stake_amount`  | decimal | Total ticket amount (stake)              |
| `amount_won`    | decimal | Win amount                               |

### Example Request

```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/writers/{id}/writer-winnings/" \
  -H "Authorization: Bearer <your-jwt-token>"
```

```json
{
    "count": 6,
    "next": null,
    "previous": null,
    "results": [
        {
            "ticket_id": "c3cfe3bc-d6cc-4f",
            "ticket_number": "204562360309503498718027017",
            "event_number": 86,
            "game": "5/90 Noonrush",
            "play": "Direct 5",
            "datetime": "06/04/2026 18:43:53",
            "stake_amount": "15.00",
            "amount_won": "250.00"
        },
        {
            "ticket_id": "9da97824-acc7-40",
            "ticket_number": "295943210730285437897410591",
            "event_number": 39,
            "game": "5/90 Original",
            "play": "Direct 1",
            "datetime": "06/04/2026 18:43:53",
            "stake_amount": "20.00",
            "amount_won": "1000.00"
        },
        {
            "ticket_id": "6b93ca85-5b92-4e",
            "ticket_number": "997655458880124027097593535",
            "event_number": 48,
            "game": "5/90 Original",
            "play": "Perm 2",
            "datetime": "06/04/2026 18:43:53",
            "stake_amount": "5.00",
            "amount_won": "2500.00"
        },
        {
            "ticket_id": "01d7f37b-f5cf-41",
            "ticket_number": "202603302352170004067108",
            "event_number": 2,
            "game": "5/90 Noonrush",
            "play": "Perm 2",
            "datetime": "05/04/2026 22:26:18",
            "stake_amount": "206.00",
            "amount_won": "1200.00"
        },
        {
            "ticket_id": "35574f13-3312-42",
            "ticket_number": "202603262252170004718559",
            "event_number": 1,
            "game": "Morning VAG",
            "play": "Direct 3",
            "datetime": "05/04/2026 22:26:18",
            "stake_amount": "0.40",
            "amount_won": "200.00"
        },
        {
            "ticket_id": "8d629032-edc8-43",
            "ticket_number": "202603300552170004529643",
            "event_number": 1,
            "game": "Morning VAG",
            "play": "Perm 2",
            "datetime": "05/04/2026 22:26:18",
            "stake_amount": "101.00",
            "amount_won": "960.00"
        }
    ]
}
```



---

## 28. Writer Top-Ups Endpoint

### Purpose
Returns a paginated list of top-up transactions for a specific writer. This powers
the "Top-Ups" tab on the writer detail page.

### URL
`GET /api/v1/writers/{id}/writer-topups/`

### Authentication
Requires JWT. Minimum role: **LMC Owner** (lmc_owner, operator, admin).

### Response Fields (each row)

| Field            | Type    | Description                                |
| ---------------- | ------- | ------------------------------------------ |
| `date`           | string  | Top-up date (e.g. "Mon, 06 Apr 2026")     |
| `time`           | string  | Top-up time (e.g. "02:31:52 PM")          |
| `source`         | string  | Source phone/identifier from payment data  |
| `network`        | string  | Payment channel/network or top-up method   |
| `bank_batch_ref` | string  | Payment reference                          |
| `transaction_ref`      | string  | Provider transaction ID                    |
| `amount`         | decimal | Top-up amount (GHS)                        |
| `balance`        | string  | Balance after top-up (N/A if unavailable)  |

### Example Request

```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/writers/{id}/writer-topups/" \
  -H "Authorization: Bearer <your-jwt-token>"
```
```json
{
    "count": 12,
    "next": null,
    "previous": null,
    "results": [
        {
            "date": "Mon, 06 Apr 2026",
            "time": "06:43:53 PM",
            "source": null,
            "network": "mobile_money",
            "bank_batch_ref": null,
            "transaction_ref": null,
            "amount": "1264.00",
            "balance": "N/A"
        },
        {
            "date": "Mon, 06 Apr 2026",
            "time": "06:43:53 PM",
            "source": null,
            "network": "mobile_money",
            "bank_batch_ref": null,
            "transaction_ref": null,
            "amount": "1712.00",
            "balance": "N/A"
        },
        {
            "date": "Mon, 06 Apr 2026",
            "time": "06:43:53 PM",
            "source": null,
            "network": "mobile_money",
            "bank_batch_ref": null,
            "transaction_ref": null,
            "amount": "1478.00",
            "balance": "N/A"
        },
{    [
```


---

## 29. Writer Cashouts Endpoint

### Purpose
Returns a paginated list of successful withdrawal (cashout) transactions for a
specific writer. Only withdrawals with status "success" are included. This powers
the "Cashout" tab on the writer detail page.

### URL
`GET /api/v1/writers/{id}/writer-cashouts/`

### Authentication
Requires JWT. Minimum role: **LMC Owner** (lmc_owner, operator, admin).

### Response Fields (each row)

| Field            | Type    | Description                                |
| ---------------- | ------- | ------------------------------------------ |
| `date`           | string  | Cashout date (e.g. "Mon, 06 Apr 2026")    |
| `time`           | string  | Cashout time (e.g. "02:31:52 PM")         |
| `source`         | string  | Recipient mobile number                    |
| `network`        | string  | Mobile money provider (MTN, VOD, ATL)      |
| `bank_batch_ref` | string  | Withdrawal reference                       |
| `transaction_ref`      | string  | Provider transaction ID                    |
| `amount`         | decimal | Withdrawal amount (GHS)                    |
| `balance`        | string  | Balance after cashout (N/A if unavailable) |

### Example Request

```bash
curl -X GET "https://onassismystrocore-production.up.railway.app/api/v1/writers/{id}/writer-cashouts/" \
  -H "Authorization: Bearer <your-jwt-token>"
```

---

## Last Updated
April 6, 2026

## API Version
v1
