docker-maven
============

# Supported tags and respective Dockerfile links

* [oracle-jdk-7](https://github.com/emilianobonassi/docker-maven/blob/master/oracle-jdk-7/Dockerfile)
* [oracle-jdk-7-onbuild](https://github.com/emilianobonassi/docker-maven/blob/master/oracle-jdk-7/onbuild/Dockerfile)
* [latest, oracle-jdk-8](https://github.com/emilianobonassi/docker-maven/blob/master/oracle-jdk-8/Dockerfile)
* [onbuild, oracle-jdk-8-onbuild](https://github.com/emilianobonassi/docker-maven/blob/master/oracle-jdk-8/onbuild/Dockerfile)

# What is Maven?

[Apache Maven](http://maven.apache.org) is a software project management and comprehension tool.
Based on the concept of a project object model (POM),
Maven can manage a project's build,
reporting and documentation from a central piece of information.


# How to use this image

## Create a Dockerfile in your Maven project

    FROM emilianobonassi/maven:oracle-jdk-8
    CMD ["do-something-with-built-packages"]

Put this file in the root of your project, next to the pom.xml.

This image includes multiple ONBUILD triggers which should be all you need to bootstrap.
The build will `COPY . /usr/src/app` and `RUN mvn install`.

You can then build and run the image:

    docker build -t my-maven .
    docker run -it --name my-maven-script my-maven


## Run a single Maven command

For many simple projects, you may find it inconvenient to write a complete `Dockerfile`.
In such cases, you can run a Maven project by using the Maven Docker image directly,
passing a Maven command to `docker run`:

    docker run -it --rm --name my-maven-project -v "$(pwd)":/usr/src/mymaven -w /usr/src/mymaven emilianobonassi/maven:oracle-jdk-8 mvn clean install
