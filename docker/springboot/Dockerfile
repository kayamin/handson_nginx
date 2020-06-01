FROM openjdk:8

RUN git clone https://github.com/kayamin/springboot.git
WORKDIR ./springboot/experiment

EXPOSE 8080

RUN ./gradlew --full-stacktrace -q build

CMD ./gradlew bootRun