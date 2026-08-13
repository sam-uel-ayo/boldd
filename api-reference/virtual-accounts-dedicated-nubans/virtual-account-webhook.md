# Virtual Account Webhook

Dedicated-account (NUBAN) deposits are delivered through the same webhook system as [**Webhook Notifications**](../../getting-started/webhooks-and-notifications/webhook-notifications.md), with `paid_through: "dedicatedAccount"` and a richer payload describing the sender.

#### Sample Payload

```json
{
  "event_type": "transactions",
  "event_status": "success",
  "AccountNo": "0123456789",
  "paid_through": "dedicatedAccount",
  "trans_status": "01",
  "transmode": "live",
  "Reference": "957421812B73017",
  "SourceName": "Jogh PETER",
  "AmountPaid": "50000",
  "SettledAmount": 4975,
  "Charged": 25,
  "TrackingID": "0150240",
  "TrackingRef": "0150240",
  "AccountRef": "50240",
  "ClientID": "019",
  "transactionType": "Credit",
  "Narration": "FROM UBA Jogh PETER UNOGWU-USSD-NIP",
  "CustomerDetails": {
    "AccountName": "",
    "AccountNo": "0123456789",
    "BankName": "Providus Bank",
    "TrackingId": "0150240"
  },
  "SourceDetails": {
    "SourceName": "Jogh PETER",
    "SourceAcct": "0219110003",
    "SourceBank": "UNITED BANK FOR AFRICA",
    "Narration": "FROM UBA Jogh PETER-USSD-NIP"
  },
  "transerror": "0"
}
```

`SourceDetails` tells you who sent the money and from which bank - useful for reconciliation when multiple customers share visibility into the same virtual account activity.

Set up delivery the same way as any other webhook. See [**Webhook Notifications**](../../getting-started/webhooks-and-notifications/webhook-notifications.md) for endpoint configuration and the retry policy.
