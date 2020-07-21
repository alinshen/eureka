1.打开Gradle的安装目录下的init.d文件夹，在里面新建一个init.gradle文件，将以下内容粘贴到文件中

allprojects{
    repositories {
        def REPOSITORY_URL = 'http://maven.aliyun.com/nexus/content/groups/public/'
        all { ArtifactRepository repo ->
            if(repo instanceof MavenArtifactRepository){
                def url = repo.url.toString()
                if (url.startsWith('https://repo1.maven.org/maven2') || url.startsWith('https://jcenter.bintray.com/')) {
                    remove repo
                }
            }
        }
        maven {
            url REPOSITORY_URL
        }
    }
}




2.打开的eureka源码中修改一下build.grade文件

buildscript {
//    repositories { jcenter() }
    repositories {
        maven {
            url 'http://maven.aliyun.com/nexus/content/groups/public/'
        }
    }

    dependencies {
        classpath 'com.netflix.nebula:gradle-extra-configurations-plugin:2.2.+'
    }
}

3.可以切换到 v1.7.2版本