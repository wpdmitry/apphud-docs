---
description: This guide describes how to add and configure Telegram integration.
---

# Telegram

Receive notifications about subscription events to [Telegram](https://telegram.org/).

## How to Add Integration?

### Authorize the bot

* On Integrations page in Apphud click on _"Add Integration"_ button for Telegram.
* Click on _"Launch Apphud Bot"_ or find [`@ApphudBot`](http://t.me/apphudbot) in Telegram app.
* Start the bot and enter `/login` command.
* You will be prompted to enter your Apphud account email address.&#x20;
* Get a security code that will be sent with an email.
* Enter this security code in a bot chat.
* Bot is now authorized! Now link your app.

### Link your app to receive notifications

* Once authorized, you can enter `/link_apps` **** command to select the app and environments that you need.
* You can use `/unlink_apps` command to disable connection with your app.

### Adding bot to a group

You can add Apphud bot to a group or channel to receive notifications there.&#x20;

{% hint style="danger" %}
Authorizing the bot directly in a group will not work. You must authorize it using private chat first.
{% endhint %}

* Authorize bot using private chat. Do **not** call `/link_apps` yet.
* Add bot to your desired group or channel.
* Call `/link_apps@ApphudBot` inside a group to link your app with it.
* If you have already linked your app with private chat, don't worry, you can re-link your app at any time.

## Events

This is a table of all possible events that are being sent to Telegram.

{% hint style="info" %}
You can get more details regarding events [here](../../events/events.md).
{% endhint %}

| Event                                                                             | Default Name                     |
| --------------------------------------------------------------------------------- | -------------------------------- |
| **TRIAL PERIOD**                                                                  | ****                             |
| Trial period started                                                              | `Trial Started`                  |
| Successful conversion from trial period to regular subscription                   | `Trial Converted`                |
| Failed conversion from trial period to regular subscription                       | `Trial Expired`                  |
| **INTRODUCTORY OFFER**                                                            |                                  |
| Introductory offer started                                                        | `Intro Started`                  |
| Introductory offer renewed                                                        | `Intro Renewed`                  |
| Successful conversion from introductory offer to regular subscription             | `Intro Converted`                |
| Failed conversion from introductory offer to regular subscription or failed renew | `Intro Expired`                  |
| Refund during introductory offer                                                  | `Intro Refunded`                 |
| **REGULAR SUBSCRIPTION**                                                          |                                  |
| Subscription started                                                              | `Subscription Started`           |
| Subscription renewed                                                              | `Subscription Renewed`           |
| Subscription expired                                                              | `Subscription Expired`           |
| Subscription refunded                                                             | `Subscription Refunded`          |
| **PROMOTIONAL OFFER**                                                             |                                  |
| Promotional offer started                                                         | `Promo Started`                  |
| Promotional offer renewed                                                         | `Promo Renewed`                  |
| Successful conversion from promotional offer to regular subscription              | `Promo Converted`                |
| Failed conversion from promotional offer to regular subscription or failed renew  | `Promo Expired`                  |
| Refund during promotional offer                                                   | `Promo Refunded`                 |
| **CANCELLATIONS**                                                                 |                                  |
| Trial Canceled                                                                    | `Trial Canceled`                 |
| Subscription Canceled                                                             | `Subscription Canceled`          |
| Autorenew disabled (Deprecated)                                                   | `Autorenew Disabled`             |
| Autorenew enabled                                                                 | `Autorenew Enabled`              |
| **OTHER EVENTS**                                                                  |                                  |
| Non renewing purchase                                                             | `Non Renewing Purchase`          |
| Non renewing purchase refunded                                                    | `Non Renewing Purchase Refunded` |
| Billing Issue                                                                     | `Billing Issue`                  |

## Send Test Event

You can test Telegram integration by clicking _"…"_ and then in dropdown click on _"Send test event"_:

![](<../../.gitbook/assets/telegram-test-event (1).png>)
