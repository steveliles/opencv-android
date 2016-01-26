# opencv-android

OpenCV4Android, packaged as a .aar for direct use without depending on the stupid OpenCV Manager app.

### Building an .aar of OpenCV-3.x.y for yourself

Building OpenCV-3.x.y for Android is actually quite simple, its just not obvious where to get the pieces and the OpenCV docs hard-sell the "OpenCV Manager" in favour of the better and easier direct integration approach.

Here's the steps I used to create my .aar:

1. Download and extract the OpenCV4Android bundle
2. Create a Library Project in Android Studio
3. Copy the java source files from OpenCV4Android into src/main/java
4. Drop the OpenCV native libraries into src/main/jniLibs
5. Run the gradle build
6. Et voila, .aar file

### Using your glorious new .aar

Reference the maven repository you've deployed your .aar to, e.g. mine (which I can't stop you from using ;)) is:

    allprojects {
      repositories {
        jcenter()
        maven {
           url  "http://dl.bintray.com/steveliles/maven" 
        }
      }
    }

Include the .aar in your build.gradle file:

    dependencies {
      compile 'org.opencv:OpenCV-Android:3.1.0'
    }
    
Bootstrap OpenCV in your Java code:
    
    import org.opencv.android.OpenCVLoader;
    
    ...
    
    if (OpenCVLoader.initDebug()) {
      // do some opencv stuff
    }

Optional but recommended: to keep the downloaded APK size to a minimum, build separate APK's per architecture (approx 10MB each vs 42MB for universal) by placing the following inside the 'android' gradle directive of your application's build.gradle:

    splits {
      abi {
        enable true
        reset()
        include 'x86', 'x86_64', 'armeabi', 'armeabi-v7a', 'mips', 'mips64', 'arm64-v8a'
        universalApk false
      }
    }

Disclaimer: This project is simply my bundling of OpenCV as an Android Library. I am not otherwise involved in the OpenCV project, and all credit for the wonderful OpenCV library goes to the developers thereof.







