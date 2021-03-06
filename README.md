# BaltoSDK

BaltoSDK is a SDK for [Balto](https://www.balto.io/).  
Balto is the place where beta meets feedback. Distribute your test apps and get instant feedback from your team directly from the app.

## **Notification!**

Version 4.0.0 is a big update. Specification has been greatly changed.  
But do not be tired.  
To migrate to version 4.0.0, just remove `Balto.returnFromBalto` method and it will be completed.

## Installation

**Notice**

Requires iOS 9.0+  
Requires Xcode 8.3.3+

### CocoaPods

Add the following lines to your Podfile:

```
use_frameworks!
target 'TargetName' do
  pod 'BaltoSDK', '>= 4.0.0'
end
```

### Carthage

Add the following lines to your Cartfile:

```
github "goodpatch/BaltoSDK"
```

### To manually add to your project

1. Open your Xcode project.
2. Drag & drop BaltoSDK.framework in the `Xcode->Project->General->Embedded Binaries`.

## Setup

You need to add script phase from 'BuildPhases'.

1. Open your Xcode project. (If you use CocoaPods, open your Xcode workspace.)
2. Add `Xcode->Project->BuildPhases->Run Script`
3. Add the following a line to script editor:

```bash
/bin/sh "${PROJECT_DIR}/BaltoSDK.framework/run.sh"
# If you use CocoaPods
#/bin/sh "${SRCROOT}/Pods/BaltoSDK/BaltoSDK.framework/run.sh"
# If you use Carthage.
#/bin/sh "${SRCROOT}/Carthage/Build/iOS/BaltoSDK.framework/run.sh"
```

## Usage

Add the following lines to `AppDelegate.swift` or `AppDelegate.m`.

```swift
import BaltoSDK

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
    Balto.with()
    return true
}
```

```objective-c
#import <BaltoSDK/BaltoSDK.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [Balto with];
    return YES;
}
```

If you want to set other gesture, you can choose some gestures.

```swift
// Custom swipe gesture.
Balto.withCustomSwipe(numberOfTouchesRequired: Int, direction: UISwipeGestureRecognizerDirection)
// Long press. Default minimum press duration is 0.5.
Balto.withLongPress()
// Custom long press
Balto.withLongPress(minimumPressDuration: CFTimeInterval)
```

If you want to hide the menu of Balto, please add option parameter.

```swift
Balto.with(options: [kBaltoHideMenu: true])
Balto.withLongPress(minimumPressDuration: 2.0, options: [kBaltoHideMenu: true])
Balto.withCustomSwipe(numberOfTouchesRequired: 2, direction: .down, options: [kBaltoHideMenu: true])
```

```objective-c
[Balto withOptions: @{[Balto kBaltoHideMenu]: @YES}];
[Balto withLongPressWithMinimumPressDuration: 2.0 options: @{[Balto kBaltoHideMenu]: @YES}];
[Balto withCustomSwipeWithNumberOfTouchesRequired: 2 direction: UISwipeGestureRecognizerDirectionDown options: @{[Balto kBaltoHideMenu]: @YES}];
```

If you want to change the display for each screen, please call these methods at that timing.

```swift
Balto.show()
Balto.hide()
```

You need some setting if you use the Objective-C.

`Xcode->Project->Build Settings->Build Options->Embedded Content Contains Swift Code->YES`
