---
description: This guide describes how to add and use Apphud SDK to your Flutter app
---

# Flutter

## Installation

Please check the [guide at pub.dev](https://pub.dev/packages/apphud/install).

## Initialize SDK

To initialize Apphud SDK you will need API Key. It is a unique identifier of your Apphud application. You can get it in your Apphud application settings under General tab

Basic initialization looks like this:

```jsx
await Apphud.start(apiKey: "apiKey");
```

Initialization options:

| property     | type   | platform     | required |
| ------------ | ------ | ------------ | -------- |
| apiKey       | String | iOS, Android | yes      |
| userId       | String | iOS, Android | no       |
| deviceId     | String | Android      | no       |
| observerMode | Bool   | iOS          | no       |

You can also initialise SDK with custom Device ID. This should be used if you plan to use logout / login features. This method can also be used for user uniqueness to be by your own User ID.\
&#x20;If you purchase IAPs using Apphud SDK, you should pass `observerMode` as `false`. You can safely pass the same identifier to Device ID and User ID:

```jsx
await Apphud.startManually(
          apiKey: "apiKey",
          userID: "userID",
          deviceID: "userID",
          observerMode: true,
        );
```

{% hint style="info" %}
More information regarding User ID uniqueness and User merging can be found [here](common.md).
{% endhint %}

Log out method will clear all saved data and reset SDK to uninitialised state:

```jsx
await Apphud.logout();
```

{% hint style="warning" %}
When adding new subscriptions in Google Play Console, do not add more than one base plans inside existing subscription. Create a separate subscription with a new Product ID instead. [Google Play Product Setup More information](../product-hub/google-play-subscriptions-setup.md)
{% endhint %}

## Get Paywalls (version 2.0.6 or above)

To get a paywall use:

```jsx
await Apphud.getPaywalls() 
```

## Purchase using Apphud SDK

To make a purchase call:

```jsx
await Apphud.purchase(product: product)
```

## Purchase in Observer Mode (Android)

If you use your own billing on Android then you should sync purchases each time user makes any purchase or restoration. Just call after purchase or restore:

```jsx
await Apphud.syncPurchases();
```

{% hint style="danger" %}
Keep in mind, that you are responsible for acknowledging or consuming all purchases in observer mode!
{% endhint %}

## Purchase in Observer Mode (iOS)

Apphud SDK automatically intercepts purchases on iOS and passes receipt data to Apphud servers. No additional code required.

## Check Subscription Status

```jsx
await Apphud.hasActiveSubscription();
```

Returns `true` if a user has an active subscription. Use this method to determine whether to unlock premium functionality to the user.

## Get Products

{% hint style="warning" %}
Please NOTE: the method`Apphud.products()`has been deprecated. Use `Apphud.getPaywalls`instead.
{% endhint %}

Apphud automatically fetches `SKProduct`/`SkuDetails` objects upon launch. Make sure products identifiers are added to Apphud products. To get your products call:

```jsx
await Apphud.products();
```

## Get Subscription Details

To get the subscription object (which contains an expiration date, autorenewal status, etc.) use the following method:

```jsx
await Apphud.subscription();
```

## Check Non-renewing Purchase Status

Use this method to check whether the user has purchased an in-app purchase and it's not refunded. Returns `false` if was never purchased or is refunded.

```jsx
await Apphud.isNonRenewingPurchaseActive("productIdentifier")
```

## Get Non-renewing Purchase Details

To get non-renewing purchases, which contain purchase date, product identifier and cancellation date, use the following method:

```jsx
await Apphud.nonRenewingPurchases();
```

## Get User ID

To get user id you can use this method:

```jsx
await Apphud.userId();
```

## Integrations

Submit attribution data to Apphud from your attribution network provider.

```jsx
 Map<String,dynamic> data = {"key":"value"};
 ApphudAttributionProvider provider = ApphudAttributionProvider.appsFlyer;

await AppHud.addAttribution(data: data, provider: provider);
```

## Restore Purchases&#x20;

If your app doesn't have a login system, which identifies a premium user by his credentials, then you need a "restore" mechanism.

```jsx
await Apphud.restorePurchases();
```

Basically, it just sends App Store Receipt (iOS) or PlayMarket Purchase Tokens (Android) to Apphud and returns subscriptions info (or null, if subscriptions are never purchased), non-renewing purchases (or null, if there are no any), and an optional error.

## Migrate existing purchases

Please read [here](../data-migration-guide.md).
