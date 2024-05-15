# Configuring CI/CD for a React-Native App with AppCenter
*Max Orlov - December 6, 2023*

## Android 

### Building assembleRelease (APK)
**1. Create a project in AppCenter:**
    - Enter the app name and upload an icon;
    - OS: Android;
    - Add the app;
    - Platform: React Native, Check: [Flutter Integration with AppCenter](https://flutter.dev/docs/deployment/cd#app-center);

**2. Navigate to the "Build" tab.**

**3. Connect your GitHub repository.**

**4. Configure the build:**
1. Click the gear icon on the right side;
    - Turn "Build Android App Bundle" to On;
2. Choose "Automatically increment version code" (Off or On):
    - Use the Build number format as "Build ID";
3. Enable "Environment variables":
    - Refer to the troubleshooting section [Build assembleRelease (APK)](#troubleshooting-android-1);
4. Turn "Sign builds" to On:
    - Check [Build bundleRelease (AAB)](#build-bundle-release);
5. Enable "Distribute":
    - Check [Distribute android build](#distribute-android);
6. Enable "Test on a real device":
    - It's free, but it add about 10 minutes to the build time.
7. Save and Build:
    - TA DAAAAAAAAAA! Congratulations, you now have your first APK file with AppCenter!

## Build bundleRelease (AAB) <a id="build-bundle-release"></a>
1. Check react-native docs to Sign your App:
    - Read docs [Publishing to Google Play Store](https://reactnative.dev/docs/signed-apk-android);
    - rootFolder/cd android/cd app
    - sudo keytool -genkey -v -keystore testci-cd-nlt.keystore -alias testci-cd-nlt-alias -keyalg RSA -keysize 2048 -validity 10000;
2. Send .keystore file to your team/tech Lead or CTO;
3. Go to project build configuration "Sign builds":
    - if your doing standard react-native configuration check auto signIn or upload your keystore file.
    - Upload keystore:
        Keystore password:testci-cd-nlt.keystore
        Key alias:testci-cd-nlt-alias
        Key password:testCiCdNltDev
4. Save and Build:
    - TA DAAAAAAAAAA! Its your first aab file with AppCenter!;

<!-- ## Distribute build to Play Market
**Not working**
1. Go to your Google Play Console;
<!-- ![Where is Security token](/assets/apiAccess.png) -->
<!--
2. How to get Api access: https://help.radio.co/en/articles/6232140-how-to-get-your-google-play-json-key -->

# IOS

## Build archive
1. Create project in AppCenter:
    - Enter app name and icon;
    - OS: IOS;
    - Platform: React Native Check: [Flutter Integration with AppCenter](https://flutter.dev/docs/deployment/cd#app-center);
    - Add app;
2. Go to "Build" tab.
3. Connect your github repository.
4. Configure build:
    - Press gear icon on right side
    - Set "Automatically increment version code" to Off or On:
        - Build number format "Build ID"
    - Set "Sign builds" to On:
        - Check "Build signed archive"
    - Save and Build:
        - TA DAAAAAAAAAA!;

## Build signed archive
1. Create App Store connect project;
2. Get/Create Apple Distribution provision profile and Certificate:
    - Certificate extension must be a `.p12`, to do this, install certificate to your PC and export from your keychain.
    - Read: https://stackoverflow.com/questions/66846068/;using-appcenter-ms-trying-to-build-for-ios-invalid-p12-certificate
3. Go to Xcode and add team to project;
4. Build archive manually 
5. Commit and push;
6. Go to project build configuration:
    - Upload Profile and certificate to "Sign builds";
    - Set "Test on a real device" to On:
        - It is free but add 10 minutes to build time.
    - Set "Distribute" to On:
        - Check "Distribute build";
7. Save and Build;

# Distribute build

## IOS
**1.Colaborators**
1. Go to distribute tab;
2. Create groups or add collaborators;
3. Configure dev brunch to distribute with collaborators
4. Configure main brunch to distribute with testers

**2.Store and TestFlight**
1. Go to distribute tab => Stores;
2. Connect with Apple developer or add api key, [how to get api key](https://developer.apple.com/documentation/appstoreconnectapi/creating_api_keys_for_app_store_connect_api):
    - Go to Users and Access at [appstoreconnect](https://appstoreconnect.apple.com/) and then select the API Keys tab
    - Click Generate API Key or the Add (+) button.
    - Enter a name for the key. The name is for your reference only and is not part of the key itself.
    - Under Access, select the role for the key.
    - Click Generate.
    ![Where is Security token](/assets/apiKeyIos.png)
    - Appcenter cannot create a version, it only uploads a new build to the existing version, so make the first build manually
    - Return to distribute tab => Stores and connect to TestFlight
    - Go to "Distribute build" in Build Configure:
        - Select "Store"
        - Choose AppStore or TestFlight
    - Save and Build:
        - TA DAAAAAAAAAA! Check your TestFlight;

## Android<a id="distribute-android"></a>
**1.Colaborators**
1. Go to distribute tab;
2. Create groups or add collaborators;
3. Configure dev brunch to distribute with collaborators
4. Configure main brunch to distribute with testers

# Troubleshooting
## IOS
#### 1. Build signed archive error: `Not found appcenter: null`

I create an Apple distribution and Development profiles/certs but got an error:
=================================================|
Task         : Command Line
Description  : Run a command line with arguments
Version      : 1.1.3
Author       : Microsoft Corporation
Help         : [More Information](https://go.microsoft.com/fwlink/?LinkID=613735)
=================================================|
[error]Failed which: Not found appcenter: null
(node:11523) Warning: Use Cipheriv for counter mode of aes-256-ctr
(node:11523) Warning: Use Cipheriv for counter mode of aes-256-ctr
(node:11523) Warning: Use Cipheriv for counter mode of aes-256-ctr

Resolve this: Add variable `JAVA_HOME : $(JAVA_HOME_11_X64)`


## Android
#### 1. Build assembleRelease (APK) <a id="troubleshooting-android-1"></a>
I have a bug with "Users/runner/work/1/s/android/gradlew failed with return code: 1", I resolve it by adding "Environment variables" in build configuration:
- Add variable: `JAVA_HOME : $(JAVA_HOME_11_X64)`

# Links
1. [AppCenter](https://appcenter.ms/)
2. [Flutter Integration with AppCenter](https://flutter.dev/docs/deployment/cd#app-center)
3. [Integrate Flutter with other services](https://mittalkartik1.medium.com/the-complete-guide-to-deploy-flutter-builds-using-app-center-3f784fefd5fe)
4. [Android configure video](https://www.youtube.com/watch?v=su-qGafvkCU)
5. [IOS configure video](https://www.youtube.com/watch?v=ttNbomU8yBI)
