FROM eclipse-temurin:17-jdk-alpine as main-builder
COPY Main.java /usr/src/Main.java
WORKDIR /usr/src
RUN javac Main.java

FROM eclipse-temurin:17-jre-alpine
COPY --from=main-builder /usr/src/Main.class /usr/src/Main.class
WORKDIR /usr/src
ENTRYPOINT ["java", "Main"]