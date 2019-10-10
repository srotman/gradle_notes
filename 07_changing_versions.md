# Changing modules (or Snapshots)
By default, Gradle caches dynamic versions and changing modules for 24h[[1](https://docs.gradle.org/current/userguide/troubleshooting_dependency_resolution.html#sub:dynamic_versions_and_changing_modules)]

This can be changed by:
* Command line flag `--refresh-depencies` (Force fresh resolve and ignore dependency cache)
* Always use dependency cache (and avoid network access) using the `--offline` flag
* Set `resolutionStrategy`:
```
configurations.all {
    // for dynamic version cache
    resolutionStrategy.cacheDynamicVersionsFor 4, 'hours'

    // for changing modules
    resolutionStrategy.cacheChangingModulesFor 10, 'minutes'
```


# Ensuring versions
* Consider [Dependency Locking](https://docs.gradle.org/current/userguide/dependency_locking.html#dependency_locking)
* Especially when using [Dynamic Versioning](https://docs.gradle.org/current/userguide/declaring_dependencies.html#sub:declaring_dependency_with_dynamic_version)


# Publishing snapshots to snapshot repo:
```groovy
publishing {
    repositories {
        maven {
            def releasesRepoUrl = "$buildDir/repos/releases"
            def snapshotsRepoUrl = "$buildDir/repos/snapshots"
            url = version.endsWith('SNAPSHOT') ? snapshotsRepoUrl : releasesRepoUrl
        }
    }
}
```
https://docs.gradle.org/current/userguide/publishing_maven.html#publishing_maven:snapshot_and_release_repositories
