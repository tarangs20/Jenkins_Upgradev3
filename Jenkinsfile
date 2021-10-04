pipeline{
  agent any
  stages{

    stage('Building Package'){
      steps{
        sh 'mvn -f java-tomcat-sample/pom.xml clean package'
      }

      post {
        success{
          echo "Artifacts has been created...Archiving it"
          archiveArtifacts artifacts: '**/*.war'
        }
      }
    }

    stage('Deploying to Staging'){
      steps{
      copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, flatten: true, projectName: 'Pipeline_Package_Creation', target: '/opt/tomcat/staging'
      }
    }

  }
}
