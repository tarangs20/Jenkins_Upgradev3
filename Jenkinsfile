pipeline{
  agent any
  options { timestamps () }
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

    stage('Deploying to Production'){
      steps{
      copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, flatten: true, projectName: 'Pipeline_Package_Creation', target: '/opt/tomcat/staging'
      echo "Artifacts copied to Staging"
      }
    }

    stage('Production Deployment'){
      steps{
        timeout(2){
          input message: "Proceed to Production?"
        }
        sh '''
          set +x
          mv /opt/tomcat/staging/java-tomcat-maven-example.war /opt/tomcat/apache-tomcat-9.0.53_prod/webapps/prod.war
        '''
      }
    }

  }
}
