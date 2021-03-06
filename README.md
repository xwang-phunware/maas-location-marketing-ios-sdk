Location Marketing Sample Application for iOS
==================

Version 3.0

This is Phunware's iOS SDK for the Location Marketing module. 


Requirements
------------

- iOS 6.0 or greater
- Xcode 5 or greater



Installation
------------

The recommended way to use PWLocalpoint is via [CocoaPods](http://cocoapods.org). Add the following pod to your `Podfile` to use PWLocalpoint:
````
pod 'PWLocalpoint', :git => 'git@github.com:xwang-phunware/maas-location-marketing-ios-sdk.git'
````




Documentation
------------
PWLocalpoint documentation is included in the Documents folder in the repository as both HTML and as a .docset. 

Here are some resources to help you configure your app for Apple Push Notifications:
- [Apple's documentation](https://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Introduction.html)
- [Apple Push Notification services (APNs) Tutorial (1/2)](http://www.raywenderlich.com/32960/apple-push-notification-services-in-ios-6-tutorial-part-1)
- [Apple Push Notification services (APNs) tutorial (2/2)](http://www.raywenderlich.com/32963/apple-push-notification-services-in-ios-6-tutorial-part-2)




Application Setup 
-----------------
At the top of your application delegate (.m) file, add the following:

````objective-c
#import <PWLocalpoint/PWLocalpoint.h>
````

Inside your application delegate, you will need to initialize MaaSCore in the application:didFinishLaunchingWithOptions: method. 

````objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
// LM Step 1.0(Required):
// Set a explicit configuration for LM
[PWLPConfiguration useConfiguration:[PWLPConfiguration defaultConfiguration]];

// LM Step 1.1(Required):
// Start the standard service
[PWLocalpoint start];

// LM Step 1.2(Required):
// Notify LM the app finishes launching
[PWLocalpoint didFinishLaunchingWithOptions:launchOptions];

return YES;
}
````

Since PWLocalpoint v3.0, the *application developer* is not responsible with registering for remote notifications with Apple. Apple has three primary methods for handling remote notifications. You will need to implement these in your application delegate, forwarding the results to PWAlerts:

````objective-c
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
// LM Step 2.0(Required):
// Notify LM the app succeed to register for remote notification
[PWLocalpoint didRegisterForRemoteNotificationsWithDeviceToken:deviceToken];
}

- (void)application:(UIApplication *)application didFailToRegisterForRemoteNotificationsWithError:(NSError *)error {
// LM Step 3.0(Required):
// Notify LM the app fail to register for remote notification
[PWLocalpoint didFailToRegisterForRemoteNotificationsWithError:error];
}

- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
// LM Step 4.0(Required):
// Notify LM the app receives a remote notificaiton
[PWLocalpoint didReceiveRemoteNotification:userInfo];
}
````
