# opencv-android-3.0.0

### TL;DR

Include the "example" .aar in your build.gradle file:

    dependencies {
      compile ''
    }

Build separate APK's per architecture, to keep the downloaded APK size to a minimum:

    splits {
      abi {
        enable true
        reset()
        include 'x86', 'x86_64', 'armeabi', 'armeabi-v7a', 'mips', 'mips64', 'arm64-v8a'
        universalApk false
      }
    }

### Details

An "Example" Android Library Project for OpenCV 3.0.0

OpenCV is awesome, but getting started using it on Android is too awkward: Why can't I just reference a gradle dependency and just get on with it?

The OpenCV documentation for Android recommends using the "dynamic" method for making OpenCV available to your apps, via the OpenCV Manager application. The claimed advantages of the dynamic method are:

* minimal download
* automatic updates to newer opencv versions
* some mysterious optimisations are turned on

If you don't like the user-experience that this presents, or are worried that an automatic update might break your app in a way that is outside of your control, you need to use the "static" approach of bundling the native libs in your own project. This isn't particularly well documented, and unless you know how to set up your application project properly you'll end up with 50MB+ APK's stuffed full of native libs.

### Building an .aar of OpenCV-3.x

Building OpenCV-3.0.0 for Android is actually quite simple:

1. Create a Library Project in Android Studio
2. Drop the OpenCV native libraries into src/main/jniLibs
3. Run the gradle build
4. Et voila, .aar file

If you naively build an app with this .aar file, it will include all of the native libs for all architectures in a single APK, which will immediately push your APK over 50MB without counting any of your own code, resources or assets.

To minimize the build size you'll need to split your APK's by ABI. To do this, add the "splits" section to the configuration of the android gradle plugin in your app's build.gradle (see the splits example above).









