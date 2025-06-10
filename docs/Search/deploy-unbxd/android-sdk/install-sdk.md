---
title: 'Install SDK '
deprecated: false
hidden: false
metadata:
  robots: index
---
Android SDK is hosted in a private maven repository and is integrated as a Gradle dependency.

The first step in installing the Android SDK is to update the Android app’s `build.gradle` file to add a dependency on the mobile app, then do a gradle sync, and you are ready to go

To add dependency,  go to file` build.gradle` and go to the dependencies sections and add the code as shown below:

Unbxd would provide credentials. Unbxd employees can view the credentials and procedures [here](https://drive.google.com/file/d/1G5SV8RvifROoG2bICUcc89PtdCei6yfV/view).

After changes to build. Gradle are done, do a Gradle sync so that Gradle pulls in all the required resources for your project and checks all the references to make sure everything’s okay.

```Text Kotlin
repositories  
{
               maven {
               url 'http://3.95.143.246:8081/artifactory/libs-release-local/' 
               credentials {
               username ""
               password "" 
                           }
                      }
}
dependencies {  
               implementation fileTree(include: ['*.jar'], dir: 'libs')
                  - 
                  - 
                  -
               implementation 'com.squareup.okhttp3:okhttp:3.8.1'
               implementation (group: 'com.unbxd.sdk', name:'unbxdsdk', version: '1.0.7', ext:'aar')
               implementation project(path: ':unbxdsdk') 
              }
```
```java
repositories {
  maven {
    url 'http://3.95.143.246:8081/artifactory/libs-release-local/' 
    credentials {
      username ""
      password "" 
    }
  }
}
dependencies {  
  implementation fileTree(include: ['*.jar'], dir: 'libs')
  implementation 'com.squareup.okhttp3:okhttp:4.6.0'
  implementation(group: 'com.unbxd.sdk', name: 'unbxdsdk', version: '1.0.7', ext: 'aar')
}
```