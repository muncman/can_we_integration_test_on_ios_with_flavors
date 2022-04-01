# can_we_integration_test_on_ios_with_flavors

`WidgetTester`-based integration tests (non-Driver) will only run against Android currently; not iOS. This issue has been around for multiple Flutter versions.

<details>
<summary>flutter doctor</summary>
<br>

```
Doctor summary (to see all details, run flutter doctor -v):

[✓] Flutter (Channel unknown, 2.10.3, on macOS 12.3.1 21E258 darwin-arm, locale en-US)
[✓] Android toolchain - develop for Android devices (Android SDK version 31.0.0)
[✓] Xcode - develop for iOS and macOS (Xcode 13.3)
[✓] Chrome - develop for the web
[✓] Android Studio (version 2021.1)
[✓] Android Studio (version 2021.1)
[✓] IntelliJ IDEA Ultimate Edition (version 2021.3.3)
[✓] IntelliJ IDEA Ultimate Edition (version 2021.3.2)
[✓] VS Code (version 1.66.0)
[✓] Connected device (3 available)
[✓] HTTP Host Availability

• No issues found!
```

</details>

The issue is **definitely when flavors are in the mix**. And maybe my issue is an _incomplete_ flavor configuration, but I created a second, [bare-bones app to isolate/reproduce against](https://github.com/muncman/can_we_integration_test_on_ios_with_flavors).

If something else needs to be tweaked in terms of flavors, that would be great news -- I'd be happy to be wrong with my config! 😅 As it stands, though, when using iOS the app launches on a simulator, but the test eventually just times out. The test isn't even app-related, yet it never gets executed.

_Maybe this demo app can be the additional info to re-open this issue?_

<details>
<summary>The output of running the app above</summary>
<br>

```
$flutter test --flavor flavor2 integration_test/

Running "flutter pub get" in can_we_integration_test_on_ios_with_flavors...      2,543ms
00:05 +0: loading /Users/muncman/work/can_we_integration_test_on_ios_with_flavors/integration_test/app_test.dart                                                                 R00:06 +0: loading /Users/muncman/work/can_we_integration_test_on_ios_with_flavors/integration_test/app_test.dart                                                          1,178ms
00:24 +0: loading /Users/muncman/work/can_we_integration_test_on_ios_with_flavors/integration_test/app_test.dart
00:43 +0: loading /Users/muncman/work/can_we_integration_test_on_ios_with_flavors/integration_test/app_test.dart                                                            19.2s
Xcode build done.                                           36.5s
12:00 +0 -1: loading /Users/muncman/work/can_we_integration_test_on_ios_with_flavors/integration_test/app_test.dart [E]
  TimeoutException after 0:12:00.000000: Test timed out after 12 minutes.
  package:test_api/src/backend/invoker.dart 333:28  Invoker._handleError.<fn>
  dart:async/zone.dart 1418:47                      _rootRun
  dart:async/zone.dart 1328:19                      _CustomZone.run
  package:test_api/src/backend/invoker.dart 331:10  Invoker._handleError
  package:test_api/src/backend/invoker.dart 287:9   Invoker.heartbeat.<fn>.<fn>
  dart:async/zone.dart 1426:13                      _rootRun
  dart:async/zone.dart 1328:19                      _CustomZone.run
  package:test_api/src/backend/invoker.dart 286:38  Invoker.heartbeat.<fn>
  dart:async-patch/timer_patch.dart 18:15           Timer._createTimer.<fn>
  dart:isolate-patch/timer_impl.dart 395:19         _Timer._runTimers
  dart:isolate-patch/timer_impl.dart 426:5          _Timer._handleMessage
  dart:isolate-patch/isolate_patch.dart 192:12      _RawReceivePortImpl._handleMessage

12:00 +0 -1: Some tests failed.
```

</details>
