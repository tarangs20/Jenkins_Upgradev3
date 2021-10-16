pipeline {
 agent any
 options { timestamp() }

 stages{
  stage('Building Application Package'){
    steps{
     sh 'maven -f java-tomcat-sample-docker/pom.xml clean package'
    }

    post{
      success {
        archiveArtifacts artifacts: '**/*.war'
      }
    }
  }

  stage ('Building Docker Image'){
    steps{
      docker build . -t tomcat_docker_sample
    }
  }
 }
}
