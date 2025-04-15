# Etapa 1: Construcción del JAR con Maven
FROM maven:3.8.6-openjdk-17-slim AS build

# Establecer el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiar el archivo pom.xml y las dependencias necesarias para descargar dependencias
COPY T3Chauca/pom.xml .

# Descargar las dependencias de Maven
RUN mvn dependency:go-offline

# Copiar el código fuente de tu aplicación
COPY T3Chauca/src /app/src

# Ejecutar Maven para compilar y generar el archivo JAR
RUN mvn clean package -DskipTests

# Etapa 2: Imagen para ejecutar la aplicación con el archivo JAR
FROM openjdk:21-jdk-slim

# Establecer el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copiar el JAR generado desde la etapa de construcción
COPY --from=build /app/target/T3Chauca-0.0.1-SNAPSHOT.jar app.jar

# Exponer el puerto en el que la aplicación se ejecutará
EXPOSE 8080

# Comando para ejecutar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]
