## Dependency Management

## Transitive dependencies
* Use `constraints` for version hints
~~~groovy
dependencies {
    constraints {
        implementation('org.foo:foo-api:1.1') {
            because '1.0 was broken' // provide a hint WHY we set this constraint
        }
    }
}
~~~

* Exclude transitive dependencies  
for a specific dependency
~~~groovy
dependencies {
    constraints {
        implementation('org.foo:foo-api:1.1') {
            exclude group: 'com.foo', module: 'panda'
        }
    }
}
~~~
or for a whole configuration
~~~groovy
dependencies {
    implementation {
        exclude group: 'com.foo', module: 'chicken'
    }
}
~~~

* Force a specific version,  
either by dependency declaration
~~~groovy
dependencies {
    implementation('com.foo:panda:1.0') {
      force = true
    }
}
~~~
or by `resolutionStrategy` for a configuration
~~~groovy
dependencies {
    implementation {
      resolutionStrategy.force 'com.foo:panda:1.0'
    }
}
~~~

* Disable transitive dependencies  
for a dependency
~~~groovy
dependencies {
    implementation('com.foo:panda:1.0') {
    transitive = false
    }
}
~~~
or globally  

~~~groovy
configurations.all {
    transitive = false
}

dependencies {
    implementation 'com.foo:panda:1.0'
}
~~~

## Other Conflict Resolution strategies

### Troubleshooting
https://docs.gradle.org/current/userguide/troubleshooting_dependency_resolution.html

### Resolution strategy (Dependency Resolve)
Useful for version conflicts
https://docs.gradle.org/current/userguide/customizing_dependency_resolution_behavior.html#sec:releasable_unit

### Dependency substitution
E.g. for switching out artifacts and projects
https://docs.gradle.org/current/userguide/customizing_dependency_resolution_behavior.html#sec:dependency_substitution_rules

### Component selection
Useful for blacklisting, especially in combination with dynamic versioning
https://docs.gradle.org/current/userguide/customizing_dependency_resolution_behavior.html#sec:component_selection_rules


### Module replacement
e.g. for library renames or forks
https://docs.gradle.org/current/userguide/customizing_dependency_resolution_behavior.html#sec:module_replacement
