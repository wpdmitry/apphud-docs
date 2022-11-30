---
description: This page describes how to configure integration with Asapty
---

# Asapty

## About Integration

Apphud can send subscription events to Asapty. Using this integration you can optimize your Search Ads campaigns.

## Requirements

* This integration works only on iOS 14.3+ devices regardless ATT consent.
* This integration is dependent on Apple Search Ads integration. First, set up integration with [Apple Search Ads](../attribution/apple-search-ads.md#how-does-integration-work) via AdServices framework (iOS 14.3+). After that you can continue setting up integration with Asapty.
* Client id, team id, key id credentials generated using Asapty's public key **will not work** in Apphud, because their private keys differ. And vice versa, credentials generated using Apphud's public key will not work in Asapty. [Read here](asapty.md#credentials-issue-between-apphud-and-asapty) about how to fix this issue.

## How to add integration?

{% tabs %}
{% tab title="Step 1" %}
{% hint style="info" %}
Before adding integration please check [requirements](asapty.md#requirements) above
{% endhint %}

At [Apphud](https://app.apphud.com/) go to _"Integrations"_ section and add Asapty:

![](../../.gitbook/assets/asapty\_2.png)
{% endtab %}

{% tab title="Step 2" %}
Insert your Asapty ID:

![](../../.gitbook/assets/asapty\_4.png)
{% endtab %}

{% tab title="Step 3" %}
You can enter your custom event names or disable some:

![](../../.gitbook/assets/asapty\_3.png)
{% endtab %}

{% tab title="Step 4" %}
Enable integration and Save changes:

![](../../.gitbook/assets/asapty\_5.png)
{% endtab %}
{% endtabs %}

## View Apphud events in Asapty

You can view events in Optimization tab. Just add desired columns:

![](../../.gitbook/assets/asapty\_dash.png)

## Credentials issue between Apphud and Asapty

The issue is that both Apphud and Asapty services require Account Manager role to be added to Apple Search Ads account with public key provided. However, since both services generate their own public-private key pair, API account credentials generated using first service's public key will not work for other service, because their private keys are different.

There are 2 options to fix this issue:

### Generate own public-private key

Generate public-private key on your own computer and upload the same private key to both services:

#### Gerenate private key

To generate private key run in Terminal:

```
openssl ecparam -genkey -name prime256v1 -noout -out private-key.pem
```

You will need to paste this private key to Apple Search Ads integration page in Apphud by clicking on _"paste it"_ button. See the screenshot below:

![](../../.gitbook/assets/asa\_private\_key.png)

Upload the same private key to Asapty.

#### Generate public key

To extract public key from your private key run in Terminal:

```
openssl ec -in private-key.pem -pubout -out public-key.pem
```

You will need to paste this public key in your Apple Search Ads settings page of Apple ID account with API Account Manager role. Use generated team id, client id and key id values for both Apphud and Asapty services.

### Create another Apple ID account

You can create another Apple ID account with Account Manager API role and use different Apple ID accounts for both services as well as different public private keys.
