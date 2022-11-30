---
description: Reduced commission rate support in Apphud
---

# App Store Small Business Program

## What happened?

Apple recently announced the App Store Small Business Program, whose goal is to reduce Apple's commission of App Store sales for small businesses from 30% to 15%.

Generally speaking, developers who earn less than $1 million in App Store revenue per year can apply. You can read more about the program [here](https://developer.apple.com/app-store/small-business-program/).

The reduced rate will affect the data in Apphud's analytics as well as the integration events we send to you. So, it's crucial to let us know about membership in the Small Business Program in your iOS app settings.

{% hint style="info" %}
If you’re already a member of the Apple Developer Program and submit your enrollment for the App Store Small Business Program, your proceeds will be adjusted 15 days after the end of the fiscal calendar month in which your enrollment is approved.
{% endhint %}



## How to apply?

To apply for the App Store Small Business Program, browse to the [Apple Developer website](https://developer.apple.com/app-store/small-business-program/). To enroll, you’ll need to be the Account Holder in the Apple Developer Program, review and accept the latest Paid Apps agreement posted December 2020 in App Store Connect, and if applicable, list all of your Associated Developer Accounts.

After you've read the terms of the program, click **Enroll now**. Apple will request a sign-in to your Apple Developer account, and will automatically fill in information like your name, email, and Team ID.

Once you enroll, you will receive an email confirming that your registration is being reviewed.

## Letting us know

To acknowledge Apphud about your participation in the program select an Entry date in the app's settings.

Since a developer could have multiple apps from different companies in their Apphud account, the Small Business Program membership status is set on a per-app basis.

Review your iOS app settings in the Apphud's Settings and you will find the Apple Small Business Program section at the bottom of the page.

![](<../.gitbook/assets/Screenshot 2020-12-21 at 16.47.16.png>)

{% hint style="info" %}
Avoid setting the Entry date to a date in the past. We won't re-send webhooks and integration events for transactions that have already occurred. To ensure the correct data is sent to your integrations, set your effective entry date as soon as possible.
{% endhint %}

## Leaving Apple Small Business Program

If you left the program, you must put an exit date to your iOS app settings as soon as possible, otherwise, we will continue calculating your sales with the reduced commission.
