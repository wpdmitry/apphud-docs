---
description: >-
  Promote your app on the App Store via Apple Search Ads and analyse revenue and
  other metrics segmented by keywords or campaigns in Apphud.
---

# Apple Search Ads

There are two ways to get Apple Search Ads attribution data: via **iAd** framework or via new **AdServices** framework. The last one is available on iOS 14.3+ devices.

| Framework  | Supported iOS versions    | Requires user ATT consent | Requires generating private key | Available on free plan |
| ---------- | ------------------------- | ------------------------- | ------------------------------- | ---------------------- |
| iAd        | Deprecated since iOS 14.5 | Yes                       | No                              | Yes                    |
| AdServices | iOS 14.3+                 | No                        | Yes                             | No                     |

As you can see in the table above, attribution using AdServices framework **works regardless of user's ATT consent**. However it's a little bit complicated to set up auth credentials.

## Apple Search Ads Attribution via AdServices framework (iOS 14.3+) <a href="#how-does-integration-work" id="how-does-integration-work"></a>

{% hint style="info" %}
Available on paid plans only
{% endhint %}

{% tabs %}
{% tab title="Step 1" %}
Pass attribution token from the app to Apphud.

{% hint style="warning" %}
Don't get confused between `appleAdsAttribution` and `appleSearchAds` enum cases!&#x20;
{% endhint %}

```swift
private func trackAppleSearchAds() {
        if #available(iOS 14.3, *) {
            DispatchQueue.global(qos: .default).async {
                if let token = try? AAAttribution.attributionToken() {
                    DispatchQueue.main.async {
                        Apphud.addAttribution(data: nil, from: .appleAdsAttribution, identifer: token, callback: nil)
                    }
                }
            }
        } else {
        // optionally send Search Ads attribution data from older iOS versions
            ADClient.shared().requestAttributionDetails { data, _ in
                data.map { Apphud.addAttribution(data: $0, from: .appleSearchAds, callback: nil) }
            }
        }
    }
```
{% endtab %}

{% tab title="Step 2" %}
* At [Apphud](https://app.apphud.com) go to Settings > Search Ads Settings.
* By default, Apphud generates public-private key pair automatically so you will need just to **copy public key** value. However, if you are already using services like Asapty or own solution, you will need to paste private key instead. [Read here](../marketing/asapty.md#credentials-issue-between-apphud-and-asapty) for details.
{% endtab %}

{% tab title="Step 3" %}
In your [Apple Search Ads account](https://searchads.apple.com) go to _Settings_  > _User Management_ page. In order for Apphud to fetch attribution data you need to **invite another Apple ID account** and grant it **API Account Manager** access.

{% hint style="info" %}
For unknown reason, granting API Account Read Only role _doesn't work_.\
Please grant Account Manager role as described.
{% endhint %}

![](<../../.gitbook/assets/asa\_access (1).png>)
{% endtab %}

{% tab title="Step 4" %}
* Log out from your primary Search Ads Account
* Log in to Apple Search Ads with Apple ID that has API access that you invited from the step 3.
* Go to _Settings_ > [API](https://app.searchads.apple.com/cm/app/settings/apicertificates) and paste your public key to generate credentials.
* Copy _Client ID_, _Team ID_, and _Key ID_ fields.

![](<../../.gitbook/assets/2 (1).png>)
{% endtab %}

{% tab title="Step 5" %}
Go to Apphud Settings > Search Ads Settings and fill all the fields.\
If all done correctly Access Token field with Organisations list will show up in the page:

![](../../.gitbook/assets/asa\_settings.png)
{% endtab %}

{% tab title=" Done! ✅" %}
Click Save and you're al set!
{% endtab %}
{% endtabs %}

## Apple Search Ads Attribution via iAd framework <a href="#how-does-integration-work" id="how-does-integration-work"></a>

This is the old way to get attribution data and is deprecated since iOS 14.5. \
Integration is very simple. Just import `iAd` framework and call the following method at any point:

{% tabs %}
{% tab title="Swift" %}
```swift
import iAd

func fetchAppleSearchAdsAttrubutionData() {
    ADClient.shared().requestAttributionDetails { data, _ in
        data.map { Apphud.addAttribution(data: $0, from: .appleSearchAds, callback: nil) }
    }
}
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
#import <iAd/iAd.h>

- (void) fetchAppleSearchAdsAttrubutionData {
    [[ADClient sharedClient] requestAttributionDetailsWithBlock:^(NSDictionary<NSString *,NSObject *> * _Nullable attributionDetails, NSError * _Nullable error) {
        if (attributionDetails != nil) {
            [Apphud addAttributionWithData:attributionDetails from:ApphudAttributionProviderAppleSearchAds identifer:nil callback:nil];
        }
    }];
}
```
{% endtab %}
{% endtabs %}

## View Apple Search Ads Attribution Data in Apphud

Regardless of what of two methods you use you can view attribution data from Apple Search Ads in Apphud charts or in user page.

![](../../.gitbook/assets/asa\_charts.png)

![](../../.gitbook/assets/apple-search-ads-view-user.png)

## Troubleshooting

### I see `Undetermined [0123456789]` attribution in Charts

Make sure your credentials are accurately set up as per [documentation above](apple-search-ads.md#how-does-integration-work).

### I don't see any attribution data in Charts

Make sure you pass attribution information from within the app. See [Step 1](apple-search-ads.md#how-does-integration-work) of the documentation.

### I unable to paste public key copied from Apphud

In this case generate your own public-private key pair on your computer. Please follow these two steps:

#### 1. Gerenate private key

To generate private key run in Terminal:

```
openssl ecparam -genkey -name prime256v1 -noout -out private-key.pem
```

Paste this private key contents to Apple Search Ads integration page in Apphud by clicking on _"paste it"_ button. See the screenshot below:

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

#### 2. Generate public key

To extract public key from your private key run in Terminal:

```
openssl ec -in private-key.pem -pubout -out public-key.pem
```

Paste this public key in your Apple Search Ads settings page of Apple ID account with API Account Manager role.&#x20;

Use generated team id, client id and key id values and paste them to Apphud ASA settings page.
