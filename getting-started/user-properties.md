---
description: This page describes how to set or update user properties
---

# User Properties

Set custom User Properties (or User Attributes) through SDK. These attributes will be displayed in Apphud User Page and can be segmented in charts and filters. For example, you can view revenue or MRR chart segmented by your own user attribute.

#### Features:

* Set user property using system reserved or custom keys
* Increment user property with integer or floating value
* Set once, so it will not be overwritten.

### Usage examples

{% tabs %}
{% tab title="Swift" %}
```swift
Apphud.setUserProperty(key: .email, value: "user4@example.com", setOnce: true)
Apphud.setUserProperty(key: .age, value: 31)
Apphud.setUserProperty(key: .init("custom_test_property_1"), value: true)
Apphud.setUserProperty(key: .gender, value: "male")
Apphud.setUserProperty(key: .init("custom_email"), value: "user2@example.com", setOnce: true)
Apphud.incrementUserProperty(key: .age, by: 1)
Apphud.incrementUserProperty(key: .init("progress"), by: 0.5)
```
{% endtab %}

{% tab title="Objective-C" %}
```objectivec
[Apphud setUserPropertyWithKey:[ApphudUserPropertyKey email] value:@"user@example.com" setOnce:YES];
[Apphud setUserPropertyWithKey:[ApphudUserPropertyKey age] value:@25 setOnce:false];
[Apphud setUserPropertyWithKey:[[ApphudUserPropertyKey alloc] init:@"custom_property"] value:@"test" setOnce:false];
[Apphud incrementUserPropertyWithKey:[[ApphudUserPropertyKey alloc] init:@"coins_count"] by:@5];
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
Apphud.setUserProperty(ApphudUserPropertyKey.Email, "user@example.com", true)
Apphud.setUserProperty(ApphudUserPropertyKey.CustomProperty("custom_increment_value_1"), 2.1f)
Apphud.setUserProperty(ApphudUserPropertyKey.Age, 29)
Apphud.incrementUserProperty(ApphudUserPropertyKey.CustomProperty("custom_increment_value_2"), 0.01f)
```
{% endtab %}

{% tab title="Flutter" %}
```
await AppHud.setUserProperty(key: ApphudUserPropertyKey.email, value:’user4@example.com’ , setOnce:true);
await AppHud.setUserProperty(key: ApphudUserPropertyKey.age, value:31);
await AppHud.setUserProperty(key:ApphudUserPropertyKey.customProperty
(‘custom_test_property_1’), value:true);
await AppHud.setUserProperty(key:ApphudUserPropertyKey.gender, value:’male’);
await AppHud.setUserProperty(key:ApphudUserPropertyKey.customProperty
(‘custom_email’), value:’user2@example.com’,setOnce:true);
await AppHud.incrementUserProperty( key: ApphudUserPropertyKey.age, by: 1,);
await AppHud.incrementUserProperty( key:ApphudUserPropertyKey.customProperty
(‘progress’), by: 0.5);
```
{% endtab %}
{% endtabs %}

### System Reserved User Properties

| Key       | Value                                    |
| --------- | ---------------------------------------- |
| `$email`  | String                                   |
| `$phone`  | String                                   |
| `$name`   | String                                   |
| `$cohort` | String                                   |
| `$age`    | Int                                      |
| `$gender` | Must be one of `male`, `female`, `other` |

### Limitations

* Value must be one of: `Int`, `Float`, `Double`, `Bool`, `String`, `NSNumber`, `NSString`, `NSNull`, `nil` or `null`.
* Key must be 30 characters maximum.
* Each user may have maximum 50 attributes.
