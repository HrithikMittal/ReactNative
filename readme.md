# React Native

### More on Flexbox

React Native uses Flexbox to position elements and create layouts. It also uses a set of CSS properties you can use to style your elements.

One important thing to note is, that it uses Flexbox and these properties but that it doesn't really use CSS! You don't write real CSS code here, you still write everything in JavaScript.

Not even close to all CSS properties and features are supported therefore.

If you want to get a full list about the supported properties, the following cheat sheet will be useful to you: <a href="https://github.com/vhpoet/react-native-styling-cheat-sheet">https://github.com/vhpoet/react-native-styling-cheat-sheet</a>

If you want to learn more about Flexbox, don't miss this awesome article: <a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox/">https://css-tricks.com/snippets/css/a-guide-to-flexbox/</a>

### UseFull Resources

<ul>
<li>Understand the Basics: <a href="https://github.com/react-community/create-react-native-app">https://github.com/react-community/create-react-native-app</a></li>
<li>Understand Flexbox: <a href="https://css-tricks.com/snippets/css/a-guide-to-flexbox/">https://css-tricks.com/snippets/css/a-guide-to-flexbox/</a></li>
<li>More about images: <a href="https://facebook.github.io/react-native/docs/images.html">https://facebook.github.io/react-native/docs/images.html</a>
</li>
</ul>

### Debugging React Native

<ul>
<li>React Native Debugger:<a href="https://github.com/jhen0409/react-native-debugger"> https://github.com/jhen0409/react-native-debugger</a>
</li><li>More about Debugging:<a href="https://facebook.github.io/react-native/docs/debugging.html"> https://facebook.github.io/react-native/docs/debugging.html</a>
</li>
</ul>

### vAutomatic Linking
a lot of libraries take some extra steps during the linking process which can't be automated.

For libraries that don't require such extra steps, there is an automated way of linking available though.

You'll need to install an extra package: 

```
react-native-cli
``` 

It's actually installed locally in your project already but if you want to run commands with it, you need to install it globally.

Install it globally via 
```
npm install -g react-native-cli 
```
Thereafter, in your project folder, you can run 
```
react-native link 
```
 to automatically link all libraries that require linking.

Important: ALWAYS check the docs (e.g. on the Github repo page) of the library you're using! You definitely have to ensure that no additional steps are required!


### Fixing Installation Issues with React Native Navigation
In the next two lectures, we'll install React Native Navigation for both iOS and Android.

All instructions are given in the following lectures but experience shows that problems can arise.

You can skip this lecture for now but please have a look at it if you are facing problems in the next two videos (i.e. with the installation of React Native Navigation).

---

Really important: Make sure you're installing React Native Navigation 1 - NOT version 2. Version 2 has a totally different syntax and whilst you're of course free to explore it for your own projects, for this course, we'll use the proven version 1.

```
npm install --save react-native-navigation@1
```

iOS Setup

Official Setup Docs: https://github.com/wix/react-native-navigation/blob/v1/docs/installation-ios.md

The link to the AppDelegate.m file will not work there - this is the correct one: https://github.com/wix/react-native-navigation/blob/v1/example/ios/example/AppDelegate.m

Normally, no other steps should be required, installing React Native Navigation v1

Android Setup

1) Add the following to android/settings.gradle
```
include ':react-native-navigation'
project(':react-native-navigation').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-navigation/android/app/')
```
2) In the android/app/build.gradle file, replace the dependencies:

```
implementation "com.android.support:appcompat-v7:${rootProject.ext.supportLibVersion}"
implementation 'com.android.support:design:27.1.0' 
implementation "com.facebook.react:react-native:+" // From node_modules
compile fileTree(dir: "libs", include: ["*.jar"]) 
compile project(':react-native-vector-icons') 
compile project(':react-native-navigation')
```
Important: For compile project(':react-native-vector-icons') to work, make sure you installed react-native-vector-icons as described here: https://github.com/oblador/react-native-vector-icons#option-manually-1

If you installed React Native Vector Icons via Gradle (https://github.com/oblador/react-native-vector-icons#option-with-gradle-recommended), you might be running into issues, hence use the manual approach linked above!

3) As a next step, adjust your android/app/src/main/java/.../MainActivity.java file to look like this:

```
package YOUR_PACKAGE_NAME; // You can leave your file default here
 
import com.facebook.react.ReactActivity;
import com.reactnativenavigation.controllers.SplashActivity;
 
public class MainActivity extends SplashActivity {
 
}
```
Any methods you had in the MainActivity before can be deleted or commented out.

4) Finally, adjust your android/app/src/main/java/.../MainApplication.java file to look like this:
```
package YOUR_PACKAGE_NAME; // You can leave your file default here
 
import android.app.Application;
 
import com.facebook.react.ReactApplication;
import com.facebook.react.ReactNativeHost;
import com.facebook.react.ReactPackage;
import com.facebook.react.shell.MainReactPackage;
import com.facebook.soloader.SoLoader;
import com.reactnativenavigation.NavigationApplication;
import com.oblador.vectoricons.VectorIconsPackage;
 
import java.util.Arrays;
import java.util.List;
 
public class MainApplication extends NavigationApplication {
 
  @Override
  public boolean isDebug() {
    // Make sure you are using BuildConfig from your own application
    return BuildConfig.DEBUG;
  }
 
  protected List<ReactPackage> getPackages() {
    // Add additional packages you require here
    // No need to add RnnPackage and MainReactPackage
    return Arrays.<ReactPackage>asList(
      new VectorIconsPackage()
    );
  }
 
  @Override
  public List<ReactPackage> createAdditionalReactPackages() {
    return getPackages();
  }
 
  @Override
  public String getJSMainModuleName() {
    return "index";
  }
}
---
```
With these steps, the application should work - I tested the entire setup (including React Native Vector Icons and React Redux) with version 0.59 of React Native and had no issues on iOS or Android.

Author - ADHIKANSH MITTAL 
