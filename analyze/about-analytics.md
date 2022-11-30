---
description: Here we describe common points regarding Apphud analytics platform
---

# About Analytics

### User's First Seen Date

This is user's earliest activity date tracked. For example, for legacy subscribers, it can be the date of initial purchase. First Seen date will replace User Creation Date in cohort charts, such as ARPU, Subscribers Retention, and more.&#x20;

### Value Added Tax Deduction

Starting July 1, 00:00 UTC, Value-Added Tax is deducted from the Proceeds metric for iOS and Android apps. It affects analytics, integrations, server-to-server webhooks, and other services, where the Proceeds metric is used.

> Example: For the GBP3.99 sale, assuming store commission is 15%, proceeds value will be GBP2.82

### Charge Date

As known, iTunes and Google Play accounts are charged for renewal within 24-hours prior to the end of the current period, which is now being reflected in Apphud Revenue Charts: starting July 1, 00:00 UTC, Gross, Sales and Proceeds charts for iOS and Android apps show revenue based on transaction charge date, not on the subscription renewal date.

> Example: For a subscription period which ends on July 7, a transaction charge may occur on July 6. In this case, sales chart will show revenue on July 6.
