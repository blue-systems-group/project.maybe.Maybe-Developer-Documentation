# Polyglot

[Polyglot](http://www.cs.cornell.edu/projects/polyglot/) is
a highly extensible compiler front end for the Java programming language.

The maybe fork of polyglot is: https://github.com/blue-systems-group/project.maybe.polyglot

It can rewrite maybe syntax, but there're some features need to implement and bugs need to fix.
For example:
1. it's now based on Java 1.4, but the Android support Java 1.7,
so we need provide Java 1.7 support.
2. We need generate metadata for package.
3. Directly declare maybe variable can't compile

If you find any bugs or have any idea,
please check [the issues page](https://github.com/blue-systems-group/project.maybe.polyglot/issues).

# Gradle
The second step is Gradle integration. You can find more information from [Gradle User Guide](https://docs.gradle.org/current/userguide/userguide.html) if you are not familiar with Gradle.

The main idea is to **replace all `JavaCompile` tasks to our custom `JavaExec` tasks**.
Because polyglot extension need to run start with `java` not `javac`.
But for some reason, the output `class` files of Maybe compiler can't converted to `dex` file.
So we insert a `java-to-java` task before every `JavaCompile` task.

# Android Plugin for Gradle
You can find:
1. general introduction from https://developer.android.com/tools/building/plugin-for-gradle.html
2. full Gradle Plugin User Guide from http://tools.android.com/tech-docs/new-build-system/user-guide

In my experiment, there're 5 tasks is `JavaCompile` type:
1. `compileDebugAndroidTestJavaWithJavac`
2. `compileDebugJavaWithJavac`
3. `compileDebugUnitTestJavaWithJavac`
4. `compileReleaseJavaWithJavac`
5. `compileReleaseUnitTestJavaWithJavac`

~~~I'm not sure could we replace all 5 tasks with custom `JavaExec` type tasks, without any compatible issue.~~~

~~~Perhaps we have to dig into the implementation of Android Plugin.~~~

~~~Learn how to build it: http://tools.android.com/build/gradleplugin~~~

~~~BTW: You need Java 1.6~~~

Currently, the [build.gralde](https://github.com/blue-systems-group/project.maybe.android.library/blob/master/demo/build.gradle) already support to build Android Application.
In short, it insert a task for every `JavaCompile` task to translate maybe syntax to ordinary Java source code.

If we don't have time to publish all our `jar/aar` files to [Maven Central Repository](http://central.sonatype.org/). We can use the [gradle download task](https://github.com/michel-kraemer/gradle-download-task) to download files from our server. But we need first **finish gradle plugin**!

Current implementation: https://github.com/blue-systems-group/project.maybe.maybe-gradle-plugin

It has been published to gradle portal: https://plugins.gradle.org/plugin/edu.buffalo.cse.maybe

# Android Studio Support
The IDE can't recognize maybe syntax, so it'll show errors for codes with maybe syntax.

We need a plugin that let IDE recognize maybe syntax and suppress related errors.

More information can be found from [Plugin Development Guidelines](https://www.jetbrains.com/idea/help/plugin-development-guidelines.html)
