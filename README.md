# Sample app to expose a bug on OneSignal Flutter SDK

This happens after adding the google servics plugin inside of the android app, which expose some dependency resolution issue with google services.

To silence the issue you can this on `app/gradle.build`:

```grooby
googleServices { disableVersionCheck = true }
```


# Stacktrace building on android
```
Launching lib/main.dart on Android SDK built for x86 in debug mode...
Running Gradle task 'assembleDebug'...

FAILURE: Build failed with an exception.

* What went wrong:
Could not determine the dependencies of task ':app:compileDebugJavaWithJavac'.
> In project 'app' a resolved Google Play services library dependency depends on another at an exact version (e.g. "[10.2.
  1, 16.0.99]", but isn't being resolved to that version. Behavior exhibited by the library will be unknown.

  Dependency failing: com.onesignal:OneSignal:3.15.1 -> com.google.android.gms:play-services-location@[10.2.1, 16.0.99], b
  ut play-services-location version was 16.0.0.

  The following dependencies are project dependencies that are direct or have transitive dependencies that lead to the art
  ifact with the issue.
  -- Project 'app' depends onto com.google.android.gms:play-services-location@{strictly 16.0.0}
  -- Project 'app' depends onto com.onesignal:OneSignal@{strictly 3.15.1}
  -- Project 'app' depends on project 'onesignal_flutter' which depends onto com.onesignal:OneSignal@3.15.1

  For extended debugging info execute Gradle from the command line with ./gradlew --info :app:assembleDebug to see the dep
  endency paths to the artifact. This error message came from the google-services Gradle plugin, report issues at https://
  github.com/google/play-services-plugins and disable by adding "googleServices { disableVersionCheck = false }" to your b
  uild.gradle file.

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 5s
Exception: Gradle task assembleDebug failed with exit code 1

```