# p4
PROGRAM 4: BUILD AND RUN A JAVA APPLICATION WITH MAVEN, MIGRATE THE SAME APPLICATION TO GRADLE

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PRE-REQUISITES CHECK

Open Command Prompt and verify:

java -version
mvn -version
gradle -version

If Gradle is not installed:
Download from gradle.org/releases and add GRADLE_HOME\bin to PATH environment variable.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PART A — BUILD & RUN WITH MAVEN

STEP 1: CREATE THE MAVEN PROJECT

cd D:\exam

mvn archetype:generate -DgroupId=com.ksit -DartifactId=HelloMaven -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

cd HelloMaven

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PROJECT STRUCTURE

HelloMaven/

├── pom.xml
└── src/
├── main/
│   └── java/com/ksit/App.java
└── test/
└── java/com/ksit/AppTest.java

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

STEP 2: EDIT THE SOURCE FILE

Open:

src\main\java\com\ksit\App.java

Replace with:

package com.ksit;

public class App {

```
public static void main(String[] args) {

    System.out.println("Hello KSIT, from Maven Build!");

}
```

}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

STEP 3: UPDATE pom.xml

Open pom.xml and make sure it contains:

<project xmlns="http://maven.apache.org/POM/4.0.0"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
      xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
      http://maven.apache.org/xsd/maven-4.0.0.xsd">

<modelVersion>4.0.0</modelVersion>

<groupId>com.ksit</groupId> <artifactId>HelloMaven</artifactId> <version>1.0-SNAPSHOT</version> <packaging>jar</packaging>

  <properties>
    <maven.compiler.source>21</maven.compiler.source>
    <maven.compiler.target>21</maven.compiler.target>
  </properties>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.13.2</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>

```
  <plugin>
    <groupId>org.codehaus.mojo</groupId>
    <artifactId>exec-maven-plugin</artifactId>
    <version>3.1.0</version>

    <configuration>
      <mainClass>com.ksit.App</mainClass>
    </configuration>

  </plugin>

</plugins>
```

  </build>

</project>

keep pom as its self build
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

STEP 4: COMPILE, TEST, PACKAGE, AND RUN

(a) Compile Source Code

mvn compile

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

(b) Run Unit Tests

mvn test

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

(c) Package into JAR

mvn package

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

(d) Run the Application

mvn exec:java

OR

java -cp target\HelloMaven-1.0-SNAPSHOT.jar com.ksit.App

Expected Output:

Hello KSIT, from Maven Build!

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PART B — MIGRATE TO GRADLE

STEP 5: CREATE A SEPARATE GRADLE PROJECT

cd D:\exam

mkdir HelloGradle

cd HelloGradle

gradle init --java application

mkdir src\main\java\com\ksit

mkdir src\test\java\com\ksit

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

COPY THE SAME App.java INTO GRADLE PROJECT

copy ..\HelloMaven\src\main\java\com\ksit\App.java src\main\java\com\ksit\App.java

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

EDIT App.java

package com.ksit;

public class App {

```
public static void main(String[] args) {

    System.out.println("Hello KSIT, from Gradle Build!");

}
```

}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

STEP 6: CREATE build.gradle

Create build.gradle in:

D:\exam\HelloGradle\

Add:

plugins {
id 'java'
id 'application'
}

group = 'com.ksit'

version = '1.0-SNAPSHOT'

application {
mainClass = 'com.ksit.App'
}

repositories {
mavenCentral()
}

dependencies {
testImplementation 'junit:junit:4.13.2'
}

java {
sourceCompatibility = JavaVersion.VERSION_21
targetCompatibility = JavaVersion.VERSION_21
}

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

STEP 7: CREATE settings.gradle

Create settings.gradle:

rootProject.name = 'HelloGradle'

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

STEP 8: INITIALIZE GRADLE WRAPPER

gradle wrapper

This creates gradlew.bat for reproducible builds.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

STEP 9: BUILD, TEST, AND RUN WITH GRADLE

Compile:

gradle compileJava

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Run Tests:

gradle test

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Build Project:

gradle build

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Run Application:

gradle run

Expected Output:

> Task :run

Hello KSIT, from Gradle Build!

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
