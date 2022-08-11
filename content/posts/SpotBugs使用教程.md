---
title: "SpotBugs使用教程"
date: 2022-05-15T21:56:56+08:00
draft: false
categories: [工具教程]
---
## pom文件下添加配置,

```text
            <plugin>
                <groupId>com.github.spotbugs</groupId>
                <artifactId>spotbugs-maven-plugin</artifactId>
                <version>3.1.12</version>
                <configuration>
                    <excludeFilterFile>ignore.xml</excludeFilterFile>
                </configuration>
                <dependencies>
                    <!-- overwrite dependency on spotbugs if you want to specify the version of spotbugs -->
                    <dependency>
                        <groupId>com.github.spotbugs</groupId>
                        <artifactId>spotbugs</artifactId>
                        <version>4.0.0</version>
                    </dependency>

                </dependencies>
                <executions>
                    <execution>
                        <id>spotbugs</id>
                        <phase>verify</phase>
                        <goals>
                            <goal>check</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
```