# Bangladesh Tax Verification API

A Cloudflare Workers-based service to verify tax return filing status from the Bangladesh National Board of Revenue (NBR) eTax system.

## 🌐 API Endpoint
```
https://bangladesh-tax-verification-api.zenjahid-api.workers.dev/
```

## ✨ Features
- Verify tax return filing status for Bangladesh taxpayers
- Real-time verification using official eTax NBR API
- Simple JSON response format
- Built on Cloudflare Workers for global edge performance
- Input validation for TIN and assessment year formats

## 🚀 Usage

### Base Endpoint
```http
GET /
```
Returns basic API information.

### Tax Verification Endpoint
```http
POST /api/v1/verify-tax
```

#### 📥 Request Parameters (JSON Body)
| Parameter        | Type   | Required | Description                                    |
|------------------|--------|----------|------------------------------------------------|
| `tin_no`         | string | Yes      | 12-digit Tax Identification Number (TIN)      |
| `assessment_year`| string | Yes      | Assessment year in YYYY-YYYY format           |

#### 📤 Response Format
**Successful Response:**
```json
{
  "success": true,
  "data": {
    "tinNo": "1177203828XX",
    "assessmentYear": "2023-2024",
    "submissionStatus": "OFFLINE",
    "assesName": "Nazma Akthar",
    "isNameChanged": false,
    "taxPayername": null
  }
}
```

**Error Responses:**
```json
{
  "success": false,
  "error": "No Data Found!"
}
```

**Validation Error:**
```json
{
  "error": {
    "code": 400,
    "message": "Invalid TIN format. TIN should be 12 digits."
  }
}
```

#### 📋 Example Requests

**cURL:**
```bash
curl -X POST "https://bangladesh-tax-verification-api.zenjahid-api.workers.dev/api/v1/verify-tax" \
-H "Content-Type: application/json" \
-d '{
  "tin_no": "1177203828XX",
  "assessment_year": "2023-2024"
}'
```

**Python:**
```python
import requests

url = "https://bangladesh-tax-verification-api.zenjahid-api.workers.dev/api/v1/verify-tax"
payload = {
    "tin_no": "1177203828XX",
    "assessment_year": "2023-2024"
}

response = requests.post(url, json=payload)
print(response.json())
```

**JavaScript:**
```javascript
fetch('https://bangladesh-tax-verification-api.zenjahid-api.workers.dev/api/v1/verify-tax', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    tin_no: "1177203828XX",
    assessment_year: "2023-2024"
  }),
})
.then(response => response.json())
.then(data => console.log(data));
```

**PHP:**
```php
<?php
$url = 'https://bangladesh-tax-verification-api.zenjahid-api.workers.dev/api/v1/verify-tax';
$data = [
    'tin_no' => '1177203828XX',
    'assessment_year' => '2023-2024'
];

$options = [
    'http' => [
        'header' => "Content-type: application/json\r\n",
        'method' => 'POST',
        'content' => json_encode($data)
    ]
];

$context = stream_context_create($options);
$result = file_get_contents($url, false, $context);
$response = json_decode($result, true);

print_r($response);
?>
```

## 📝 Validation Rules

### TIN Number
- Must be exactly **12 digits**
- Only numeric characters allowed
- Example: `1177203828XX`

### Assessment Year
- Must be in **YYYY-YYYY** format
- Example: `2023-2024`, `2024-2025`

## ⚖️ Legal Disclaimer
1. This API uses **publicly accessible** information provided by the Bangladesh National Board of Revenue (NBR) through their official eTax portal at [api.etaxnbr.gov.bd](https://api.etaxnbr.gov.bd)

2. All data accessed by this API is already publicly available through NBR's official verification system

3. This project does not:
   - Store or cache any personal tax data
   - Modify or alter original data in any way
   - Bypass any authentication or security systems
   - Access non-public or confidential tax information

4. The API simply provides a programmatic interface to access tax filing verification that is already openly available through the official eTax portal

5. Users of this API are responsible for complying with all applicable laws and regulations regarding tax data usage in Bangladesh

## 🛠️ Error Handling
Common error responses include:
- `Missing required parameters: tin_no and assessment_year`
- `Invalid TIN format. TIN should be 12 digits.`
- `Invalid assessment year format. Use format: YYYY-YYYY`
- `No Data Found!` (when no tax filing record exists)
- `Request timeout - eTax service is slow` (when NBR service is unavailable)
- `Service temporarily unavailable` (during system maintenance)

## ⚠️ Limitations
- Requires internet connection
- Dependent on NBR eTax system availability
- May experience slower response times during peak hours
- Limited to publicly available tax filing status information only

## 🏗️ Technical Details
- **Platform**: Cloudflare Workers
- **Runtime**: V8 JavaScript Engine
- **Global Edge**: Deployed across Cloudflare's global network
- **Uptime**: 99.9%+ availability
- **Response Time**: Typically <2 seconds (depends on NBR API)

## 📊 Rate Limits
- No explicit rate limits applied
- Please use responsibly and avoid excessive requests
- Consider implementing client-side caching for repeated queries

## 🔒 Privacy & Security
- No user data is logged or stored
- All requests are processed in real-time
- HTTPS encryption for all communications
- No authentication required for public tax verification data

## 👨‍💻 Author
**[@zenjahid](https://zenjahid.com)** - For support, questions, or business inquiries, please contact the developer.

## 📄 License
This project is open source and available under the [MIT License](LICENSE).

---

**⚠️ Important Note**: This API is not officially affiliated with the Bangladesh National Board of Revenue (NBR) or the Government of Bangladesh. It provides a convenient interface to publicly available tax verification services. Use at your own discretion and ensure compliance with local laws and regulations.

**🤝 Contributing**: Issues and pull requests are welcome! Visit the [GitHub repository](https://github.com/zenjahid/api-worker-tax-verification) for more details.

