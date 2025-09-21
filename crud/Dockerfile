# Multi-stage build
# Stage 1: Build the application
FROM maven:3.9.4-openjdk-21 AS build

# Set working directory
WORKDIR /app

# Copy pom.xml and download dependencies
COPY pom.xml .
RUN mvn dependency:go-offline -B

# Copy source code
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests

# Stage 2: Create runtime image
FROM tomcat:9.0-jdk21

# Set working directory
WORKDIR /usr/local/tomcat/webapps/

# Copy the WAR file to Tomcat's webapps directory
COPY --from=build /app/target/employeedb.war ./employeedb.war

# Expose the Tomcat port
EXPOSE 8090
