pipeline{
  agent any
  options { timestamps () }
  stages{

    stage('Building_UAT_Package'){
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

    stage('UAT_Deployment'){
      steps{
      copyArtifacts filter: '**/*.war', fingerprintArtifacts: true, flatten: true, projectName: 'Pipeline_Package_Creation_Deployment', target: '/opt/tomcat/staging'
      echo "Artifacts copied to Staging"
        
        sh '''
          set +x
          sudo /opt/tomcat/apache-tomcat-9.0.53_prod/bin/shutdown.sh
          sudo rm -rf /opt/tomcat/apache-tomcat-9.0.53_prod/webapps/UAT/
          sudo rm -rf /opt/tomcat/apache-tomcat-9.0.53_prod/webapps/UAT.war
          mv /opt/tomcat/staging/java-tomcat-maven-example.war /opt/tomcat/apache-tomcat-9.0.53_prod/webapps/UAT.war
          echo "Deployed to UAT"
          sudo /opt/tomcat/apache-tomcat-9.0.53_prod/bin/startup.sh
        '''
      }
    }

    stage('Production Deployment'){
      steps{
        timeout(2){
          input message: "Proceed to Production?"
        }
        
      }
    }

  }
}
