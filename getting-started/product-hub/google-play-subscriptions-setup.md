---
description: Important information before setting up your purchases in Google Play.
---

# Google Play Subscriptions Setup

{% hint style="warning" %}
We are working on supporting updates Google Play Billing Library version 5.0
{% endhint %}

When adding new subscriptions in Google Play Console, **don't add more than one base plan to a subscription**. Apphud is limited in the functionality of **Multi-quantity purchase** model for In-app products, **offers/multiple offers** for subscriptions and **multiple subscription durations.**\
****Apphud SDK doesn’t yet support the current [Billing Library v5](https://developer.android.com/google/play/billing/migrate-gpblv5).\
If you need multiple subscription durations - create a new subscription with its single base plan instead. Your subscriptions should show **Backwards Compatible** badge.

Your application should be compiled with Google Play Billing Library version 4.

Billing Library dependency in app’s `build.gradlefile`:

<pre class="language-java"><code class="lang-java"><strong>// Some code
</strong>def billingVersion = "4.0.0"
implementation "com.android.billingclient:billing:$billingVersion"</code></pre>

<figure><img src="../../.gitbook/assets/Снимок экрана 2022-11-18 в 17.26.43.png" alt=""><figcaption><p>Multi-quantity purchases should be turned off</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Снимок экрана 2022-11-21 в 16.54.33.png" alt=""><figcaption><p>Don't add more than one base plan to a subscription</p></figcaption></figure>
