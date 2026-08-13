# Accept a Dispute

Concede a dispute and authorize a refund to the customer.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/accept-dispute`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field           | Type   | Required | Description                          |
| --------------- | ------ | -------- | ------------------------------------ |
| `sesscode`      | string | Yes      | Session code                         |
| `userid`        | string | Yes      | Your user ID                         |
| `businessid`    | string | Yes      | Your business ID                     |
| `disputeid`     | string | Yes      | From **Fetch Disputes**              |
| `transref`      | string | Yes      | The disputed transaction's reference |
| `customername`  | string | Yes      | Customer's name                      |
| `customeremail` | string | Yes      | Customer's email                     |
| `customerphone` | string | Yes      | Customer's phone number              |
| `dclaim`        | string | No       | Notes on the dispute claim           |
| `torefund`      | string | Yes      | Amount to refund                     |

**cURL**

```bash
curl --location '{{base_url}}/business/accept-dispute' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "sesscode": "YOUR_SESSION_CODE",
    "userid": "YOUR_USER_ID",
    "businessid": "YOUR_BUSINESS_ID",
    "disputeid": "5",
    "transref": "83810B1637657021448",
    "customername": "John Doe",
    "customeremail": "example@gmail.com",
    "customerphone": "09012345678",
    "dclaim": "Customer confirmed non-delivery",
    "torefund": "100.00"
}'
```

**Sample response:** follows the standard envelope (`status`, `message`).

{% hint style="info" %}
**Review:** the Postman collection has this endpoint's saved method set to `GET` even though it sends a JSON body — almost certainly a saved-request mismatch, since GET requests with bodies aren't standard practice. Documented as `POST` here to match the method declared in the legacy docs and to follow normal REST conventions; also no populated sample response exists in any source for this endpoint. Recommend a live test before publishing.
{% endhint %}
