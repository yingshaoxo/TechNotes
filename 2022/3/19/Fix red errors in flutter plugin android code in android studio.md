# Fix red errors in flutter plugin android code in android studio

## Problem
You see errors in:

```kotlin
import io.flutter.embedding.engine.plugins.FlutterPlugin
import io.flutter.embedding.engine.plugins.activity.ActivityAware
import io.flutter.embedding.engine.plugins.activity.ActivityPluginBinding
import io.flutter.plugin.common.MethodCall
import io.flutter.plugin.common.MethodChannel
import io.flutter.plugin.common.MethodChannel.MethodCallHandler
import io.flutter.plugin.common.MethodChannel.Result
```

The `io` is red. How do you do?

## Solution
You add the following to the `build.gradle`:

```bash
dependencies {
    compileOnly files("/opt/homebrew/Caskroom/flutter/2.8.1/flutter/bin/cache/artifacts/engine/android-arm/flutter.jar")

    compileOnly 'androidx.annotation:annotation:1.1.0'
}
```

