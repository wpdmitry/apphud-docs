---
description: Popular integrations issues with description
---

# Integrations Issues

### Common Issues

**Pending Status**

Event is scheduled for sending or is waiting for attribution data, like AppsFlyer ID, Adjust ID, etc. Facebook integration delays every event for 10 minutes due to waiting for IDFA.

**Skipped Status**

This means event was not send due to one of the following reasons:

* _No device found –_ Could not found device identifiers for given event.
* _IDFA restricted -_ User didn't grant access to IDFA. Check the [following](../getting-started/idfa-ios-14.md).
* _too old event_ - Events that occurred 24 hours earilier than user installation date will be skipped.
* _account suspended –_ Your Apphud account is suspended, all integrations are disabled.
* _family shared subscription –_ Apphud skips family shared subscriptions from integrations.
* _anonymous customer –_ Unable to identify user because it came from Apple Notifications. Cannot send event to integrations because User ID is unknown.
* _event disabled_ - this event is disabled in the integration settings. Check integration settings, and turn on this event if needed.

### Pushwoosh

* _missing token_ - Auth Token is missing in integration settings.
* _missing app\_id_ - Application ID is missing in integration settings.

### Оnesignal

* missing app\_id - Application ID is missing in integration settings.

### Asapty

* _missing application\_id_ - Application ID is missing in integration settings.
* _Apple Search Ads not configured -_ You must first Configure Apple Search Ads in Apphud > Settings > Search Ads Settings. Having credentials issues? Check the [`following`](https://docs.apphud.com/integrations/marketing/asapty#credentials-issue-between-apphud-and-asapty).

### Segment

* _missing write\_key -_ Write Key is missing in integration settings.

### Telegram

* _missing chat id -_ Incorrectly integrated Telegram. Please check documentation and try again.

### TikTok Web2App

* _missing pixel id –_ Pixel ID is missing in integration settings.
* _not a matched customer_ - the customer is outside of the integration environment, i.e. installed the app not from TikTok ad.
* _match found, but the ttclid parameter is missing –_ please check that query parameters are correctly added to the URL.

### Tenjin

* _missing token –_ Token is missing.
* _missing sandbox app id_ - Application ID is missing.

### Facebook

* _missing app id_ - Facebook App ID is missing.
* _missing client token -_ Facebook Client token is missing.
* _missing IDFA_ - User didn't grant access to IDFA. Check the [following](../getting-started/idfa-ios-14.md).

### Facebook Web2App

* _missing pixel id -_ Pixel ID is missing in integration settings.
* _missing client token -_ Facebook Client Token is missing in integration settings.
* _not a matched customer_ - the customer is outside of the integration environment, i.e. installed the app not from Facebook ad.
* _match found, but the fbc parameter is missing -_ please check that Apphud Script is correctly installed to the landing page.

### AppsFlyer

* _missing App ID_ - App ID is missing in integration settings.

### Mixpanel

* _missing token -_ Token is missing in integration settings.

### Firebase

* _missing Firebase App Instance ID_ - Analytics Instance ID is missing. Please check that you correctly matched users in your app's code.
* _missing Firebase api secret -_ API Secret is missing in integration settings. Please check documentation about how to get it.
* _missing Firebase app id –_ Firebase App ID is missing in integration settings.

### Appmetrica

* _missing post\_api\_key –_ POST API key is missing in integration settings.
* _missing application\_id –_ Application ID is missing in integration settings.

### Amplitude

* _missing the API key_ - API key is missing in integration settings.

### Server-to-Server webhooks

* _HTTP status "0"_ - A status code of "0" generally means there was no respons from your server.

###

