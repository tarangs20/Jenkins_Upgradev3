pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                
                sh 'mvn -f java-tomcat-sample/pom.xml clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                    sh "pwd"
                    sh "mkdir -p java-tomcat-sample-docker/artifacts "
                    sh "cp java-tomcat-sample/target/java-tomcat-maven-example.war java-tomcat-sample-docker/artifacts/app.war "
                    sh "ls"
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "ls -a"
                sh "docker build ./java-tomcat-sample-docker -t tomcatsamplewebapp"
                cleanWs()
            }
        }

    }
}
