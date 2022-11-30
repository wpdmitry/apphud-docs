# Cohorts

Cohort analysis is a great tool for a deep understanding how users are renewing subscriptions and how subscribers and revenue retains.

There are two charts available in the Cohorts section: subscribers and net revenue retention. It's better to analyze the subscriber's behavior using both of them.

#### **Cohorts**

Cohorts are calculated based on user's [first seen date](about-analytics.md#users-first-seen-date).

That's why. Users can spend some time deciding whether they want to pay you something or not. Also, you may have trials that delay the conversion to the paid user.

So, if cohorts were calculated from the purchase, it might be tricky to determine what happened with users, who came from marketing, say in March (because some purchased in March and others in April after the trial).

{% hint style="info" %}
You can view cohorts formed on a weekly, monthly, quarterly, and yearly basis.
{% endhint %}

#### **Renewal periods**

The charts have _Renewals 0-N_ columns. This means Nth renewal of user subscription. These renewals may occur in not-fixed periods of time. So, during the grace billing period, the subscriber remains active.

{% hint style="warning" %}
Renewal 0 is the initial subscription purchase, the moment when user paid some money (not a trial start).&#x20;
{% endhint %}

When the subscription expired, we consider this as an end of consecutive user renewals. If the user resubscribes, he will be calculated as a new subscriber and retention will be counted from the start.

### **Subscribers retention**

![](<../.gitbook/assets/Screenshot 2021-06-03 at 15.43.32 (1).png>)

Shows how app subscribers retain (in other words, how many of them renewing their subscriptions).

{% hint style="warning" %}
Subscribers, who made a full refund of their App Store/Google Play subscriptions are not counted in the _Renewal 0_ group.
{% endhint %}

**ARPPU**

Average Revenue Per Paying User (LTV) for each cohort. Sum of all cohort's subscriptions revenue divided by subscribers count.

**Average renewals count**

How many times an average user in the cohort renews the subscription&#x20;

{% hint style="info" %}
For example, "in May cohort average user is renewing subscription 1,35 times"
{% endhint %}

### **Net revenue retention**

![](<../.gitbook/assets/Screenshot 2021-06-03 at 15.50.31.png>)

Shows your in-apps revenue retention (i.e. how much money left in each cohort after Nth renewal). It's crucial to be aware of how in-app subscription drops.

Net revenue is the amount of money left after each renewal.&#x20;

{% hint style="warning" %}
Revenue is counted as PROCEEDS – after App Store/Google Play commissions and refunds deduction.
{% endhint %}

**Total**

Summarized revenue for each cohort.

****
