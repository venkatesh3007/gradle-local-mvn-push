gradle-local-mvn-push
===============

This work is forked from Chris Bane's [gradle-mvn-push](https://github.com/chrisbanes/gradle-mvn-push). Thank's to Crhis for his work, as it really saved me a lot of hours. You're my hero :)

The initial idea of this script is to automate the deploy of android aar libraries into a local maven repository. The whole picture is to use github as a maven repository by just comitting the changes generated in the local one after executing the script.


## Usage


### 1. Setup your local repository path

Modify (or create) the file  `USER_HOME/.gradle/gradle.properties` to include the path to your local repository.

```properties
REPOSITORY_PATH = file://path/to/your/repo
```
Be sure you don't include the / at the end of the path

The script will deploy the artifacts into a release subfolder, or into a snapshot folder if they have the SNAPSHOT word in the `VERSION_NAME` variable.

### 2. Create your gradle.properties

You can create a single properties file in your module folder (if you are just uploading one) or split it into several files, placing in your project root properties the common values and adding one properties file into each module for specific settings.

This is an example of the supported properties:

```properties
VERSION_NAME=1.0.0
VERSION_CODE=1
GROUP=com.blindbugs.android

POM_DESCRIPTION=My fancy library uploaded to a maven repo
POM_URL=https://github.com/sergiandreplace/mylib
POM_SCM_URL=https://github.com/sergiandreplace/mylib
POM_SCM_CONNECTION=scm:git@github.com:sergiandreplace/mylib.git
POM_SCM_DEV_CONNECTION=scm:git@github.com:sergiandreplace/mylib.git
POM_LICENCE_NAME=The Apache Software License, Version 2.0
POM_LICENCE_URL=http://www.apache.org/licenses/LICENSE-2.0.txt
POM_LICENCE_DIST=repo
POM_DEVELOPER_ID=BlindBugs
POM_DEVELOPER_NAME=Sergi Martínez

POM_NAME=My Lib
POM_ARTIFACT_ID=mylib
POM_PACKAGING=aar

```


### 3. Call the script from each sub-modules build.gradle

Add the following at the end of the `build.gradle` for each module you wish to upload:

```groovy
apply from: 'https://raw.github.com/sergiandreplace/gradle-local-mvn-push/master/gradle-local-mvn-push.gradle'
```

### 4. Build and Push

You can now build and push:

```bash
$ gradle clean build uploadArchives
```
Note for Windows users: remember that if you are using the graddle wrapper, you must execute gradlew instead gradle

## License

    Copyright 2013 Chris Banes

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
