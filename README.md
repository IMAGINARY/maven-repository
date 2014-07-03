maven-repository
================

Maven repository for artifacts released by IMAGINARY

Using this repository in gradle build scripts
---------------------------------------------

```
repositories {
    maven { url "https://raw.github.com/IMAGINARY/maven-repository/master/" }
}
```

Uploading artifacts to this repository using gradle 1.12+ build@Test\n    public void scripts
-----------------------------------------------------------------------

Command line:
```
git clone https://github.com/IMAGINARY/maven-repository.git
```

Gradle build script additions for your project:
```
group = 'your.group.id'
version = 'x.x.x'

apply plugin: 'java'
apply plugin: 'maven-publish'

task sourceJar(type: Jar) {
    from sourceSets.main.allJava
}

publishing {
    publications {
        mavenJava(MavenPublication) {
            from components.java

            artifact sourceJar {
                classifier "sources"
            }
        }
    }
    repositories {
        maven {
            // change to path you cloned this repository into
            url "$projectDir/../maven-repository"
        }
    }
}
```

Command line (within local repository folder):
```
git add *
git commit -m "group:name:version"
git push
```



