---
description: >-
  This guide describes what are Screens and how to configure them using Apphud
  Visual Editor.
---

# Screens

Using Apphud Visual Editor you can create different screens without coding. These screens can be used in [Rules](rules.md) to win back lapsed customers, get cancellation insights, reduce churn and in many other cases.

{% hint style="success" %}
You can also read our great [blog post](https://apphud.com/blog/understanding-rules-in-apphud) about Rules & Screens.
{% endhint %}

{% hint style="info" %}
You can read more about Rules in [this section](rules.md).
{% endhint %}

There are 4 types of screens available in Apphud Visual Editor:

* **Promo offer screen.** This is a purchase screen with a personal discount. Based on promotional offers for iOS subscriptions.
* **Survey screen.** This is a screen showing a test where you can ask user for something with a set of different options.
* **Feedback screen.** This is a screen showing a question without any predefined options. A user can leave feedback using this screen.
* **Billing issue screen.** This is screen usually shown in case of billing issue. It contains a button by tapping on which user will be redirected to his App Store billing info settings.&#x20;

Apphud offers many templates of purchase screens for every taste.

## Configure Screen

Pick a screen you would like to use in _"Screens"_ section of Apphud and properly configure it.

{% hint style="warning" %}
We require to upload Subscription Key in order to use Promo offer screen. Here is the [guide](../getting-started/promo-offers.md) how to do it.
{% endhint %}

While configuring _Confirmation button_ in Promo offer screens you will have to provide _Product ID_ and _Promotional offer ID_ that will be purchased when a user taps the button.&#x20;

You have an option to use just the _Product ID_ (with lower price) and not adding _Promotional offer ID._

{% hint style="info" %}
You can read more about products configuration [here](broken-reference) and about promotional offers [here](../getting-started/promo-offers.md).
{% endhint %}

You can also use _Price macroses_ in any text. These _macroses_ will be replaced with a proper value of Subscription or Promotional offer price using a user's local currency.
