Citrus Docker Container ![Logo][1]
==============

This project builds [Docker](https://www.docker.com/) images for running [Citrus](http://citrusframework.org) integration tests.

Build image
---------

This project contains `Dockerfiles` for the Citrus Docker images. You can build the images locally with Maven calling

```
mvn docker:build
```

After that you should have a set of new images on your Docker host named `consol/citrus`. You can use this base image in other
Maven projects in order to execute the Citrus tests within Docker boundaries. This is extremely useful in case the Citrus tests need
to participate as container in the Docker universe e.g. for accessing other containers with Docker networking and DNS resolving features.
 
Also this image can be used to be part of [Kubernetes](https://kubernetes.io/) or [Openshift](https://www.openshift.com/). When run as a 
Pod in Kubernetes the Citrus in-container test cases are able to access exposed services via Kubernetes service discovery.

Usage
---------

The Citrus Docker image executes Citrus integration tests as Maven build within the container. The
image is based on the Maven Docker image and executes a Maven project build on container startup.

The image has a prepared Maven repository containing all available Citrus artifacts. The container executes
Maven POMs in the app directory (default `/maven`). Therefore the image is well suited for usage with the
[Fabric8 Docker Maven plugin](https://github.com/fabric8io/docker-maven-plugin) that is able to assemble Maven projects in `/maven`. 

Your Citrus Maven project just needs to add the following POM configuration of the Fabric8 Docker plugin in order to
bootstrap the complete Citrus Docker image:

```xml
<plugin>
    <groupId>io.fabric8</groupId>
    <artifactId>docker-maven-plugin</artifactId>
    <version>${fabric8.docker.plugin.version}</version>
    <configuration>
      <verbose>true</verbose>
      <images>
        <image>
          <alias>my-app-tests</alias>
          <name>citrus/my-app-tests:${project.version}</name>
          <build>
            <from>consol/citrus:2.7.6</from>
            <tags>
              <tag>latest</tag>
            </tags>
            <assembly>
              <descriptorRef>project</descriptorRef>
            </assembly>
          </build>
          <run>
            <namingStrategy>alias</namingStrategy>
            <log>
              <enabled>true</enabled>
              <color>green</color>
            </log>
          </run>
        </image>
      </images>
    </configuration>
</plugin>
```

The Docker Maven plugin descriptor reference *descriptorRef=project* will automatically add the complete Maven project to the container.
When the container is run the Maven build is automatically started and all Citrus test cases are executed within the container.

On a Docker Maven plugin enabled project you may execute:

```
mvn docker:build
mvn docker:start
mvn docker:stop
```

Team
---------

```
ConSol Software GmbH
citrus-dev-l@consol.de

http://www.citrusframework.org
```

Information
---------

For more information on Citrus see [www.citrusframework.org][2], including
a complete [reference manual][3].

 [1]: http://www.citrusframework.org/img/brand-logo.png "Citrus"
 [2]: http://www.citrusframework.org
 [3]: http://www.citrusframework.org/reference/html/