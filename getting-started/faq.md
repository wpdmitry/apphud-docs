---
description: Here are the answers to frequently asked questions about Apphud.
---

# FAQ

## Common Questions

### **What platforms do you support?**

Currently we support iOS and Android.

### **What SDKs do you have?**

Currently we have following open-source SDKs:

* [iOS (Swift)](https://github.com/apphud/ApphudSDK)
* [Android (Kotlin)](https://github.com/apphud/ApphudSDK-Android)
* [React Native (React)](https://github.com/apphud/ApphudSDK-React-Native)
* [Flutter (Dart)](https://github.com/apphud/ApphudSDK-Flutter)

### **Do you support Huawei Store?**

No, we only support Google Play store.

### What does Apphud do?

Apphud is a platform for developers to integrate and analyze subscriptions in iOS and Android apps.&#x20;

* Implement subscriptions in your mobile app in a few lines of code.
* Non-renewing purchases are also supported.
* View and analyze subscription metrics. Add Integrations a large set of analytics and marketing tools: Amplitude, Mixpanel, AppsFlyer, Branch, Adjust, etc.
* Increase app revenue up to 5% by sending automated discounts for lapsed customers.
* Learn why customers cancel trials and subscriptions.
* Fix failed renewals by sending Push notifications and in-app reminders to update billing info.
* Run A/B experiments to find your best paywall screen
* Optimize for purchase events in your marketing campaigns

### Do I need to rewrite my purchase flow using Apphud SDK?

No. You don’t need to replace your existing code with Apphud SDK. You can run Apphud in observer mode and only listen for purchases.

### Can I use Apphud just for analytics?

Yes, you can. In this case all you need is to integrate SDK.

You will be able to view Dashboard and Users list. However, if you want to use Integrations, you need to add more code. See docs describing how to add desired integration. If you would like to use Rules, implement Push Notifications, as described [here](push.md).

### How should I pass Advertising Identifier (IDFA) in iOS 14.5?

Please read [here](idfa-ios-14.md).

### **What timezone is used in Apphud?**

For Dashboard and Charts we use UTC or Browser timezone based on your setting. There is an option to switch between the two time zones.

In Events and Users pages, items are sorted by UTC date. However, local date is also displayed near UTC date.

However, when viewing user page, all dates are displayed in your browser's timezone.

### **How do you convert currencies?**

US Dollar is a base currency in Apphud. All transactions are automatically converted to USD by the exchange rates at the time of event using [OpenExchangeRates](https://openexchangerates.org/). We update conversion rates several times a day.

### **What currency do you use for sending revenue in Integrations?**

When sending revenue to 3rd party analytics platforms, we send local currency where applicable. In particular, we send revenue in local currency to AppsFlyer, Branch and Adjust and send revenue in USD to Amplitude and Mixpanel.

### **How does Apple charge users for subscription upgrades?**

It depends on subscription level and subscription duration of current and purchasing subscription. For example, if the user purchased promo offer of the same subscription, user will be charged only after current period is over. However, if the user purchased another subscription, he may be charged immediately with partial refund of remainder of current subscription if new subscription duration is the same or subscription level is higher. Read more about subscription levels [here](https://blog.apphud.com/subscription-levels/).

### **Do you support Google Play promo-codes?**

Yes.

### **What is the difference between “In Billing Grace Period” and “In Billing Retry Period”?**

Billing Grace Period is Apple’s new feature. With Billing Grace Period turned on, Apple extends subscription for additional 16 days (or 6 days in case of weekly period). During grace period developer must grant premium access to subscriber. Once Apphud detects grace period, user's subscription goes to _Grace_ state, and Apphud SDK  `isActive()` method will return `true`. Existing billing cycle will not break, which means days within grace period will count as paid days. After grace period is over, if subscription wasn't recovered it will go to _Expired_ state. Apple will still attempt to recover subscription within up to 60 days unless manually canceled by user.

With Billing Grace Period turned off, after subscription expires it goes immediately to _Expired_ state and `isActive()` method returns `false`. Existing billing cycle will break, which means that even if subscription is recovered a new billing cycle will start. Apple will attempt to recover subscription within up to 60 days unless manually canceled by user.

In both cases when subscription is reactivated, it will go to _Regular_ state. You can manage Billing Grace Period feature in your app’s “Features” tab in App Store Connect.

### **Who are the users with anon\_XXX prefix?**

Sometimes you may see in Apphud users with anon\_ prefix in User ID. These are anonymous users.\
Anonymous users are being created from App Store Server Notifications, when our backend fails to find an owner of the receipt from notification. This is uncommon situation and you shouldn't have too much anon users. However here are the situations when anon users are being created:

* Notification is sent for the subscriber that didn't yet update and launch the app with Apphud SDK onboard. When you recently joined Apphud with your existing live app, all user purchase activities from previous app versions will count as anonymous. After the user updates and launches the app with Apphud SDK onboard, he will be automatically de-anonymised.
* App Store Notification arrived earlier than SDK submitted a receipt. This scenario goes away pretty fast – try to refresh the page, probably that anon user was already de-anonymised and merged by SDK.
* Transaction was interrupted and user didn't navigate back to the app. Purchase interruption can happen, for example, when users are navigated to payment settings to approve the transaction or update their payment info or when users need to agree to updated App Store terms and conditions before completing a purchase. See also [Strong Customer Authentication transactions in the European Economic Area](https://developer.apple.com/support/psd2/). If user didn't go back to the app, SDK unable to submit receipt to backend. However, right after the user opens the app, receipt will be submitted automatically.
* Unknown error occurred. SDK failed to submit receipt to our backend for unknown reason. In this case SDK will retry the request until success.

### What will happen if your server is down? Is Apphud stable?

Apphud is absolutely stable. Most of the data is cached on device. However, if there are issues with subscription verification, our SDK tries to re-submit data until success.

### Can I use Apphud to sign my subscription offers?

Yes, you can. Just follow [this guide](promo-offers.md).

### **I have problems with sandbox In-App Purchase testing.**

Please read our [In-App Purchase Testing Tips](../testing/ios.md).

### **How to test integrations?**

Please read [here](sdk-integration/#testing-integrations-in-sandbox).

## Features

#### What are Screens? How to use Screens?

Screens are a part of Rules. As for now, **Rules are available only on iOS** you can only present Screens in your app by using Rules. There are 4 types of Screens are available now:

* _Promo offer screen_. To show a discount for lapsed or existing customers.
* _Survey screen_. To ask a customer a question with a set of available options.
* _Feedback screen_. To ask a customer for a text feedback.
* _Billing issue screen_. To ask a user to update their billing info. Typically, used in case of billing issue.

#### Can I combine Screens?

Yes. You can combine different screens to implement complex scenarios. For example, you may create a survey with a set of options. You may also push another screen if user selects certain option. For example, you may push Promo offer screen with a discount for lapsed subscriber after a user selects “Too expensive” option when answering to a “Why did you cancel a subscription?” question.

#### **Gross revenue inside Rule Analyze section is less than expected.**

There may be three reasons:

* If user purchased free trial offer, he won't be charged immediately.
* If user upgraded to another subscription, he won't be charged immediately in some cases. See: "_How does Apple charge users for subscription upgrades?_ "
* User still may cancel auto renewal before actually being charged.

#### **My customer purchased promo offer from your Screen but wasn't charged.**

See "_Gross revenue inside Rule Analyze section is less than expected._" above.

#### Do you have REST API?

Yes. We have REST API to get current customer by their user ID. REST API is available on paid plans.

#### What are Webhooks? Do you have any?

Apphud can send POST requests to your server about subscription events. These requests are called Webhooks (server-to-server notifications). They are available on paid plans. You can use these events to implement custom logics or send data to in-house analytics. Read more about webhooks [here](../integrations/webhook.md).

## Integrations

#### I can’t see my events in AppsFlyer or not all events are shown.

AppsFlyer shows events in “Events” tab according to app installation date. Let imagine, you select certain date range in AppsFlyer. It will show all events occurred to users who installed the app within this date range. However, under "Activity > Activity Summary > In App Events" AppsFlyer shows all events occurred within selected date range regardless app installation date.

#### Facebook ad campaigns installs are shown as organic.

Apphud only shows data received from attribution platform. If you face this issue, please make sure you accepted [Facebook Advanced Mobile Measurement Terms](https://www.facebook.com/ads/manage/advanced\_mobile\_measurement/app\_based\_tos/). If you have done this already, but attribution still not showing in Apphud, please check documentation of your attribution platform.

## Billing

#### What will happen if I exceed the free plan limit, i.e. my MTR is over $10K? Will Apphud continue working?

Once you exceed the free plan limit, 14-days grace period will start. During this time you should choose and activate paid plan. Otherwise, Integrations and Rules will stop working. Nonetheless, the core functionality of Apphud won’t be disabled. Thus, in-app purchases will continue working in your app.
