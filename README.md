# mary

This is a custom maven repository created for convenience and developing speed 
- #### Maven Central

Maven Central is, unfortunately, a pain to setup and Nexus is too slow, up to 20s for a simple platform
and 10m for a proper project, with several projects and up to tens pushes a day, all these overheads eat too much 
precious developing time, which, in my case, is quite scarce.

- #### Jitpack

On the other side, Jitpack is, unfortunately, broken by design:
- they rewrite the POM, which sometimes it creates [defective artifacts](https://github.com/jitpack/jitpack.io/issues/4476)
- if you have a multi-module build the produce a non-sense catch-all artifact and provide wrong instructions
- you cannot easily use the coordinates you use for normal publishing
- when first requesting a version, it first has to be built, this can need significant time and lead to timeouts, 
  if you just re-request the resolution might suddenly work as the build finished, but build tools also tend to cache 
  resolution results so might not immediately retry
- when a build fails, you only get "dependency not found" and have to dig deep for the reason if you even consider looking for it
- it partly uses Git revisions as versions which results in broken odering, so any sane conflict resolution that uses the newer version if two different version are found in the transitive dependencies cannot work properly as the ordering of versions is wrong
- it cannot be indexed by IDEs or similar to provide a selection of what dependencies and versions are available
- it cannot be properly indexed by things like mvnrepository.com 
  
Ps: the last two should be also valid for this repository solution, though

However, it's still perfectly fine using jitpack on consumer sides, in this case just:

- Add it in your root build.gradle at the end of repositories:

      allprojects {
          repositories {
              ...
              maven("https://jitpack.io") // should be the last entry
          }
      }

- Add the dependency

      dependencies {
          implementation("kotlin.graphics:unsigned:..")
          implementation("kotlin.graphics:glm:..")
      }

### Plugins

In order to use kotlin-graphics plugins, in Gradle KTS you need to include this repo by adding the following to your `settings.gradle.kts`:

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

### Releases

Releases, which are less frequent, would be instead published on [scijava](https://maven.scijava.org/) (there is none yet).
