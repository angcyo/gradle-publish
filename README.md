#Gradle 发布项目到 Jcenter
只介绍关于bintray.gradle的使用,其他介绍请自行百度参考;

##使用步骤
###1.配置[bintray](https://bintray.com/)账号(只针对Win用户)
```
请在 C:\Users\Administrator\.gradle\gradle.properties 文件中配置:
BINTRAY_USER=r***
BINTRAY_KEY=9688c4f63b14a93f0***
```
###2.在Project或者Module中的build.gradle文件中 添加依赖
```groovy
    classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.5'
    //新版查询地址: http://jcenter.bintray.com/com/jfrog/bintray/gradle/gradle-bintray-plugin/
    
    classpath "org.jfrog.buildinfo:build-info-extractor-gradle:3.2.0"
    //新版查询地址:http://jcenter.bintray.com/org/jfrog/buildinfo/build-info-extractor-gradle/
```
添加后是这样的:
```groovy
    dependencies {
        classpath 'com.android.tools.build:gradle:2.0.0-alpha2'
        classpath 'com.jfrog.bintray.gradle:gradle-bintray-plugin:1.5'        //添加
        classpath "org.jfrog.buildinfo:build-info-extractor-gradle:3.2.0"     //添加
    }
```

###3.在Project根目录中的gradle.properties文件中,新增以下内容(所有内容,请替换成自己的...):
```java
PROJ_GROUP=com.angcyo
PROJ_VERSION=1.1.8
PROJ_NAME=l
PROJ_WEBSITEURL=https://github.com/angcyo/Log
PROJ_ISSUETRACKERURL=https://github.com/angcyo/Log/issues
PROJ_VCSURL=https://github.com/angcyo/Log.git
PROJ_DESCRIPTION=android-log-angcyo-2015-12-10
PROJ_ARTIFACTID=L

DEVELOPER_ID=angcyo
DEVELOPER_NAME=angcyo
DEVELOPER_EMAIL=angcyo@126.com

POM_SCM_URL=PROJ_WEBSITEURL
POM_SCM_CONNECTION=scm:git@github.com:angcyo/Log.git
POM_SCM_DEV_CONNECTION=scm:git@github.com:angcyo/Log.git
```

###4.在需要上传的module项目中build.gradle文件,最后一行添加:
```groovy
apply from: 'https://raw.githubusercontent.com/angcyo/gradle-publish/master/bintray.gradle'
```
添加之后是这样的:
```groovy
apply plugin: 'com.android.library'
android {
    compileSdkVersion 23
    buildToolsVersion "23.0.2"
    defaultConfig {
        minSdkVersion 15
        targetSdkVersion 23
        versionCode 1
        versionName "1.0"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    productFlavors {
    }
}

dependencies {
    compile fileTree(include: ['*.jar'], dir: 'libs')
    testCompile 'junit:junit:4.12'
    compile 'com.android.support:appcompat-v7:23.1.1'
}
apply from: 'https://raw.githubusercontent.com/angcyo/gradle-publish/master/bintray.gradle' //添加
```

###5.在Android Studio中 Terminal窗口中,输入以下命令:
```C++
gradlew bintrayUpload
```
当你看到 
```C
BUILD SUCCESSFUL
```
OK...之后,,,你懂的;

#参考文章:
https://github.com/msdx/gradle-publish
