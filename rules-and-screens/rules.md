---
description: >-
  This guide describes how to create and manage Rules to win back lapsed
  subscribers, reduce churn rate, get cancellation insights, and more.
---

# Rules

Apphud may win back lapsed subscribers, reduce churn rate, get cancellation insights and many more using the mechanics below. This mechanics are called Rules. The Rules are a combination of automated push notifications with in-app interactions like surveys, discount offerings, and more, that serve to engage and re-engage subscribers.\
\
**Using Rules developers can:**

• Win back lapsed subscribers \
• Reduce churn rate \
• Get cancellation insights \
• Reduce subscription renewal billing issues \
• Attract non-paying users\
\
All of these and more can be achieved using just a web editor with zero lines of code.

{% hint style="info" %}
In order to make rules work you must:

1. Add App Store Server Notifications URL to your app settings in [App Store Connect](https://appstoreconnect.apple.com/). Read more [here](../getting-started/creating-app.md#app-store-server-notifications-url).
2. Configure Push notifications. [View instructions](../getting-started/push.md) how to do it.
{% endhint %}

You may build a new Rule from scratch or use one of [templates](rule-templates/).

## Why Rules?

* With Apphud Rules you can **increase your monthly app revenue for up to 10%** and get useful insights. Learn more in our [blog post](https://apphud.com/blog/increase-app-revenue).
* **Automatic payment processing** in the in-app screens with powerful Rules-derived revenue analytics are those features that differentiate Apphud’s Rules from other Push Notification SaaS platforms.
* Screens are configured in Web Editor and **doesn't require app resubmission**.

## Create New Rule

Rules can be configured in _"Rules"_ section. To add a new rule, click _"Add a rule"_ button.

### 1. Select [template](rule-templates/) or start from blank rule

### 2. Setup

* **Rule name.** A name of the rule.
* **What type of rule would you like to create?** Choose between manual, scheduled and event-triggered rule types. Manual rules will be performed by a button click, scheduled rule will be performed on a certain time, event-triggered rule will be triggered after certain event.
* **When to perform rule?** Available for event-triggered rules only. Select events that will trigger this rule. You can optionally set up filters for each event.
* **How many times rule can be performed for each user?** If you select "_Just once_", rule will be performed only once per each app user.

### 3. Rules Types

* **Manual Rules** -  Manual Rule lets you run a push notifications campaign with a click. There is no condition by event, just define your audience and set up a push notification and/or in-app screen. Manually triggered push campaigns let you interact with your customers whenever and however you want.\

* **Scheduled Rules** - You can also schedule a Rule for a particular date in the future, for example, Christmas or Thanksgiving day. Deliver important messages and in-app interactions on your specified day and hour. Create as many push notification campaigns as you want.\
  ****\
  ****\* _One-time_ - The rule will be performed just once at the selected time.     \
  \* _Repeating_ - The rule will trigger periodically at the selected days and time.   &#x20;

![Scheduled Rule](<../.gitbook/assets/Снимок экрана 2022-05-06 в 14.20.14.png>)

* **Event-Triggered -** For an event-triggered rule, you can set a delay that is limited to 24 hours max. After the timer fires, a push notification will be sent to a user. And if a user opens an app, an in-app interaction, if set, will be triggered as well.\
  \
  \- "_When to perform rule?_" option - Choose any triggers to perform the rule.\
  \- "_When to execute actions?_" option - You can choose whether to perform rule immediately or after custom delay using _hh/mm_ format.\
  &#x20;\- "_How many times rule can be performed for each user?_" option - You can perform the rule unlimited times per user or only once per user.

![Event-Triggered Rule](<../.gitbook/assets/Снимок экрана 2022-05-06 в 14.21.45.png>)

### 4. User segments

* **For whom rule will be performed?** Define your target audience. Default is "_All Users_".

![For whom rule will be performed?](<../.gitbook/assets/Снимок экрана 2022-05-06 в 14.23.30.png>)

### 5. Actions

* **Send Push notification.** Configure Push notification: set up _Title_ (optional) and _Text_ (required). You may localize Push notification.
* **Present screen.** Select screen that will be shown to a user at next app launch or click "_Build new screen_".

### 6. Review your rule and save changes

Don't forget to enable "_Enable this rule_" checkbox.

### 7. Rule Statuses

![Rules statuses example](<../.gitbook/assets/4 (1).png>)

* **Manual Rules**:\
  \- DRAFT - The rule is in the creation process and one or more of the mandatory screens are empty.\
  \- NEW - The rule was created but not started.\
  \- RUNNING - The rule is in progress, push notifications are being sent.\
  \- COMPLETED - All push notifications has been sent.\
  \- DISABLED - The rule has been disabled.\
  \- ARCHIVED - To hide the rule from the main list, click "_Archive_". It can be recovered (unarchived) for future use.\

* **Event-triggered Rules**:\
  \- DRAFT - The rule is in the creation process and one or more of the mandatory screens are empty.\
  \- NEW - The rule was created but not started.\
  \- RUNNING - Running Rules. They are in this state after launch, waiting for events. Can be edited.\
  \- COMPLETED - All push notifications sent.\
  \- DISABLED - The rule has been disabled.\
  \- ARCHIVED - To hide the rule from the main list, click "_Archive_". It can be recovered (unarchived) for future use.\

* **One-Time Scheduled Rules**:\
  \- DRAFT - The rule is in the creation process and one or more of the mandatory screens are empty.\
  \- NEW - The rule was created but not started.\
  \- UPCOMING - Started rules which are waiting for the execution time.\
  \- RUNNING - The rule is in progress, push notifications are being sent.\
  \- COMPLETED - All push notifications sent.\
  \- DISABLED - The rule has been disabled.\
  \- ARCHIVED - To hide the rule from the main list, click "_Archive_". It can be recovered (unarchived) for future use.\

* **Repeating Scheduled Rules**:\
  \- DRAFT - The rule is in the creation process and one or more of the mandatory screens are empty.\
  \- NEW - The rule was created but not started.\
  \- UPCOMING - Started rules which are waiting for the execution time.\
  \- RUNNING - The rule is in progress, push notifications are being sent.\
  \- COMPLETED - All push notifications sent.\
  \- DISABLED - The rule has been disabled.\
  \- ARCHIVED - To hide the rule from the main list, click "_Archive_". It can be recovered (unarchived) for future use.

## Test Rules

{% hint style="warning" %}
Testing Rules using Local StoreKit purchases is not supported. Please use Sandbox purchases using your sandbox Apple ID / password.
{% endhint %}

To test a rule simply create any and click _"Test"_. Enter user ID on whom you want to test the rule and click Perform now.

![Enter your User id and click "Send"](<../.gitbook/assets/Снимок экрана 2022-05-06 в 14.27.51.png>)

## **Rules delegate methods  (iOS only)**

Rules - an array of notifications in apphud, when the user was shown the rule’s screen then the rule is marked as “Read” and removed from rule notifications response.\
Apphud has the `ApphudUIDelegate.swift` class to improve rule’s experience in your project: Include some functions:

* `func apphudShouldPerformRule` -> You can return false to ignore this rule. You should only do this if you want to handle your rules by yourself. A default implementation is true.
* `func apphudShouldShowScreen` → you can return false to this delegate method if you want to delay the Apphud Screen presentation. The controller will be kept in memory until you present it via the `Apphud.showPendingScreen()`method. If you don't want to show the screen at all, you should check the `apphudShouldPerformRule` delegate method.
* `func apphudScreenPresentationStyle` → Pass your own modal presentation style to Apphud Screens. This is useful since iOS 13 presents in page sheet style by default. To get full screen style you should pass `.fullScreen` or `.overFullScreen`.
* `func apphudScreenDidAppear` → Called when screen successfully loaded and is visible to the user.
* `func apphudDidDismissScreen/apphudScreenWillDismiss` → Notifies that Apphud Screen did dismiss/is about to dismiss.

## Analyze Rules

You can view results of rules efficiency in _"Analyze"_ section. Click "..." and select "Analyze".
