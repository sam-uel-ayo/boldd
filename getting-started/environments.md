---
icon: codepen
---

# Environments

## Sandbox & Live

Boldd provides two environments for your integration: **Sandbox (Test)** and **Production (Live)**.

Both environments share the same API endpoints and request structure. Which environment a request runs in is determined by the **API key** used in your `Authorization` header — test and live keys are distinguished by their prefix.

### Sandbox (Test) Environment

Use the Sandbox to build, test, and debug your integration without moving real money.

* **Trigger:** Use your test-mode Secret or Public key.
* **Behavior:** Transactions are simulated — no real funds move.
* **Webhooks:** Events triggered in Sandbox are sent as test events, so you can build and verify your listeners safely.

### Production (Live) Environment

The Production environment is where real business happens.

* **Trigger:** Use your live-mode Secret or Public key.
* **Behavior:** Actions here are final — real money moves, real cards are issued, real bank accounts are debited or credited.

{% hint style="info" %}
Never use real customer data, real bank accounts, or real card numbers while testing in Sandbox — and never run tests against Live keys.
{% endhint %}

## Base URL

Both environments share a single base URL. The key you authenticate with determines which environment handles the request:

```
{{base_url}} = https://api.oneappgo.com/v1
```
