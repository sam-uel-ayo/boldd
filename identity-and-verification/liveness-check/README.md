---
icon: image-portrait
---

# Liveness Check

Confirm that a real, present customer is completing verification during onboarding or before high-risk actions. Liveness Check helps prevent identity theft and fraud by using a secure face-liveness challenge.

#### Integration Flow

{% stepper %}
{% step %}
#### Create a Liveness Session

Initiate a new face-liveness session for an existing KYC customer profile. Create Liveness Session
{% endstep %}

{% step %}
#### Configure Liveness Settings

Save your default app origin, liveness UI URLs, and webhook callbacks. Configure Liveness Settings
{% endstep %}

{% step %}
#### Liveness Callback

Receive real-time webhook callback notifications with match confidence scores when a user completes the challenge. Liveness Callback Webhook
{% endstep %}
{% endstepper %}

{% hint style="info" %}
Liveness checking requires the `liveness` service grant activated on your developer account. See Service Access & Limits for details.
{% endhint %}
