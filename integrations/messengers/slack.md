---
description: This guide describes how to add and configure Slack integration.
---

# Slack

Receive notifications about subscription events to [Slack](https://slack.com/).

## How to Add Integration?

{% tabs %}
{% tab title="Step 1" %}
Add [incoming webhook](https://slack.com/apps/A0F7XDUAZ-incoming-webhooks) in your Slack account.
{% endtab %}

{% tab title="2" %}
Copy given _Webhook URL_.
{% endtab %}

{% tab title="3" %}
At [Apphud](https://app.apphud.com/) go to _"Integrations"_ and add Slack:&#x20;

![](../../.gitbook/assets/slack-adding-integration.png)
{% endtab %}

{% tab title="4" %}
Paste _Webhook URL_ into _"Webhook"_ field. Enter username which will be shown in notifications and channel name:

![](../../.gitbook/assets/slack-name-channel.png)
{% endtab %}

{% tab title="5" %}
You can disable events you don't need:

![](<../../.gitbook/assets/slack-disable-events (1).png>)
{% endtab %}

{% tab title="6" %}
Make sure _"Enable this integration"_ is checked:

![](../../.gitbook/assets/slack-enable-integration.png)
{% endtab %}

{% tab title="✅ 7" %}
Save changes:

![](<../../.gitbook/assets/slack-save (1).png>)
{% endtab %}
{% endtabs %}

## Events

This is a table of all possible events that are being sent to Slack.

{% hint style="info" %}
You can read more about events [here](../../events/events.md).
{% endhint %}

| Event                                                                             | Default Name                     |
| --------------------------------------------------------------------------------- | -------------------------------- |
| **TRIAL PERIOD**                                                                  |                                  |
| Trial period started                                                              | `Trial Started`                  |
| Successful conversion from trial period to regular subscription                   | `Trial Converted`                |
| Failed conversion from trial period to regular subscription                       | `Trial Expired`                  |
| **INTRODUCTORY OFFER**                                                            | ****                             |
| Introductory offer started                                                        | `Intro Started`                  |
| Introductory offer renewed                                                        | `Intro Renewed`                  |
| Successful conversion from introductory offer to regular subscription             | `Intro Converted`                |
| Failed conversion from introductory offer to regular subscription or failed renew | `Intro Expired`                  |
| Refund during introductory offer                                                  | `Intro Refunded`                 |
| **REGULAR SUBSCRIPTION**                                                          | ****                             |
| Subscription started                                                              | `Subscription Started`           |
| Subscription renewed                                                              | `Subscription Renewed`           |
| Subscription expired                                                              | `Subscription Expired`           |
| Subscription refunded                                                             | `Subscription Refunded`          |
| **PROMOTIONAL OFFER**                                                             | ****                             |
| Promotional offer started                                                         | `Promo Started`                  |
| Promotional offer renewed                                                         | `Promo Renewed`                  |
| Successful conversion from promotional offer to regular subscription              | `Promo Converted`                |
| Failed conversion from promotional offer to regular subscription or failed renew  | `Promo Expired`                  |
| Refund during promotional offer                                                   | `Promo Refunded`                 |
| **CANCELLATIONS**                                                                 | ****                             |
| Trial Canceled                                                                    | `Trial Canceled`                 |
| Subscription Canceled                                                             | `Subscription Canceled`          |
| Autorenew disabled (Deprecated)                                                   | `Autorenew Disabled`             |
| Autorenew enabled                                                                 | `Autorenew Enabled`              |
| **OTHER EVENTS**                                                                  |                                  |
| Non renewing purchase                                                             | `Non Renewing Purchase`          |
| Non renewing purchase refunded                                                    | `Non Renewing Purchase Refunded` |
| Billing Issue                                                                     | `Billing Issue`                  |

## Send Test Event

You can test Slack integration by clicking _"…"_ and then in dropdown click on _"Send test event"_:

![](<../../.gitbook/assets/slack-test-event (1).png>)
