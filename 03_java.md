# Java
* Doku: [Java Plugin](https://docs.gradle.org/current/userguide/java_plugin.html)


* Doku: [Building Java & JVM Projects](https://docs.gradle.org/current/userguide/building_java_projects.html)
* Doku: [Testing in Java & JVM Projects](https://docs.gradle.org/current/userguide/java_testing.html)


## Java Library
* [Java Library Guide](https://guides.gradle.org/building-java-libraries)
* [Java Library Plugin](https://docs.gradle.org/5.0/userguide/java_library_plugin.html)

'Main Configurations:
* `api`  exposed to consumers (transitive)
* `implementation`  not exposed to consumers (non-transitive)

--> prefer `implementation` over `api`  
--> [All Configurations](https://docs.gradle.org/5.0/userguide/java_library_plugin.html#sec:java_library_configurations_graph)

## Spring Boot
https://guides.gradle.org/building-spring-boot-2-projects-with-gradle

```
plugins {
    id 'java'
    id 'com.gradle.build-scan' version '2.0.2'
    id 'org.springframework.boot' version '2.0.5.RELEASE'
    id 'io.spring.dependency-management' version '1.0.7.RELEASE'
}


```
