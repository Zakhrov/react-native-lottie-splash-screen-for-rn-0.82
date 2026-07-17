# @ravinandan25/react-native-lottie-splash-screen

[![npm](https://img.shields.io/badge/npm-@ravinandan25/react--native--lottie--splash--screen-blue)](https://www.npmjs.com/package/@ravinandan25/react-native-lottie-splash-screen)
[![PRs Welcome](https://img.shields.io/badge/PRs-Welcome-brightgreen.svg)](https://github.com/ravinandan25/react-native-lottie-splash-screen/pulls)
[![License MIT](https://img.shields.io/badge/license-MIT-orange.svg)](https://opensource.org/licenses/MIT)

Fixed version of `react-native-lottie-splash-screen` — resolves gray overlay and status bar issues on Android. Works on React Native 0.82+ with Swift implementation on iOS.

## Contents

- Version Compatibilities
- Examples
- Installation
- iOS Setup
- Android Setup
- Usage
- API
- Contribution

## Versions Compatibilities

| React Native     | Package Version |
|------------------|-----------------|
| >= 0.82          | 4.x             |
| >= 0.80 & < 0.82 | 3.x             |
| >= 0.70 & < 0.77 | 2.x             |  
| < 0.70           | 1.x             |

## Examples

![Android](screenshot/Lottie-Splash-Screen-Android.gif)
![iOS](screenshot/Lottie-Splash-Screen-IOS.gif)

Run examples:

```bash
yarn install
yarn bare8x:install
yarn bare8x:ios
yarn bare8x:android

```

## Installation

```bash
yarn add "@ravinandan25/react-native-lottie-splash-screen"
cd ios && bundle install && bundle exec pod install
```

## iOS Setup

1. Add your Lottie JSON (e.g., `loading.json`) to the Xcode project and include it in your app target.  
2. Replace or edit your `AppDelegate.swift`:

```swift
import UIKit
import SplashScreen

@main
class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?

  func application(_ application: UIApplication,
                   didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {

    SplashScreen.setupLottieSplash(
      in: window,
      lottieName: "loading",
      backgroundColor: UIColor.white,
      forceToCloseByHideMethod: false
    )

    return true
  }
}
```

1. Remove the default launch screen or make it blank in `LaunchScreen.storyboard`.

## Android Setup

1. Create `android/app/src/main/res/layout/launch_screen.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    tools:context=".MainActivity"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@color/primary"
>
    <com.airbnb.lottie.LottieAnimationView
        android:id="@+id/lottie"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:lottie_rawRes="@raw/loading"
        app:lottie_autoPlay="true"
        app:lottie_loop="true"
    />
</LinearLayout>

```

1. Place your Lottie JSON at `android/app/src/main/res/raw/loading.json`.

2. Add colors in `android/app/src/main/res/values/colors.xml`:

```xml
<resources>
  <color name="windowSplashScreenBackground">#ffffff</color>
</resources>
```

1. Add styles in `android/app/src/main/res/values/styles.xml`:

```xml
<resources>
    <style name="AppTheme" parent="Theme.MaterialComponents.DayNight.NoActionBar">
        <item name="android:editTextBackground">@drawable/rn_edit_text_material</item>
        <item name="android:statusBarColor">@android:color/transparent</item>
        <item name="android:navigationBarColor">@android:color/transparent</item>
    </style>
    <style name="SplashScreen_SplashTheme" parent="Theme.MaterialComponents.DayNight.NoActionBar">      

        <!-- Fullscreen flags -->
        <item name="android:windowFullscreen">true</item>
        <item name="android:windowTranslucentStatus">false</item>
        <item name="android:windowTranslucentNavigation">false</item>
        <item name="android:windowDrawsSystemBarBackgrounds">true</item>

        <!-- System bars -->
        <item name="android:statusBarColor">@android:color/transparent</item>
        <item name="android:navigationBarColor">@android:color/transparent</item>

        <!-- No title -->
        <item name="android:windowNoTitle">true</item>
        <item name="android:windowActionBar">false</item>

        <!-- For notches/cutouts -->
        <item name="android:windowLayoutInDisplayCutoutMode">shortEdges</item>
    </style>
</resources>
```

1. Update `MainActivity.kt`:

```kotlin
import android.os.Bundle
import org.devio.rn.splashscreen.SplashScreen
import com.facebook.react.ReactActivity

class MainActivity : ReactActivity() {
  override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    SplashScreen.show(this, R.style.SplashScreen_SplashTheme, R.id.lottie, false)
  }
}
```

## Usage

```react
import { useEffect } from "react";
import LottieSplashScreen from "@ravinandan25/react-native-lottie-splash-screen";

export default function App() {
  useEffect(() => {
    LottieSplashScreen?.hide();
  }, []);
  return null;
}
```

## API

| Method | Type     | Description                     |
|--------|----------|---------------------------------|
| hide() | function | Hides the Lottie splash overlay |

## Contribution

Issues and PRs are welcome. Include a minimal repro if possible.

**MIT Licensed**  
by Ravinandan
