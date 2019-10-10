# Shared dependencies

## Centralized version declarations:
* Use `constraints`

~~~groovy
dependencies {
  constraints {
    implementation "org.slf4j:slf4j-api:1.7.28"
    implementation "org.slf4j:log4j-over-slf4j:1.7.28"
  }
}

dependencies {
  implementation 'org.slf4j:log4j-over-slf4j'
}
~~~

* Consider centralizing versions as well:

~~~groovy
ext.versions = [
    slf4j: '1.7.28'
]

dependencies {
    implementation 'org.slf4j:slf4j-api'
}

dependencies {
    constraints {
        implementation "org.slf4j:slf4j-api:${versions.slf4j}"
    }
}
~~~

* Or even centralizing library definitions:

~~~groovy
ext.versions = [
    slf4j: '1.7.28'
]

ext.libraries = [
    slf4j: 'org.slf4j:slf4j-api'
]

dependencies {
    implementation libraries.slf4j
}

dependencies {
    constraints {
        implementation "${libraries.slf4j}:${versions.slf4j}"
    }
}
~~~

*libraries and versions could also be defined in separate files and 'applied'*

## Centralized Plugin versions
Use new `pluginManagement` block in `settings` script (See [plugin version management](https://docs.gradle.org/5.6/userguide/plugins.html#sec:plugin_version_management))
~~~groovy
pluginManagement {
  plugins {
        id 'org.gradle.sample.hello' version "${helloPluginVersion}"
    }
}
~~~
~~~groovy
plugins {
    id 'org.gradle.sample.hello'
}
~~~

Plugin versions can be loaded from `gradle.properties` 

## Platform projects (like BOM)
https://docs.gradle.org/current/userguide/java_platform_plugin.html
* Uses `constraints`

* Consume with `platform` or `enforcedPlatform`

~~~groovy
plugins {
  id 'java-platform'
  id 'maven-publish'
}

dependencies {
  constraints {
    api 'com.foo:foo-api:1.0'
    runtime 'com.foo:foo-server:1.0'
  }
}

publishing {
  publications {
    myPlatform(MavenPublication) {
      from components.javaPlatform
    }
  }
}
~~~

~~~
plugins {
  id 'java'
}

dependencies {
  //api platform(project(':platform'))
  api platform("com.foo:foo-dependencies:1.0") // provide version recommendations
  api enforcedPlatform("com.foo:foo-dependencies:1.0") //enforcedPlatform wins for version conflicts
  api 'com.foo:foo-api'
}
~~~

## Consider Plugins for sharing configuration
https://docs.gradle.org/current/userguide/custom_plugins.html
