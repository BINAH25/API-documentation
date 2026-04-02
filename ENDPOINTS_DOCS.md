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
