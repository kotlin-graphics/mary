# mary

This is a custom maven repository created for convenience and developing speed 

### Plugins

For kotlin-graphics plugins, add the following to your `settings.gradle.kts`:

```kotlin
pluginManagement {
    repositories {
        gradlePluginPortal()
        maven("https://raw.githubusercontent.com/kotlin-graphics/mary/master")
    }
}
```

### Snapshots

Same for the snapshots of the different projects, they are also published on this repository. 
So if you want to use it, just add to your `build.gradle.kts`

```kotlin
repositories {
    maven("https://raw.githubusercontent.com/kotlin-graphics/mary/master")
}
```
