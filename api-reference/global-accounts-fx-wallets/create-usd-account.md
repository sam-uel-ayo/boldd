# Create USD Account

**Endpoint**

<mark style="color:green;">`POST`</mark> `{{base_url}}/business/create-globalaccount.php` (or `POST {{base_url}}/business/create-globalaccount`)

**Request Headers**

| Header          | Type     | Required | Description                                                  |
| --------------- | -------- | -------- | ------------------------------------------------------------ |
| `Authorization` | `String` | Yes      | Bearer token authentication (e.g. `Bearer YOUR_SECRET_KEY`). |
| `Content-Type`  | `String` | Yes      | Request body format (e.g. `application/json`).               |

#### Request Body

| Field                  | Type    | Required | Description                                                                                                                                                                                                                                                                                     |
| ---------------------- | ------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `customerid`           | string  | Yes      | Tracking ID from **Create Customer (Full KYC)**                                                                                                                                                                                                                                                 |
| `account_type`         | string  | Yes      | `USD` for this page (also accepts `EUR`, `MXN`)                                                                                                                                                                                                                                                 |
| `monthly_volume`       | string  | Yes      | Expected monthly payment volume: `0_4999`, `5000_9999`, `10000_49999`, or `50000_plus`                                                                                                                                                                                                          |
| `source_of_funds`      | string  | Yes      | One of: `company_funds`, `ecommerce_reseller`, `gambling_proceeds`, `gifts`, `government_benefits`, `inheritance`, `investments_loans`, `pension_retirement`, `salary`, `sale_of_assets_real_estate`, `savings`, `someone_elses_funds`                                                          |
| `expected_montly_fund` | string  | Yes      | Same value set as `monthly_volume`                                                                                                                                                                                                                                                              |
| `account_purpose`      | string  | Yes      | One of: `charitable_donations`, `ecommerce_retail_payments`, `investment_purposes`, `operating_a_company`, `other`, `payments_to_friends_or_family_abroad`, `personal_or_living_expenses`, `protect_wealth`, `purchase_goods_and_services`, `receive_payment_for_freelancing`, `receive_salary` |
| `occupation`           | string  | Yes      | Customer's most recent occupation                                                                                                                                                                                                                                                               |
| `pepstatus`            | boolean | Yes      | Whether the customer is a Politically Exposed Person                                                                                                                                                                                                                                            |
| `agreeto_term`         | boolean | Yes      | Customer's acceptance of account terms                                                                                                                                                                                                                                                          |
| `proof_of_address`     | string  | No       | URL to a proof-of-address document (e.g. utility bill)                                                                                                                                                                                                                                          |

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" lineNumbers="true" %}
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
  "account_type": "USD",
  "occupation": "Software Engineer",
  "proof_of_address": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png"
}'
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript (Fetch)" %}
{% code overflow="wrap" lineNumbers="true" %}
```javascript
const response = await fetch('{{base_url}}/business/create-globalaccount', {
  method: 'POST',
  headers: {
    'Authorization': 'Bearer YOUR_SECRET_KEY',
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    customerid: 'BLD12211916',
    monthly_volume: '0_4999',
    pepstatus: false,
    source_of_funds: 'gifts',
    expected_montly_fund: '0_4999',
    account_purpose: 'payments_to_friends_or_family_abroad',
    agreeto_term: true,
    account_type: 'USD',
    occupation: 'Software Engineer',
    proof_of_address: 'https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png'
  })
});
const data = await response.json();
```
{% endcode %}
{% endtab %}

{% tab title="Node.js (Axios)" %}
{% code overflow="wrap" lineNumbers="true" %}
```json
var request = require('request');
var options = {
  'method': 'POST',
  'url': '{{base_url}}/business/create-globalaccount',
  'headers': {
    'Authorization': 'BEARER SECRET_KEY'
  },
  body: '{
  "customerid": "BLD12211916",
  "monthly_volume": "0_4999",
  "pepstatus": false,
  "source_of_funds": "gifts",
  "expected_montly_fund": "0_4999", 
  "account_purpose": "payments_to_friends_or_family_abroad", 
  "agreeto_term": true,
  "account_type": "USD",
  "occupation": "Software Engineer",
  "proof_of_address": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png"
}'

};
request(options, function (error, response) {
  if (error) throw new Error(error);
  console.log(response.body);
});

```
{% endcode %}
{% endtab %}

{% tab title="Python (Requests)" %}
{% code overflow="wrap" lineNumbers="true" %}
```python
import requests
import json

url = "{{base_url}}/business/create-globalaccount"

payload = json.dumps({'customerid': 'BLD12211916', 'monthly_volume': '0_4999', 'pepstatus': False, 'source_of_funds': 'gifts', 'expected_montly_fund': '0_4999', 'account_purpose': 'payments_to_friends_or_family_abroad', 'agreeto_term': True, 'account_type': 'USD', 'occupation': 'Software Engineer', 'proof_of_address': 'https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png'})
headers = {
  'Authorization': 'Bearer YOUR_SECRET_KEY',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```
{% endcode %}
{% endtab %}

{% tab title="PHP (cURL)" %}
{% code overflow="wrap" lineNumbers="true" %}
```php
$curl = curl_init();

curl_setopt_array($curl, array(
  CURLOPT_URL => '{{base_url}}/business/create-globalaccount',
  CURLOPT_RETURNTRANSFER => true,
  CURLOPT_ENCODING => '',
  CURLOPT_MAXREDIRS => 10,
  CURLOPT_TIMEOUT => 0,
  CURLOPT_FOLLOWLOCATION => true,
  CURLOPT_HTTP_VERSION => CURL_HTTP_VERSION_1_1,
  CURLOPT_CUSTOMREQUEST => 'POST',
  CURLOPT_POSTFIELDS =>'{
  "customerid": "BLD12211916",
  "monthly_volume": "0_4999",
  "pepstatus": false,
  "source_of_funds": "gifts",
  "expected_montly_fund": "0_4999",
  "account_purpose": "payments_to_friends_or_family_abroad",
  "agreeto_term": true,
  "account_type": "USD",
  "occupation": "Software Engineer",
  "proof_of_address": "https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png"
}',
  CURLOPT_HTTPHEADER => array(
    'Authorization: Bearer YOUR_SECRET_KEY',
    'Content-Type: application/json'
  ),
));

$response = curl_exec($curl);

curl_close($curl);
echo $response;
```
{% endcode %}
{% endtab %}

{% tab title="Dart" %}
{% code overflow="wrap" lineNumbers="true" %}
```dart
var headers = {
  'Authorization': 'Bearer YOUR_SECRET_KEY',
  'Content-Type': 'application/json'
};
var request = http.Request('POST', Uri.parse('{{base_url}}/business/create-globalaccount'));
request.body = json.encode({'customerid': 'BLD12211916', 'monthly_volume': '0_4999', 'pepstatus': False, 'source_of_funds': 'gifts', 'expected_montly_fund': '0_4999', 'account_purpose': 'payments_to_friends_or_family_abroad', 'agreeto_term': True, 'account_type': 'USD', 'occupation': 'Software Engineer', 'proof_of_address': 'https://res.cloudinary.com/site/image/upload/v1714257348/idcard2.png'});
request.headers.addAll(headers);

http.StreamedResponse response = await request.send();

if (response.statusCode == 200) {
  print(await response.stream.bytesToString());
}
else {
  print(response.reasonPhrase);
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Sample response

{% code title="Sample response" overflow="wrap" %}
```json
{
  "status": true,
  "message": "Your USD account request has been submitted successfully. You will be notified once it's ready.",
  "tracking": "DLE23210UA24400"
}
```
{% endcode %}

### Business Eligibility Rules

To successfully submit a Global Account request for a customer:

* The **business account** must be active and granted `globalaccount`, `virtualaccount`, or `usdaccount` service access.
* The **business itself** must have completed Business KYC approval (`business_kyc_verified: true`).
* The **selected customer** (`customerid`) must already be a fully KYC'd business customer.
* The customer record must include the identity and address data required for global account onboarding (e.g., `proof_of_address`, `taxno`).

### KYC Rejection Payload Example

When validation fails, the API returns a safe, normalized rejection payload detailing missing fields and specific rejection reasons instead of a blank or unhandled error:

```json
{
  "status": false,
  "responseCode": "00",
  "reason_code": "kyc_incomplete",
  "reason": "Customer KYC is incomplete. Please complete the missing fields and try again.",
  "missing_fields": [
    "proof_of_address",
    "taxno"
  ],
  "received_fields": [
    "bvn",
    "government_id_front",
    "government_id_back"
  ],
  "data": {
    "missing_fields": [
      "proof_of_address",
      "taxno"
    ],
    "rejection_reasons": {
      "proof_of_address": "Missing required KYC field: Proof of address",
      "taxno": "Missing required KYC field: Tax identification number"
    },
    "customer_trackingid": "BLD123456789",
    "business_kyc_verified": true
  }
}
```
