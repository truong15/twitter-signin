[![npm version](https://badge.fury.io/js/@react-native-twitter-signin%2Ftwitter-signin.svg)](https://badge.fury.io/js/@react-native-twitter-signin%2Ftwitter-signin.svg)

**Note: This package is a fork of [GoldenOwlAsia/react-native-twitter-signin](https://github.com/GoldenOwlAsia/react-native-twitter-signin) with added support for TwitterKit 5**

Note: this guide is for TwitterKit 5 and ReactNative 0.60+.

# React Native : Twitter Signin
This package provides necessary code to get your social sign in using Twitter works with least pain possible.

## Table of contents
- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Usage](#usage)
- [Todo](#todo)
- [Copyright and license](#copyright-and-license)
- [Inspiration](#inspiration)

## Prerequisites

Go to [Twitter Apps](https://apps.twitter.com/) to create your app so that you can obtain API key and secret, note:

 - Remember to set a Callback Url, whatever will work
 - By default, Twitter won't allow you to grab user's email, so you have to apply for a permission for your app to retrieve user's email

Here is how callbacks would look like:
![callbacks](https://github.com/react-native-twitter-signin/twitter-signin/blob/master/Example/img/callbacks.png?raw=true)

From Twitter Kit 3.3, Fabric is no longer required.

## Setup

Firstly, install the npm package:

    yarn add @truong15/react-native-twitter-signin@https://github.com/truong15/twitter-signin

### iOS

 - run `cd ios && pod install`
 - Configure Info.Plist like below, replace `<consumerKey>` with your own key:

```
// Info.plist
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array>
      <string>twitterkit-<consumerKey></string>
    </array>
  </dict>
</array>
<key>LSApplicationQueriesSchemes</key>
<array>
    <string>twitter</string>
    <string>twitterauth</string>
</array>
```
  - Modify AppDelegate.m to `#import <TwitterKit/TWTRKit.h>` and handle openUrl
````
- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<NSString *,id> *)options {
  return [[Twitter sharedInstance] application:app openURL:url options:options];
}
````

<details>
<summary>Linking Package Manually (not recommended)</summary>

 - Add `TwitterKit`:

 #### With CocoaPods

 - Add TwitterKit to your `Podfile`
 ```
 // Podfile
 target 'MyApp' do
   # use_frameworks!
   pod 'TwitterKit5', '~> 3.3.0'
 end
 ```
 - Run `pod install`

 #### Manually

 - Download TwitterKit 3.3 from here https://ton.twimg.com/syndication/twitterkit/ios/3.3.0/Twitter-Kit-iOS.zip
 - Add TwitterKit, TwitterCore and 2 other bundle files into your root folder in Xcode
 - In `Build Phases → Link Binary with libraries` add `Twitter.framework` and `LibRBTwitterSignin.a`

</details>

### Android

For React Native 0.60+, no additional setup is required for android.

<details>
<summary>Linking Package Manually (not recommended)</summary>


Run `react-native link react-native-twitter-signin`, or:

On Android, it will use `Gradle` so all you need to do is to point to the correct project location:

  - In your `${project_dir}/android/settings.gradle` add this:

        include ':react-native-twitter-signin'
        project(':react-native-twitter-signin').projectDir = new File(rootProject.projectDir,'../node_modules/react-native-twitter-signin/android')
  - In your `${project_dir}/android/app/build.gradle` add this:

        depedencies {
           ...
           compile project(':react-native-twitter-signin')
           ...
        }
  - In you `MainApplication.java` makes use of the package as following:

```java

        /**
        * A list of packages used by the app. If the app uses additional views
        * or modules besides the default ones, add more packages here.
        */
        @Override
        protected List<ReactPackage> getPackages() {
           return Arrays.<ReactPackage>asList(
             new MainReactPackage(),
             new FacebookLoginPackage(),
             new TwitterSigninPackage(),
             new RNGoogleSigninPackage(this),
             new VectorIconsPackage(),
             new RNSvgPackage()
           );
         }
```

Keeps in mind that all the configure is for your build tools to recognise the files. So open your Xcode and Android Studio to try making builds and make sure they pass.

</details>

## Usage

 - See the `Example` project.

![Sample](https://github.com/GoldenOwlAsia/react-native-twitter-signin/blob/master/Example/img/android.png?raw=true)



## Todo
The code was extracted from my project so it satisfies my current need, if you need extra functions, feel free to submit to issue list or fork it.

## Copyright and license

Code and documentation copyright 2016 Justin Nguyen. Code released under [the MIT license](https://github.com/GoldenOwlAsia/react-native-twitter-signin/blob/master/LICENSE).

## Inspiration

[react-native](http://facebook.github.io/react-native/)
[react-native-facebook-login](https://github.com/magus/react-native-facebook-login)

