[![Maven Central](https://maven-badges.herokuapp.com/maven-central/de.quantummaid/quantummaid-opensource-parent/badge.svg)](https://maven-badges.herokuapp.com/maven-central/de.quantummaid/quantummaid-opensource-parent)

# quantummaid-java-standards

Contains the java quality standards for quantummaid projects

## Usage
Replace the top section of your pom with the following:
```xml
<!--
  ~ Copyright (c) 2018 Richard Hauswald - https://quantummaid.de/.
  ~
  ~ Licensed to the Apache Software Foundation (ASF) under one
  ~ or more contributor license agreements.  See the NOTICE file
  ~ distributed with this work for additional information
  ~ regarding copyright ownership.  The ASF licenses this file
  ~ to you under the Apache License, Version 2.0 (the
  ~ "License"); you may not use this file except in compliance
  ~ with the License.  You may obtain a copy of the License at
  ~
  ~   http://www.apache.org/licenses/LICENSE-2.0
  ~
  ~ Unless required by applicable law or agreed to in writing,
  ~ software distributed under the License is distributed on an
  ~ "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
  ~ KIND, either express or implied.  See the License for the
  ~ specific language governing permissions and limitations
  ~ under the License.
  -->

<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>de.quantummaid</groupId>
        <artifactId>quantummaid-opensource-parent</artifactId>
        <version>1.0.0</version>
    </parent>
```

Also make sure that the `README.md` of the project clearly recommends the usage of the `pgpverify-maven-plugin` by
providing the link https://youtu.be/ES9hWkn_WBA?t=27m29s . It can be found under 
https://www.simplify4u.org/pgpverify-maven-plugin/ usage instructions. 
 
## Checkstyle
Checkstyle is enabled after using this pom as parent in a maven project and executed before tests are run.

### Registering Checkstyle suppressions
Add the following to your pom:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
        ...
    <properties>
        ...
        <checkstyle.suppressions.location>
            ${project.basedir}/src/test/checkstyle/checkstyle-suppressions.xml
        </checkstyle.suppressions.location>
    </properties>
    ...
</project>
```
And create the suppression configuration file under `/src/test/checkstyle/checkstyle-suppressions.xml` with the 
contents of your choosing based on the following example:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--
  ~ Copyright (c) 2018 Richard Hauswald - https://quantummaid.de/.
  ~
  ~ Licensed to the Apache Software Foundation (ASF) under one
  ~ or more contributor license agreements.  See the NOTICE file
  ~ distributed with this work for additional information
  ~ regarding copyright ownership.  The ASF licenses this file
  ~ to you under the Apache License, Version 2.0 (the
  ~ "License"); you may not use this file except in compliance
  ~ with the License.  You may obtain a copy of the License at
  ~
  ~   http://www.apache.org/licenses/LICENSE-2.0
  ~
  ~ Unless required by applicable law or agreed to in writing,
  ~ software distributed under the License is distributed on an
  ~ "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
  ~ KIND, either express or implied.  See the License for the
  ~ specific language governing permissions and limitations
  ~ under the License.
  -->

<!DOCTYPE suppressions PUBLIC
        "-//Puppy Crawl//DTD Suppressions 1.1//EN"
        "http://www.puppycrawl.com/dtds/suppressions_1_1.dtd">
<suppressions>
    <suppress checks="VisibilityModifier" files=".*AggregatedValidationException.java" />
    <suppress checks="IllegalCatchCheck" files="NamedMethodSerializationCPMethod.java" />
    <suppress checks="IllegalCatchCheck" files="Deserializer.java" />
</suppressions>
```

The checkstyle step can be skipped for a run with `-Dcheckstyle.skip`

### Intellij integration
Install the CheckStyle-IDEA plugin. Afterwards, open Settings -> Other Settings -> Checkstyle and add a new Checkstyle
configuration file, name it QuantumMaidOpenSource and use 
`https://raw.githubusercontent.com/quantummaid/quantummaid-opensource-parent/master/checkstyle/checkstyle.xml` as a URL location.

## Spotbugs
Spotbugs is enabled after using this pom as parent in a maven project and executed before tests are run.

### Registering Spotbugs exclusions
Add the following to your pom:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
        ...
    <properties>
        ...
        <spotbugs.excludeFilterFile>
            ${project.basedir}/src/test/spotbugs/spotbugs-exclude.xml
        </spotbugs.excludeFilterFile>
    </properties>
    ...
</project>
```
And create the suppression configuration file under `/src/test/spotbugs/spotbugs-exclude.xml` with the contents of your
choice based on the following example:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!--
  ~ Copyright (c) 2018 Richard Hauswald - https://quantummaid.de/.
  ~
  ~ Licensed to the Apache Software Foundation (ASF) under one
  ~ or more contributor license agreements.  See the NOTICE file
  ~ distributed with this work for additional information
  ~ regarding copyright ownership.  The ASF licenses this file
  ~ to you under the Apache License, Version 2.0 (the
  ~ "License"); you may not use this file except in compliance
  ~ with the License.  You may obtain a copy of the License at
  ~
  ~   http://www.apache.org/licenses/LICENSE-2.0
  ~
  ~ Unless required by applicable law or agreed to in writing,
  ~ software distributed under the License is distributed on an
  ~ "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
  ~ KIND, either express or implied.  See the License for the
  ~ specific language governing permissions and limitations
  ~ under the License.
  -->

<FindBugsFilter
		xmlns="https://github.com/spotbugs/filter/3.0.0"
		xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		xsi:schemaLocation="https://github.com/spotbugs/filter/3.0.0 https://raw.githubusercontent.com/spotbugs/spotbugs/3.1.0/spotbugs/etc/findbugsfilter.xsd">
    <Match>
         <Class name="de.quantummaid.someClass"/>
         <Method name="aSpecificMethod"/>
         <Bug pattern="RCN_REDUNDANT_NULLCHECK_OF_NONNULL_VALUE"/>
    </Match>
    
    <Match>
         <Class name="de.quantummaid.differentClass"/>
         <Bug category="PERFORMANCE"/>
    </Match>

</FindBugsFilter>
```

More information about exclusions can be found on the spotbugs website: https://spotbugs.readthedocs.io/en/stable/filter.html#examples

### Intellij integration
Install the Findbugs-IDEA plugin.

## Compiler
The compiler is configured for all child projects and should not be modified in any of the child projects of this pom.
Following this recommendation provides child projects with the following benefits:
- Encoding and Java version of the sources and compiled classes are managed
- A configuration bug fix, that will prevent the maven-compiler-plugin from swallowing compilation errors and hence 
  failing with 'unknown compilation error'
- Building the child project in Intellij will be possible with warnings
- Building the child project using maven will be possible with warnings, if built with `-DskipTests=true` 
- Testing the child project using maven will be possible with warnings, if built with 
  `-Dmaven.compiler.failOnWarning=false` 
- Building/Testing the child project will fail, if the source code is causing compiler warnings
- Releasing the child project will fail, if the source code is causing compiler warnings

## Skipping tests
Just run the maven command with `-DskipTests=true`.

## Long running tests, that should be executed before every release, but not on every verify
Surefire will set a SystemProperty `testMode` to either `NORMAL` or `RELEASE` depending on the active profile.

In the test, an if statement can be used:
```java
final Boolean runThisTest = Optional.ofNullable(System.getProperty("testMode")).map(s -> s.equals("RELEASE")).orElse(false);
if (runThisTest) {
    //test you long running stuff
} else {
    System.out.println("Skipping this test, since system property testMode is not set to RELEASE");
}
```

## Releasing a version to maven central
The problem with releasing to maven central using a CI/CD pipeline is complicated, since both, the nexus staging account
and the gpg key must be kept private. If a very bad person gains access to one or both of these credentials users of
our open source products are in grave danger (https://youtu.be/ES9hWkn_WBA?t=27m29s). A bitbucket pipeline can output 
secure environmental variables with some neat tricks. Since we would need to store both valuable credentials as such,
that operation can only be done manually outside the bitbucket cloud environment:

* Ensure the gpg private key with the id `0xACB977BA5C6D5C6E` installed in the gpg key store.
* Ensure the maven settings.xml file contains the following section:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
		  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
	...
	<servers>
		<server>
			<id>quantummaid.opensource.sonatype.staging</id>
			<username>the username of the sonatype nexus staging account</username>
			<password>{the encrypted password of the Sonatype nexus staging account created using mvn --encrypt-password}</password>
		</server>
	</servers>
	...
</settings>
```
* ensure the project version has been set to the appropriate value
* run the following command to test the project:
```bash
mvn clean verify
```
* run the following command to release the project in case the tests passed:
```bash
mvn -DdeployToMavenCentral -DskipTests=true clean deploy
```

## Excluding modules from being released to maven central
Sometimes a project needs a [test]module, that is not supposed to be released as an artifact to maven central. This is
a tough nut, since the nexus staging plugin will only deploy to staging, if the last module of a multi modules build,
is actually one that is supposed to be released. Especially test modules tend to be the last ones built and are not
to be deployed, so disabling the staging plugin in these modules will essentially end up in the whole project not being
released to staging. In these cases 2 profiles will do the trick. One that is called `development`, which includes 
ALL the modules and is activated on the missing property named `deployToMavenCentral`. 
The other profile is called `deployToMavenCentral`, contains only the modules that are intended to be released to
maven central and is activated on the presence of the property named `deployToMavenCentral`. Example:
```xml
<profiles>
    <profile>
        <id>development</id>
        <activation>
            <activeByDefault>false</activeByDefault>
            <property>
                <name>!deployToMavenCentral</name>
            </property>
        </activation>
        <modules>
            <module>core</module>
            <module>integrations</module>
            <module>tests</module>
        </modules>
    </profile>
    <profile>
        <id>deployToMavenCentral</id>
        <activation>
            <activeByDefault>false</activeByDefault>
            <property>
                <name>deployToMavenCentral</name>
            </property>
        </activation>
        <modules>
            <module>core</module>
            <module>integrations</module>
        </modules>
    </profile>
</profiles>
```
