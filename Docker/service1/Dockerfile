FROM kartikeyasoft/jdk17_onlineexam:v1.0.2 AS builder_image
RUN ls
RUN git clone https://github.com/ksrepo9/ksk8spro.git
RUN cd /ksapp/ksk8spro/service1 && mvn install

FROM kartikeyasoft/jdk17:latest
COPY --from=builder_image /ksapp/ksk8spro/service1/target/*.jar ksservice1.jar
EXPOSE 9001
ENTRYPOINT [ "java","-jar","ksservice1.jar" ]