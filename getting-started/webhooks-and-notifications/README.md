---
icon: webhook
---

# Webhooks & Notifications

Webhooks allow Boldd to send real-time HTTP callbacks to your application backend whenever status updates occur (such as a successful card charge or a completed bank transfer payout).

### Integration Steps

{% stepper %}
{% step %}
#### Webhook Notifications

Understand webhook payloads, verify cryptographic signatures, and check sample event JSONs. Webhook Notifications Guide
{% endstep %}

{% step %}
#### Repush Notification

Learn how to manually trigger a retry request for webhook events that your server missed or failed to process. Repush Notification Guide
{% endstep %}
{% endstepper %}

{% hint style="info" %}
To guarantee deliverability, your webhook listener must respond with an HTTP `200 OK` within 5 seconds.
{% endhint %}
