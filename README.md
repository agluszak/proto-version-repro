`bazel build //...` will fail with

```
ERROR: /home/andrzej.gluszak/code/junk/bazel_version/java/com/basicapp/BUILD:8:16: Parsing Android Resources in java/com/basicapp/basic_lib_symbols/assets.bin failed: (Exit 1): java failed: error executing ParseAndroidResources command (from android_library rule target //java/com/basicapp:basic_lib) external/rules_java++toolchains+remotejdk17_linux/bin/java -Xms3G -Xmx3G -XX:+ExitOnOutOfMemoryError -jar ... (remaining 8 arguments skipped)

Use --sandbox_debug to see verbose messages from the sandbox and retain the sandbox build root for debugging
Exception in thread "main" java.lang.ExceptionInInitializerError
        at com.google.devtools.build.android.AndroidDataSerializer.flushTo(AndroidDataSerializer.java:71)
        at com.google.devtools.build.android.AndroidResourceParsingAction.main(AndroidResourceParsingAction.java:80)
        at com.google.devtools.build.android.ResourceProcessorBusyBox$Tool$2.call(ResourceProcessorBusyBox.java:74)
        at com.google.devtools.build.android.ResourceProcessorBusyBox.processRequest(ResourceProcessorBusyBox.java:238)
        at com.google.devtools.build.android.ResourceProcessorBusyBox.main(ResourceProcessorBusyBox.java:175)
Caused by: com.google.protobuf.RuntimeVersion$ProtobufRuntimeVersionException: Detected incompatible Protobuf Gencode/Runtime versions when loading Header: gencode 4.33.4, runtime 4.33.1. Runtime version cannot be older than the linked gencode version.
        at com.google.protobuf.RuntimeVersion.validateProtobufGencodeVersionImpl(RuntimeVersion.java:153)
        at com.google.protobuf.RuntimeVersion.validateProtobufGencodeVersion(RuntimeVersion.java:72)
        at com.google.devtools.build.android.proto.SerializeFormat$Header.<clinit>(SerializeFormat.java:87)
        ... 5 more
Target //java/com/basicapp:basic_lib failed to build
Use --verbose_failures to see the command lines of failed build steps.
INFO: Elapsed time: 169.595s, Critical Path: 54.10s
INFO: 1230 processes: 315 internal, 898 linux-sandbox, 17 worker.
ERROR: Build did NOT complete successfully
```

(no matter if you use precompiled protoc or not).
Bumping bazel version to 9.0.0rc5 has the same effect as adding probuf bazel_dep version 33.4 on earlier bazels

