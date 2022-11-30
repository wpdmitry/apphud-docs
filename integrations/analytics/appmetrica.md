---
description: This guide describes how to add and configure AppMetrica integration.
---

# AppMetrica

[AppMetrica](https://appmetrica.yandex.ru/) is a free real-time ad tracking and mobile app analytics solution.

Since AppMetrica doesn't support "fake" sessions so far, all events are being sent in **background** mode. So, they won't appear in the User profile, but you can see these in Devices events instead.

As soon as AppMetrica release "fake" sessions for server-to-server events, we will change it back to **foreground** mode.

Currently, POST API events are unavailable in Profiles. Looking forward AppMetrica will implement this (no particular date).

Keep in mind, that the data sent from the AppMetrica Post API is [synchronized every 4 hours](https://appmetrica.yandex.ru/docs/mobile-api/post/about.html).

{% hint style="warning" %}
Sending built-in revenue in AppMetrica is not yet supported due to limitations of their Server-to-Server API. Currently, we send all revenue values as custom parameters: `usd_price` __ and `local_price`
{% endhint %}

## How to Add Integration?

{% tabs %}
{% tab title="Step 1" %}
* [Integrate](../../getting-started/sdk-integration/#configure-apphud-sdk) Apphud SDK.
* [Integrate](https://appmetrica.yandex.ru/docs/mobile-sdk-dg/concepts/mobilesdk-about.html) AppMetrica.
* [Match User IDs](appmetrica.md#match-user-ids) between AppMetrica and Apphud.
{% endtab %}

{% tab title="Step 2" %}
* Open [AppMetrica](https://appmetrica.yandex.com) and go to Settings of your app.
* Copy **Application ID** and **Post API Key** fields (_not API key!_).

![](../../.gitbook/assets/step-2.jpg)
{% endtab %}

{% tab title="Step 3" %}
At [Apphud](https://app.apphud.com) go to _"Integrations"_ section and add AppMetrica:

![](../../.gitbook/assets/step-3.png)
{% endtab %}

{% tab title="Step 4" %}
Enter _Post API Key_ and _Application ID_ values into their corresponding fields:

![](../../.gitbook/assets/step-4.png)
{% endtab %}

{% tab title="Step 5" %}
You can enter your custom event names or disable some:

![](../../.gitbook/assets/step-5.png)
{% endtab %}

{% tab title="Step 6" %}
Enable integration and click Save:

![](../../.gitbook/assets/step-6.png)
{% endtab %}
{% endtabs %}

## Match User IDs

Here is an example of initialising both SDKs with User IDs matching.

{% tabs %}
{% tab title="Swift" %}
```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

    Apphud.start(apiKey: "YOUR_API_KEY")
    Apphud.setDelegate(self)
    
    if let configuration = YMMYandexMetricaConfiguration.init(apiKey: "AppMetrica-API-Key") {
        YMMYandexMetrica.activate(with: configuration)
        YMMYandexMetrica.setUserProfileID(Apphud.userID())
    }

    return true
}

// implement ApphudDelegate
func apphudDidChangeUserID(_ userID: String) {
    // Match again
    YMMYandexMetrica.setUserProfileID(Apphud.userID())
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
Apphud.start(apiKey: "YOUR_API_KEY")
val config: YandexMetricaConfig = YandexMetricaConfig.newConfigBuilder(Constants.Appmetrica_API_KEY).build()
YandexMetrica.activate(applicationContext, config)
YandexMetrica.setUserProfileID(Apphud.userId())
YandexMetrica.enableActivityAutoTracking(this)
```
{% endtab %}

{% tab title="Java" %}
```java
Apphud.start(apiKey: "YOUR_API_KEY")
YandexMetricaConfig config = YandexMetricaConfig.newConfigBuilder(API_key).build();
YandexMetrica.activate(getApplicationContext(), config);
YandexMetrica.setUserProfileID(Apphud.userId());
YandexMetrica.enableActivityAutoTracking(this);
```
{% endtab %}
{% endtabs %}

## Events Cheat Sheet

This is a list of all possible events and their parameters that are being sent to AppMetrica.&#x20;

{% hint style="info" %}
You can read more about subscription events [here](../../events/events.md) and about parameters [here](../../events/parameters-and-properties.md).
{% endhint %}

{% tabs %}
{% tab title="Trial" %}
### Trial period started

_Default event name:_ `[Apphud] trial_started`

_Parameters:_

* `product_id`: String
* `unit`: String
* `units_count`: Integer

### Successful conversion from trial period to regular subscription

_Default event name:_ `[Apphud] trial_converted`

_Parameters:_

* `product_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float

### Failed conversion from trial period to regular subscription

_Default event name:_ `[Apphud] trial_expired`

_Parameters:_

* `product_id`: String
* `reason`: String
{% endtab %}

{% tab title="Cancellations" %}
### Trial Canceled

&#x20;_Default event name:_ `[Apphud] trial_canceled`

_Parameters:_

* `product_id`: String

### Subscription Canceled

&#x20;_Default event name:_ `[Apphud] subscription_canceled`

_Parameters:_

* `product_id`: String

### Autorenew disabled (Deprecated)

&#x20;_Default event name:_ `[Apphud] autorenew_disabled`

_Parameters:_

* `product_id`: String

### Autorenew enabled

_Default event name:_ `[Apphud] autorenew_enabled`

_Parameters:_

* `product_id`: String
{% endtab %}

{% tab title="Introductory Offer" %}
### Introductory offer started

&#x20;_Default event name:_ `[Apphud] intro_started`

_Parameters:_

* `product_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float
* `offer_type`: String
* `unit`: String
* `units_count`: Integer

### Introductory offer renewed

_Default event name:_ `[Apphud] intro_renewed`

_Parameters:_

* `product_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float
* `offer_type`: String
* `unit`: String
* `units_count`: Integer

### Successful conversion from introductory offer to regular subscription

_Default event name:_ `[Apphud] intro_converted`

_Parameters:_

* `product_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float
* `offer_type`: String

### Failed conversion from introductory offer to regular subscription or failed renew

_Default event name:_ `[Apphud] intro_expired`

_Parameters:_

* `product_id`: String
* `reason`: String
* `offer_type`: String

### Refund during introductory offer

_Default event name:_ `[Apphud] intro_refunded`

_Parameters:_

* `product_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float
* `reason`: String
* `offer_type`: String
{% endtab %}

{% tab title="Regular" %}
### Subscription started

&#x20;_Default event name:_ `[Apphud] subscription_started`

_Parameters:_

* `product_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float

### Subscription renewed

_Default event name:_ `[Apphud] subscription_renewed`

_Parameters:_

* `product_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float

### Subscription expired

_Default event name:_ `[Apphud] subscription_expired`

_Parameters:_

* `product_id`: String
* `reason`: String

### Subscription refunded

_Default event name:_ `[Apphud] subscription_refunded`

_Parameters:_

* `product_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float
* `reason`: String
{% endtab %}

{% tab title="Promo Offer" %}
### Promotional offer started

&#x20;_Default event name:_ `[Apphud] promo_started`

_Parameters:_

* `product_id`: String
* `offer_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float
* `offer_type`: String
* `unit`: String
* `units_count`: Integer

### Promotional offer renewed

_Default event name:_ `[Apphud] promo_renewed`

_Parameters:_

* `product_id`: String
* `offer_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float
* `offer_type`: String
* `unit`: String
* `units_count`: Integer

### Successful conversion from promotional offer to regular subscription

_Default event name:_ `[Apphud] promo_converted`

_Parameters:_

* `product_id`: String
* `offer_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float
* `offer_type`: String

### Failed conversion from promotional offer to regular subscription or failed renew

_Default event name:_ `[Apphud] promo_expired`

_Parameters:_

* `product_id`: String
* `offer_id`: String
* `reason`: String
* `offer_type`: String

### Refund during promotional offer

_Default event name:_ `[Apphud] promo_refunded`

_Parameters:_

* `product_id`: String
* `offer_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float
* `reason`: String
* `offer_type`: String
{% endtab %}

{% tab title="Other Events" %}
### Non renewing purchase

&#x20;_Default event name:_ `[Apphud] non_renewing_purchase`

_Parameters:_

* `product_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float

### Non renewing purchase refunded

_Default event name:_ `[Apphud] non_renewing_purchase_refunded`

_Parameters:_

* `product_id`: String
* `local_price`: Float
* `currency`: String
* `usd_price`: Float
* `reason`: String

### Billing issue

&#x20;_Default event name:_ `[Apphud] billing_issue`

_Parameters:_

* `product_id`: String

### Billing issue Resolved

&#x20;_Default event name:_ `[Apphud] billing_issue_resolved`

_Parameters:_

* `product_id`: String
{% endtab %}
{% endtabs %}
