pipeline {
 agent any
  options { timestamps () }

 stages{
  stage('Building Application Package'){
    steps{
     sh 'mvn -f java-tomcat-sample-docker/pom.xml clean package'
    }

    post{
      success {
        archiveArtifacts artifacts: '**/*.war'
      }
    }
  }

  stage ('Building Docker Image'){
    steps{
      sh "docker build . -t tomcat_docker_sample"
    }
  }
 }
}
