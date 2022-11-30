# Apple App Privacy

In order to submit new apps and updates to the App Store, you need to tell what types of data you collect in App Store Connect.&#x20;

Apphud collects several types of data. Please, mention this information while submitting the app for review on App Store Connect.

## **Data Types Collected by Apphud**

| Data Type               | Required? | Comment                                                                                                                                                                                                     |
| ----------------------- | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Contact info            | Optional  | Only if you collect identifiable contact information such as name or email address and send them to Apphud using User Properties feature.                                                                   |
| Identifiers - User ID   | Optional  | User ID – you will need to select it if you are identifying users with a custom app user ID.                                                                                                                |
| Identifiers - Device ID | Yes       | Device ID – you will need to select it if you are using integrations that utilize an advertising identifier, like IDFA. Keep in mind, that starting iOS 14.5 IDFA is not automatically collected by Apphud. |
| Purchases               | Yes       | If you are using Apphud, you must disclose that your app collects _Purchases_ information from the App Privacy tab in App Store Connect.                                                                    |

Your app or other SDKs still may collect and use other data types. Please see[ this help](https://developer.apple.com/app-store/app-privacy-details/#data-type-usage) for details.

## Usage Purposes

For each type of data you must specify the usage purpose. For every type of data set both **Analytics** and **App Functionality** at usage purposes section.

* Selecting _Analytics_ ensures compliance for Apphud’s features including Dashboard, Users, Charts, and Rules.
* Selecting _App Functionality_ ensures compliance for receipt validation in order to prevent fraud.

If your app or other SDKs integrated into it collect the same data for different purposes, this must be specified additionally. Read more on [App Store help page](https://developer.apple.com/app-store/app-privacy-details/#data-type-usage).

## Linking to User's Identity

Apphud, as a third-party tool, does not inherently link collected data to a user's identity.

When filling any section, like User ID, Device ID or Purchase History, Apple will ask if this data is linked to user’s identity. At any section, if you are using Apphud’s anonymous app user ID’s, and do not have a way to identify individual users, select **No**.

However, if you are using an app user ID that can be tied to a user’s email address or other contact information via your own server or other third-parties, or if you send personal contact information to Apphud via User Properties you should select **Yes**.

If your app or other SDKs integrated into it collect the same data for different purposes, this must be specified additionally. Read more on [App Store help page](https://developer.apple.com/app-store/app-privacy-details/#data-type-usage).

## Tracking Purposes

### Purchase History

Apphud, as a third-party tool, does not inherently use purchase history to track users across different apps for advertising.

If you don't use Apphud Integrations or other SDK’s that do this or if you don't manually send purchase data to attribution platforms, you can select **No**.

However, if you use Apphud integrations with attribution platforms such as AppsFlyer, Branch, Facebook, etc., or if you manually send purchase data to these attribution platforms for tracking effectiveness of your marketing campaigns, you should select **Yes**.

### User ID

Apphud, as a third-party tool, does not inherently use User ID to track users across different apps for advertising.

If you don't use Apphud Integrations or other SDK’s that do this or if you don't manually send User ID to attribution platforms, you can select **No**.

However, if you use Apphud integrations with attribution platforms such as AppsFlyer, Branch, Facebook, etc., or if you manually send User ID to these attribution platforms for tracking effectiveness of your marketing campaigns, you should select **Yes**.

### Device ID

Apphud, as a third-party tool, does not inherently use Device ID (like, IDFA) to track users across different apps for advertising.

If you don't use Apphud Integrations or other SDK’s that do this or if you don't manually send Device ID to attribution platforms, you can select **No**.

However, if you use Apphud integrations with attribution platforms such as AppsFlyer, Branch, Facebook, etc., or if you manually send Device ID to these attribution platforms for tracking effectiveness of your marketing campaigns, you should select **Yes**.

### Contact Info (optional)

If you use Apphud User Properties and collect user personal information, it is not used for tracking purposes. We don't send User Properties to attribution platforms through Apphud Integrations.&#x20;
