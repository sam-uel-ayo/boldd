---
icon: lock
---

# Authentication

Boldd authenticates your API requests using your account's API keys. If a request is missing a key, or the key is incorrect or outdated, the API returns an authentication error.

### API Key Types

Every Boldd account has access to two types of API keys:

* **Secret Key** - the most powerful key type, authorized to execute any state-changing action on your account (initializing transactions, sending money, creating cards, etc.). Never expose this key publicly.
* **Public Key** - used for public, read-only call scenarios where data exposure is non-critical, such as client-side integrations (e.g. **Get Available Banks**, **Data Plans**, **Electricity Billers**).

Live keys are distinguished from test keys by a prefix on the key string itself (for example, a live secret key looks like `1applive_sk_...` in the system) rather than by separate named variables - see **Environments** for how this determines which mode a request runs in.

Having the right key type isn't always enough - some endpoints (cards, transfers, global accounts, identity checks) also require a **service grant** on your account. See **Service Access & Limits**.

### Managing Your API Keys

1. Create an account or log in at [useboldd.com](https://useboldd.com/).
2. Navigate to **Settings**.
3. Select the **API Keys/Webhook** tab under Developers to view, copy, or regenerate your keys.

{% hint style="info" %}
**Keep your secret key confidential.** Store it only on your backend, ideally as an environment variable. Never commit it to a public repository or use it in client-side code. If you suspect a key has been compromised, reset it immediately from your dashboard.
{% endhint %}

### Authorizing API Calls

All requests must be made over HTTPS and must include an `Authorization` header. Requests without one fail automatically.

```
Authorization: Bearer YOUR_SECRET_KEY
```

```
Authorization: Bearer YOUR_PUBLIC_KEY
```

{% hint style="info" %}
**Test vs. live mode:** requests run in test or live mode depending on the key pair used, and data between the two modes is fully isolated. See **Environments** for details.
{% endhint %}

## Base URL

Prefix every endpoint in this reference with:

```
{{base_url}} = https://api.oneappgo.com/v1
```
