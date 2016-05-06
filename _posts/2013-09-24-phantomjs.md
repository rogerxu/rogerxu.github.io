---
layout: post
title: PhantomJS
---

## Introduction

PhantomJS - Scriptable Headless WebKit

Documentation: <http://phantomjs.org/>

## Installation

* [Download and Installation](http://phantomjs.org/download.html)

### Windows

Download `phantomjs-2.1.1-windows.zip` and extract the content.

The executable `phantomjs.exe` is ready to use.

### Mac OS X

    TODO

### Linux

```sh
$ wget -e https_proxy=http://localhost:8123/ https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
$ tar -xvjf phantomjs-2.1.1-linux-x86_64.tar.bz2
$ sudo cp -r phantomjs-2.1.1-linux-x86_64 /usr/local/share
$ sudo ln -s /usr/local/share/phantomjs-2.1.1-linux-x86_64/ /usr/local/share/phantomjs
$ sudo ln -s /usr/local/share/phantomjs/bin/phantomjs /usr/local/bin/phantomjs
$ whereis phantomjs
$ phantomjs --version
```

## Usage

```sh
$ phantomjs hello.js
```

### Headless Testing

```sh
$ phantomjs runner.js http://localhost:8080/web/test.qunit.html
```

### Continuous Integration

Integration with Maven and Jenkins

1. Use `jetty-maven-plugin` to start Jetty server.
2. Use `exec-maven-plugin` to execute `phantomjs` command to run QUnit tests and generate JUnit report.
3. Use `maven-failsafe-plugin` to collect the test results.

```sh
$ mvn clean integration-test -P test.build
```

```xml
<!-- Profile for Test Runner -->
<profile>
    <id>test.build</id>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>

        <!-- local server -->
        <local.server.host>localhost</local.server.host>
        <local.server.port>${jetty.port}</local.server.port>
        <local.server.protocol>http</local.server.protocol>
        <local.server.url>${local.server.protocol}://${local.server.host}:${local.server.port}</local.server.url>

        <!-- phantomjs command arguments -->
        <phantomjs.runner>${project.basedir}/src/test/config/phantomjs/runner.js</phantomjs.runner>
        <testpage.url>${local.server.url}/${web.context.name}/test-resources/testsuite.qunit.html</testpage.url>
        <testreport.dir>${project.build.directory}/failsafe-reports</testreport.dir>
    </properties>
    <build>
        <plugins>
            <!-- Jetty 8 for JVM 1.6 -->
            <plugin>
                <groupId>org.mortbay.jetty</groupId>
                <artifactId>jetty-maven-plugin</artifactId>
                <version>${jetty8.version}</version>
                <executions>
                    <execution>
                        <id>start-jetty</id>
                        <phase>pre-integration-test</phase>
                        <goals>
                            <goal>run</goal>
                        </goals>
                        <configuration>
                            <scanIntervalSeconds>10</scanIntervalSeconds>
                            <daemon>true</daemon>
                        </configuration>
                    </execution>
                    <execution>
                        <id>stop-jetty</id>
                        <phase>post-integration-test</phase>
                        <goals>
                            <goal>stop</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <scanIntervalSeconds>10</scanIntervalSeconds>
                    <stopPort>9999</stopPort>
                    <stopKey>foo</stopKey>
                    <webAppSourceDirectory>${web.src.dir}</webAppSourceDirectory>
                    <webApp>
                        <contextPath>/${web.context.name}</contextPath>
                        <defaultsDescriptor>${basedir}/src/main/config/jetty-8/webdefault.xml</defaultsDescriptor>
                    </webApp>
                </configuration>
            </plugin>

            <!-- Launch phantomjs command to run qunit tests -->
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>1.2.1</version>
                <executions>
                    <execution>
                        <id>PhantomJS Unit Testing</id>
                        <phase>integration-test</phase>
                        <goals>
                            <goal>exec</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <executable>phantomjs</executable>
                    <arguments>
                        <argument>${phantomjs.runner}</argument>
                        <argument>${testpage.url}</argument>
                        <argument>${testreport.dir}</argument>
                    </arguments>
                </configuration>
            </plugin>

            <!-- Enable the failsafe plugin for the integration-test phase -->
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-failsafe-plugin</artifactId>
                <version>2.17</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>integration-test</goal>
                            <goal>verify</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</profile>
```

### Screen Capture

```javascript
page.render();
```
