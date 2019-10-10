## Composite vs Multi-Project

For projects that have a tightly-coupled dependency between them and/or always released together, use multi-project builds.

For projects that have independent release cycles, and a 'loose' dependency - for instance a library on which an application depends, composite builds can be used (caveats apply -- see below).

Alternatively, it could be considered to decouple the two projects altogether...

## Composite Builds
Doku: https://docs.gradle.org/current/userguide/composite_builds.html

Related to [dependency substitution](https://docs.gradle.org/current/userguide/customizing_dependency_resolution_behavior.html#sec:dependency_substitution_rules).

* dependency on an 'external' artifact (not on a project)
* the artifact's build can be included command-line `gradle --include-build '<path>' build`
* or in `settings.gradle` using `includeBuild '<path>'`

### [Current Limitations](https://docs.gradle.org/current/userguide/composite_builds.html#included_build_substitution_limitations)
In following cases build substitutions won't work (meaning project can't/shouldn't be used as a composite):
* publication of configuration, other than `default`
* Using `maven-publish` or `ivy-publish` plugins
* `POM` or `ivy.xml` tweakage as part of publication


## Multi-Project builds
Doku: https://docs.gradle.org/current/userguide/multi_project_builds.html
* in `settings.gradle` using `include '<childpath>'`

Project tree:
```
$ gradle -q projects
```
### Decoupling
* Any other interaction, other than project or task dependencies leads to coupling. [[1](https://docs.gradle.org/current/userguide/multi_project_builds.html#sec:decoupled_projects)]

Recomendations:
* Avoid a subproject’s build script referencing other subprojects; preferring cross configuration from the root project.
* Avoid changing the configuration of other projects at execution time.
