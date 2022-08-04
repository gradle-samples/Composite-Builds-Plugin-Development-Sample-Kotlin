## Composite build to develop a Gradle plugin Kotlin

NOTE: You can open this sample inside an IDE using the [IntelliJ native importer](https://www.jetbrains.com/help/idea/gradle.html#gradle_import_project_start) or [Eclipse Buildship](https://projects.eclipse.org/projects/tools.buildship).

This sample demonstrates a composite build used to develop a Gradle plugin in conjunction with a consuming build.

The plugin could be in the same repository (only used by this build) or it could be in a different repository (used by many other builds).

This removes the need for the special `buildSrc` project and makes prototyping plugins even easier.

## Buildscript dependencies are substituted

In a composite build, dependencies declared in the `plugins { }` block or in the `buildscript` `classpath` configuration are substituted in the same way as other dependencies. In this sample, the build declares that plugin 'org.sample.greeting', and this dependency is substituted by the `greeting-plugin` included build.

Without ever publishing the `greeting-plugin` project to a repository, it is possible to build the project with the locally developed 'org.sample.greeting' plugin.

```
> gradle --include-build ../greeting-plugin greeting
[composite-build] Configuring build: /home/user/gradle/sample/compositeBuilds/plugin-dev/greeting-plugin
:greeting-plugin:compileJava
:greeting-plugin:pluginDescriptors
:greeting-plugin:processResources
:greeting-plugin:classes
:greeting-plugin:jar
:my-greeting-app:greeting
Hi Bob!!!
```

## Plugin changes can be tested

This sample can be used to demonstrate the development lifecycle of a Gradle plugin. Edit the file `greeting-plugin/src/main/java/org/sample/GreetingTask.java` to change the greeting, and re-execute the consumer build:

```
> gradle --include-build ../greeting-plugin greeting
[composite-build] Configuring build: /home/user/gradle/sample/compositeBuilds/plugin-dev/greeting-plugin
:greeting-plugin:compileJava
:greeting-plugin:pluginDescriptors
:greeting-plugin:processResources
:greeting-plugin:classes
:greeting-plugin:jar
:my-greeting-app:greeting
G'day Bob!!!
```

