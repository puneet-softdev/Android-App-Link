# Android-App-Link
Handling Android App Links

-- What is Android App Links --

Android App Links, available on Android 6.0 (API level 23) and higher, are web links that use the HTTP and HTTPS schemes and contain the autoVerify attribute.
This attribute allows your app to designate itself as the default handler of a given type of link.
So when the user clicks on an Android App Link, your app opens immediately if it's installed—the disambiguation dialog doesn't appear

-- Steps --

1. Update the Android Manifest
First we must update all intent filters that can respond to an HTTP link with the android:autoVerify=”true” attribute

2. Create the assetlinks.json file

Option 1:- Create an empty file named assetlinks.json
If working with a single application, place the following information inside this file:

[{
  "relation": ["delegate_permission/common.handle_all_urls"],
  "target": {
    "namespace": "android_app",
    "package_name": "<Your App’s package name>",
    "sha256_cert_fingerprints":
    ["<Your App’s SHA256 finger print>"]
  }
}]

Option 2:- Use Android Studio’s App Link Assistant

Option 3:- Use Google’s statement list generator tool

3. Deploy the assetlinks.json file to host(s)

After generating the digital asset links file, deploy it to the host (or hosts if handling multiple domains) under a .well_known directory:-
https://www.doordash.com/.well-known/assetlinks.json

4. Verify that the assetlinks.json file is correct

Google provides a Digital Asset Links API to verify the accuracy of the assetlinks.json file: 

https://digitalassetlinks.googleapis.com/v1/statements:list?source.web.site=<https://domain.name:optional_port>&relation=delegate_permission/common.handle_all_urls

5. Verify your changes on Android

adb shell am start -a android.intent.action.VIEW \
    -c android.intent.category.BROWSABLE \
    -d "PLACE_YOUR_DEEPLINK_HERE"
    
This ADB command launches an implicit intent with the action VIEW, category BROWSABLE,
all of which is similar to the implicit intent executed when clicking on a link

    
    
