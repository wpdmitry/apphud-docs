---
description: >-
  This page describes how to migrate your existing purchase data when adding
  Apphud SDK to your live app.
---

# Data Migration Guide

If you have a live app with subscriptions or non renewing purchases, you may want to migrate all your existing and historical data to Apphud. There are two ways of doing this: client side and server side.

{% hint style="info" %}
If you don't have historical purchases data stored on your own server or other subscription tracking platform, all you can do is set up client side migration and App Store / Google developer notifications.
{% endhint %}

## Client Side Migration

This way of migration means syncing existing purchases from the app at first launch. When old user updates the app with Apphud SDK onboard, a sync method needs to be called by developer. You **should do this just once** for your paid users. Store flag in your app after method is called.&#x20;

{% tabs %}
{% tab title="Swift" %}
```swift
// hasPurchases - is your own boolean value indicating that current user is paying user.
if hasPurchases {    
    Apphud.migratePurchasesIfNeeded {_, _, _ in} // Swift      
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
// hasPurchases - is your own boolean value indicating that current user is paying user.
if (hasPurchases) {    
    Apphud.syncPurchases()     
}
```
{% endtab %}

{% tab title="Java" %}
```java
// hasPurchases - is your own boolean value indicating that current user is paying user.
if (hasPurchases) {    
    Apphud.syncPurchases();    
};
```
{% endtab %}

{% tab title="Flutter" %}
```dart
await Apphud.syncPurchases();
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Do not migrate purchases on every app launch. One successful time is enough. Store flag in your app if purchases were successfully migrated.
{% endhint %}

Keep in mind, that unless user has updated and launched the app, we will not be able to properly record subscription data for this user unless you set up App Store / Google notifications.

If we receive purchase data from App Store / Google notification and can't find such user in our database, then we create [anonymous customer](faq.md#who-are-the-users-with-anon\_xxx-prefix) and do not send their events to any integrations.

It may take a few weeks or even months depending on your subscription duration and users activity to migrate all data.

{% hint style="info" %}
There is even a case when user's purchase data may be migrated up to 12 months after switching to Apphud. This may happen when user recently purchased a 1 year subscription and never launched the app. Or even deleted it. We will not create this user in our database and we will not receive any App Store / Google notification until subscription renews. And if you don't set up App Store / Google notifications, then we won't be able to track his purchase data at all.
{% endhint %}

### App Store Server Notifications

When moving your existing iOS app to Apphud it is required to set Apphud URL for [App Store Server Notifications](data-migration-guide.md#app-store-server-notifications) in order to get cancellations and other updates in real time.&#x20;

Already using App Store Notifications? Not a problem, consider using our App Store Server Notifications [Proxy](creating-app.md#app-store-server-notifications-proxy) feature.

### Google Real-time Developer Notifications

When moving your existing Android app to Apphud it is also required to set up [Google Real-time Developer Notifications](creating-app.md#google-real-time-developer-notifications) in order to get cancellations and other updates in real time.

## Server side migration

If you have your own server with existing purchases data, you can import all data using REST API or .csv file.

### **Import using REST API**

You will need to pass the following parameters to REST API endpoint:

* `user_id`
* `base64_receipt` (iOS only)
* `purchase_token` (Android only)
* `product_id`
* `price`
* `currency`
* `country_code`
* `idfa` (optional. On Android `advertising id` is passed also as idfa parameter)

[Email us](mailto:support@apphud.com) to get all the REST API details.

### **Import using CSV**

For large amount of data it is better to send us a CSV file. Note that importing might take a few days depending on the file size.

The fields are the following:

* `user_id`
* `base64_receipt` (iOS only)
* `purchase_token` (Android only)
* `product_id`
* `price`
* `currency`
* `country_code`
* `idfa` (optional. On Android `advertising id` should be passed as `idfa` parameter)

Missing some fields? [Email us](mailto:support@apphud.com) and we will figure out something.

{% hint style="warning" %}
On Android, only the last transaction can be imported and only if it occurred within the last 90 days.
{% endhint %}

## Migrate from other subscription tracking platform

If you are planning to move from another subscription tracking platform (thank you, you will not regret!), a preferred way of data migration will be importing via CSV file. Please kindly ask your platform support team to provide the CSV file with the fields described above. Again, feel free to [email us](mailto:support@apphud.com) to get more information.
