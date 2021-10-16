pipeline {
    agent any
    stages {
        stage('Build Application') {
            steps {
                
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                    
                }
            }
        }

        stage('Create Tomcat Docker Image'){
            steps {
                sh "pwd"
                sh "ls -a"
                sh "docker build . -t tom_sample"
                
            }
        }

    }
}
