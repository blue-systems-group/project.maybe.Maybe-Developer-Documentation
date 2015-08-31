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

I have a toy implementation repo for this purpose:
https://github.com/xcv58/gradle-practice-maybe

Perhaps a better way is fork Java/Android plugin and create a new one?

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

I'm not sure could we replace all 5 tasks with custom `JavaExec` type tasks,
without any compatible issue.

Perhaps we have to dig into the implementation of Android Plugin.

Learn how to build it: http://tools.android.com/build/gradleplugin

BTW: You need Java 1.6

# Android Studio Support
The IDE can't recognize maybe syntax, so it'll show errors for codes with maybe syntax.

We need a plugin that let IDE recognize maybe syntax and suppress related errors.

More information can be found from [Plugin Development Guidelines](https://www.jetbrains.com/idea/help/plugin-development-guidelines.html)
