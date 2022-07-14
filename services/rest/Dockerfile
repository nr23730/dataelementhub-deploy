FROM maven:3.8.5-openjdk-17-slim as build

RUN apt-get update && apt-get -y install git

RUN git clone https://github.com/mig-frankfurt/maven.git /maven
WORKDIR /maven
RUN git checkout 061d99ff7da75f53b2b27b6193dcf2a9d254ed93 && mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/maven.spring.git /maven-spring
WORKDIR /maven-spring
RUN git checkout 322fa274c9532b89b61d69b1785060e9c391aee4 && mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/dataelementhub.maven.git /dehub-parent
WORKDIR /dehub-parent
RUN git checkout bff16bc88486891d0c8d3ba3ec22d4ad7c539749 && sed -i '8 i <version>11.0.0</version>' pom.xml
RUN mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/dataelementhub.maven.spring.git /dehub-maven-spring
WORKDIR /dehub-maven-spring
RUN git checkout d3e6bed8ead13396e0a52127fef9f685aebbec84 && mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/dataelementhub.dal.git /dehub-dal
WORKDIR /dehub-dal
RUN git checkout 079da7a05cd4ab29cc45ee2c19749c6baa82b3ea && mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true -Dmaven.compiler.release=17

RUN git clone https://github.com/mig-frankfurt/dataelementhub.model.git /dehub-model
WORKDIR /dehub-model
RUN git checkout 95819de23aa5b561782ff47135ef7e350a031e77 && mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

RUN git clone https://github.com/mig-frankfurt/dataelementhub.rest.git /dehub-rest
WORKDIR /dehub-rest
RUN git checkout c285267c7182840c21a0f44736167ca218502ea8 && sed -i 's/3.0.0-SNAPSHOT/3.0.0/' pom.xml && sed -i 's/2.0.0-SNAPSHOT/2.1.0-SNAPSHOT/' pom.xml
RUN mvn install -Dmaven.javadoc.skip=true -Dmaven.test.skip=true

FROM gcr.io/distroless/java17-debian11
COPY --from=build /dehub-rest/target/dehub-rest-*-SNAPSHOT.jar /app/dehub.jar
CMD ["/app/dehub.jar"]