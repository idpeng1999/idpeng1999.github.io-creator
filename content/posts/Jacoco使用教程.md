---
title: "Jacoco使用教程"
date: 2022-04-10T23:21:11+08:00
draft: false
categories: [工具教程]
---

* 在`pom.xml`添加配置
```
  <plugin>
                <groupId>org.jacoco</groupId>
                <artifactId>jacoco-maven-plugin</artifactId>
                <version>0.8.5</version>
                <executions>
                    <execution>
                        <id>default-prepare-agent</id>
                        <goals>
                            <goal>prepare-agent</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>default-report</id>
                        <phase>verify</phase>
                        <goals>
                            <goal>report</goal>
                        </goals>
                    </execution>
                    <execution>
                        <id>default-check</id>
<!--                        <goals>-->
<!--                            <goal>check</goal>-->
<!--                        </goals>-->
                        <configuration>
                            <rules>
                                <rule>
                                    <element>BUNDLE</element>
                                    <limits>
                                        <limit>
                                            <counter>COMPLEXITY</counter>
                                            <value>COVEREDRATIO</value>
                                            <minimum>0.60</minimum>
                                        </limit>
                                    </limits>
                                </rule>
                            </rules>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
```

* 当JaCoCo插件配置好以后，要获得 JaCoCo的统计数据，就要执行mvn install 命令。
* 执行完以后，target/site/jacoco/目录下会生成一个index.html文件.
* 这是统计数据总览页面，可以在浏览器打开查看

* 在该目录下可查看测试报告
![目录](/img/Jacoco使用教程/img.png)
