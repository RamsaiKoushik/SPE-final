# # Use the official OpenJDK image as a base
# FROM openjdk:17-jdk-slim

# # Set the working directory
# WORKDIR /app

# # Copy the Spring Boot application JAR file
# COPY target/demo-0.0.1-SNAPSHOT.jar backend.jar

# # Expose the port your Spring Boot application runs on
# EXPOSE 8080

# # Run the Spring Boot application
# ENTRYPOINT ["java", "-jar", "backend.jar"]

# Use Maven with OpenJDK 17 as the base image
FROM maven:3.8.4-openjdk-17-slim

# Set the working directory inside the container
WORKDIR /app

# Copy the Maven project descriptor to the working directory
COPY pom.xml ./

# Download dependencies to speed up subsequent builds
RUN mvn dependency:go-offline -B

# Copy the rest of the application source code
COPY src ./src

# Expose the port the Spring Boot application will run on
EXPOSE 8080

# Command to run the Spring Boot application
CMD ["mvn", "spring-boot:run"]
