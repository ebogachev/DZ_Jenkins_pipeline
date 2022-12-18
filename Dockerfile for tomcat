FROM adoptopenjdk/openjdk11:jre-11.0.6_10-alpine
RUN wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.70/bin/apache-tomcat-9.0.70.tar.gz -O /tmp/tomcat.tar.gz
RUN cd /tmp && tar xvfz tomcat.tar.gz
RUN mkdir /usr/local/tomcat
RUN cp -Rv /tmp/apache-tomcat-9.0.70/* /usr/local/tomcat
EXPOSE 8080
CMD ["/usr/local/tomcat/bin/catalina.sh", "run"]
