[//]: # (title: Android dependencies)

The workflow for adding Android-specific dependencies to a KMM module is the same as it is for pure Android projects: add a line to your Gradle build script declaring the dependency you need and import the project. You’ll then be able to use this dependency in your Kotlin code.

We recommend adding Android dependencies to KMM projects by adding them to a specific Android source set:

<tabs group="build-script">
<tab title="Kotlin" group-key="kotlin">

```kotlin
sourceSets["androidMain"].dependencies {
        implementation("com.example.android:app-magic:12.3")
}
```

</tab>
<tab title="Groovy" group-key="groovy">

```groovy
sourceSets {
    androidMain {
        dependencies {
            implementation 'com.example.android:app-magic:12.3'
        }
    }
}
```

</tab>
</tabs>

Moving what was a top-level dependency in an Android project to a specific source set in a KMM project might be difficult if the top-level dependency had a non-trivial configuration name. For example, to move а `debugImplementation` dependency from the top level of an Android project, you’ll need to add an implementation dependency to the source set named `androidDebug`.
To minimize the effort you have to put in to deal with migration problems like this, you can add a `dependencies` block inside the `android` block:

<tabs group="build-script">
<tab title="Kotlin" group-key="kotlin">

```kotlin
android {
    ...

    dependencies {   
        implementation("com.example.android:app-magic:12.3")
    }
}
```

</tab>
<tab title="Groovy" group-key="groovy">

```groovy
android {
    ...

    dependencies {
        implementation 'com.example.android:app-magic:12.3'
    }
}
```

</tab>
</tabs>

Dependencies declared here will be treated exactly the same as dependencies from the top-level block, but declaring them this way will also separate Android dependencies visually in your build script and make it less confusing.

Putting dependencies into a standalone `dependencies` block at the end of the script, in a way that is idiomatic to Android projects, is also supported. However, we strongly recommend **against** doing this because configuring a build script with Android dependencies in the top-level block and other target dependencies in each source set is likely to cause confusion.

Learn more about [adding dependencies in Android documentation](https://developer.android.com/studio/build/dependencies).
