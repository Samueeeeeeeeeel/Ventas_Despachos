# Etapa 1: Construcción (Build) usando Maven
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

# Copiamos los archivos de dependencias y el código fuente
COPY pom.xml .
COPY src ./src

# Compilamos el proyecto omitiendo los tests para que sea más rápido
RUN mvn clean package -DskipTests

# Etapa 2: Ejecución
FROM openjdk:17-jdk-slim
WORKDIR /app

# Copiamos el archivo .jar generado en la etapa anterior
COPY --from=build /app/target/*.jar app.jar

# Exponemos el puerto de Spring Boot (por defecto es 8080)
EXPOSE 8080

# Comando para ejecutar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]