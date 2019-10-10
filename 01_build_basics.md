* Tasks are guaranteed to be executed in the order of their dependencies
* Task are guaranteed to execute only once
* Tasks form a directed Acyclic Graph
  * Build scripts => build *configuration* scripts

## Build Lifecycle / Build phases
Doku: [Build Lifecycle](https://docs.gradle.org/current/userguide/build_lifecycle.html)

## Build phases

### 1. Initialization
determines *which* projects are part of the build, and creates `Project` instance for each.
* `settings.gradle`

### 2. Configuration
configures `Project` objects. Executes **all** project `build scripts`.
All Tasks to execute are created and configured, but *not yet executed*.
Creates the 'task graph'

### 3. Execution
Task execution. `doFirst` closures are executed before `doLast` closures


## Build environment
Doku: [Build Environment](https://docs.gradle.org/current/userguide/build_environment.html)

### `settings.gradle`
* Read during initialization phase
* Contains `rootProject.name`
* Contains project definitions for multi-project or composite builds (`include`, `includeBuild`)

### `gradle.properties`
Can be  in project root, `GRADLE_USER_HOME`, or gradle installation directory
* Properties that control the build environment, e.g.
  * `org.gradle.caching=(true|false)` -> En/Disable Build Cache
  * `org.gradle.daemon=(true|false)` -> En/Disable Daemon
  * `org.gradle.parallel=(true|false)` -> En/Disable parallel project execution for decoupled projects
    * Note: Using `allprojects` and `subprojects` *will* couple all projects
  * `org.gradle.workers.max=N` -> Max workers for parallel compilation (native)
* Project Properties (e.g. `version`, `sourceCompatibility`, `targetCompatibility`)
  * can also be in the build file of the root project directly.
* System Properties (e.g. `systemProp.http.proxyHost`)
* Gradle properties precedence:
  1. System properties (-Dgradle.user.home, ...)
  1. `gradle.properties` in GRADLE_USER_HOME
  1. `gradle.properties` in project root
  1. `gradle.properties` in Gradle installation directory

Build Environment Order of precedence:
1. Command-line flags
1. System Properties
1. Gradle Properties
1. Environment variables (`GRADLE_OPTS`, `GRADLE_USER_HOME`, `JAVA_HOME`)
