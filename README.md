Use **spring+gradle** to create restful api

**First**

create directory in your computer such as _RestService_
and create sub directory RestService/main/java/hello which will
be used to put the java classes

**Second**

Create the build.gradle file, we will use gradle to build
our project and put the following content in build.gradle


```
buildscript {
    //this configured for the build script level
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.5.8.RELEASE")
    }
}
//the new plugin DSL to add the plugins
plugins {
    id 'com.gradle.build-scan' version '1.10.2' // this plugin is used to publish the build records to the server
    id 'base'
}
//this configuration is used to accept the license of scan server
buildScan {
    licenseAgreementUrl = 'https://gradle.com/terms-of-service'
    licenseAgree = 'yes'
}

//create a zip Task, then run command gradle zip/gradlew zip
task zip(type:Zip){
    from 'src'
}
//add a "Hello World" example, when run gradle hello, we will see 'hello world' in the console
task hello(){
    doLast{
        println 'hello world'
    }
}
//the older way to add plugins
apply plugin: 'java' //the language plugin built on top the base plugin
apply plugin: 'eclipse'
apply plugin: 'idea'
apply plugin: 'org.springframework.boot'

apply plugin: 'war' //this plugin will package the files as war format which will be used in server container

war {
    baseName = 'hello'
    version =  '0.5.0'
}


jar {
    baseName = 'gs-rest-service'
    version =  '0.1.0'
}
// this is configures for the project level
repositories {
    mavenCentral()
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile("org.springframework.boot:spring-boot-starter-web")
    providedRuntime("org.springframework.boot:spring-boot-starter-tomcat")
    testCompile('org.springframework.boot:spring-boot-starter-test')
}
```
for more details about gradle, please refer to _https://guides.gradle.org_

**Third**

Create the rest controller and the model to represent the message

**Forth**

Make the application executable, there are two ways to run the application
one is that run the command ```gradle bootRun```
the other one is use the war file in build/libs directory

how to use the war file in Tomcat
1.  copy the war in somewhere on the computer such as D:\study\demo\xxx.war
2.  modify the server.xml file under the directory conf of tomcat and 
add the following line code in the host node

```<Context docBase="D:\study\demo\xxx.war" path="/greeting" reloadable="true"/>```

then you can access the restful service by 
_http://localhost:8080/greeting_
