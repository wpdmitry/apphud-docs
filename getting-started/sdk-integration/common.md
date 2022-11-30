---
description: This page describes common questions for all SDKs.
---

# Common

## User Merging (iOS)

By default, users are being merged only if their App Store Receipts match. For example, if Apphud has a customer A with App Store Receipt A and we receive a new request from customer B with App Store Receipt A, then both customers are merged into customer A and User ID of latter one is changed to A.

In other words, Apphud merges users by their original transaction id.

## User Merging (Android)

By default, users are being merged only if their Google Play purchase tokens match. For example, if Apphud has a customer A with Google Play purchase token A and we receive a new request from customer B with Google Play purchase token A, then both customers are merged into customer A and User ID of latter one is changed to A.

In other words, Apphud merges users by their Google Play purchase tokens.

## User Uniqueness (iOS)

Device ID is the main identifier that uniquely identifies a customer. So even if you initialise SDK with the same custom User ID on different devices, several new users with the same User ID will be created since they have different Device ID.

{% hint style="info" %}
Device ID is also being saved to Keychain, so even if you delete the app, the old device ID will be restored as well as user info.

To test a fresh install see [this guide](../../testing/ios.md#test-a-fresh-install).
{% endhint %}

If you still would like to use your custom User ID as unique identifier across the app, you should you use Apphud.startManually method. Passing the same ID to userID and deviceID fields will guarantee that the same user will be returned in case of passing same User IDs on multiple devices.

```swift
Apphud.startManually(apiKey: "YOUR_API_KEY", userID: "SOME_USER_ID", deviceID: "SOME_USER_ID")
```

## User Uniqueness (Android)

User ID is the main identifier that uniquely identifies a customer. So if you initialise SDK with different User ID on the same device, a new user will be created. It is recommended to use Apphud login system (not passing any `userID` at all).

{% hint style="warning" %}
As known, Android does not have Keychain, so re-installing the app will cause a new fresh user to be created.
{% endhint %}

If you still would like to use your custom User ID as unique identifier across the app, just pass your User ID when initialising the app:

```swift
Apphud.start(apiKey: "YOUR_API_KEY", userID: "SOME_USER_ID")
```

## Cross Platform Support

If you have both iOS and Android apps you should decide whether you need cross platform support or not. This is basically means adding both platforms in one Apphud app rather than creating two different apps for each platform. Cross platform support has prons and cons.

{% hint style="info" %}
If you use cross platform Apphud app, then User ID will be the main user identifier across both apps.
{% endhint %}

### **When you should choose cross platform support?**

If you added both platforms in one app, you will get:

* Ability to have single subscription per user. If you have your own login system, you can use Apphud for cross-platform subscription support. If user purchases subscription on iOS, he will get that premium subscription on Android as well (if Apphud SDK started with the same user id).
* One dashboard for both apps. You will be able to see summarised revenue in dashboard and charts.

### **When you should NOT choose cross platform support?**

* You don't have login system in your apps. So users from two platforms can't be merged.
* You don't want Android app revenue to be shared with iOS app revenue. This might be useful, if you have different Apphud Members on each platform.
* You don't want to have universal dashboard or charts.

Later this fall, we will add more filters in dashboard and charts so you can split data across platforms.
