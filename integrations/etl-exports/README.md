# ETL Exports

{% hint style="info" %}
ETL Exports are available on "Grow" and "Enterprise" plans.
{% endhint %}

Export transaction data on daily basis to your Cloud Storage Provider. Data is being uploaded as gzip compressed `.csv` file.

## Data Format

| Column Name               | Nullable? | Description                                                                                  |
| ------------------------- | :-------: | -------------------------------------------------------------------------------------------- |
| `id`                      |           | Internal ID of the event                                                                     |
| `created_at`              |           | Date when event was created in Apphud                                                        |
| `updated_at`              |           | Date when event was updated in Apphud                                                        |
| `event_name`              |           | <p>Name of the event, i.e.<br><code>trial_started</code></p>                                 |
| `purchased_at`            |           | Date of purchase                                                                             |
| `expires_at`              |     ✅     | For auto-renewable subscriptions, date of expiration                                         |
| `cancelled_at`            |     ✅     | Date of refund                                                                               |
| `transaction_id`          |           | <p>Transaction identifier.</p><p>Order ID on Android</p>                                     |
| `original_transaction_id` |           | Original Transaction Identifier. Purchase token on Play Store                                |
| `price_usd`               |           | Price of transaction in USD                                                                  |
| `price`                   |           | Price of transaction on local currency                                                       |
| `proceeds_usd`            |           | Proceeds amount in USD                                                                       |
| `proceeds`                |           | Proceeds amount in local currency                                                            |
| `quantity`                |           | Always `1`                                                                                   |
| `commission`              |           | Comission amount: `0.3` or `0.15`                                                            |
| `product_id`              |           | Product Identifier                                                                           |
| `store`                   |           | Store of the app                                                                             |
| `trial_period`            |           | Whether transaction is a free trial                                                          |
| `intro_period`            |           | Whether transaction is within intro period                                                   |
| `is_upgraded`             |           | Whether subscription was upgraded                                                            |
| `family_shared`           |           | Whether current purchase was granted to a family member for free                             |
| `subscription_type`       |           | Type of purchase: `autorenewable` or `nonrenewable`                                          |
| `environment`             |           | `production` or `sandbox`                                                                    |
| `user_id`                 |           | Public User ID                                                                               |
| `internal_user_id`        |           | Internal ID of the user                                                                      |
| `currency`                |           | Purchase currency code                                                                       |
| `store_country`           |           | Purchase store country code                                                                  |
| `store`                   |           | <p>Store of the app, i.e.<br><code>app_store</code> or <em></em> <code>play_store</code></p> |

## Available Cloud Storage Providers

{% content-ref url="amazon-s3.md" %}
[amazon-s3.md](amazon-s3.md)
{% endcontent-ref %}
