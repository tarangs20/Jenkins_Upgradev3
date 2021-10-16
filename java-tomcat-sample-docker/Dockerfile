FROM tomcat:8.0
ADD /var/lib/jenkins/workspace/docker_int/java-tomcat-sample/target/java-tomcat-maven-example.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
