# Secret Santa Generator 🎅

A simple Secret Santa Generator web application built using **Spring Boot**.

The application allows users to add participants and generate Secret Santa matches.

I used this project to practice **CI/CD with Jenkins and Docker**.

## Technologies

* Java
* Spring Boot
* Spring MVC
* Thymeleaf
* Spring Data JPA
* H2 Database
* Maven
* Git & GitHub
* Jenkins
* Docker
* Docker Hub

## Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/bmanisha04/secretsanta-generator.git
```

### 2. Go to the project directory

```bash
cd secretsanta-generator
```

### 3. Build the application

```bash
mvn clean package
```

### 4. Run the application

```bash
java -jar target/secretsanta-0.0.1-SNAPSHOT.jar
```

Open the application in your browser:

`http://localhost:8080`

## Run with Docker

### 1. Build the application

```bash
mvn clean package
```

### 2. Build the Docker image

```bash
docker build -t manisha417/secretsanta-generator:latest .
```

### 3. Run the Docker container

```bash
docker run -d \
  --name secretsanta-container \
  -p 7777:8080 \
  manisha417/secretsanta-generator:latest
```

The application will be available at:

`http://localhost:7777`

The application runs on port **8080** inside the container. Port **7777** is mapped to the application port on the local machine.

## Jenkins CI/CD

I created a Jenkins pipeline to automate the build and deployment process.

### Pipeline Flow

```text
GitHub
   ↓
Checkout
   ↓
Maven Build
   ↓
Test
   ↓
Build Docker Image
   ↓
Push Image to Docker Hub
   ↓
Run Docker Container
```

### Jenkins Stages

#### Checkout

Jenkins gets the latest source code from GitHub.

#### Build

Maven builds the Spring Boot application and creates the JAR file.

```bash
mvn clean package
```

#### Test

The application tests are executed as part of the Maven build.

#### Build Docker Image

Jenkins creates the Docker image:

```bash
docker build -t manisha417/secretsanta-generator:latest .
```

#### Push Docker Image

The image is pushed to Docker Hub:

```bash
docker push manisha417/secretsanta-generator:latest
```

#### Run Docker Container

Before starting the new container, the existing container is removed:

```bash
docker rm -f secretsanta-container || true
```

Then the latest image is used to start the application:

```bash
docker run -d \
  --name secretsanta-container \
  -p 7777:8080 \
  manisha417/secretsanta-generator:latest
```

## Dockerfile

The application is packaged into a Docker image using the following Dockerfile:

```dockerfile
FROM openjdk:8u151-jdk-alpine3.7

WORKDIR /app

COPY target/*.jar app.jar

ENTRYPOINT ["java", "-jar", "app.jar"]
```

## Database

The application uses an **H2 in-memory database**.

Database URL:

```text
jdbc:h2:mem:testdb
```

To enable the H2 console, add this property to `application.properties`:

```properties
spring.h2.console.enabled=true
```

The H2 console can then be accessed at:

`http://localhost:8080/h2-console`

## Screenshots

<img width="1910" height="966" alt="image" src="https://github.com/user-attachments/assets/a9f024fc-8504-42d6-9bd8-65b7e687804b" />

## Docker Hub

Docker image:

```text
manisha417/secretsanta-generator:latest
```

## DevOps Implementation

* Maven build and testing
* Jenkins pipeline
* Dockerfile creation
* Docker image building
* Docker container management
* Docker Hub authentication and image push
* Local container deployment
* Jenkins credentials
* CI/CD automation

## Author

**Manisha Banne**
