# Revenue API

## About Revenue API

As the world’s #1 in App revenue tracking accuracy, we want to share our tracking engine with external users. That is why we are excited to offer the Revenue API.

[Revenue API](https://revenue.apphud.com) – is an API made specially for enterprise games and apps, which lets you retrieve accurate proceeds value with all the fees and taxes deducted, and using Apple’s/ Google’s currency exchange rates. API is using the same core backend as Apphud does, but is deployed on the dedicated server. It works SDK-less and is available for use within the app, or Server-to-Server. As designed for high load, Revenue API may be useful not only for games or apps, but even for other SaaS services.

## API Request

{% swagger baseUrl="https://api.apphud.com/v3" path="/revenues" method="get" summary="Get accurate proceeds and tax information" %}
{% swagger-description %}
Example: 

[https://api.apphud.com/v3/revenues?price=4.99&store=app_store&country_code=FR&currency_code=EUR&fee=0.15&api_key=YOUR_API_KEY](https://api.apphudhud.com/v3/revenues?price=4.99&store=app_store&country_code=FR&currency_code=EUR&fee=0.15&api_key=YOUR_API_KEY)


{% endswagger-description %}

{% swagger-parameter in="query" name="api_key" required="true" type="String" %}
API Key obtained from Sales Manager
{% endswagger-parameter %}

{% swagger-parameter in="query" name="price" type="Float" required="true" %}
In-App Purchase Price (Gross)
{% endswagger-parameter %}

{% swagger-parameter in="query" name="country_code" required="true" type="String" %}
Product Locale's Country, ex. 

`GB`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="currency_code" required="true" type="String" %}
Product Locale's Currency, ex. 

`GBP`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="store" required="true" type="String" %}
Either 

`app_store`

 

__

 or 

`play_store`
{% endswagger-parameter %}

{% swagger-parameter in="query" name="purchase_date" type="Int64" %}
Optional. Unix timestamp of the purchase, ex. 

`1663143775`

. Current time will be used, if not passed.
{% endswagger-parameter %}

{% swagger-parameter in="query" name="fee" type="Float" %}
Optional. Store fee, either 

`0.3`

 or 

`0.15`

. Default is 

`0.3`
{% endswagger-parameter %}

{% swagger-response status="200" description="" %}
```json
{
  "data": {
    "price_usd": 8982000,
    "proceeds_usd": 1122750,
    "proceeds": 62375000,
    "tax": 83166667,
    "tax_usd": 1497000,
    "exchange_rate": 0.0166311,
    "valid_till": 1663200000,
    "exchange": "internal"
  }
}
```
{% endswagger-response %}
{% endswagger %}

## Response Description

|                |                                                                                                                                                                                                                                                            |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| price\_usd     | Gross price converted to USD, in millicents                                                                                                                                                                                                                |
| proceeds\_usd  | Developer Proceeds converted to USD, in millicents                                                                                                                                                                                                         |
| proceeds       | Developer Proceeds in local currency, in millicents                                                                                                                                                                                                        |
| tax            | Tax amount in local currency, in millicents                                                                                                                                                                                                                |
| tax\_usd       | Tax amount converted to USD, in millicents                                                                                                                                                                                                                 |
| exchange\_rate | Exchange rate that was used to convert price to USD                                                                                                                                                                                                        |
| valid\_till    | The date until the given exchange rate is valid, in Unix timestamp                                                                                                                                                                                         |
| exchange       | Possible values: "internal" or "openexchangerates". The second option will be used only as a fallback, if our system is unable to retrieve internal exchange rate. Any fallbacks are treated as a system failure and will be displayed in our Status Page. |

