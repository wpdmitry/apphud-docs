---
description: >-
  This guide describes events that are registered by Apphud and can be sent to
  third party analytics services and messengers.
---

# Events

## Free Trial Events

### Trial Started

This event is created when user purchases a subscription with free trial period.

Event is sent to analytics under `trial_started` name.

### Trial Active

This event is created whenever a free trial has not been canceled for at least 1 hour after the trial start date.

Event is sent to analytics under `trial_active` name.

### Trial Converted

This event is created after trial period is finished and user has been charged for the first time with regular subscription price.

Event is sent to analytics under `trial_converted` name.

### Trial Canceled

This event is created when auto-renew is turned off for any free trial subscription. Note that current subscription period may not yet be over.

Event is sent to analytics under `trial_canceled` name.

### Trial Expired

This event is created after free trial period is over without conversion.

Event is sent to analytics under `trial_expired` name.

Has the following expiration reasons (iOS only):

* User canceled subscription manually – `user_canceled`;
* There was a billing error – `billing_issue`;
* User did not agree to a recent price increase – `declined_price_increase`;
* Product was not available for purchase at the time of renewal – `unavailable_product`;
* Unknown error occurred – `unknown_error`.

## Regular Subscriptions

These are events that are created for a subscription with a regular price.

### Subscription Started

This event is created when user has purchased subscription with a regular price.

Event is sent to analytics under `subscription_started` name.

### Subscription Renewed

This event is created when subscription has been renewed and user has been charged a regular price.

Event is sent to analytics under `subscription_renewed` name.

### Subscription Canceled

This event is created when auto-renew is turned off for any paid subscription.

Event is sent to analytics under `subscription_canceled` name.

### Subscription Expired

This event is created when subscription period is over without renew.

Event is sent to analytics under `subscription_expired` name.

{% hint style="info" %}
This event has the same set of expiration reasons as `trial expired` event.
{% endhint %}

### Subscription Refunded

This event is created when user has refunded subscription.

Event is sent to analytics under `subscription_refunded` name.

{% hint style="info" %}
This event has the same set of refund reasons as a refund during introductory offer.
{% endhint %}

## Paid Introductory Offers

Introductory offer is a discount that can be applied to new subscribers.

{% hint style="success" %}
You can read more about iOS introductory offer types in our [blog](https://blog.apphud.com/introductory-offers-in-ios/).
{% endhint %}

### Intro Started

This event is created when user purchases a subscription with introductory offer.

Event is sent to analytics under `intro_started` name.

### Intro Renewed

This event is created when subscription renews during introductory offer.

Event is sent to analytics under `intro_renewed` name.

### Intro Converted

This event is created when introductory offer is finished and user has been charged for the first time with regular subscription price.

Event is sent to analytics under `intro_converted` name.

### Intro Expired

This event is created when subscription period is over without renew.

Event is sent to analytics under `intro_expired` name.

{% hint style="info" %}
This event has the same set of expiration reasons as trial period.
{% endhint %}

### Intro Refunded

This event is created when user has refunded subscription with an introductory offer.

Event is sent to analytics under `intro_refunded` name.

Has the following refund reasons (iOS only):

* User canceled his subscription due to an actual or perceived issue within your app – `app_issue`;
* Subscription was canceled for another reason, for example, if the user made the purchase accidentally – `another_reason`.

## Promotional Offers

In iOS Apps these are purchases made by using promotional offers.

In Android these are purchases made by using promo codes.

### Promo Started

This event is created when user activates a promotional offer (iOS) or activates promo code (Android).

Event is sent to analytics under `promo_started` name.

### Promo Renewed (iOS only)

This event is created when subscription renews during promotional offer with "pay as you go" type.

Event is sent to analytics under `promo_renewed` name.

### Promo Converted

This event is created when promotional offer is finished and user has been charged with regular subscription price.

Event is sent to analytics under `promo_converted` name.

### Promo Expired

This event is created when subscription lapses during promotional offer.

Event is sent to analytics under `promo_expired` name.

{% hint style="info" %}
This event has the same set of expiration reasons as trial period.
{% endhint %}

### Promo Refunded (iOS only)

This event is created when user has refunded subscription with a promotional offer through Apple Care support.

Event is sent to analytics under `promo_refunded` name.

Has the following refund reasons:

* User canceled his subscription due to an actual or perceived issue within your app – `app_issue`;
* Subscription was canceled for another reason, for example, if the user made the purchase accidentally – `another_reason`.

## Paywall Events

### Paywall Shown

This event is created when paywall has been viewed by a user.

Event is sent to analytics under `paywall_shown` name.

{% hint style="info" %}
This event is sending manually with paywallShown() method.
{% endhint %}

### Paywall Closed

This event is created when the user has closed the paywall with a cross icon or any other cancellation link.

Event is sent to analytics under `paywall_closed` name.

{% hint style="info" %}
This event is sending manually with paywallClosed() method.
{% endhint %}

### Paywall Checkout Initiated

This event is created when the user tap on the selected product (or Continue button) on the paywall and system checkout popup appears.

Event is sent to analytics under `paywall_checkout_initiated` name.

### Paywall Checkout Cancelled

This event is created when the user cancels a purchase on a system checkout popup.

Event is sent to analytics under `paywall_checkout_cancelled` name.

## Other Events

### Autorenew Enabled (iOS only)

This event is created when subscription auto-renew is turned back on.

Event is sent to analytics under `autorenew_enabled` name.

### Autorenew Disabled (Deprecated, iOS only)

This event is created when subscription auto-renew is turned off. Includes both trial and paid subscriptions.

_This event is marked for removal. Please use Trial Canceled and Subscription Canceled Events._&#x20;

Event is sent to analytics under `autorenew_disabled` name.

### Billing Issue

This event is created when subscription renewal failed because of billing issue.

Event is sent to analytics under `billing_issue` name.

### Non Renewing Purchase

This event is created when user purchased non-renewable product.

Event is sent to analytics under `non_renewing_purchase` name.

### Non Renewing Purchase Refunded

This event is created when user has refunded non-renewable product.

Event is sent to analytics under `non_renewing_purchase_refunded` name.

### User Created

This event is created when user is created in Apphud.

Event is sent to analytics under `user_created` name.

{% hint style="warning" %}
This event is not created by default. You should first enable it in integration settings, then it will start appearing.
{% endhint %}

## When Events are Created?

Apphud regularly sends requests to App Store or Google Play to update subscriptions state and to create new events if necessary.
