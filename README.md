# ZenoPay-Exchange-Rate-API
# ZenoPay Exchange Rate API


A RESTful API for retrieving current exchange rates and calculating conversion amounts between different currencies.

## Table of Contents
- [Features](#features)
- [API Documentation](#api-documentation)
  - [Authentication](#authentication)
  - [Request](#request)
  - [Response](#response)
  - [Error Handling](#error-handling)
- [Examples](#examples)
  - [cURL](#curl)
  - [JavaScript](#javascript)
  - [Python](#python)
- [Rate Limits](#rate-limits)
- [Support](#support)

## Features
- Real-time currency exchange rates
- Bidirectional conversion (source → destination and destination → source)
- Simple RESTful JSON interface
- Secure API key authentication

## API Documentation

### Authentication
All requests require an API key in the header:

```http
x-api-key: your_api_key_here
```

### Request
**Endpoint:** `POST https://zenoapi.com/api/payment/exchange-rate/`

**Headers:**
- `Content-Type: application/json`
- `x-api-key: YOUR_API_KEY`

**Body:**
```json
{
  "source_currency": "TZS",
  "destination_currency": "USD",
  "destination_amount": 7000
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `source_currency` | string | Yes | ISO currency code (e.g., "TZS") |
| `destination_currency` | string | Yes | ISO currency code (e.g., "USD") |
| `destination_amount` | number | Yes | Amount in destination currency |

### Response
**Success Response (200 OK):**
```json
{
  "status": "SUCCESS",
  "resultCode": "000",
  "message": "Transfer amount fetched successfully",
  "data": {
    "source_currency": "TZS",
    "destination_currency": "USD",
    "destination_amount": 7000.0,
    "amount_receive": 18387999.0,
    "selling_rate": 2626.857,
    "buying_rate": 2789.343
  }
}
```

### Error Handling
| Status Code | Description |
|-------------|-------------|
| 400 | Bad Request - Invalid parameters |
| 401 | Unauthorized - Invalid API key |
| 403 | Forbidden - Insufficient permissions |
| 429 | Too Many Requests - Rate limit exceeded |
| 500 | Internal Server Error |

## Examples

### cURL
```bash
curl -X POST 'https://zenoapi.com/api/payment/exchange-rate/' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: YOUR_API_KEY' \
  -d '{
    "source_currency": "TZS",
    "destination_currency": "USD",
    "destination_amount": 7000
  }'
```

### JavaScript
```javascript
const response = await fetch('https://zenoapi.com/api/payment/exchange-rate/', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'x-api-key': 'YOUR_API_KEY'
  },
  body: JSON.stringify({
    source_currency: "TZS",
    destination_currency: "USD",
    destination_amount: 7000
  })
});
const data = await response.json();
```

### Python
```python
import requests

url = "https://zenoapi.com/api/payment/exchange-rate/"
headers = {
    "Content-Type": "application/json",
    "x-api-key": "YOUR_API_KEY"
}
payload = {
    "source_currency": "TZS",
    "destination_currency": "USD",
    "destination_amount": 7000
}

response = requests.post(url, headers=headers, json=payload)
data = response.json()
```

## Rate Limits
- 100 requests per minute
- 1,000 requests per hour
- 10,000 requests per day

## Support
For support or questions, please contact:
- Email: support@zenopay.com
- Slack: [Join our workspace](https://slack.zenopay.com) <!-- Replace with actual link -->
- Twitter: [@ZenoPaySupport](https://twitter.com/ZenoPaySupport) <!-- Replace with actual handle -->

---

📄 **License**: [MIT](LICENSE)  
📅 **Last Updated**: 2023-11-15