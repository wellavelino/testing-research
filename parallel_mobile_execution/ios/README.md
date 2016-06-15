## iOS Build cheatsheet


### Provisioning profile

A provisioning profile consists of several items. The most important are:

* App ID
* Signing certificates
* List of device UDIDs that the app is allowed to run on

### Signing certificate

A signing certificate is a security certificate unique to a person. It is used by Apple to identify the person and the private key for the certificate is used to sign the application.

There are two types of signing certificates:

* Development certificate
* Distribution certificate

Development certificates are used by individual developers for development and debugging. They allow the developer to deploy apps to test devices (UDIDs listed in the provisioning profile) and debug them.

Distribution certificates are used for publishing apps (e.g. to the App store).

### Creating and downloading certificates

Before issuing a certificate, your Apple ID should be added to the development team on [developer.apple.com]().

After being added, follow the wizard on [developer.apple.com]() to create and download the certificate and add it to your keychain.

To verify and complete this process:

* Open Xcode
* Go to Preferences -> Accounts
* If your Apple ID is not displayed, add a new account and sign in with your Apple ID
* After clicking on your Apple ID, your team should be displayed in the teams list
* Select your team and click “View Details…”
* Select “iOS Development” from Signing identities list and click create
* Select desired provisioning profile from Provisioning profiles list and click download
* Click “Done”

For further information visit [apple developer documentation]().

### Building your app for the iOS Simulator

Prerequisites:

* ios-sim installed (CLI tool used for launching iOS simulators - can be installed with Homebrew)
* Desired simulator version installed (simulators can be installed in Xcode preferences -> Components)
* CocoaPods gem installed (gem install cocoapods) - used for managing dependencies

To build the app:

* Navigate to project folder (folder containing the project .xcworkspace folder)
* Run `pod setup`
* Run `pod install`
* Run xcodebuild command with needed arguments:

```
xcodebuild -workspace projectName.xcworkspace -scheme schemeName -destination ‘platform=iOS Simulator,name=iPhone6,OS=9.3’ -derivedDataPath /desired/folder/for/appFile build
```

Note: If build schemes are missing:

Open .xcworkspace file with Xcode and close Xcode
Run `xcodebuild -list` and use one of the listed schemes

After building the app, you can launch it with `ios-sim`.

```
ios-sim launch /desired/folder/for/appFile/Build/Products/Debug-iphonesimulator/YourApp.app --devicetypeid 'com.apple.CoreSimulator.SimDeviceType.iPhone-6, 9.3’
```


