# Java

The purpose of this style guide is to provide some conventions for working on Java code within GDS. The old [Sun/Oracle Java style guide](https://www.oracle.com/technetwork/java/index-135089.html), the more recent [Google Java style guide](https://google.github.io/styleguide/javaguide.html) and the more far-reaching _[Java for Small Teams](https://ncrcoe.gitbooks.io/java-for-small-teams/)_ book are useful starting points.

Generally [IntelliJ IDEA](https://www.jetbrains.com/idea/) is used within GDS and consistency of its use helps when pairing and mob programming.

We favour consistency across our code, so when considering using a new or different method or paradigm to what exists already, ensure that you have agreement of your team.

### Code formatting

Variable and field names should match the class they are instantiating, or have a descriptive name in the context of their use.

Always use curly braces around the body of an `if` statement, even if it’s only a single line.

Use the [GDS Way EditorConfig file](editorconfig), which has settings for things like code indentation. Place a copy of this file named `.editorconfig` in the root of your project to have IntelliJ IDEA and some other editors automatically apply the settings. If your editor does not support EditorConfig, manually configure its settings to match.

### Dependency injection (DI)

Consider whether dependency injection is appropriate for your project before using it. Some programmes use the [Guice](https://github.com/google/guice) dependency injection framework.

### Imports

No wildcard imports should be used.  IntelliJ can be configured to explicitly import all classes and static methods in Preferences → Editor → Code Style → Java → Imports with “Class count to use import with *” and “Names count to use static import with *” both set to a very high number e.g. 1000.

The IntelliJ “Optimize Imports” command sorts imports and removes any that are unused. Before committing some changes, you can select all the classes in the modified files pane and then use this command to fix the imports for just the classes you modified.

### Prefer functionality in the Java standard library

Where possible, use functionality from the Java standard library rather than external libraries.

Be mindful that improvements to the Java standard library mean that some external libraries that were popular in the past now add less value. For example, while Joda-Time was significantly better than the date and time libraries built in to older Java versions, the `java.time` package introduced in Java 8 renders it redundant. Similarly, [Google’s Guava](https://github.com/google/guava) is very useful (and recommended) but the unmodifiable collections built in to Java 9 largely obviate the need for Guava’s immutable collections.

When using external libraries, favour those that play nicely with the Java standard library. For example, be wary of any library that introduces a new type that replicates the functionality of an existing type in the Java standard library without implementing the same interfaces (e.g. a list type that does not implement `java.util.List`).

### Testing

Use JUnit for unit tests (it can also be used for many integration tests). For new projects, use the latest [JUnit 5](https://junit.org/junit5/). It’s probably not worth migrating existing projects from [JUnit 4](https://junit.org/junit4/) to JUnit 5 while JUnit 4 is still supported.

Use [Mockito](https://site.mockito.org/) for mocking. 

### Code checking

The use of static analysis is encouraged. Static analysis tools for Java include [SonarQube](https://www.sonarqube.org/), [Codacy](https://www.codacy.com/), [FindBugs](http://findbugs.sourceforge.net/) and [CheckStyle](http://checkstyle.sourceforge.net/). However, be aware that such tools can detect an overwhelming number of problems if applied to an existing project, which tends to result in their checks being ignored.

Try to minimise compiler warnings. If you cannot remove a warning, use an appropriate annotation to suppress it, preferably with a comment explaining why. For example:

```java
public void frobulateFoos() {
    LOGGER.info("Frobulating foos");

    // LibFoo returns a raw list but every element is always a Foo
    @SuppressWarnings("unchecked")
    List<Foo> foos = (List<Foo>) fooService.getFoos();

    foos.forEach(foo -> foo.frobulate());
}
```

### Build tools

Either Gradle or Maven should be used as the build tool.

### Web frameworks

We use [Dropwizard](https://www.dropwizard.io/) as our web framework of choice.

Dropwizard has built-in support for validating requests with Hibernate Validator. Use [Dropwizard’s validation](https://www.dropwizard.io/1.3.9/docs/manual/validation.html) in preference to rolling your own except in cases where Dropwizard’s built-in functionality cannot meet your validation requirements.

If you are sending logs to a service that requires them in a specific format, you may find our [dropwizard-logstash](https://github.com/alphagov/dropwizard-logstash) logging extension useful.

### JDK

The [Oracle JDK](https://www.oracle.com/technetwork/java/javase/downloads/index.html) is no longer free for production use. OpenJDK remains free to use (under the GPLv2 with the Classpath Exception) but Oracle only provide general-availability [OpenJDK builds](http://jdk.java.net/) for the latest release.

The [AdoptOpenJDK](https://adoptopenjdk.net/) project (backed by big names including IBM and Microsoft) provides fully open-source pre-built OpenJDK binaries. For LTS releases (such as Java 8 and Java 11), AdoptOpenJDK have committed to releasing free updates for several years.

In addition, AdoptOpenJDK has niceties such as being available in package repositories, having friendly installers for desktop use, and offering ready-made [Docker images containing OpenJDK](https://hub.docker.com/u/adoptopenjdk).
