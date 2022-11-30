---
description: >-
  If you have a purchase system and/or want to test Apphud without full
  integration, you can use Observer mode.
---

# Observer Mode

If you have a purchase system and/or want to test Apphud without full integration, you can use Observer mode.

To use Apphud SDK in Observer mode:

{% tabs %}
{% tab title="iOS/macOS" %}
In Observer Mode Apphud iOS SDK **will not finish transactions** automatically and will only listen for purchases. Use **observerMode** parameter in `start` method:

```
Apphud.start(apiKey: "apiKey", userID: Apphud.userID(), observerMode: true)
```
{% endtab %}

{% tab title="Android" %}
On Android initialization in Observer mode doesn't have any changes, because Android doesn't have actual observer mode.

However, If you use your own billing then you should **sync purchases** every time user makes any purchase or restoration. Just call after purchase or restore:

```
Apphud.syncPurchases()
```

Also, it is highly recommended to set up `obfuscatedAccountId` in `BillingFlowParams` object. See [here](observer-mode.md#set-obfucatedaccountid-parameter-on-android) for details.

{% hint style="danger" %}
Keep in mind, that you are responsible for acknowledging or consuming all purchases on Android while using Apphud SDK in Observer mode!
{% endhint %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Don't forget to set up the App Store / Google server notifications in Apphud settings in order to get real time updates.
{% endhint %}

### Observer Mode vs Full Mode integration

| Advantages:             | Observer Mode | Full Mode |
| ----------------------- | :-----------: | :-------: |
| Integrations            |     Yes\*     |   Yes\*   |
| Analytics               |      Yes      |    Yes    |
| Paywalls management     |       No      |    Yes    |
| Experiments (A/B Tests) |   Yes\*\*\*   |    Yes    |
| Rules (iOS)             |    Yes\*\*    |  Yes\*\*  |
| Web2App                 |      Yes      |    Yes    |

### Experiments(A/B Tests) in Observer Mode

If you want to use A/B experiments while running SDK in `Observer Mode` you should manually send paywall identifier to Apphud using this method:

{% tabs %}
{% tab title="iOS/macOS" %}
You must call this method right before your own purchase method.

```
Apphud.willPurchaseProductFromPaywall("main_paywall")
```
{% endtab %}

{% tab title="Android" %}
You must call this method right after your own purchase method.

```
Apphud.syncPurchases(paywallIdentifier: "main_paywall")
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Note that you have to add paywalls in Apphud Dashboard > Product Hub > Paywalls.
{% endhint %}



\* requires few more lines of code, like User ID Matching. See documentation of your integration.

\*\* requires push notification handling. See [here](push.md#handle-incoming-push-payload).

\*\*\* requires additional client functions.

### Pass `obfucatedAccountID` parameter (Android)

To increase data matching in Observer Mode, it is highly recommended to set up this parameter while using your own billing:

{% code title="Android (Kotlin)" overflow="wrap" %}
```kotlin
val builder = BillingFlowParams.newBuilder().setSkuDetails(skuProduct)
builder.setObfuscatedAccountId(Apphud.deviceId())
```
{% endcode %}
