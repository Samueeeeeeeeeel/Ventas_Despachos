# Etapa 1: Construcción (Build) usando Maven y Temurin
FROM maven:3.9-eclipse-temurin-17 AS build
WORKDIR /app

# Copiamos los archivos de dependencias y el código fuente
COPY pom.xml .
COPY src ./src

# Compilamos el proyecto omitiendo los tests para que sea más rápido
RUN mvn clean package -DskipTests

# Etapa 2: Ejecución con la imagen moderna de Java 17
FROM eclipse-temurin:17-jdk-alpine
WORKDIR /app

# Copiamos el archivo .jar generado en la etapa anterior
COPY --from=build /app/target/*.jar app.jar

# Exponemos el puerto de Spring Boot (por defecto es 8080)
EXPOSE 8080

# Comando para ejecutar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]