# Phone Lookup API

REST API to get carrier name, line type (mobile/landline/VoIP), and phone number details for any phone number worldwide. 200 free lookups/month.

## Features

- Identify carrier name for any phone number (Verizon, AT&T, T-Mobile, etc.)
- Detect line type — mobile, landline, or VoIP
- Validate phone numbers and get formatted output
- Supports international numbers in E.164 format
- 200 requests/month on free tier
- Example Response:
```json
{
  "is_valid_number": true,
  "line_type": "mobile",
  "carrier": "Verizon Wireless",
  "phone_number": "+12128148373",
  "national_format": "(212) 814-8373",
  "country_code": "US",
  "calling_country_code": "1",
  "mobile_country_code": "310",
  "mobile_network_code": "012"
}
```

## Get API Key

Create an account at [omkar.cloud](https://www.omkar.cloud/auth/sign-up?redirect=/api-key) to get your API key, and use it in requests. 200 requests are free every month.

## Quick Start

```bash
curl -X GET "https://carrier-lookup-api.omkar.cloud/lookup?phone=%2B14082292600" \
  -H "API-Key: YOUR_API_KEY"
```

```json
{
  "is_valid_number": true,
  "line_type": "mobile",
  "carrier": "Verizon Wireless",
  "phone_number": "+12128148373",
  "national_format": "(212) 814-8373",
  "country_code": "US",
  "calling_country_code": "1",
  "mobile_country_code": "310",
  "mobile_network_code": "012"
}
```

## Installation

### Python

```bash
pip install requests
```

```python
import requests

response = requests.get(
    "https://carrier-lookup-api.omkar.cloud/lookup",
    params={"phone": "+14082292600"},
    headers={"API-Key": "YOUR_API_KEY"}
)

data = response.json()
print(f"Carrier: {data['carrier']}, Line Type: {data['line_type']}")
```

### Node.js

```bash
npm install axios
```

```javascript
import axios from "axios";

const response = await axios.get("https://carrier-lookup-api.omkar.cloud/lookup", {
    params: { phone: "+14082292600" },
    headers: { "API-Key": "YOUR_API_KEY" }
});

console.log(`Carrier: ${response.data.carrier}, Line Type: ${response.data.line_type}`);
```

## API Reference

### Endpoint

```
GET https://carrier-lookup-api.omkar.cloud/lookup
```

### Headers

| Header | Required | Description |
|--------|----------|-------------|
| `API-Key` | Yes | API key from [omkar.cloud/api-key](https://www.omkar.cloud/api-key) |

### Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `phone` | Yes | Phone number to look up. Include country code in E.164 format (e.g., `+14082292600`) |

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `is_valid_number` | boolean | Whether the phone number is valid |
| `line_type` | string | Type of phone line: `mobile`, `landline`, or `voip` |
| `carrier` | string | Carrier name (e.g., "Verizon Wireless", "AT&T") |
| `phone_number` | string | Number in E.164 international format |
| `national_format` | string | Number formatted for local use (e.g., "(212) 814-8373") |
| `country_code` | string | ISO country code (e.g., "US", "IN", "GB") |
| `calling_country_code` | string | Country dialing code (e.g., "1" for US) |
| `mobile_country_code` | string | MCC identifying the country of the mobile network |
| `mobile_network_code` | string | MNC identifying the specific carrier |

## Examples

### Detect line type before sending SMS

```python
response = requests.get(
    "https://carrier-lookup-api.omkar.cloud/lookup",
    params={"phone": "+14082292600"},
    headers={"API-Key": "YOUR_API_KEY"}
)

data = response.json()
if data["line_type"] == "mobile":
    print("Safe to send SMS")
elif data["line_type"] == "landline":
    print("Cannot send SMS to landline — skip this number")
elif data["line_type"] == "voip":
    print("VoIP number detected — flag for review")
```

### Validate and enrich phone numbers

```python
response = requests.get(
    "https://carrier-lookup-api.omkar.cloud/lookup",
    params={"phone": "+447911123456"},
    headers={"API-Key": "YOUR_API_KEY"}
)

data = response.json()
if data["is_valid_number"]:
    print(f"Carrier: {data['carrier']}, Country: {data['country_code']}")
else:
    print("Invalid phone number")
```

### Flag VoIP numbers for fraud prevention

```python
response = requests.get(
    "https://carrier-lookup-api.omkar.cloud/lookup",
    params={"phone": "+12125551234"},
    headers={"API-Key": "YOUR_API_KEY"}
)

data = response.json()
if data["line_type"] == "voip":
    print("⚠️ VoIP number — possible fraud risk")
```

## Error Handling

```python
response = requests.get(
    "https://carrier-lookup-api.omkar.cloud/lookup",
    params={"phone": "+14082292600"},
    headers={"API-Key": "YOUR_API_KEY"}
)

if response.status_code == 200:
    data = response.json()
elif response.status_code == 401:
    # Invalid API key
    pass
elif response.status_code == 429:
    # Rate limit exceeded
    pass
```

## Rate Limits

| Our Tier | Our Price | Our Requests |
|----------|----------|-------------|
| Free     | $0       | 200         |
| Starter  | $16      | 1600        |
| Grow     | $48      | 4800        |
| Scale    | $148     | 14800       |

## Use Cases

- **SMS Delivery Optimization** — Check if a number is mobile before sending SMS. Skip landlines to cut failed delivery costs.
- **Fraud Prevention** — Flag VoIP numbers during signup. Fraudsters use disposable VoIP numbers to create fake accounts.
- **User Verification** — Confirm a phone number is valid and identify the carrier before sending OTP codes.
- **Data Enrichment** — Add carrier and line type data to your customer database for better segmentation.

## Questions? We have answers.

Reach out anytime. We will solve your query within 1 working day.

[![Contact Us on WhatsApp about Phone Lookup API](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20Phone%20Lookup%20API.)

[![Contact Us on Email about Phone Lookup API](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=Phone%20Lookup%20API%20Question)
