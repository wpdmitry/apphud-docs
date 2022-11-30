---
description: >-
  This page describes common reasons for data discrepancies between Apphud and
  other platforms.
---

# Data Discrepancies

## General Information

Data discrepancies may occur when comparing Apphud data with other systems, like App Store Connect, Google Play Console, AppsFlyer, etc. In this page we will provide information on how Apphud collects data and generates analytics, as the in-depth understanding of this could be helpful when comparing revenues between Apphud and other platforms. We will also cover the features of some systems (Apple / Google) and their data processing methods.

It is important to know that Apphud does not yet receive data directly from App Store Connect or Google Play. Apphud collects data from SDK and Apple / Google Server Notifications.&#x20;

You can connect SDK in two modes: Observer mode or Full mode. How you connect SDK does not affect the data quality.

If you have a live app with subscriptions or non renewing purchases, you may want to [migrate](../getting-started/data-migration-guide.md) all your existing and historical data once integrating Apphud, otherwise their data will not be counted in Analytics until Apphud receives purchase details from the app. All charts and analytics are based on the information provided above.

## **Common Reasons for Discrepancies**

### Time Z**one D**ifferences

When comparing data, pay attention to the selected time zones on the site, as the numbers between the different time zones may differ.

### Day to Day Comparison

App Store Connect shows charts based on the time the money was debited, however Apphud shows charts based on the declared renewal time. Therefore, there might be cases when the user's subscription money was debited a couple of hours earlier, and the Apple event was displayed a day earlier than the Apphud event, due to the time difference.

So, day to day comparison may not always be accurate; please kindly compare wider date range.

### Abandoned Users Data

We will not be able to track users that did not launch the app with Apphud SDK at least once. Futhermore, `migratePurchases / syncPurchases` method should be called right after SDK initialization, which will migrate all existing purchases to Apphud. You can notify users about a new app version to push them update their app. See migration [guide](../getting-started/data-migration-guide.md) for details.

Hence, there might be some users that made purchases in the past but were not yet tracked by Apphud. These abandoned users could even uninstall the app. We will not be able to track their purchases unless they updated the app or were triggered by Server Notifications (for example, renewal event occured).

### App Store / Google Play Server Notifications

Providing App Store Server Notifications URL is important. It helps to detect cancellations, refunds and other events in real-time. Also it provides renewals from abandoned users, which positively affects data quality.

So, if we don't receive Server Notifications, you may get incorrect data.

### Currency Exchange Rates

The user's receipt does not contain all information about the purchase, i.e. exchange rates are not included in the data received. All purchases are made in the user's local currency and then converted into US dollars. So Apphud converts the purchase price to USD using [OpenExchangeRates](https://openexchangerates.org/). If the exchange rate is not stable, the difference can be up to 5-7%. Note: Different analytical services use different tools for currency rates.

### Cohort Charts

For some charts Apphud uses cohorts. The data in such cases is based on users creation date, but not on the transaction/event date. If the user was created outside the selected period, events of this user will not be counted. Learn more about charts [here](https://docs.apphud.com/analyze/charts) and [here](https://docs.apphud.com/analyze/cohorts).

### Refunds

All services have various policies to process refunds. Some of them show income in real time, like Apphud does, while others deduct a refund at the end of the month. Also, the display of refunds is affected by time zones.

### App Store Payments and Financial Reports

Apple Fiscal Calendar does not use a calendar month for payments and reporting; their financial reports are based on custom periods. You can check our version of Apple's Fiscal Calendar [here](https://apphud.com/fiscal-calendar). App Store converts incomings into one single currency on the day of payment. However in Apphud, the conversion is made immediately after the purchase. Thus, total revenue for reported fiscal month may differ.

### Apple Small Business Program

Apphud does not recalculate Apple's commission for previous usage periods, so add your entry date as soon as possible. Double check your date is correct.

### Facebook Ads Manager Discrepancies

Facebook Ads Manager shows events only for consented users (must provide IDFA to Apphud). Facebook Ads Manager often has delays in displaying events on the dashboard.

### AppsFlyer Discrepancies

Appsflyer displays events data based on user install date, not event date. Apphud sends data to AppsFlyer only if we have attribution data for particular user. So, implementing delegate methods is required. Check [documentation](../integrations/attribution/appsflyer.md#pass-attribution-data-to-apphud-required) for details.
