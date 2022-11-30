# IDFA Consent in iOS 14

Starting iOS 14.5 access to IDFA requires user consent. You should request IDFA manually using `AppTrackingTransparency` framework and pass it to Apphud. Update Apphud SDK to `1.0.5` or higher.

{% hint style="warning" %}
Don't forget to add **Privacy - Tracking Usage Description** (`NSUserTrackingUsageDescription`) to your app's `Info.plist`
{% endhint %}

Here is code snippet how you can request IDFA:

{% tabs %}
{% tab title="Swift" %}
```swift
#if canImport(AppTrackingTransparency)
    import AppTrackingTransparency
#endif

func requestIDFA() {
    if #available(iOS 14.5, *) {
        ATTrackingManager.requestTrackingAuthorization { status in
            guard status == .authorized else {return}
            let idfa = ASIdentifierManager.shared().advertisingIdentifier.uuidString
            Apphud.setAdvertisingIdentifier(idfa)
        }
    }
}
```
{% endtab %}

{% tab title="Flutter" %}
```
On Flutter please use the following plugin:
https://pub.dev/packages/app_tracking_transparency

and then use:
static Future<void> setAdvertisingIdentifier(String idfa) async
```
{% endtab %}
{% endtabs %}

Advertising Identifier is required for use in attribution integrations: AppsFlyer, Branch, Facebook, Adjust, Tenjin.

Despite IDFA, filling correct[ App Store Privacy](../other/apple-app-privacy.md) Information is also required. For more information, read [here](https://developer.apple.com/news/?id=8h0btjq7).&#x20;
