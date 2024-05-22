# Fase de construcción
FROM gradle:7.6.1-jdk17 as builder

# Clona el repositorio code-processing
RUN git clone https://github.com/IngSis-Group-9/code-processing.git /home/gradle/src

# Da permisos de ejecución al script gradlew
WORKDIR /home/gradle/src
RUN chmod +x ./gradlew

# Ejecuta la tarea bootJar de Gradle para construir el JAR ejecutable
RUN ./gradlew bootJar

# Fase de ejecución
FROM openjdk:17-jdk-slim

# Establece el directorio de trabajo
WORKDIR /app

# Copia el archivo JAR desde la etapa de construcción anterior
COPY --from=builder /home/gradle/src/build/libs/code-processing-0.0.1-SNAPSHOT.jar code-processing.jar

# Establece el comando de inicio de la aplicación
ENTRYPOINT ["java", "-jar", "code-processing.jar"]
