# Splashscreen in react-native android.
Watch video for better understanding [here](https://www.youtube.com/watch?v=cdNBd63H54g)
## Follow the given steps

1.) Initialise a bare react native app (if not already done).
2.) Install react-native-splash-screen and link the library.
```
npm i react-native-splash-screen
```
```
react-native link react-native-splash-screen
```

3.) Add splash.png to all minmap folders.
 - Go to android/app/src/main/res
 - There you will find minmap folders

4.) Inside the **res** directory, create a folder named **drawable**. Inside that, ceate a file named **background_splash.xml**
 - Add the below code to the file
```
<?xml version="1.0" encoding="utf-8"?>
<layer-list xmlns:android="http://schemas.android.com/apk/res/android">
 <item
 android:drawable="@mipmap/splash"
 android:gravity="fill" />
</layer-list>
```
5.) Inside the **res** directory, create a folder named **layout**. Inside that, ceate a file named **launch_screen.xml**
 - Add the below code to the file
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
 android:orientation="vertical"
 android:layout_width="match_parent"
 android:layout_height="match_parent"
 android:background="@drawable/background_splash"
/>
```

6) Go to **res/values/styles.xml** and add
```
<style name="SplashTheme" parent="Theme.AppCompat.Light.NoActionBar">
 <item name="android:windowBackground">@drawable/background_splash</item>
</style>
```
7) Modify your **AndroidManifest.xml** to look like this.
```
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
  package="com.splashexample">

    <uses-permission android:name="android.permission.INTERNET" />

    <application
      android:name=".MainApplication"
      android:label="@string/app_name"
      android:icon="@mipmap/ic_launcher"
      android:roundIcon="@mipmap/ic_launcher_round"
      android:allowBackup="false"
      android:theme="@style/AppTheme">
+      <activity
+        android:name=".SplashActivity"
+        android:theme="@style/SplashTheme"
+        android:label="@string/app_name">
+        <intent-filter>
+          <action android:name="android.intent.action.MAIN" />
+          <category android:name="android.intent.category.LAUNCHER" />
+        </intent-filter>
+     </activity>

      <activity
        android:name=".MainActivity"
        android:label="@string/app_name"
        android:configChanges="keyboard|keyboardHidden|orientation|screenSize|uiMode"
        android:launchMode="singleTask"
        android:windowSoftInputMode="adjustResize"
+       android:exported="true">
-       <intent-filter>
-          <action android:name="android.intent.action.MAIN" />
-          <category android:name="android.intent.category.LAUNCHER" />
-        </intent-filter>
      </activity>
    </application>
</manifest>
```

8) Create **SplashActivity.java** in main/java/com/{your_package_name}
```
package com.splashexample; //change your package name
import android.content.Intent;
import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
public class SplashActivity extends AppCompatActivity {
     @Override
     protected void onCreate(Bundle savedInstanceState) {
         super.onCreate(savedInstanceState);
         Intent intent = new Intent(this, MainActivity.class);
         startActivity(intent);
         finish();
     }
}
```
9) Go to **MainActivity.java**
```
package com.splashexample; // change package name

import com.facebook.react.ReactActivity;
import org.devio.rn.splashscreen.SplashScreen; // add this
import android.os.Bundle; // add this


public class MainActivity extends ReactActivity {

  /**
   * Returns the name of the main component registered from JavaScript. This is used to schedule
   * rendering of the component.
   */
  @Override                                             // add this
  protected void onCreate(Bundle savedInstanceState) {  // add this
    SplashScreen.show(this);                            // add this
    super.onCreate(savedInstanceState);                 // add this
  }                                                     // add this
  @Override
  protected String getMainComponentName() {
    return "splashexample";
  }
}

```

10.) Go to **App.js** in the *src* folder.
 - at the top
```import SplashScreen from 'react-native-splash-screen';```
 - inside App function add useEffect (Make sure to import it)
 ```
 useEffect(() => {
    SplashScreen.hide();
  }, [])
```
**Best part begins-**
 - Hit the terminal and write ```react-native run-android```
 - You will find a beautiful spalsh screen welcoming you.

