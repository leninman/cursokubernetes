FROM openjdk:17-jdk-alpine as builder
WORKDIR /app/msvc-usuarios
COPY ./pom.xml /app
COPY ./msvc-usuarios/.mvn ./.mvn
COPY ./msvc-usuarios/mvnw .
COPY ./msvc-usuarios/pom.xml .

RUN ./mvnw clean package -Dmaven.test.skip -Dmaven.main.skip -Dspring-boot.repackage.skip && rm -r ./target/
#RUN ./mvnw dependency:go-offline

COPY ./msvc-usuarios/src ./src

RUN ./mvnw clean package -DskipTests

FROM openjdk:17-jdk-alpine

WORKDIR /app
RUN mkdir ./logs

COPY --from=builder /app/msvc-usuarios/target/msvc-usuarios-0.0.1-SNAPSHOT.jar .



EXPOSE 8001
#CMD sleep 20 && java -jar msvc-usuarios-0.0.1-SNAPSHOT.jar
CMD ["java","-jar","msvc-usuarios-0.0.1-SNAPSHOT.jar"]
