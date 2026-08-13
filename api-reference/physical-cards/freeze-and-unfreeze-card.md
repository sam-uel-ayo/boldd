# Freeze and Unfreeze Card

Disable or re-enable a physical card. This uses the **same endpoint** as the virtual card version - see [**Virtual Cards**](../virtual-cards/) **→** [**Freeze and Unfreeze Card**](../virtual-cards/freeze-and-unfreeze-card.md) for the full reference. The field is still named `vcardid` regardless of card type.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/vcard-update`

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

| Field        | Type   | Required | Description            |
| ------------ | ------ | -------- | ---------------------- |
| `vcardid`    | string | Yes      | The card's ID          |
| `updatetype` | string | Yes      | `freeze` or `unfreeze` |

#### Sample response

{% code title="Sample response" overflow="wrap" %}
```json
{
  "status": true,
  "responsecode": "01",
  "message": "Card successfully updated"
}
```
{% endcode %}
