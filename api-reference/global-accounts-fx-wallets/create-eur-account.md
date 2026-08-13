# Create EUR Account

Identical endpoint and fields to **Create USD Account** - only `account_type` changes.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/create-globalaccount`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

**cURL**

```bash
curl --location '{{base_url}}/business/create-globalaccount' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
  "customerid": "BLD12211916",
  "monthly_volume": "0_4999",
  "pepstatus": false,
  "source_of_funds": "gifts",
  "expected_montly_fund": "0_4999",
  "account_purpose": "payments_to_friends_or_family_abroad",
  "agreeto_term": true,
  "account_type": "EUR",
  "occupation": "Software Engineer",
  "proof_of_address": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png"
}'
```

#### Sample response

{% code title="Sample response" overflow="wrap" %}
```json
{
  "status": true,
  "message": "Your EUR account request has been submitted successfully. You will be notified once it's ready.",
  "tracking": "DLE23210UA24400"
}
```
{% endcode %}

See **Create USD Account** for the full field reference.
