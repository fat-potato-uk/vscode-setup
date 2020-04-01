# Vs Code Setup

These tutorials have been written with a focus on IntelliJ. If you however feel more "at home" with VS Code, this
brief guide may serve as an initial how to.

First, you must download [VS Code](https://code.visualstudio.com/). Depending on your platform, the format may differ.
If you are using a Mac (congratulations, you are a better person), the application will come in the form of a simple
binary in a zip file. Extract/install this to wherever you see fit.

Next, you will need to install some extensions. This can be accessed via the left hand menu or by using the ⇧⌘X shortcut
on MacOS:

![Extensions](extensions.png?raw=true "Extensions")

This is a list of the extensions I have installed. If you search for `Java` you should find all of these near the top
of the list. Not all are essential, but they should help significantly in setting up your environment.

Next, we need to download and install [Maven](https://maven.apache.org/download.cgi). Unlike IntelliJ, VS Code is not
bundled with any tooling, so download this and unzip it to a known location.

To finish setting up VS Code, go to the settings menu and search for `java.home`:

![Settings](settings.png?raw=true "Settings")

This will give you the option to configure the property via editing the `settings.json`. Click this and add the following
properties within the main code block:

```json
{
...
    "java.home": "/Users/<UserName>/java/jdk-13.0.2.jdk/Contents/Home",
    "maven.executable.path": "/Users/<UserName>/maven/apache-maven-3.6.3/bin/mvn",
    "maven.terminal.useJavaHome": true
...
}
```
The maven properties can be edited via the settings menu directly but it's easier to do them all at once.

Now you should be ready to create a new project!

### Creating a project

This guide jumps ahead slightly with some concepts that are discussed in the later tutorials. This is down to the tooling
but we'll try to keep it high level enough to get going!

First things first then, we are going to use the `Spring Initializr` plugin we installed earlier to create a new project.
Open up the command palette via the menu or by using the ⇧⌘P shortcut:

![CommandMenu](commandMenu.png?raw=true "CommandMenu")

Next, start to type `Spring` and you should see the following:

![VsCommandConsole](vsCommandConsole.png?raw=true "VsCommandConsole")

Select the `Spring Initializr: Generate a Maven Project` option. You will then be navigated through the wizard. First you
will be asked the language, select `Java`:

![ProjectLanguage](projectLanguage.png?raw=true "ProjectLanguage")

Next, the group ID and project artifact name (I am using an example partially based on [Challenge 2](https://github.com/fat-potato-uk/rest-demo-2a):

![ProjectGroupName](projectGroupName.png?raw=true "ProjectGroupName")

![ProjectArtifactName](projectArtifactName.png?raw=true "ProjectArtifactName")

Next, you can select the Spring Boot version. This is not a hard and fast option, as it is constantly changing (and may
be overwritten when doing the tutorials), so just pick the latest for now:

![SpringVersionSelector](springVersionSelector.png?raw=true "SpringVersionSelector")

Finally, you can in some dependencies. For simplicity, you can ignore this for now as most of these will be covered
in the tutorials:

![SpringDependencyViewer](springDependencyViewer.png?raw=true "SpringDependencyViewer")

You should now have a project created! The vanilla setup should look something like this:

![ProjectLayout](projectLayout.png?raw=true "ProjectLayout")

Some of these are not needed (and may be platform specific). You should therefore be safe to remove the following:

![AdditionalArtifacts](additionalArtifacts.png?raw=true "AdditionalArtifacts")

It's worth noting a few interesting bits from the wizard setup. The `pom.xml` generated looks something like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.6.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>rest.demo</groupId>
    <artifactId>rest-demo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>demo</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
            <exclusions>
                <exclusion>
                    <groupId>org.junit.vintage</groupId>
                    <artifactId>junit-vintage-engine</artifactId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

Ignoring the Java version and other properties, the main takeaway is this snippet:

```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
        <exclusions>
            <exclusion>
                <groupId>org.junit.vintage</groupId>
                <artifactId>junit-vintage-engine</artifactId>
            </exclusion>
        </exclusions>
    </dependency>
```

As of `Spring Boot 2.2.0`, `JUnit5` has been enabled as the default testing framework. `Spring Initializr` has therefore
chosen to disable the `Junit4` to prevent any "accidents" happening during development. Under normal circumstances this 
would be fine, but as the tutorials switch back and forth, you may want to copy the `pom.xml`'s from each tutorial as you
progress.

Finally, once you have something you wish to build, you can run a `mvn install` via the left hand explorer pane:

![MvnInstall](mvnInstall.png?raw=true "MvnInstall")

Good luck!


 





    
