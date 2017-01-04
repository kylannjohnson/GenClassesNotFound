# GenClassesNotFound

This repo is created to show a bug in the `kapt` plugin for Kotlin 1.0.6.  Previously in `1.0.5-3`, @Modules created in the test package would result in Inject Adapters and Module Adapters in the `build/generated/source/kapt/debugUnitTest/` directory.  In `1.0.6`, that no longer happens.

## To reproduce

Run `./gradlew clean assemble test`

  That results in : 

  ```
  java.lang.IllegalStateException: Module adapter for class com.example.genclassesnotfound.ExampleUnitTest$TestModule could not be loaded. Please ensure that code generation was run for this module.
      at dagger.internal.FailoverLoader$1.create(FailoverLoader.java:45)
      at dagger.internal.FailoverLoader$1.create(FailoverLoader.java:40)
      at dagger.internal.Memoizer.get(Memoizer.java:58)
      ...    
  ```

Simply revert kotlin to `1.0.5-3` to make the test pass

  - Change `ext.kotlin_version` in `build.gradle` from `1.0.6` -> `1.0.5-3`
