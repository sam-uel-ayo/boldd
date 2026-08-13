# Decline a Dispute

Contest a dispute and submit evidence.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/decline-dispute`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field        | Type   | Required | Description                                                |
| ------------ | ------ | -------- | ---------------------------------------------------------- |
| `sesscode`   | string | Yes      | Session code                                               |
| `userid`     | string | Yes      | Your user ID                                               |
| `businessid` | string | Yes      | Your business ID                                           |
| `disputeid`  | string | Yes      | From **Fetch Disputes**                                    |
| `txref`      | string | Yes      | The disputed transaction's reference                       |
| `name`       | string | Yes      | Customer's name                                            |
| `email`      | string | Yes      | Customer's email                                           |
| `phone`      | string | Yes      | Customer's phone number                                    |
| `claim`      | string | No       | Notes on the dispute claim                                 |
| `descres`    | string | Yes      | Description of your response/evidence                      |
| `receipt`    | string | Yes      | URL to supporting evidence (receipt, delivery proof, etc.) |

**cURL**

```bash
curl --location '{{base_url}}/business/decline-dispute' \
--header 'Authorization: Bearer YOUR_SECRET_KEY' \
--header 'Content-Type: application/json' \
--data '{
    "sesscode": "YOUR_SESSION_CODE",
    "userid": "YOUR_USER_ID",
    "businessid": "YOUR_BUSINESS_ID",
    "disputeid": "4",
    "txref": "83810B1637750693902",
    "name": "John Doe",
    "email": "example2@gmail.com",
    "phone": "09012345678",
    "claim": "Customer disputes a delivered order",
    "descres": "Delivery confirmed with signed proof of receipt",
    "receipt": "https://res.cloudinary.com/site/image/upload/receipt.png"
}'
```

**Sample response:** follows the standard envelope (`status`, `message`).

{% hint style="info" %}
**Review:** same as Accept a Dispute — no populated sample response exists in the source material. Recommend a live test before publishing.
{% endhint %}
