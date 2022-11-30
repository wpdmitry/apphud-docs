---
description: >-
  This guide describes how to test in-app purchases in your Android app and
  provides useful tips.
---

# Testing & Troubleshooting (Android)

## Making Test Purchases

Testing purchases in Android is the same as real purchases. However, you will need to add your Google account to [application license testing](https://support.google.com/googleplay/android-developer/answer/6062777) in order to make purchases for free. For more information about testing purchase, please read official [documentation](https://developer.android.com/google/play/billing/test).

## Test a Fresh Install

To test a fresh install you will need to:

* Delete user in Apphud
* Delete the app

Android SDK doesn't save User ID / Device ID to device keychain. This means that deleting the app and user in Apphud will generate a new User ID / Device ID pair. When launching the app after re-install, you will get a fresh user without purchases.

However, if restore purchases is called, Apphud will merge existing user with a new user. In a result, User ID will change to original one and user will have two devices, with old and new Device ID. Original purchases history will be restored.&#x20;

## Clear Purchases History

Google Play doesn't fully clear purchases history. The best way is to change Google account on device, but if this is not an option, you can **refund / cancel** transactions in _Google Play console > Order management._

## Troubleshooting

### Common steps

In case you experience any issues with in-app purchases in your Android app, please check the following:

* Make sure you have correctly set up [Google Play Service Credentials](../getting-started/creating-app.md#google-play-service-credentials).
* View debug logs in Android Studio. To enable debug logs call: `Apphud.enableDebugLogs()` before SDK initialisation. If you have any issues with in-app purchase, the error will populate in console.
* Make sure you have entered correct Android Package Name in Apphud app settings.
* If you don't use Apphud billing client, make sure `Apphud.syncPurchases()` is called after successful purchase or restoration.
