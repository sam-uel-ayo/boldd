# WordPress

## WordPress

The Boldd WooCommerce plugin lets you accept payments on any WordPress/WooCommerce store.

#### Installation

**Option A — Upload via WordPress Admin**

1. Download the plugin.
2. Go to **Plugins → Add Plugin → Upload Plugin**, select the downloaded zip, then **Install** and **Activate**.

**Option B — Manual Upload**

1. Copy the plugin folder to `wp-content/plugins/boldd_woocommerce`.
2. Activate it under **Plugins** in WordPress Admin.
3. Configure it under **WooCommerce → Settings → Payments → Boldd Payment**.

#### Basic Setup

1. **Get API credentials:** sign up at [useboldd.com](https://useboldd.com), then go to **Dashboard → Developer → Settings** to get your Public and Secret keys.
2. **Enter your keys:** go to **WooCommerce → Settings → Payments → Boldd Payment** and paste them in.
3. **Choose a checkout mode:**
   * **Inline** — customer pays in a popup without leaving your site.
   * **Standard** — customer is redirected to Boldd's hosted checkout page.
4. **Save and test** using your test credentials before going live.

{% hint style="info" %}
Copy your webhook/callback URL from the plugin settings and paste it into your Boldd Dashboard's live webhook URL field so order statuses update automatically.
{% endhint %}

#### For Customers

* Select "Boldd Payment" at checkout.
* Complete payment via popup or hosted checkout, depending on your configured mode.
* Order status updates automatically once payment is confirmed. If payment is pending, the customer is notified and can retry verification.

#### For Admins

* Monitor pending orders under **WooCommerce → Orders**.
* The plugin automatically re-verifies pending orders every 5 minutes.
* Check **WooCommerce → Status → Logs** for transaction-level detail.
* Use the dashboard link in your gateway settings to jump straight to Boldd's transaction view.

Need help? Email [**hi@useboldd.com**](mailto:hi@useboldd.com).
