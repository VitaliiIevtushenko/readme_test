# Javadoc Coverage
Provides javadoc coverage analytics.

## Prerequisites

* JDK 8+
* Gradle
* Git

## Usage

#### 1. Plug in maven-javadoc plugin with TEG javadoc-coverage Doclet

```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-javadoc-plugin</artifactId>
    <version>3.2.0</version>
    <configuration>
        <sourcepath>
            ${project.build.directory}/delombok:${project.build.directory}/generated-sources/annotations
        </sourcepath>
    </configuration>
    <executions>
        <!-- Exports JavaDocs to regular HTML files -->
        <execution>
            <id>javadoc-html</id>
            <phase>package</phase>
            <goals>
                <goal>javadoc</goal>
            </goals>
        </execution>
        <!-- Generates the JavaDoc coverage report -->
        <execution>
            <id>javadoc-coverage</id>
            <phase>package</phase>
            <goals>
                <goal>javadoc</goal>
            </goals>
            <configuration>
                <doclet>com.transportexchangegroup.docket.CoverageDoclet</doclet>
                <docletArtifacts>
                    <docletArtifact>
                        <groupId>com.transportexchangegroup.javadoc-coverage</groupId>
                        <artifactId>jdk8</artifactId>
                        <version>1.1</version>
                    </docletArtifact>
                </docletArtifacts>
                <useStandardDocletOptions>false</useStandardDocletOptions>
            </configuration>
        </execution>
    </executions>
</plugin>
```
Use 
```xml
<artifactId>jdk8</artifactId>
```
for Doclet in case your project uses java 8 or 
```xml
<artifactId>jdk9</artifactId>
```
if java 9 and later.

#### 2. Plug in suppressions to maven-checkstyle-plugin 
```xml
<suppressionsLocation>cx-checkstyle-suppressions.xml</suppressionsLocation>
```
In case your project has already had suppressions file add rule to suppress checkstyle violations in autogenerated classes:
```xml
<suppress files="[\\/]generated-sources[\\/]" checks="[a-zA-Z0-9]*"/>
```

#### 3. In case your project uses querydsl dependency
- Add 
```xml
<classifier>jpa</classifier> 
```
to  querydsl-apt dependency:
```xml
<dependency>
    <groupId>com.querydsl</groupId>
    <classifier>jpa</classifier>
    <artifactId>querydsl-apt</artifactId>
    <version>4.1.4</version>
</dependency>
```
- Remove plugin:    
```xml
<plugin>
    <groupId>com.mysema.maven</groupId>
    <artifactId>apt-maven-plugin</artifactId>
    <version>1.1.3</version>
    <executions>
        <execution>
            <goals>
                <goal>process</goal>
            </goals>
            <configuration>
                <outputDirectory>target/generated-sources/java</outputDirectory>
                <processor>com.querydsl.apt.jpa.JPAAnnotationProcessor</processor>
            </configuration>
        </execution>
    </executions>
</plugin>
```
#### 4. Error handling
- In case of Error `Class file for javax.interceptor.InterceptorBinding not found` replace all 
```java
import javax.transaction.Transactional;
```
with
```java
import org.springframework.transaction.annotation.Transactional;
```

## Authors

* Dmitriy Shyshkin
