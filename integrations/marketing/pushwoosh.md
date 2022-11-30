---
description: This guide describes how to add and configure Pushwoosh integration.
---

# Pushwoosh

## About Integration

Apphud can send all user events in Pushwoosh, which you can use in [Journeys builder](https://docs.pushwoosh.com/platform-docs/send-messages/customer-journey-builder) and create your custom push campaign.

{% tabs %}
{% tab title="Step 1" %}
* [Integrate](../../getting-started/sdk-integration/#configure-apphud-sdk) Apphud SDK on iOS or Android.
*   [Integrate](https://docs.pushwoosh.com/platform-docs/getting-started/basic-concepts) Pushwoosh.

    Note :  If you haven't got a push certificate, Pushwoosh can generate it automatically. Push notification request will appear on app launch by default.
{% endtab %}

{% tab title="Step 2" %}
* At [Apphud](https://app.apphud.com) go to _"Integrations"_ section and add Pushwoosh:

![](<../../.gitbook/assets/Снимок экрана 2021-10-28 в 17.54.55.png>)
{% endtab %}

{% tab title="Step 3" %}
* Enter _Application ID, Sandbox Application ID (optional),_ :

![](<../../.gitbook/assets/Снимок экрана 2021-10-28 в 17.58.09.png>)
{% endtab %}

{% tab title="Step 4" %}
* You can enter your _custom event_ names or disable some:

![](<../../.gitbook/assets/Снимок экрана 2021-10-28 в 18.05.36.png>)
{% endtab %}

{% tab title="Step 5" %}
* Enable integration and click Save:

![](<../../.gitbook/assets/Снимок экрана 2021-10-28 в 18.07.25.png>)
{% endtab %}
{% endtabs %}



## Match User IDs

> _By default, when an app with Pushwoosh SDK is launched for the first time, it sets a device HWID as a UserID. You can call **setUserId** on a login to set any required value to associate a device with a particular user. When a user logs out, you can reset this value to a default one with another **setUserId** call, e.g. to an initial HWID value._

You can set Apphud User ID property to Pushwoosh's `setUserId` function:

{% tabs %}
{% tab title="Swif" %}
```
// assuming both Apphud and Pushwoosh SDKs are initialized:
Pushwoosh.sharedInstance()?.setUserId(Apphud.userID())
```


{% endtab %}
{% endtabs %}



## Custom events

If Apphud events are not enough for you, you can add Pushwoosh **Recommended, General  and Custom** Events in your code.

* Create custom event in Puswoosh -> Dashboard -> Events -> Add event
* Use it in your App:

{% tabs %}
{% tab title="Swift" %}
```
// How to integrate Event into your app
 let attributes: [String : Any] = [
  "Custom event attribute" : "string value"
]
PWInAppManager.shared().postEvent("Custom event name", withAttributes: attributes)
```
{% endtab %}

{% tab title="Objective-C" %}
```
// How to integrate Event into your app
NSDictionary *attributes = @{
  @"Custom event attribute" : @"string value"
};
[[PushNotificationManager pushManager] postEvent:@“eventName” withAttributes:attributes];
```
{% endtab %}

{% tab title="Java" %}
```
// How to integrate Event into your app
TagsBundle attributes = new TagsBundle.Builder()
    .putString("Custom event attribute", "string value")
    .build();
  
PushwooshInApp.getInstance().postEvent("Custom event name", attributes);
```
{% endtab %}
{% endtabs %}

