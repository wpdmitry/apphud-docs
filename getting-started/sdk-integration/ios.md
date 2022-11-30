---
description: This guide describes how to add and use Apphud SDK to your iOS or macOS app.
---

# iOS/macOS

## Requirements

Apphud SDK requires minimum iOS 11.2 and Xcode 10 and Swift version 5.0. for iOS. Minimum OSX 10.14.4 for macOS.

{% hint style="warning" %}
macOS don't support UIKit, currently you can't use Rules in your macOS project.
{% endhint %}

## Installation

Apphud SDK can be installed via CocoaPods, Carthage, Swift Package Manager or manually.

### Install via CocoaPods

Add the following line to your `Podfile`:

```swift
pod 'ApphudSDK'
```

{% hint style="warning" %}
In Objective-C project make sure `use_frameworks!` is added in your `Podfile`.
{% endhint %}

### Install via Carthage

Add the following line to your `Cartfile`:

```swift
github "apphud/ApphudSDK"
```

And then run in the Terminal:

```swift
carthage update
```

### Install via Swift Package Manager

Add package dependency with the following URL:

```swift
https://github.com/apphud/ApphudSDK
```

### Manual Installation

Copy all files from `ApphudSDK` folder to your project from [this](https://github.com/apphud/ApphudSDK) link.

### Kids Category

Latest Apphud SDK version doesn't use AdSupport framework and doesn't access IDFA so it is safe to use SDK for Kids Category apps.

## Configure Apphud SDK

Integration process consists of following parts:

* [Initialize SDK](ios.md#initialize-sdk)
* [Configure push notifications](./#configure-push-notifications)
* [Handle in-app purchases](ios.md#handle-in-app-purchases)
* [Read In-App Purchase Testing Tips](../../testing/ios.md)
* [Handle promoted in-app purchases](ios.md#handle-promoted-in-app-purchases)
* [Migrate existing subscribers (for live apps)](ios.md#migrate-existing-paying-users)
* [Set up analytics integrations (iOS part)](ios.md#match-user-ids-for-integrations)

## Initialise SDK

To initialise Apphud SDK you will need SDK Token. It is a unique identifier of your Apphud application. You can get it in your Apphud application settings under `General` tab.

Basic initialisation looks like this:

{% tabs %}
{% tab title="Swift" %}
```swift
import ApphudSDK

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

  Apphud.start(apiKey: "YOUR_API_KEY")
  
  // the rest of your code
  return true
}
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
#import <ApphudSDK-Swift.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    
    // set observerMode to YES if you are running SDK in Observer (Analytics) mode.
    // set your custom userID or nil to let Apphud automatically generate User ID (recommended)
    [Apphud startWithApiKey:@"YOUR_API_KEY" userID:@"CUSTOM_USER_ID_OR_NIL" observerMode:NO];
    // the rest of your code
    return YES;
}
```
{% endtab %}
{% endtabs %}

### Initialisation Options

There are additional parameters, like setting your custom unique User ID or running the SDK in [observer mode](../observer-mode.md):

{% tabs %}
{% tab title="Swift" %}
```swift
Apphud.start(apiKey: "API_KEY", userID: "CUSTOM_USER_ID", observerMode: true)
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
[Apphud startWithApiKey:@"API_KEY" userID:@"CUSTOM_USER_ID" observerMode:NO];
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
When `observerMode` is `true`, Apphud SDK will not finish transactions automatically and will only listen for purchases. If you handle payments by your own code, then set `true`. Otherwise, if you purchase products using `Apphud.purchase(product){}` method, then you should set `observerMode` parameter to `false`. Default value is `false`.
{% endhint %}

You can also initialise SDK with custom Device ID. This should be used if you plan to use logout / login features. This method can also be used for user uniqueness to be by your own User ID.\
&#x20;You can safely pass the same identifier to Device ID and User ID:

```swift
Apphud.startManually(apiKey: "YOUR_API_KEY", userID: "SOME_USER_ID", deviceID: "SOME_USER_ID")
```

{% hint style="info" %}
More information regarding User ID uniqueness and User merging can be found [here](common.md).
{% endhint %}

Log out method will clear all saved data and reset SDK to uninitialised state:

```swift
// log out:
Apphud.logout()
// then start Apphud SDK again:
Apphud.startManually(apiKey: "YOUR_API_KEY", userID: "ANOTHER_USER_ID", deviceID: "ANOTHER_USER_ID")
```

## Configure Push Notifications

Configuring [push notifications](../push.md) is highly recommended in order to use [Rules](../../rules-and-screens/rules.md) – a powerful feature that lets you increase your app revenue by automatically offering a discount to a user at the specified moment.

## Configure App Store Server Notifications

Make sure you have correctly set up App Store Server Notifications. It helps to detect in-app purchase events in real-time. Read more [here](../creating-app.md#app-store-server-notifications).

## Handle In-App Purchases

{% hint style="info" %}
If you have a live app and already implemented purchasing logic, it's **not** necessary to rewrite your purchase code with Apphud methods. Apphud SDK will still automatically track all purchases in your app.
{% endhint %}

Apphud SDK provides a set of methods to manage subscriptions and non-renewing purchases. All these methods can be used regardless of how you purchased the product (via Apphud SDK or your existing code).

### &#x20;Get Paywalls (version 2.3.0 or above)

&#x20;To get a paywalls use:&#x20;

First option - “paywalls” Returns paywalls with their `SKProducts`, if configured in Apphud Products Hub. Returns `nil` if StoreKit products are not yet fetched from the App Store. To get notified when paywalls are ready to use, use `paywallsDidLoadCallback` – when it’s called, paywalls are populated with their `SKProducts`.

{% tabs %}
{% tab title="Swift" %}
```swift
var paywall: ApphudPaywall?
var products: [ApphudProduct]?

Apphud.paywalls.map { (paywalls) in
     // retrieve current paywall with identifier
        paywall = paywalls.first(where: { $0.identifier == "current_paywall_id" })

     // retrieve the products [ApphudProduct] from current paywall
        products = paywall?.products
}

```
{% endtab %}
{% endtabs %}

Second option - “paywallsDidLoadCallback” callback is called when paywalls are fully loaded with their StoreKit products. Callback is called immediately if paywalls are already loaded. It is safe to call this method multiple times – previous callback will not be overwritten, but will be added to array and once paywalls are loaded, all callbacks will be called.

{% tabs %}
{% tab title="Swift" %}
```swift
var paywall: ApphudPaywall?
var products: [ApphudProduct]?

Apphud.paywallsDidLoadCallback { (paywalls) in
     // retrieve current paywall with identifier
        paywall = paywalls.first(where: { $0.identifier == "current_paywall_id" })

     // retrieve the products [ApphudProduct] from current paywall
        products = paywall?.products
}

```
{% endtab %}
{% endtabs %}

Paywall is an array of `ApphudPaywall` objects. `ApphudPaywall` contains the list of products `[ApphudProducts]` , paywall’s identifier, and several other properties. To show Products in your app you need to get a Paywall by its identifier.

{% hint style="warning" %}
Please NOTE:

1. &#x20;You have to use methods `Apphud.paywallShown(paywall)` and `Apphud.paywallClosed(paywall)` if you want to show these events in Apphud. We don't track them automatically.&#x20;
2. The method`Apphud.getPaywalls()`has been deprecated in 2.3.0
{% endhint %}

### Get StoreKit Products

{% hint style="warning" %}
Please NOTE: the method`Apphud.products()`has been deprecated. Use `Apphud.getPaywalls`instead.
{% endhint %}

Apphud automatically fetches `SKProduct` objects upon launch. Make sure products identifiers are [added](https://docs.apphud.com/getting-started/adding-products) in Apphud products. To get your products call:

{% tabs %}
{% tab title="Swift" %}
```swift
// returns nil, if products are not yet loaded from the App Store
Apphud.products()
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
[Apphud products];
```
{% endtab %}
{% endtabs %}

Keep in mind that `Apphud.products()` array is `nil` at launch. It takes some time to fetch product identifiers from Apphud and later load `SKProducts` from StoreKit. To get notified when products are loaded, use **any** of the following:

* `productsDidFetchCallback(_ callback: @escaping ([SKProduct]) -> Void)` method.
* `didFetchProductsNotification()` notification method.
* `apphudDidFetchStoreKitProducts(`**`_`**` ``products: [SKProduct])` delegate method of `ApphudDelegate`.

You can use whatever method you want.

You can also force refresh products by calling `refreshStoreKitProducts(_ callback: (([SKProduct]) -> Void)?)` method. A new request will be sent to the App Store for fetching `SKProducts` even if initial request is still loading. So you should only use this method as a fallback in your UI. See `Apphud.swift` file for details.

### Make a Purchase

To make a purchase call:

{% tabs %}
{% tab title="Swift" %}
```swift
Apphud.purchase(product) { result in
   if let subscription = result.subscription, subscription.isActive(){
      // has active subscription
   } else if let purchase = result.nonRenewingPurchase, purchase.isActive(){
      // has active non-renewing purchase
   } else {
      // handle error or check transaction status.
   }
}
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
[Apphud purchase:product callback:^(ApphudPurchaseResult * result) {
    if (result.subcription.isActive){
      // has active subscription
    } else if (result.nonRenewingPurchase.isActive){
      // has active non-renewing purchase
    } else {
      // handle error or check transaction status
    }
}];
```
{% endtab %}
{% endtabs %}

This method will return an `ApphudPurchaseResult` object, which contains subscription model with all info about your subscription. `ApphudPurchaseResult` may also contain `transaction`, `error` and `nonRenewingPurchase` objects in case user purchased non-renewing purchase. See `ApphudPurchaseResult.swift` and `ApphudSubscription.swift` files for details.

You can also read [In-App Purchase Testing Tips](../../testing/ios.md).

### Check Subscription Status

{% tabs %}
{% tab title="Swift" %}
```swift
Apphud.hasActiveSubscription()
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
[Apphud hasActiveSubscription];
```
{% endtab %}
{% endtabs %}

Returns `true` if user has active subscription. Use this method to determine whether to unlock premium functionality to the user.&#x20;

### Get Subscription Details

To get subscription object (which contains expiration date, autorenewal status, etc.) use the following method:

{% tabs %}
{% tab title="Swift" %}
```swift
Apphud.subscription()
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
[Apphud subscription];
```
{% endtab %}
{% endtabs %}

See `ApphudSubscription.swift` file for details.

### Check Non-renewing Purchase Status

Use this method to check whether the user has purchased in-app purchase and it's not refunded. Returns `false` if was never purchased or is refunded.

{% tabs %}
{% tab title="Swift" %}
```swift
Apphud.isNonRenewingPurchaseActive(productIdentifier: "productID")
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
[Apphud isNonRenewingPurchaseActiveWithProductIdentifier:@"producID"];
```
{% endtab %}
{% endtabs %}

### Get Non-renewing Purchase Details

To get non-renewing purchases, which contain purchase date, product identifier and cancellation date, use the following method:

{% tabs %}
{% tab title="Swift" %}
```swift
Apphud.nonRenewingPurchases()
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
[Apphud nonRenewingPurchases];
```
{% endtab %}
{% endtabs %}

It will return array of all non-renewing in-app purchases user has ever purchased. In-app purchases are sorted by purchase date.

### Restore Purchases

If your app doesn't have a login system, which identifies a premium user by his credentials, then you need a "restore" mechanism. If you already have a "restore purchases" mechanism by calling `SKPaymentQueue.default().restoreCompletedTransactions()`, then you have nothing to worry about: Apphud SDK will automatically intercept and send the latest App Store Receipt to Apphud servers when your restoration is completed. However, better to call our restore method from SDK:

{% tabs %}
{% tab title="Swift" %}
```swift
Apphud.restorePurchases{ subscriptions, purchases, error in 
   if Apphud.hasActiveSubscription(){
     // has active subscription  
   } else {
     // no active subscription found, check non-renewing purchases or error
   }
}
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
[Apphud restorePurchasesWithCallback:^(NSArray<ApphudSubscription *> * _Nullable subscriptions, NSArray *purchases, NSError * _Nullable error) {
   if (Apphud.hasActiveSubscription){
     // has active subscription
   } else {
     // no active subscription found, check non-renewing purchases or error
   }
   
}];
```
{% endtab %}
{% endtabs %}

Basically it just sends App Store Receipt to Apphud and returns subscriptions (or `nil`, if subscriptions are never purchased), non-renewing purchases (or `nil`, if there are no any) and an optional error.

## Handle Promoted In-App Purchases

{% hint style="info" %}
Do not get confused with Promotional Offers! Promoted in-app purchases are the ones that appear in the App Store page.
{% endhint %}

If you have in-app purchases that can be purchased directly from the App Store, you should implement a logic to continue a payment in the app.

To continue an in-app purchase transaction initiated from the App Store page, please implement the following `ApphudDelegate` method:

{% tabs %}
{% tab title="Swift" %}
```swift
func apphudShouldStartAppStoreDirectPurchase(_ product: SKProduct) -> ((ApphudPurchaseResult) -> Void) {
    // manage your UI here, show a progress hud, etc.
    let callback : ((ApphudPurchaseResult) -> Void) = { result in 
        // check the result, hide a progress hud, etc.
    }
    return callback
}
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
- (void (^)(ApphudPurchaseResult * _Nonnull))apphudShouldStartAppStoreDirectPurchase:(SKProduct *)product {
    // manage your UI here, show a progress hud, etc.
    return ^(ApphudPurchaseResult * _Nonnull result) {
        // check the result, hide a progress hud, etc.
    };
}
```
{% endtab %}
{% endtabs %}

You must return a callback block which will be called when a payment is finished. If you don't implement this method or return `nil` then a payment will not start; you can also save the product and return nil to initiate a payment later by yourself. You can also read [Apple documentation](https://developer.apple.com/documentation/storekit/in-app\_purchase/promoting\_in-app\_purchases) for details.

## Migrate Existing Paying Users

Please read [here](../data-migration-guide.md).

## Match User IDs for integrations

Some integrations require you to match user ids between Apphud and corresponding integration. Please see documentation for your integration for details.

## Testing Integrations in Sandbox

To test integrations, ensure that test credentials are provided and make a sandbox in-app purchase.

{% hint style="success" %}
Starting iOS 14 you can reset your trial eligibility in iOS Settings > App Store
{% endhint %}

Apphud will send all subscription events of current user to your test analytics, if test credentials are set in integration settings.

{% hint style="success" %}
Sandbox events will never be sent to your production integrations. If test credentials are not provided, sandbox events will not be sent anywhere.
{% endhint %}

{% hint style="info" %}
You can also click on "Send Test Event" near the integration's "..." button. This feature is available only for some Integrations.
{% endhint %}

## User Properties

Please follow [this](../user-properties.md) guide.

## Other

### &#x20;User Eligibility for Introductory Offer

You can read more about eligibility testing [here](../../testing/ios.md#testing-eligibilities).

You can use Apphud to determine if user is eligible for introductory offer:

{% tabs %}
{% tab title="Swift" %}
```swift
// Check eligibility for introductory offer
Apphud.checkEligibilityForIntroductoryOffer(product: myProduct) { result in
  // handle result
}

// Check eligibility for multiple products at one call
Apphud.checkEligibilitiesForIntroductoryOffers(products: products) { resultDict in
    // handle result
}
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
// Check eligibility for introductory offer
[Apphud checkEligibilityForIntroductoryOfferWithProduct:myProduct callback:^(BOOL eligible) {
    // handle result
}];
    
// Check eligibility for multiple products at one call
[Apphud checkEligibilitiesForIntroductoryOffersWithProducts:productsArray callback:^(NSDictionary * resultDict) {
    // handle result
}];
```
{% endtab %}
{% endtabs %}

### User Eligibility for Promotional Offer

You can read more about eligibility testing [here](../../testing/ios.md#testing-eligibilities).

You can also use Apphud to determine if user is eligible for promotional offer:

{% tabs %}
{% tab title="Swift" %}
```swift
// Check eligibility for promotional offer
Apphud.checkEligibilityForPromotionalOffer(product: myProduct) { result in
  // handle result
}

// Check eligibility for multiple products at one call
Apphud.checkEligibilitiesForPromotionalOffers(products: products) { resultDict in
    // handle result
}
```


{% endtab %}
{% endtabs %}

## iOS SDK Reference

iOS SDK Reference is available [here](https://apphud.github.io/ApphudSDK/documentation/apphudsdk/).
