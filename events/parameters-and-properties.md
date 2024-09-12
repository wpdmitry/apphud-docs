---
description: >-
  This guide describes possible parameters and user properties that can be sent
  to integrations.
---

# Event Parameters and User Properties

Apphud can send events about subscriptions and non-renewing purchases to third party services: mobile analytics and messengers.

## Events Parameters

Here is a list of all available parameters that are being sent with events:

| Parameter                                                                    | Description                                                                                                                                                                                                                                                                                                                               |
| ---------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `product_id` or`af_content_id` or `content_items[0].$sku` or `fb_content_id` | Product identifier                                                                                                                                                                                                                                                                                                                        |
| `transaction_id`                                                             | Transaction identifier                                                                                                                                                                                                                                                                                                                    |
| `unit`                                                                       | The increment of time that a subscription period is specified in. Possible values: `day`, `week`, `month`, `year`                                                                                                                                                                                                                         |
| `units_count`                                                                | The number of units per subscription period                                                                                                                                                                                                                                                                                               |
| `local_price` or`af_revenue` or `_valueToSum`                                | The cost of the product in the local currency                                                                                                                                                                                                                                                                                             |
| `currency` or`af_currency` or `fb_currency`                                  | Local currency ISO code                                                                                                                                                                                                                                                                                                                   |
| `usd_price` or`content_items[0].$price`                                      | The cost of the product in USD                                                                                                                                                                                                                                                                                                            |
| `price_description`                                                          | Price description in following format: `local_price` `currency` \~ `usd_price`, for example: 499 RUR \~ 7.8 USD                                                                                                                                                                                                                           |
| `reason`                                                                     | <p>1. The reason of an expiration of a subscription. Possible values: <code>user_canceled</code>, <code>billing_issue</code>, <code>declined_price_increase</code>, <code>unavailable_product</code>, <code>unknown_error</code><br><br>2. The reason of refund. Possible values: <code>app_issue</code>, <code>another_reason</code></p> |
| `offer_id`                                                                   | Promotional offer identifier                                                                                                                                                                                                                                                                                                              |
| `offer_type`                                                                 | Introductory or promotional offer payment mode, if applied. Possible values: `pay_up_front`, `pay_as_you_go`, `trial` (for promotional offers)                                                                                                                                                                                            |
| `app_name`                                                                   | App name                                                                                                                                                                                                                                                                                                                                  |
| `user_id`                                                                    | User identifier                                                                                                                                                                                                                                                                                                                           |
| `group_name`                                                                 | Subscription group name                                                                                                                                                                                                                                                                                                                   |

{% hint style="info" %}
To get more details about parameters in each integration, please check corresponding integration guide.
{% endhint %}

### Possible Values of `reason` Parameter

#### If subscription lapsed:

* `user_canceled`: user canceled subscription manually;
* `billing_issue`: there was an error during billing;
* `declined_price_increase`: user did not agree to a recent price increase;
* `unavailable_product`: product was not available for purchase at the time of renewal;
* `unknown_error`: unknown error occurred.

#### If subscription refunded:

* `app_issue`: user canceled his subscription due to an actual or perceived issue within your app;
* `another_reason`: subscription was canceled for another reason, for example, if the user made the purchase accidentally.

## User Properties

Besides events Apphud also sends user properties to analytics:

| Property                                                                             | Description                                                                                                  |
| ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| `[Apphud] status-<group_name>`, where `<group_name>` – name of subscription group    | Status of subscription. Possible values: `none`, `trial`, `intro`, `regular`, `grace`, `promo`, `refunded`, `expired` |
| `[Apphud] autorenew-<group_name>`, where `<group_name>` – name of subscription group | Whether autorenew option is turned on                                                                        |
| `[Apphud] total_spent`                                                               | Total amount of money that user has been charged, in USD                                                     |
| `[Apphud] paying`                                                                    | Whether user is paying or not                                                                                |
| `[Apphud] payments_count`                                                            | Number of transactions user has been charged                                                                 |

To get more details about user properties in each integration, please check corresponding integration guide.

### Possible Values of `[Apphud] status-<group_name>`

All values are applied for given subscription group:

* `none`: user has never purchased a subscription;
* `trial`: user has a subscription that is currently in trial period;
* `intro`: user has a subscription that is currently in introductory offer;
* `regular`: user has a subscription with regular price;
* `grace`: user has a subscription that is currently in grace period;
* `promo`: user has a subscription that is currently in promotional offer;
* `refunded`: user has refunded a subscription;
* `expired`: subscription lapsed.
