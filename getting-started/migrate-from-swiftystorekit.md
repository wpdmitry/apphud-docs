---
description: How to migrate your app using SwiftyStoreKit to Apphud Services.
---

# Migrate from SwiftyStoreKit

## Migrate your SwiftyStoreKit app to Apphud

SwiftyStoreKit is a great option to enter the world of iOS In-App Purchases. Apphud is more than just making a purchase and validating receipts.

* Analytics - View key subscription metrics in our [dashboard](https://docs.apphud.com/analyze/dashboard) and [charts](https://docs.apphud.com/analyze/charts), like MRR, Subscriber Retention (Cohorts), Churn rate, ARPU, Trial Conversions, Proceeds, Refunds, and more with outstanding accuracy.
* Experiments (A/B Testing) - Test different In-App Purchases and paywalls. Run experiments to find the best combination of prices and purchase screen parameters that maximize ROI.
* Paywalls - Operate with your products in more convenient way.
* Integrations - Send subscription events to your favorite third-party platforms with automatic currency conversion. Choose from 18 integrations, including AppsFlyer, Adjust, Branch, Firebase, Amplitude, Mixpanel, OneSignal, Facebook, TikTok, and more.
* Rules - Automatically re-engage your customers using in-app interactions and push notification campaigns.
* Cross-Platform - iOS/Mac, Android, Flutter, React Native support.

### 1. SDK Initialization

Initialize Apphud SDK using your API Key:

**Apphud :**

```swift
import ApphudSDK

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
  
    Apphud.start(apiKey: "YOUR_API_KEY")
    return true
}
```

**SwiftyStoreKit :**

```swift
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
    // see notes below for the meaning of Atomic / Non-Atomic
    SwiftyStoreKit.completeTransactions(atomically: true) { purchases in
        for purchase in purchases {
            switch purchase.transaction.transactionState {
            case .purchased, .restored:
                if purchase.needsFinishTransaction {
                    // Deliver content from server, then:
                    SwiftyStoreKit.finishTransaction(purchase.transaction)
                }
                // Unlock content
            case .failed, .purchasing, .deferred:
                break // do nothing
            }
        }
    }
    return true
}
```

**Migration** : Replace SwiftyStoreKit completeTransactions() with the Apphud SDK start() method. If you have a live app with subscriptions or non-renewing purchases, you may want to migrate all your existing and historical data to Apphud. You can use migratePurchasesIfNeeded{} method. For more information please follow [this](https://docs.apphud.com/getting-started/data-migration-guide#client-side-migration) link.

### 2. Load Products

At Apphud, paywalls are used to obtain products. All products of your payment screen are stored on a separate paywall. You can make multiple paywalls for multiple payment screens. Configure paywalls in Apphud Dashboard > Product Hub > Paywalls.

**Apphud :**

<pre class="language-swift"><code class="lang-swift"><strong>// To get notified when paywalls are ready to use, use
</strong>// paywallsDidLoadCallback – when it’s called,
// paywalls are populated with their SKProducts.
        Apphud.paywallsDidLoadCallback { (paywalls) in
            // retrieve current paywall with identifier
            if let paywall = paywalls.first(where: { $0.identifier == "currentPaywallIdentifier" in
                self.products = paywall.products
            })
        }</code></pre>

**SwiftyStoreKit :**

```swift
SwiftyStoreKit.retrieveProductsInfo(["com.test.purchase1"]) { result in
    if let product = result.retrievedProducts.first {
        let priceString = product.localizedPrice!
        print("Product: \(product.localizedDescription), price: \(priceString)")
    }
    else if let invalidProductId = result.invalidProductIDs.first {
        print("Invalid product identifier: \(invalidProductId)")
    }
    else {
        print("Error: \(result.error)")
    }
}
```

**Migration** : Configure products and paywalls in Apphud Dashboard > Product Hub > Paywalls, then replace retrieveProductsInfo() in SwiftyStoreKit with paywallsDidLoadCallback{} . This callback is called when paywalls are populated with their StoreKit products. Callback is called immediately if paywalls are already loaded.

### 3. Make Purchase

**Apphud :**

```swift
// Initiates purchase of `ApphudProduct` object from your `ApphudPaywall` 
// and automatically submits App Store Receipt to Apphud.
Apphud.purchase(product) { (result) in
       if result.error == nil {
          // purchase successfully done
       }
}
```

**SwiftyStoreKit :**

```swift
SwiftyStoreKit.purchaseProduct("com.musevisions.SwiftyStoreKit.Purchase1", quantity: 1, atomically: true) { result in
    switch result {
    case .success(let purchase):
       // purchase successfully done
    case .error(let error):
       // purchase faild 
    }
}
```

**Migration** : Replace SwiftyStoreKit’s `purchaseProduct()` with `Apphud.purchase()` method. Pass an `ApphudProduct` model as a parameter.

### 4. Check Availability Status

Apphud automatically verifies all receipts. You don't need any local receipt validation.

**Apphud :**

```swift
// Returns `true` if user has active subscription 
// or non renewing purchase (lifetime).
if Apphud.hasPremiumAccess() {
  // user have active purchase
}
```

**SwiftyStoreKit :**

```swift
// there is no single сhecking method
// you should track the status by yourself
let appleValidator = AppleReceiptValidator(service: .production, sharedSecret: "your-shared-secret")
SwiftyStoreKit.verifyReceipt(using: appleValidator) { result in
    switch result {
    case .success(let receipt):
        let productId = "my_product_identifier"
        // Verify the purchase of Consumable or NonConsumable
        let purchaseResult = SwiftyStoreKit.verifyPurchase(
            productId: productId,
            inReceipt: receipt)
            
        switch purchaseResult {
        case .purchased(let receiptItem):
            print("\(productId) is purchased: \(receiptItem)")
        case .notPurchased:
            print("The user has never purchased \(productId)")
        }
    case .error(let error):
        print("Receipt verification failed: \(error)")
    }
}
```

**Migration** : Use `Apphud.hasPremiumAccess()` to determine whether or not a user has access to your paid features. You can use `Apphud.subscriptions()` and `Apphud.nonRenewingPurchases()` to get detailed information about subscriptions or non-renewing purchases.

### 5. Restore **P**urchases

**Apphud :**

```swift
// Basically it just sends current App Store Receipt to Apphud 
// and returns subscriptions info.
Apphud.restorePurchases { _, _, _ in
    if Apphud.hasPremiumAccess() {
       // user have active purchase
    }
}
```

**SwiftyStoreKit :**

```swift
SwiftyStoreKit.restorePurchases(atomically: true) { results in
    if results.restoreFailedPurchases.count > 0 {
        print("Restore Failed: \(results.restoreFailedPurchases)")
    }
    else if results.restoredPurchases.count > 0 {
        print("Restore Success: \(results.restoredPurchases)")
    }
    else {
        print("Nothing to Restore")
    }
}
```

**Migration** : Replace SwiftyStoreKit’s `restorePurchases{}` with `Apphud.restorePurchases{}` method.

### 6. In-App Purchase initiated directly from the App Store

Apphud handles purchases initiated through the App Store with `ApphudDelegate’s` method.

**Apphud :**

```swift
import ApphudSDK

func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    Apphud.setDelegate(self)
}

func apphudShouldStartAppStoreDirectPurchase(_ product: SKProduct) -> ((ApphudPurchaseResult) -> Void) {
    // manage your UI here, show a progress hud, etc.
    let callback : ((ApphudPurchaseResult) -> Void) = { result in 
        // check the result, hide a progress hud, etc.
    }
    return callback
}
```

**SwiftyStoreKit :**

```swift
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  
  SwiftyStoreKit.shouldAddStorePaymentHandler = { payment, product in
    // return true if the content can be delivered by your app
    // return false otherwise
}
```

**Migration** : Replace SwiftyStoreKit’s `shouldAddStorePaymentHandler` with `apphudShouldStartAppStoreDirectPurchase{}` delegate method. You must return a callback block which will be called when payment is finished. If you don't implement this method or return `nil` a payment will not start.

### **7.** Migrate Current Subscribers

This way of migration means syncing existing purchases from the app at the first launch. When an existing user updates the app with Apphud SDK onboard, purchases migration should be initiated by the developer. You should do this just once for your paid users. Store flag in your app after the method is called.

```swift
// hasPurchases - is your own boolean value indicating that current user is paying user.
if hasPurchases {    
    Apphud.migratePurchasesIfNeeded {_, _, _ in}     
}
```

### 8. Set up App Store Server Notifications

It is required to set up [App Store Server Notifications](https://docs.apphud.com/getting-started/data-migration-guide#app-store-server-notifications) in order to get data in real-time. If you have user receipts stored on your backend, you can contact us to import them.
