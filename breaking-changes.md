---
nav-title: Breaking Changes
title: "Breaking Changes"
description: A list of breaking changes across the releases of the NativeScript framework and its tools.
position: 21
---

# NativeScript Framework Breaking Changes

This document describes the critical breaking changes and suggested workarounds, if any, in the NativeScript framework. The complete list with all the changes may be found on the respective [Github repositories](#see-also).


### 1.4.0 (2015, October 12)
-  [(#774)](https://github.com/NativeScript/NativeScript/issues/774) Animation class no longer has a **finished** property because an animation can be played multiple times. The **play** method now returns a new Promise each time it is invoked. Use this to listen for the animation finishing or being cancelled. When upgrading to version 1.4.0 or above simply remove **.finished** from your code.

**Old Code (JavaScript)**:
```JavaScript
animation1.play().finished.then(function () { console.log("Finished"); });
```
**New Code (JavaScript)**:
```JavaScript
animation1.play().then(function () { console.log("Finished"); });
```
**Old Code (TypeScript)**:
```JavaScript
animation1.play().finished.then(()=>console.log("Finished"));
```
**New Code (JavaScript)**:
```JavaScript
animation1.play().then(()=>console.log("Finished"));
```

### 1.3.0 (2015, September 16)

There are multiple breaking changes in this release.

NativeScript modules use and depend on the app-compatibility library (android-support-v7-appcompat) for Android. To work properly the theme of the application should be based on **Theme.AppCompat.Light.NoActionBar**. If you have defined custom Android `style.xml` files in the `App_Resources\Android\values[-v21]` folders, you will have to change the parent theme of the `AppTheme`(or `AppThemeBase` if you have such) to **Theme.AppCompat.Light.NoActionBar** (in both `values` and `values-v21` folders). For reference the default content of those files can be found in the [default project template for android](https://github.com/NativeScript/android-runtime/tree/master/build/project-template-gradle/src/main/res).

Core NativeScript modules are published as a separate [package](https://www.npmjs.com/package/tns-core-modules) in [npmjs.com](https://www.npmjs.com).

`library add` command is deprecated and will be removed completely in one of our next releases (currently scheduled for 1.5).

You cannot create NativeScript plugins with Android native code using Eclipse projects. You need to import your Eclipse project into Android Studio, convert it to Gradle build and consume the produced AAR file.

You cannot use Apache Ant to create new projects for Android but you can continue build your existing Ant-based projects. Starting with NativeScript 1.3, Android builds require Gradle. Run `tns doctor` on the command line to learn more.

Building NativeScript projects for Android requires Android SDK 22, Android SDK Build-tools 22, Android Support Repository and ANDROID_HOME environment variable set.

NSDecimalNumber is marshalled as Objective-C object wrapper instead of JavaScript number.

### 1.2.0 (2015, July 24)

There are changes in how the **Android ActionBar/IOS NavigationBar** is configured. Ut is now defined with `page.actionBar` instead of `page.optionsMenu`. [See an example...](./ApiReference/ui/action-bar/HOW-TO.md) 

### 0.10.0 (2015, April 17)

This release introduces a new project directory structure. Projects from earlier releases have the following structure:

```
.
└── hello-world
    ├── app
    │   ├── app
    │   │   ├── app.css
    │   │   ├── app.js
    │   │   ├── bootstrap.js
    │   │   ├── main-page.js
    │   │   └── main-page.xml
    │   ├── App_Resources
    │   │   └── ...
    │   └── tns_modules
    │       └── ...
    └── platforms
        └── ...
```
Starting with version 0.10, the inner app folder has been removed. Newly created projects have the following structure:

```
.
└── hello-world
    ├── app
    │   ├── app.css
    │   ├── app.js
    │   ├── bootstrap.js
    │   ├── main-page.js
    │   ├── main-page.xml
    │   ├── App_Resources
    │   │   └── ...
    │   └── tns_modules
    │       └── ...
    └── platforms
        └── ...
```

>To migrate to the new structure, complete the following steps:

>1. Manually move all files and folders from the inner app folder one level up inside the outer app folder.
>2. Remove the now empty inner app folder.

#See Also

* [Cross-platform Modules Changelog](./Changelogs/Cross-Platform Modules.md)
* [Command-line Interface Changelog](./Changelogs/CLI.md)
* [iOS Runtime Changelog](./Changelogs/iOS Runtime.md)
* [Android Runtime Changelog](./Changelogs/Android Runtime.md)
