# test_flavours

Test project to see how flutter pub run flutter_flavorizr changes files in a flutter project

## Making changes
1. sudo gem install xcodeproj (only need to do once locally)
2. Config pubspec.yaml > flavorizr key
3. Commit and push to repo
4. flutter pub run flutter_flavorizr
5. Run command for flavour
6. Discard changes by step 4


## Run Commands
Dev and test: 
flutter run --flavor flav_test -t lib/main_flav_test.dart
flutter run --flavor flav_dev -t lib/main_flav_dev.dart
Prod: 
flutter run --release --flavor flav_prod -t lib/main_flav_prod.dart

## Known Bugs
1. Execution failed for task ':app:lintVitalFlav_prodRelease' (Flutter 2.10.3): https://github.com/flutter/flutter/issues/58247
   - Potential Fix: Upgrade Flutter
     - Does not work on 
   - Temp Fixes:
     - Option 1:
       - If you don't want to mess with your CI/CD configs then just upgrade your Gradle version:

        User Android Gradle 7.0.0-alpha14 in your android/build.gradle:
        ```
        dependencies {
            classpath 'com.android.tools.build:gradle:7.0.0-alpha14'
        }
        ```
        And upgrade your Gradle version to 7.0-rc-1 in android/gradle/wrapper/gradle-wrapper.properties:
        `distributionUrl=https\://services.gradle.org/distributions/gradle-7.0-rc-1-all.zip`

     - Option 2: 
       - I wouldn't consider this a solution, but I've found a workaround. I was having the same issue and tried building --debug and then --release and it still didn't work. However, if you look at the path in your specific error, it should either end with debug/libs.jar or profile/libs.jar. This indicates which apk you need to build first. In OP's case it is debug/libs.jar so building --debug first and then --release worked. In my case, it was profile/libs.jar so building --profile and then --release worked. I'm pretty sure building the --release shouldn't have to access the debug or profile directories though.

      TL;DR
      If your error says debug/libs.jar, build --debug then --release.
      If your error says profile/libs.jar, build --profile then --release.
