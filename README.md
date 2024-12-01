# Huawei (AppGallery Connect) Setup

In this document, we are providing details about Huawei configuration in Android Studio. We are finally able to publish our app to AppGallery

Note - This document is useful for Gradle plugin version 7 and above

Last updated: 2024-11-30 07:57

## Acknowledgements

View official documentation [AppGallery Connect](https://developer.huawei.com/consumer/en/doc/AppGallery-connect-Guides/agc-get-started-android-0000001058210705#section1270317123213)

## Android

My current gradle version

- 8.6

Get the service file and put it in folder android/app

Note - Check service file package_name must match with app id eg. com.example.dev | com.example.uat | com.example.prod

```
agconnect-services.json
```

add a script in file android/build.gradle

```
  repositories {
       ...
     maven {url 'https://developer.huawei.com/repo/'}
    ...
  }

  dependencies {
      ...
        classpath("com.android.tools.build:gradle:8.0.2")
        classpath("com.huawei.agconnect:agcp:1.9.1.301")
      ...
  }

plugins {
   id 'com.android.application' version '8.2.0' apply false
   id 'com.android.library' version '8.2.0' apply false
}


allprojects {
    repositories {
        google()
        mavenCentral()
        maven { url 'https://developer.huawei.com/repo/' }  // Huawei Maven repository
    }
}
```

add a script in file android/settings.gradle top side

```
pluginManagement {
    repositories {
        gradlePluginPortal()
        google()
        mavenCentral()
        maven { url 'https://developer.huawei.com/repo/' }
    }
}
dependencyResolutionManagement {
    repositories {
        google()
        mavenCentral()
        maven {url 'https://developer.huawei.com/repo/'}
    }
}

```

Add the script to the file android/app/build.gradle

```
//Topside
apply plugin: 'com.huawei.agconnect'



dependencies {
    ...
    // The bottom line script is the plugin.
    // You can also use other plugins as per business requirements
   implementation 'com.huawei.agconnect:agconnect-core:1.9.1.301'
...

}
```

## Authors

- [@vdodke](https://github.com/VipinDodke)

