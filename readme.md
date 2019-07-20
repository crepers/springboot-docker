# Getting Started

### Maven build
You can build a tagged docker image using the command line like this:

```
$ ./mvnw install dockerfile:build
```


### Docker
You can run the docker container follow command 

```
docker run -p 8080:8080 -t springio/springboot-docker -name sboot-docker
```
and you can connect to it

```
docker exec -it {container name} /bin/sh
```

### Using Spring Profiles
```
$ docker run -e "SPRING_PROFILES_ACTIVE=prod" -p 8080:8080 -t springio/springboot-docker
```
or

```
$ docker run -e "SPRING_PROFILES_ACTIVE=dev" -p 8080:8080 -t springio/springboot-docker
```

### Debugging tha application with docker
To debug the application [JPDA Transport][jpda_link] can be used. So we’ll treat the container like a remote server. To enable this feature pass a java agent settings in JAVA_OPTS variable and map agent’s port to localhost during a container run. With the Docker for Mac there is limitation due to that we can’t access container by IP without black magic usage.

```
$ docker run -e "JAVA_OPTS=-agentlib:jdwp=transport=dt_socket,address=5005,server=y,suspend=n" -p 8080:8080 -p 5005:5005 -t springio/springboot-docker
```


[jpda_link]: https://docs.oracle.com/javase/8/docs/technotes/guides/jpda/conninv.html#Invocation
