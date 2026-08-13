# Create Wallet

## Create Wallet

Create a Boldd wallet/account programmatically — typically used by partner platforms onboarding their own end users onto Boldd. Requires an App ID/Token generated from your dashboard's "Create App" section first.

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/createwallet`

**Request Headers**

| Header                                          | Type       | Required | Description                                    |
| ----------------------------------------------- | ---------- | -------- | ---------------------------------------------- |
| \`\`\`\`\`                                      | `String`   | Yes      | Custom header value `-`.                       |
| `### Request Body`                              | `String`   | Yes      | Custom header value `-`.                       |
| \`                                              | Field      | Type     | Required                                       |
| \`                                              | ---        | ---      | ---                                            |
| \`                                              | `apptoken` | string   | Yes                                            |
| \`                                              | `email`    | string   | Yes                                            |
| \`                                              | `phoneno`  | string   | Yes                                            |
| \`                                              | `fname`    | string   | Yes                                            |
| \`                                              | `sname`    | string   | Yes                                            |
| \`                                              | `auth`     | string   | Yes                                            |
| \`                                              | `referby`  | string   | No                                             |
| `{% tabs %}`                                    | `String`   | Yes      | Custom header value `-`.                       |
| `{% tab title="cURL" %}`                        | `String`   | Yes      | Custom header value `-`.                       |
| `{% code overflow="wrap" lineNumbers="true" %}` | `String`   | Yes      | Custom header value `-`.                       |
| `Content-Type`                                  | `String`   | Yes      | Request body format (e.g. `application/json`). |

bash curl --location --request POST '\{{base\_url\}}/business/createwallet'\
\--header 'Authorization: Bearer YOUR\_SECRET\_KEY'\
\--header 'Content-Type: application/json'\
\--data '{ "apptoken": "APPID", "fname": "testname", "sname": "testsurname", "email": "email@example.com", "phoneno": "08000000000", "auth": "D@tqj8265!", "referby": "" }'

````

</div>

</div>

<div data-gb-custom-block data-tag="tab" data-title='JavaScript'>

<div data-gb-custom-block data-tag="code" data-overflow='wrap' data-lineNumbers='true'>

```javascript
const response = await fetch('{{base_url}}/business/createwallet', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    apptoken: 'APPID', fname: 'testname', sname: 'testsurname',
    email: 'email@example.com', phoneno: '08000000000', auth: 'D@tqj8265!', referby: ''
  })
});
const data = await response.json();
````

#### Sample response

{% code title="Sample response" overflow="wrap" %}
```json
{
  "status": true,
  "email": "email@example.com",
  "accountid": "3107908",
  "businessid": "",
  "msg": "Wallet successfully created!"
}
```
{% endcode %}
