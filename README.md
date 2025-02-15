# flutter_branch_sdk

This is a Flutter plugin that implemented [Branch SDK](https://branch.io).

Branch.io helps mobile apps grow with deep links that power referral systems, sharing links and invites with full attribution and analytics.

Supports Android, iOS and Web.

* Android - Branch SDK Version >= 5.0.9 [Android Version History](https://github.com/BranchMetrics/android-branch-deep-linking-attribution/releases)
* iOS - Branch SDK Version >= 1.39.3 [iOS Version History](https://github.com/BranchMetrics/ios-branch-deep-linking-attribution/releases)

Implemented functions in plugin:

Function | Android | iOS | Web 
--- | --- | --- | --- |
Test Branch Integration | X | X | Not supported
Track users | X | X | X
Enable / Disable User Tracking | X | X | X
Get First and Last Parameters | X | X | X
Generate Deep Link for Branch Universal Object (BUO)| X | X | X
Show Share Sheet for Branch Universal Object (BUO)| X | X | X
List BUO on Search / Remove BUO from Search| X | X | Not supported
Register view| X | X | X
Track User Actions and Events| X | X | X
Init Branch Session and Deep Link| X | X | X
Referral rewards| X | X | X

## Getting Started
### Configure Branch Dashboard
* Register Your App
* Complete the Basic integration in [Branch Dashboard](https://dashboard.branch.io/login)

For details see:

* [iOS - only section: **Configure Branch**](https://help.branch.io/developers-hub/docs/ios-basic-integration#configure-branch)
* [Android - only section: **Configure Branch Dashboard**](https://help.branch.io/developers-hub/docs/android-basic-integration#configure-branch-dashboard)

## Configure Platform Project
### Android Integration

Follow the steps on the page [https://help.branch.io/developers-hub/docs/android-basic-integration#configure-app](https://help.branch.io/developers-hub/docs/android-basic-integration#configure-app), session _**Configure app**_:
* Add Branch to your `AndroidManifest.xml`

### iOS Integration
Follow the steps on the page [https://help.branch.io/developers-hub/docs/ios-basic-integration#configure-bundle-identifier](https://help.branch.io/developers-hub/docs/ios-basic-integration#configure-bundle-identifier), from session ```Configure bundle identifier```:
* Configure bundle identifier
* Configure associated domains
* Configure entitlements
* Configure Info.plist
* Confirm app prefix

> Note:  In `Info.plist`  not add `branch_key` `live` and `test` at the same time.<br />
Use only `branch_key` and update as needed.

### Web Integration

You need add Branch Javascript in your `web\index.html` at the top of your `<body>` tag, to be able to use this package.

```javascript
  <script>
    (function(b,r,a,n,c,h,_,s,d,k){if(!b[n]||!b[n]._q){for(;s<_.length;)c(h,_[s++]);d=r.createElement(a);d.async=1;d.src="https://cdn.branch.io/branch-latest.min.js";k=r.getElementsByTagName(a)[0];k.parentNode.insertBefore(d,k);b[n]=h}})(window,document,"script","branch",function(b,r){b[r]=function(){b._q.push([r,arguments])}},{_q:[],_v:1},"addListener applyCode autoAppIndex banner closeBanner closeJourney creditHistory credits data deepview deepviewCta first getCode init link logout redeem referrals removeListener sendSMS setBranchViewData setIdentity track validateCode trackCommerceEvent logEvent disableTracking".split(" "), 0);
  </script>
```

Full example `index.html`:

```html
<!DOCTYPE html>
<html>
<head>
  <!--
    If you are serving your web app in a path other than the root, change the
    href value below to reflect the base path you are serving from.

    The path provided below has to start and end with a slash "/" in order for
    it to work correctly.

    Fore more details:
    * https://developer.mozilla.org/en-US/docs/Web/HTML/Element/base
  -->
  <base href="/">

  <meta charset="UTF-8">
  <meta content="IE=Edge" http-equiv="X-UA-Compatible">
  <meta name="description" content="Demonstrates how to use the flutter_branch_sdk plugin.">

  <!-- iOS meta tags & icons -->
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black">
  <meta name="apple-mobile-web-app-title" content="flutter_branch_sdk_example">
  <link rel="apple-touch-icon" href="icons/Icon-192.png">

  <!-- Favicon -->
  <link rel="icon" type="image/png" href="favicon.png"/>

  <title>flutter_branch_sdk_example</title>
  <link rel="manifest" href="manifest.json">
</head>
<body>
  <script>
    (function(b,r,a,n,c,h,_,s,d,k){if(!b[n]||!b[n]._q){for(;s<_.length;)c(h,_[s++]);d=r.createElement(a);d.async=1;d.src="https://cdn.branch.io/branch-latest.min.js";k=r.getElementsByTagName(a)[0];k.parentNode.insertBefore(d,k);b[n]=h}})(window,document,"script","branch",function(b,r){b[r]=function(){b._q.push([r,arguments])}},{_q:[],_v:1},"addListener applyCode autoAppIndex banner closeBanner closeJourney creditHistory credits data deepview deepviewCta first getCode init link logout redeem referrals removeListener sendSMS setBranchViewData setIdentity track validateCode trackCommerceEvent logEvent disableTracking".split(" "), 0);
  </script>
  <!-- This script installs service_worker.js to provide PWA functionality to
       application. For more information, see:
       https://developers.google.com/web/fundamentals/primers/service-workers -->
  <script>
    if ('serviceWorker' in navigator) {
      window.addEventListener('flutter-first-frame', function () {
        navigator.serviceWorker.register('flutter_service_worker.js');
      });
    }
  </script>
  <script src="main.dart.js" type="application/javascript"></script>
  <script src="main.dart.js" type="application/javascript"></script>
</body>
</html>

```

## Installation
To use the plugin, add `flutter_branch_sdk` as a [dependency in your pubspec.yaml file](https://pub.dev/packages/flutter_branch_sdk/install).

## How to use

### Test Branch Integration
Test your Branch Integration by calling:

```dart
FlutterBranchSdk.validateSDKIntegration();
```

Check logs to make sure all the SDK Integration tests pass.

Example of log for Android:

```java
------------------- Initiating Branch integration verification --------------------------- ... 
1. Verifying Branch instance creation ... 
Passed
2. Checking Branch keys ... 
Passed
3. Verifying application package name ... 
Passed
4. Checking Android Manifest for URI based deep link config ... 
Passed
5. Verifying URI based deep link config with Branch dash board. ... 
Passed
6. Verifying intent for receiving URI scheme. ... 
Passed
7. Checking AndroidManifest for AppLink config. ... 
Passed
8. Verifying any supported custom link domains. ... 
Passed
9. Verifying default link domains integrations. ... 
Passed
10. Verifying alternate link domains integrations. ... 
Passed
Passed
--------------------------------------------
Successfully completed Branch integration validation. Everything looks good!
 
Great! Comment out the 'validateSDKIntegration' line in your app. Next check your deep link routing.
Append '?bnc_validate=true' to any of your app's Branch links and click it on your mobile device (not the Simulator!) to start the test.
For instance, to validate a link like:
https://<yourapp>.app.link/NdJ6nFzRbK
click on:
https://<yourapp>.app.link/NdJ6nFzRbK?bnc_validate=true
```
Make sure to comment out or remove `validateSDKIntegration` in your production build.

### Initialize Branch and read deep link

To use in `Flutter Web`, it is necessary to call the method below before any command of SDK:

```dart
      FlutterBranchSdk.initWeb(
          branchKey: 'branch_key');
```
Be sure to replace `branchKey` with your actual Branch Key found in your [account dashboard](https://dashboard.branch.io/#/settings) (same value inputted in the Android / ioS project).

> Command `FlutterBranchSdk.initWeb` is ignored in the iOS / Android project


To listen to the clicks on the deep link and retrieve the data it is necessary to add the code below:

```dart
    StreamSubscription<Map> streamSubscription = FlutterBranchSdk.initSession().listen((data) {
      if (data.containsKey("+clicked_branch_link") &&
          data["+clicked_branch_link"] == true) {
         //Link clicked. Add logic to get link data
         print('Custom string: ${data["custom_string"]}');
      }
    }, onError: (error) {
      PlatformException platformException = error as PlatformException;
      print(
          'InitSession error: ${platformException.code} - ${platformException.message}');
    });
```

When a deep link is clicked the above method will be called, with the app is open or closed.

### Retrieve Install (Install Only) Parameters
If you ever want to access the original session params (the parameters passed in for the first install event only), you can use this line. This is useful if you only want to reward users who newly installed the app from a referral link.

```dart
    Map<dynamic, dynamic> params = await FlutterBranchSdk.getFirstReferringParams();
```
### Retrieve session (install or open) parameters
These session parameters will be available at any point later on with this command. If no parameters are available then Branch will return an empty dictionary. This refreshes with every new session (app installs AND app opens).

```dart
    Map<dynamic, dynamic> params = await FlutterBranchSdk.getLatestReferringParams();
```
### Create content reference
The Branch Universal Object encapsulates the thing you want to share.

```dart
    BranchUniversalObject buo = BranchUniversalObject(
      canonicalIdentifier: 'flutter/branch',
      //canonicalUrl: '',
      title: 'Flutter Branch Plugin',
      imageUrl: 'https://flutter.dev/assets/flutter-lockup-4cb0ee072ab312e59784d9fbf4fb7ad42688a7fdaea1270ccf6bbf4f34b7e03f.svg',
      contentDescription: 'Flutter Branch Description',
      keywords: ['Plugin', 'Branch', 'Flutter'],
      publiclyIndex: true,
      locallyIndex: true,
      contentMetadata: BranchContentMetaData()..addCustomMetadata('custom_string', 'abc')
          ..addCustomMetadata('custom_number', 12345)
          ..addCustomMetadata('custom_bool', true)
          ..addCustomMetadata('custom_list_number', [1,2,3,4,5 ])
          ..addCustomMetadata('custom_list_string', ['a', 'b', 'c']),
    );
```

> parameter **canonicalUrl**: 
> If your content lives both on the web and in the app, make sure you set its canonical URL (i.e. the URL of this piece of content on the web) when building any BUO.
> By doing so, we’ll attribute clicks on the links that you generate back to their original web page, even if the user goes to the app instead of your website! This will help your SEO efforts.

More information about the parameters check [Android documentation](https://help.branch.io/developers-hub/docs/android-full-reference#parameters) and [iOS documentation](https://help.branch.io/developers-hub/docs/ios-full-reference#methods-and-properties) 

### Create link reference
* Generates the analytical properties for the deep link.
* Used for Create deep link and Share deep link.

```dart
    BranchLinkProperties lp = BranchLinkProperties(
	   //alias: 'flutterplugin', //define link url,
        channel: 'facebook',
        feature: 'sharing',
        stage: 'new share',
        tags: ['one', 'two', 'three']
    );
    lp.addControlParam('url', 'http://www.google.com');
    lp.addControlParam('url2', 'http://flutter.dev');
```

> parameter **alias**:
> Instead of our standard encoded short url, you can specify the vanity alias.
> For example, instead of a random string of characters/integers, you can set the vanity alias as \*.app.link/devonaustin.
> Aliases are enforced to be unique and immutable per domain, and per link - they cannot be reused unless deleted.

More information about the parameters check [Android documentation](https://help.branch.io/developers-hub/docs/android-full-reference#creating-a-deep-link) and [iOS documentation](https://help.branch.io/developers-hub/docs/ios-full-reference#link-properties-parameters) 

           
### Create deep link
Generates a deep link within your app.

```dart
    BranchResponse response =
        await FlutterBranchSdk.getShortUrl(buo: buo, linkProperties: lp);
    if (response.success) {
      print('Link generated: ${response.result}');
    } else {
        print('Error : ${response.errorCode} - ${response.errorMessage}');
    }
```
### Show Share Sheet deep link
Will generate a Branch deep link and tag it with the channel the user selects.
> Note: _For Android additional customization is possible_

```dart
    BranchResponse response = await FlutterBranchSdk.showShareSheet(
        buo: buo,
        linkProperties: lp,
        messageText: 'My Share text',
        androidMessageTitle: 'My Message Title',
        androidSharingTitle: 'My Share with');

    if (response.success) {
      print('showShareSheet Sucess');
    } else {
      print('Error : ${response.errorCode} - ${response.errorMessage}');
    }
```
### List content on Search
* For Android list BUO links in Google Search with App Indexing
* For iOs list BUO links in Spotlight

Enable automatic sitemap generation on the Organic Search page of the [Branch Dashboard](https://dashboard.branch.io/search). 
Check the Automatic sitemap generation checkbox.

```dart
    bool success = await FlutterBranchSdk.listOnSearch(buo: buo);
    print(success);
```
### Remove content from Search
Privately indexed Branch Universal Object can be removed.

```dart
    bool success = await FlutterBranchSdk.removeFromSearch(buo: buo);
    print('Remove sucess: $success');
```

### Register Event VIEW_ITEM
Mark the content referred by this object as viewed. This increment the view count of the contents referred by this object.

```dart
FlutterBranchSdk.registerView(buo: buo);
```

### Tracking User Actions and Events
Use the `BranchEvent` interface to track special user actions or application specific events beyond app installs, opens, and sharing. You can track events such as when a user adds an item to an on-line shopping cart, or searches for a keyword, among others.
The `BranchEvent` interface provides an interface to add contents represented by `BranchUniversalObject` in order to associate app contents with events.
Analytics about your app's BranchEvents can be found on the Branch dashboard, and BranchEvents also provide tight integration with many third party analytics providers.

```dart
BranchEvent eventStandart = BranchEvent.standardEvent(BranchStandardEvent.ADD_TO_CART);
FlutterBranchSdk.trackContent(buo: buo, branchEvent: eventStandart);
```
You can use your own custom event names too:

```dart
BranchEvent eventCustom = BranchEvent.customEvent('Custom_event');
FlutterBranchSdk.trackContent(buo: buo, branchEvent: eventCustom);
```
Extra event specific data can be tracked with the event as well:

```dart
    eventStandart.transactionID = '12344555';
    eventStandart.currency = BranchCurrencyType.BRL;
    eventStandart.revenue = 1.5;
    eventStandart.shipping = 10.2;
    eventStandart.tax = 12.3;
    eventStandart.coupon = 'test_coupon';
    eventStandart.affiliation = 'test_affiliation';
    eventStandart.eventDescription = 'Event_description';
    eventStandart.searchQuery = 'item 123';
    eventStandart.adType = BranchEventAdType.BANNER;
    eventStandart.addCustomData(
        'Custom_Event_Property_Key1', 'Custom_Event_Property_val1');
    eventStandart.addCustomData(
        'Custom_Event_Property_Key2', 'Custom_Event_Property_val2');
    FlutterBranchSdk.trackContent(buo: buo, branchEvent: eventStandart);
```

You can register logs in BranchEvent without Branch Universal Object (BUO) for tracking and analytics:

```dart
BranchEvent eventStandart = BranchEvent.standardEvent(BranchStandardEvent.ADD_TO_CART);
FlutterBranchSdk.trackContentWithoutBuo(branchEvent: eventStandart);
```

You can use your own custom event names too:

```dart
BranchEvent eventCustom = BranchEvent.customEvent('Custom_event');
FlutterBranchSdk.trackContentWithoutBuo(branchEvent: eventCustom);
```

### Track users
Sets the identity of a user (email, ID, UUID, etc) for events, deep links, and referrals.

```dart
//login
FlutterBranchSdk.setIdentity('user1234567890');
```
```dart
//logout
FlutterBranchSdk.logout();
```
```dart
//check if user is identify
 bool isUserIdentified = await FlutterBranchSdk.isUserIdentified();
```

### Enable or Disable User Tracking
If you need to comply with a user's request to not be tracked for GDPR purposes, or otherwise determine that a user should not be tracked, utilize this field to prevent Branch from sending network requests. This setting can also be enabled across all users for a particular link, or across your Branch links.

```dart
FlutterBranchSdk.disableTracking(false);
```
```dart
FlutterBranchSdk.disableTracking(true);
```
You can choose to call this throughout the lifecycle of the app. Once called, network requests will not be sent from the SDKs. Link generation will continue to work, but will not contain identifying information about the user. In addition, deep linking will continue to work, but will not track analytics for the user.

### Set Request Meta data
Add key value pairs to all requests

```dart
FlutterBranchSdk.setRequestMetadata(requestMetadataKey, requestMetadataValue);
```


### Set time window (in Hours) for SKAdNetwork callouts (iOS only)
By default, Branch limits calls to SKAdNetwork to within 72 hours after first install.

```dart
FlutterBranchSdk.setIOSSKAdNetworkMaxTime(24);
```

### Apple Search Ads
Branch can help track your Apple Search Ad campaigns by fetching the search ad attribution from Apple at app install.

Add KEY ```branch_check_apple_ads``` in INFO.PLIST to enable checking for Apple Search Ads before Branch initialization.

In `ios/Runner/Info.plist`, you should have something like:

```xml
 	<key>branch_check_apple_ads</key>
	<true/>
```

### Referral System Rewarding Functionality
Reward balances change randomly on the backend when certain actions are taken (defined by your rules), so you'll need to make an asynchronous call to retrieve the balance. 

Read more here: [https://blog.branch.io/how-to-build-an-optimized-referral-program-for-your-mobile-app/](https://blog.branch.io/how-to-build-an-optimized-referral-program-for-your-mobile-app/)

#### Get Reward Balance
Reward balances change randomly on the backend when certain actions are taken (defined by your rules), so you'll need to make call to retrieve the balance. Here is the syntax:

***optional parameter***: bucket - value containing the name of the referral bucket to attempt to redeem credits from

```dart
BranchResponse response =
    await FlutterBranchSdk.loadRewards();
if (response.success) {
    credits = response.result;
    print('Crédits');
} else {
    print('Credits error: ${response.errorMessage}');
}
```

#### Redeem All or Some of the Reward Balance (Store State)
Redeeming credits allows users to cash in the credits they've earned. Upon successful redemption, the user's balance will be updated reflecting the deduction.

***optional parameter***: bucket - value containing the name of the referral bucket to attempt to redeem credits from

```dart
BranchResponse response =
    await FlutterBranchSdk.redeemRewards(count: 5);
if (response.success) {
    print('Redeeming Credits with success');
} else {
    print('Redeeming Credits with error: ${response.errorMessage}');
}
```
#### Get Credit History
This call will retrieve the entire history of credits and redemptions from the individual user. To use this call, implement like so:

***optional parameter***: bucket - value containing the name of the referral bucket to attempt to redeem credits from

```dart
BranchResponse response =
    await FlutterBranchSdk.getCreditHistory();
if (response.success) {
    print('getCreditHistory with success. Records: ${(response.result as List).length}');
} else {
    print('getCreditHistory with error: ${response.errorMessage}');
}
```
The response will return an list of map:

```json
[
    {
        "transaction": {
                           "date": "2014-10-14T01:54:40.425Z",
                           "id": "50388077461373184",
                           "bucket": "default",
                           "type": 0,
                           "amount": 5
                       },
        "event" : {
            "name": "event name",
            "metadata": { your event metadata if present }
        },
        "referrer": "12345678",
        "referree": null
    },
    {
        "transaction": {
                           "date": "2014-10-14T01:55:09.474Z",
                           "id": "50388199301710081",
                           "bucket": "default",
                           "type": 2,
                           "amount": -3
                       },
        "event" : {
            "name": "event name",
            "metadata": { your event metadata if present }
        },
        "referrer": null,
        "referree": "12345678"
    }
]
```
**referrer** : The id of the referring user for this credit transaction. Returns null if no referrer is involved. Note this id is the user id in a developer's own system that's previously passed to Branch's identify user API call.

**referree** : The id of the user who was referred for this credit transaction. Returns null if no referree is involved. Note this id is the user id in a developer's own system that's previously passed to Branch's identify user API call.

**type** : This is the type of credit transaction.

* 0 - A reward that was added automatically by the user completing an action or promo.
* 1 - A reward that was added manually.
* 2 - A redemption of credits that occurred through our API or SDKs.
* 3 - This is a very unique case where we will subtract credits automatically when we detect fraud.


### iOS 14+ App Tracking Transparency 
Starting with iOS 14.5, iPadOS 14.5, and tvOS 14.5, you’ll need to receive the user’s permission through the AppTrackingTransparency framework to track them or access their device’s advertising identifier. Tracking refers to the act of linking user or device data collected from your app with user or device data collected from other companies’ apps, websites, or offline properties for targeted advertising or advertising measurement purposes. Tracking also refers to sharing user or device data with data brokers.

See: [https://developer.apple.com/app-store/user-privacy-and-data-use/](https://developer.apple.com/app-store/user-privacy-and-data-use/)

New methods have been made available to deal with App Tracking Transparency.

First, update `Info.plist` file located in ios/Runner directory and add the `NSUserTrackingUsageDescription` key with a custom message describing your usage.

```swift
    <key>NSUserTrackingUsageDescription</key>
    <string>App would like to access IDFA for tracking purpose</string>
```

#### Show tracking authorization dialog and ask for permission

```dart
AppTrackingStatus status = await FlutterBranchSdk.requestTrackingAuthorization();
print(status);
```
> Note: After the user's response, call the `handleATTAuthorizationStatus` Branch SDK method to monitor the performance of the ATT prompt.

![App tracking dialog](https://github.com/RodrigoSMarques/flutter_branch_sdk/blob/dev/assets/app_tracking_dialog.png)


#### Get tracking authorization status

```dart
AppTrackingStatus status = await FlutterBranchSdk.getTrackingAuthorizationStatus();
print(status);
```

##### Values available for AppTrackingStatus

```dart
enum AppTrackingStatus {
  /// The user has not yet received an authorization request dialog
  notDetermined,

  /// The device is restricted, tracking is disabled and the system can't show a request dialog
  restricted,

  /// The user denies authorization for tracking
  denied,

  /// The user authorizes access to tracking
  authorized,

  /// The platform is not iOS or the iOS version is below 14.0
  notSupported,
}

```

#### Get Device Advertising Identifier

```dart
AppTrackingStatus status = await FlutterBranchSdk.getTrackingAuthorizationStatus();
print(status);
```

See: [https://developer.apple.com/documentation/adsupport/asidentifiermanager/1614151-advertisingidentifier](https://developer.apple.com/documentation/adsupport/asidentifiermanager/1614151-advertisingidentifier)


### Enable Logging
Use the Branch test key instead of the live key.

Logging is enabled by default in debug mode and disabled in release mode.

To enable/disable logging update `INFO.PLIST` on `iOS` or `AndroidManifest.xml` on Android:

For `iOS` add to `INFO.PLIST`:

To disable:

```swift
	<key>branch_enable_log</key>
	<false/>
```

To enable:

```swift
	<key>branch_enable_log</key>
	<true/>
```

For `Android` add to `AndroidManifest.xml`:

To disable:

```java
    <meta-data android:name="branch_enable_log"
        android:value="false" />
```

To enable:

```java
    <meta-data android:name="branch_enable_log"
        android:value="true" />
```

### iOS - Enabled Clipboard Deferred Deep Linking

Use iOS pasteboard to enable deferred deep linking.

To enable Clipboard Deferred Deep Linking update `INFO.PLIST` on `iOS`

Add to `INFO.PLIST`:

```swift
	<key>branch_check_pasteboard</key>
	<true/>
```

### Facebook App Install Ads

Branch links can be used together with Facebook App Install Campaign ads, allowing you to track ad-driven installs on the Branch dashboard and deep link those new users directly to content the first time they open your app.

Follow the instructions on the link
<a href="https://help.branch.io/using-branch/docs/facebook-app-install-ads" target="_blank">https://help.branch.io/using-branch/docs/facebook-app-install-ads</a>.



To read Facebook App Install deep links update `INFO.PLIST` on `iOS` or `AndroidManifest.xml` on `Android` as in the example:

For `iOS` add to `INFO.PLIST`:

```swift
	<key>branch_enable_facebook_ads</key>
	<true/>
```

For `Android` add to `AndroidManifest.xml`:

```java
    <meta-data android:name="branch_enable_facebook_ads"
        android:value="true" />
```

Follow the instructions to  install Facebook Android / iOS SDK:

`iOS`: 

<a href="https://developers.facebook.com/docs/ios/use-cocoapods" target="_blank">https://developers.facebook.com/docs/ios/use-cocoapods</a>

`Android`: 

<a href="https://developers.facebook.com/docs/android/getting-started" target="_blank">https://developers.facebook.com/docs/android/getting-started</a>



# Getting Started
See the `example` directory for a complete sample app using Branch SDK.

![Example app](https://github.com/RodrigoSMarques/flutter_branch_sdk/blob/dev/assets/example.png)

See example in Flutter Web: [https://flutter-branch-sdk.netlify.app/](https://flutter-branch-sdk.netlify.app/#/)

# Branch Universal Object best practices

Here are a set of best practices to ensure that your analytics are correct, and your content is ranking on Spotlight effectively.

1. Set the canonicalIdentifier to a unique, de-duped value across instances of the app
2. Ensure that the title, contentDescription and imageUrl properly represent the object
3. Initialize the Branch Universal Object and call `FlutterBranchSdk.registerView(buo: buo);` on `initState()`
4. Call `showShareSheet` and `getShortUrl` later in the life cycle, when the user takes an action that needs a link
5. Call the additional object events (purchase, share completed, etc) when the corresponding user action is taken

Practices to avoid:

1. Don't set the same title, contentDescription and imageUrl across all objects.
2. Don't wait to initialize the object and register views until the user goes to share.
3. Don't wait to initialize the object until you conveniently need a link.
4. Don't create many objects at once and register views in a for loop.

# Branch Documentation
Read the iOS or Android documentation for all Branch object parameters:

* Android - [https://help.branch.io/developers-hub/docs/android-advanced-features](https://help.branch.io/developers-hub/docs/android-advanced-features)
* iOS - [https://help.branch.io/developers-hub/docs/ios-advanced-features](https://help.branch.io/developers-hub/docs/ios-advanced-features)

# Author
This project was authored by Rodrigo S. Marques. You can contact me at [rodrigosmarques@gmail.com](mailto:rodrigosmarques@gmail.com)
 
