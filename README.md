## Introduction

[CrashProbe](http://crashprobe.com/) provides a set of test crashes that can be used to test crash reporting SDKs and symbolication implementations on iOS and OS X.

The project has been developed using Xcode 5.1.1 and has been tested with OS X 10.9.2 and iOS 7.1.1.

## Setup

1. Clone this repository.
2. Open the project in Xcode.
3. Integrate your crash reporting SDK into the required platform target (`CrashProbe` for OS X and `CrashProbeiOS` for iOS).
4. Build the app using the `Release` build configuration and install it on a device.

   Either use `Archive` or `Build for Profiling` and copy the app bundle onto the device. Using `Debug` build configuration will result in different results due to disabled compiler optimizations.
5. Start the app without the debugger being attached.
6. Choose a crash and trigger it.
7. Start the app again, the integrated SDK should now upload the crash report to its server.
8. Go back to step 5. and process the next crash. Otherwise continue with step 9.
9. Symbolicate the crash report(s).
10. Compare the symbolicated crash report(s) with the data available on the [CrashProbe](http://crashprobe.com/) website.

## Tool Implementations

HockeyApp: Default version: 4.1.6 , [Official tutorial website](https://support.hockeyapp.net/kb/client-integration-ios-mac-os-x-tvos/hockeyapp-for-ios)
1. Make sure you have HockeyApp SDK, the default one is inside the CrashProbe/Vender/HockeyApp-SDK-iOS-4.1.6
2. Make sure the Project Navigator in xcode is visible (⌘+1).
3. Drag the HockeySDK.embeddedframework/HockeySDK.framework from Finder to the Vendor/HockeyApp in Project Navigator.
4. Set the checkmark for your target, in this case, the CrashProbeiOS.
5. Open the CrashProbe/CrashProbe iOS/CRLAppDelegate.m file.
6. Uncomment the define HOCKEY_APP in line 29.
7. Update the APP_ID in line 53.
8. Update Bundle Identifier for CrashProbeiOS.
9. Build ipa and start test.

MobileCenter: Default version: 0.11.2 , [Official tutorial website](https://docs.microsoft.com/en-us/mobile-center/sdk/getting-started/ios)
1. Make sure you have MobileCenter SDK, the default one is inside the CrashProbe/Vender/MobileCenter-SDK-iOS-0.11.2
2. Make sure the Project Navigator in xcode is visible (⌘+1).
3. Drag the MobileCenter.framework, MobileCenterAnalytics.framework, and MobileCenterCrashes.framework from Finder to the Vendor/MobileCenter in Project Navigator.
4. Set the checkmark for your target, in this case, the CrashProbeiOS.
5. Open the CrashProbe/CrashProbe iOS/CRLAppDelegate.m file.
6. Uncomment the define MOBILE_CENTER in line 30.
7. Update the APP_SECRET in line 60.
8. Build ipa and start test.

Crashlytics: Default version: 3.8.5 , [Official tutorial website](https://fabric.io/kits/ios/crashlytics/manual-install)
1. Make sure you have HockeyApp SDK, the default one is inside the CrashProbe/Vender/Crashlytics-SDK-iOS-3.8.5
2. Make sure the Project Navigator in xcode is visible (⌘+1).
3. Drag the Crashlytics.framework and Fabric.framework from Finder to the Vendor/Crashlytics in Project Navigator.
4. Set the checkmark for your target, in this case, the CrashProbeiOS.
5. Open the CrashProbe/CrashProbe iOS/CRLAppDelegate.m file.
6. Uncomment the define CRASHLYTICS in line 31.
7. Click CrashProbe in Project Navigator and select CrashProbeiOS in TARGETS.
8. Select Build Phrases and add a New Run Build Phase.
9. Add following sentence into Shell:
```
"${PROJECT_DIR}/Vendor/Crashlytics/Fabric.framework/run" API_KEY BUILD_SECRET
```
10.Update API_KEY and BUILD_SECRET.
11.Add following setting into CrashProbe/CrashProbe iOS/Supporting Files/CrashProbe iOS-Info.plist
```
<key>Fabric</key>
<dict>
    <key>APIKey</key>
    <string>API_KEY</string>
    <key>Kits</key>
    <array>
        <dict>
            <key>KitInfo</key>
            <dict/>
            <key>KitName</key>
            <string>Crashlytics</string>
        </dict>
    </array>
</dict>
```
12.Update API_KEY
13.Update Bundle Identifier for CrashProbeiOS.
14.Build ipa and start test.

## Disclaimer

The suite of tests was developed by [Bit Stadium GmbH](http://hockeyapp.net/) for the [HockeyApp](http://hockeyapp.net) service.

## Contributing

### Code of Conduct

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

### Contributor License

You must sign a [Contributor License Agreement](https://cla.microsoft.com/) before submitting your pull request. To complete the Contributor License Agreement (CLA), you will need to submit a request via the [form](https://cla.microsoft.com/) and then electronically sign the CLA when you receive the email containing the link to the document. You need to sign the CLA only once to cover submission to any Microsoft OSS project. 

## License

This project is released under the MIT license.
