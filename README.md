# Harsha's Task-Management-System
An Agile Task Management System built using Java, SpringBoot, MySQL, RabbitMQ and Vue.js


## Local development setup

### Prerequisites

- JDK8+
- MySQL 5.7+
- RabbitMQ 3.6+
- GraphicMagick 1.3+

### Database setup

- Create database `task_agile`
- Initialize database with scripts in `setup` folder

### Add dev properties file

- Create `src/main/resources/application-dev.properties` with the following settings to override the settings in `application.properties`.

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/task_agile?useSSL=false
spring.datasource.username=<your username>
spring.datasource.password=<your password>
```

## Commands

- Use `mvn test` to run the tests of the back-end and the front-end
- Use `mvn spring-boot:run` to start the back-end
- Use `npm run serve` inside the `frontend` directory to start the front-end
- Use `mvn install` to build both the front-end and the back-end
- Use `java -jar target/app-0.0.1-SNAPSHOT.jar` to start the bundled application

## How to run application inside docker

```bash
$ mvn clean package
$ cp target/app-0.0.1-SNAPSHOT.jar docker/app.jar
$ docker build -t taskagile:dev docker/
```

### Start with dev profile locally

```bash
$ docker run --rm --name taskagile -e "SPRING_PROFILES_ACTIVE=dev" -p 8080:8080 -p 9000:9000 taskagile
```

### Start on server

With active profiles `staging` and `docker`. Make sure `docker` is the last one in the list so that the settings in `evn.list` will be applied.

```bash
$ docker run --rm --name taskagile --env-file ./docker/env.list -e "SPRING_PROFILES_ACTIVE=staging,docker" -p 8080:8080 -p 9000:9000 taskagile
```
