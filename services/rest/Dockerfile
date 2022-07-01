FROM maven:3.8.6-openjdk-11-slim as build

RUN apt-get update && apt-get -y install git

RUN git clone https://github.com/mig-frankfurt/maven.git /maven
WORKDIR /maven
RUN mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/maven.spring.git /maven-spring
WORKDIR /maven-spring
RUN git checkout 016dcc31dd5119fddf0d8f7fbd4c30b5db8f3073 && mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/dataelementhub.maven.git /dehub-parent
WORKDIR /dehub-parent
RUN mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/dataelementhub.maven.spring.git /dehub-maven-spring
WORKDIR /dehub-maven-spring
RUN git checkout 83d634e365a563ee2c7566ab40b075f6c04339f9 && mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/dataelementhub.dal.git /dehub-dal
WORKDIR /dehub-dal
RUN git checkout ca1abb3e54454d9dfb5ab58236efbf3083c99c2e && mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/dataelementhub.model.git /dehub-model
WORKDIR /dehub-model
RUN git checkout develop && sed -i 's/2.2.0/2.3.0-SNAPSHOT/' pom.xml
RUN mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/dataelementhub.rest.git /dehub-rest
WORKDIR /dehub-rest
RUN git checkout develop && sed -i 's/2.2.0/2.3.0-SNAPSHOT/' pom.xml
RUN mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

FROM gcr.io/distroless/java-debian10:11
COPY --from=build /dehub-rest/target/dehub-rest-*-SNAPSHOT.jar /app/dehub.jar
CMD ["/app/dehub.jar"]