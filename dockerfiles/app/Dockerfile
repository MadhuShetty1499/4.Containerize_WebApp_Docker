FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
WORKDIR /app
RUN git clone https://github.com/MadhuShetty1499/4.Containerize_WebApp_Docker.git
RUN cd /app/4.Containerize_WebApp_Docker && git checkout main && mvn install

FROM tomcat:9-jre11
LABEL "Project"="vprofile"
LABEL "Author"="Madhu"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE /app/4.Containerize_WebApp_Docker/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
EXPOSE 8080
CMD ["catalina.sh", "run"]