## Prerequisites

Java 8 or up

## First Install

* Using IDE integration

* Using Gradle Wrapper of different project  
`$ <path-to-other-project>/gradlew wrapper --gradle-version 5.6.2`

* Using [SDKMAN!](https://sdkman.io/)  
`$ sdk install gradle`

* See [Installation](https://gradle.org/install/)

## The Gradle Wrapper
Doku: [The Gradle Wrapper](https://docs.gradle.org/current/userguide/gradle_wrapper.html)

Get wrapper for `all` distribution:
`$ ./gradlew wrapper --gradle-version 5.6.2 --distribution-type all`

### Generate/Update gradle wrapper for Gradle version
```
$ gradle wrapper --gradle-version 5.6.2
```

## Usefull
* set alias `gradle='./gradlew'`

## Doku
* Official Doku: https://docs.gradle.org/current/userguide/userguide.html
* Tutorials and Guides: https://gradle.org/guides/ (Some are outdated!)
* 'old' Gradle Training : https://github.com/srotman/gradle-training (Heavily Outdated!)
