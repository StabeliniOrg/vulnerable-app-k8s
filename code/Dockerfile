FROM maven:3.8.4-jdk-11 as build
WORKDIR /app
COPY app /app
COPY settings.xml /app
RUN mvn clean package -s settings.xml

FROM tomcat:9.0-slim
COPY flag /flag
EXPOSE 8080
COPY --from=build /app/target/helloworld.war $CATALINA_HOME/webapps
RUN echo "deb http://archive.debian.org/debian stretch stretch-security main contrib non-free" > /etc/apt/sources.list
