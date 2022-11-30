---
description: >-
  If you have a live app with subscriptions or non-renewing purchases, you may
  want to get existing users data from Apphud.
---

# Customers API

You can use our “Customers API” to get information about a specific user using their user\_id and app apiKey

{% hint style="info" %}
Only for paid plans
{% endhint %}

{% swagger method="get" path="" baseUrl="https://api.apphud.com/v1/customers?api_key=app_XXX&user_id=XXX" summary="" %}
{% swagger-description %}

{% endswagger-description %}

{% swagger-parameter in="path" name="api_key" required="true" %}
Your AppHud app Api Key, example: app_XXX
{% endswagger-parameter %}

{% swagger-parameter in="path" name="user_id" required="true" %}

{% endswagger-parameter %}

{% swagger-response status="200: OK" description="" %}
```javascript
{
	"data": {
		"results": {
			"created_at": "2022-01-25T19:19:51.944Z",
			"user_id": "test_user_id",
			"total_spent": 0.0,
			"payments_count": 0,
			"uid": "9dec9117",
			"idfv": "4150437B-8DAE-4444-87BF-3E569E310928",
			"variations": [],
			"country_iso_code": "RU",
			"time_zone": "Europe/Moscow",
			"language": "ru",
			"paying": false,
			"email": null,
			"phone": null,
			"name": null,
			"age": "31",
			"gender": null,
			"properties": [{
				"name": "$age",
				"value": "31"
			}, {
				"name": "test_true",
				"value": "t"
			}, {
				"name": "fire_id",
				"value": "value"
			}],
			"subscriptions": [{
				"id": "1dd085dc-e6ba-471f-abfb-ff18f9162c2a",
				"status": "regular",
				"environment": "sandbox",
				"original_transaction_id": "1000000957181773",
				"expires_at": null,
				"cancelled_at": null,
				"started_at": "2022-01-26T20:19:37.000Z",
				"autorenew_enabled": false,
				"in_retry_billing": false,
				"introductory_activated": false,
				"store": "app_store",
				"group": "Premium_0001",
				"product_id": "com.apphud.gold",
				"intro_period": false,
				"trial_period": false
			}, {
				"id": "b8522957-a29b-4f97-beef-0d009e325c8c",
				"status": "regular",
				"environment": "sandbox",
				"original_transaction_id": "1000000957180212",
				"expires_at": null,
				"cancelled_at": null,
				"started_at": "2022-01-26T20:14:23.000Z",
				"autorenew_enabled": false,
				"in_retry_billing": false,
				"introductory_activated": false,
				"store": "app_store",
				"group": "Premium_0001",
				"product_id": "com.apphud.gold",
				"intro_period": false,
				"trial_period": false
			}, {
				"id": "e15e3a0f-a2c1-482c-b295-7b55d9d1c6e9",
				"status": "regular",
				"environment": "sandbox",
				"original_transaction_id": "1000000956386928",
				"expires_at": null,
				"cancelled_at": null,
				"started_at": "2022-01-25T20:11:04.000Z",
				"autorenew_enabled": false,
				"in_retry_billing": false,
				"introductory_activated": false,
				"store": "app_store",
				"group": "Premium_0001",
				"product_id": "com.apphud.gold",
				"intro_period": false,
				"trial_period": false
			}, {
				"id": "3c92697e-d8c3-4d8d-8570-d26f81e94da8",
				"status": "regular",
				"environment": "sandbox",
				"original_transaction_id": "1000000956388658",
				"expires_at": null,
				"cancelled_at": null,
				"started_at": "2022-01-25T20:15:55.000Z",
				"autorenew_enabled": false,
				"in_retry_billing": false,
				"introductory_activated": false,
				"store": "app_store",
				"group": "New_Perm_Gr",
				"product_id": "com.apphud.lifetime",
				"intro_period": false,
				"trial_period": false
			}, {
				"id": "8282713b-0953-4085-9641-17eb5c5a78d1",
				"status": "expired",
				"environment": "sandbox",
				"original_transaction_id": "1000000955290891",
				"expires_at": "2022-01-25T20:37:51.000Z",
				"cancelled_at": null,
				"started_at": "2022-01-24T12:50:22.000Z",
				"autorenew_enabled": false,
				"in_retry_billing": false,
				"introductory_activated": false,
				"store": "app_store",
				"group": "PG3",
				"product_id": "com.apphud.weekly",
				"intro_period": false,
				"trial_period": false
			}],
			"devices": [{
				"id": "e2675b4d-10c2-441c-93e9-3088880e2fda",
				"device_id": "test_device_id",
				"device_type": "iPhone 11",
				"device_family": "iPhone",
				"platform": "ios",
				"app_version": "1.0",
				"sdk_version": "2.5.5",
				"os_version": "15.2",
				"idfa": null,
				"start_app_version": "1.0",
				"carrier": null,
				"push_token": "af762ed401bafbbf53a9f65222a502874b3ad626b543cc8c4be38186e96d74e6",
				"idfv": "4150437B-8DAE-4444-87BF-3E569E310928"
			}]
		},
		"meta": null
	},
	"errors": null
}
```
{% endswagger-response %}
{% endswagger %}
